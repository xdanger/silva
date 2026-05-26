---
title: Godot 游戏导出 WASM 的实战约束 (2026-05 snapshot)
created: 2026-05-25
updated: 2026-05-25
status: stable
audience: kros-only
topic: [games, godot, wasm, web-export, engine-research]
source_type: [own_analysis, reference]
stance: practical-engineering-research
sources: [godot-docs 4.5, godotwebgpu.com beta 2026-05-10, GodotCon Boston 2025-05 .NET web prototype talk]
---

# Godot 游戏导出 WASM 的实战约束

> 2026-05-25 调研，针对 Godot 4.5 stable。版本演进快，看 expiry 字段：核心结论的 6 个月内（到 2026-11 前）仍可参考；之后请重新核对 C# / WebGPU upstream 状态。

## TL;DR — 三条硬卡口

不是所有 Godot 项目都能一键导出 WASM。如果踩到下面任意一条，要么没法导出，要么得大改：

1. **用了 C#**——4.x 全系列移除了 .NET web 导出。GodotCon Boston 2025-05 演示的 Mono 静态链接原型截至 2026-05 没进 stable。
2. **用了未做 web 适配的 GDExtension**——第三方 C++ 插件如果没单独提供 WASM side module，上不了 web。Firefox 支持比 Chromium 弱。
3. **用了 Forward+ / Mobile renderer**——这俩依赖 Vulkan-class compute；浏览器只稳定提供 WebGL2。Compatibility renderer 才是 web 唯一稳态。WebGPU 路线由社区分支 godotwebgpu.com 推进，2026-05-10 发 public beta，**不是 upstream**。

## 为什么这些限制存在（connect the dots）

| 限制 | 根因 |
|---|---|
| 多线程要 COOP/COEP header | Spectre/Meltdown (2018-01) 后浏览器收紧 SharedArrayBuffer，要 cross-origin isolation |
| AudioContext 等点击 | Chrome 66 (2018) autoplay policy，防广告自动响 |
| 无 raw TCP/UDP | 浏览器始终不暴露 raw socket，防 DDoS 工具化 |
| IndexedDB 不可靠 | 浏览器把它归类为 site data；Safari ITP 7 天清；隐私模式失效 |
| ~40 MB 空导出 | Godot servers 架构 + SCons 默认不剥离未用模块 |
| 1.5-2× 性能损失 | WASM AOT 无 CPU 特化；SIMD 默认关；Emscripten syscall 桥接固定开销 |

## 完整能力对比矩阵

| 关注点 | Native | Web (4.5 stable) | Web + WebGPU 分支 (beta) |
|---|---|---|---|
| GDScript | ✓ | ✓ | ✓ |
| C# / .NET | ✓ | ✗ prototype only | ✗ |
| GDExtension (C++) | ✓ | △ 重编为 WASM side module；Firefox 弱 | △ |
| Forward+ renderer | ✓ | ✗ | ✓ |
| Mobile renderer | ✓ | ✗ | ✓ |
| Compatibility renderer | ✓ | ✓ | ✓ |
| 多线程 | ✓ | △ 需 COOP/COEP | △ |
| 原生 TCP / UDP socket | ✓ | ✗ | ✗ |
| WebSocket | ✓ | ✓ 仅 TCP, RPC 必 reliable | ✓ |
| WebRTC | ✓ | ✓ unreliable 可用，server 端难 | ✓ |
| 任意磁盘 I/O | ✓ | ✗ | ✗ |
| `user://` | ✓ 真实文件 | △ IndexedDB ephemeral | △ |
| Audio 自动启动 | ✓ | ✗ 需 user gesture | ✗ |
| `OS.execute` / `shell_open` | ✓ | ✗ | ✗ |
| 内存上限 | RAM | ~2 GB wasm32 | ~2 GB |
| 空项目导出体积 | ~30 MB | ~40 MB | 更大 |

## 核心数字 (web vs native)

- WASM 内存：~2 GB 可用 (wasm32 实际上限)；iOS 更紧
- 空项目导出：~40 MB（Brotli 后小很多，但 .wasm 单文件 > 25 MB 时 Cloudflare Pages / GitHub 拒收）
- 首次冷加载：5–15 s（下载 + 编译 + IndexedDB 初始化）
- CPU 性能：~1.5–2× 慢于 native，纯 CPU bound 代码更糟

## Day 1 lock-ins（不锁就要重写）

1. **语言锁 GDScript**——别赌 C# web 何时进 stable
2. **渲染器锁 Compatibility**——光照/阴影方案围绕 GL ES 3.0 能做的设计
3. **避免第三方 GDExtension**——除非插件作者明确提供 WASM side module
4. **网络抽象选 WebSocket 或 WebRTC**——别在代码里硬编码 ENet 假设
5. **托管方案先定**——itch.io / GitHub Pages 默认不能开 COOP/COEP；要多线程就选自营服务器或 Cloudflare Pages + Workers / Vercel 等可配 header 的

## Day 1 best practices（refactorable 但别拖）

1. **音频挂第一次点击**——`OS.has_feature("web")` 分支里把 BGM 推迟到 input gesture 之后
2. **`user://` 视作 ephemeral**——重要存档走云端；本地只做 cache
3. **内存预算 < 1 GB 工作集**——监控 `OS.get_static_memory_usage()` 早点 surface 问题
4. **资源包 < 30 MB 压缩**——单 .wasm 文件 < 25 MB，否则 Cloudflare Pages 和 GitHub 拒收
5. **纹理用 ETC2**——BPTC / ASTC 在 WebGL2 不普及；ETC2 是最稳的最低公倍数
6. **触屏 + 鼠标 + 手柄都要测**——没有 right-click-only 路径
7. **禁用 OS.execute / shell_open / 原生文件对话框**——sandbox 一刀切
8. **自定义启动画面 + 进度条**——10 秒空白 canvas 会赶人
9. **Web 测试从 Week 1 开始**——每个 milestone 都跑一次 web export，drift 才不会失控
10. **音频 latency 设 50 ms web override**——默认 15 ms 在 Web Audio API 下会 underrun

## 路线判定

如果以下任一为真，**重新评估 Godot Web 是否合适**：

- 项目用 C# 写、且 web 是 MVP-required（不是 nice-to-have）
- 项目用大量 compute shader / 现代 PBR 流水线，且 web 是 release 目标
- 项目是 real-time competitive multiplayer，且 web 用户期望 < 50 ms latency
- 项目依赖原生 modal / file dialog / 外部进程
- 项目工作集内存 > 1.5 GB

否则按 Day 1 lock-ins 走是 OK 的。

## 引用

- [Exporting for the Web — Godot 4.5 docs](https://docs.godotengine.org/en/4.5/tutorials/export/exporting_for_web.html)
- [Web Export in 4.3 — Godot Engine 官方 progress report](https://godotengine.org/article/progress-report-web-export-in-4-3/)
- [GodotCon Boston 2025: Web .NET prototype](https://godotengine.org/article/live-from-godotcon-boston-web-dotnet-prototype/) (Adam Scott, Raul Santos, 2025-05-06)
- [godot4-web-dotnet-prototype on GitHub](https://github.com/raulsntos/godot4-web-dotnet-prototype) (try at `lab.godotengine.org/godot-dotnet-web/`)
- [Godot WebGPU community fork](https://godotwebgpu.com/) (public beta 2026-05-10)
- [GitHub issue: Re-add C# web support](https://github.com/godotengine/godot/issues/70796)
- [GitHub issue: WASM file > 25 MB blocks Cloudflare Pages / GitHub hosting](https://github.com/godotengine/godot/issues/70672)
- [Godot proposal: WebGPU support](https://github.com/godotengine/godot-proposals/issues/6646)
- [Godot proposal: WebGPU renderer backend discussion](https://github.com/godotengine/godot-proposals/discussions/4806)
- [Godot networking: WebRTC docs](https://docs.godotengine.org/en/stable/tutorials/networking/webrtc.html)
- [Godot networking: WebSocket docs](https://docs.godotengine.org/en/stable/tutorials/networking/websocket.html)
- [How to minify Godot's build size — popcar.bearblog.dev](https://popcar.bearblog.dev/how-to-minify-godots-build-size/)
- [Optimize size of Godot web releases — amann.dev](https://amann.dev/blog/2025/godot_web_size/)
