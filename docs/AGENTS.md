# silva/ — Agent Instructions

> **scope**: private (`@xdanger`) silva
> **role**: Kros 个人的外部知识 + 原创合成累积"林"

## silva 是什么

*silva*（拉丁文「林」）来自 Quintilian / Statius 的修辞学传统，本意是"writer 笔下尚未加工的素材丰盈状态"——既是字面意义的森林（heterogeneous、accretive、organic），也是 raw material 的隐喻。本目录预期 **heterogeneity**：

- 外部摘抄（*Economist* 文章、研究报告 digest）
- Kros 原创合成（财报分析、估值模型、ad-hoc deep-read）
- 持续追踪（如 `anthropic-products.md` 的 Anthropic 产品时间线）
- 技术参考（Godot WASM constraints、infrastructure 笔记）

家共享版本在 `@family/silva/`（family-readonly）。本目录仅 Kros 一人可读可写。

## 目录布局

```
silva/
├── AGENTS.md              ← 本文件
├── anthropic-products.md  ← evergreen 例外，留根；frontmatter 仍含 created+updated，无日期前缀
└── YYYY/                  ← 默认归宿，按 frontmatter `created` 年份分组
    ├── YYYYMMDD_slug.md   ← 日期已知到天 → 8 位前缀
    ├── YYYYMM_slug.md     ← 只知道月（如 clipping 自老 URL） → 6 位前缀
    ├── slug.md            ← 只知道年（年已在文件夹里）→ 无前缀
    └── ...
```

**Flat under `YYYY/`**——不按主题再分子目录，topic 信息进 frontmatter 的 `topic:` 字段。

### YYYY/ 还是根目录？

| 情况 | 归宿 | 理由 |
|---|---|---|
| 一次性写完、之后只 minor revise 的研究 / 摘抄 / 分析 / clipping | `YYYY/` | 主流情况；99% 文件归这里 |
| 持续滚动更新、几乎每天都有新增的"知识库"类长文 | 根 | `anthropic-products.md` 是当前唯一例子（scheduled task 每天累积 Anthropic 产品时间线）。**新增必须谨慎**——大部分"会更新"的文件其实是 minor revise 性质，仍归 `YYYY/` |

判定 test：**"这份文件 12 个月后还会被定期追加吗？"** 答案肯定 → 根。任何"也许会、可能不会、看情况"的犹豫 → `YYYY/`。

### `YYYY/` 的 `YYYY` 取什么年份？——按 `source_type` 分两类

| `source_type` | `YYYY` 取什么 | `created` 字段表示 |
|---|---|---|
| `own_analysis` / `tracking` / `summary`（包含 Kros 自己的合成） | **Kros 写这份文件的年份** | Kros 写这份文件的日子 |
| `clipping` / `reference`（纯外部内容、Kros 只做保存） | **原始来源发表的年份** | 原始来源发表日（粒度可到 YYYY / YYYY-MM / YYYY-MM-DD） |

理由：clipping 类的"内容年份"是源材料的年份，不是 Kros 保存它的年份。把 2007 年 Scott Adams 的文章放在 `silva/2026/` 会让"silva/2026/ 装的是 2026 年的内容"这条 mental model 失真——按源年份归档保留了 silva 作为"时间组织的知识库"的可读性。

clipping 类用 `clipped_at:` 字段记录 Kros 保存它的日子（**与 `created` 区分**——`created` 是源材料生成日，`clipped_at` 是进 dossier 的日）。

## frontmatter 规则

**所有 silva 文件必含 `created:` + `updated:`**——这是 silva-specific 规则（其他子目录通常只要 `updated:` 必含）。理由：silva 内容性质偏公开 / 偏可外泄（research、blog 草稿、reading summary 等都可能哪天分享或引用），创建时间与更新时间作为可追溯的 metadata 都重要。

完整模板：

**模板 1（own_analysis / summary 类——Kros 自己写的）：**

```yaml
---
title: SpaceX S-1 2026 Financial Analysis
created: 2026-05-21              # 必填。= Kros 写这份文件的日子；YYYY/ 子目录据此决定；filename 前缀 YYYYMMDD 与之对齐
updated: 2026-05-21              # 必填。内容刷新日；可与 created 相同
status: stable                   # 建议。draft | stable | superseded
audience: kros-only              # 建议。kros-only | family | external（决定将来能否提级到 @family/silva 或公开）
topic: [wealth, spacex, ipo]     # 建议。话题标签，flat list；替代了"主题子目录"职能
source_type: [own_analysis]      # 建议。own_analysis | summary | tracking | reference | clipping
---
```

**模板 2（clipping / reference 类——纯外部内容）：**

```yaml
---
title: The Day You Became a Better Writer
author: Scott Adams
created: "2007-06"               # 必填。= 原始来源发表日；粒度可到 YYYY / YYYY-MM / YYYY-MM-DD（YAML date 不接受月精度时用字符串）
updated: 2026-05-14              # 必填。这份 clip 上次刷新的日子（含元数据维护）
clipped_at: 2026-05-14           # clipping 专属。Kros 把它收进 silva 的日子
source_type: [clipping]
status: stable
audience: external
topic: [writing, communication, style-guide]
source_original_url: https://...  # 原始 URL（即便已失效也记录，方便去 Wayback Machine）
source_archive_url: https://web.archive.org/web/*/...    # Internet Archive 备份点（如已存档）
source_mirror: https://...        # Kros 自己的镜像 / 局部副本（如有）
source_note: |
  hosting platform / 原文章背景 / link rot 提示等
---
```

**字段语义注**：

- `created` 语义因 `source_type` 而异（见上方布局表）：own_analysis / summary / tracking → Kros 写作日；clipping / reference → 源材料发表日
- `updated`：内容上次有意义变更的日子。typo / 格式修复不算
- `clipped_at`：**仅 clipping 类用**。Kros 把它收进 silva 的日子（与源 `created` 分开）。own_analysis 等无需此字段
- `status: draft` → 还在打磨；`stable` → 此 snapshot 可作 reference；`superseded` → 被新文件取代，frontmatter 加 `superseded_by:`
- `audience: external` 意味着这份内容若 publish 出去也 OK
- `source_type` 是一组 tag，可同时多个（如一份文件既是 summary 又含 own_analysis）
- `source_*` 字段族**仅适用于** clipping / summary / reference 三类——own_analysis 和 tracking 类不需要 source_original_url（自己写的不需要"原文章"概念）。如果一份文件 `source_type: [summary, own_analysis]` 这种混合，源材料的 source URL 仍要记
- `source_original_url` 即便失效也写——后人靠它去 Wayback Machine 反查比靠记忆找快得多
- `source_archive_url` 用 Wayback Machine 的 `*` 模板（`/web/*/<original>`），自动取最新可用快照

## 文件命名

`YYYY/` 下的文件——**前缀按 `created` 的实际粒度**：

| `created` 粒度 | filename 形式 | 例 |
|---|---|---|
| 知道到天（`YYYY-MM-DD`） | `YYYYMMDD_slug.md` | `20260521_economist_musk-unproven-technology_briefing.md` |
| 只知道月（`YYYY-MM`） | `YYYYMM_slug.md` | 假设 Adams 的文章 URL 给到月：`200706_scott-adams-...md`（**当前用法是无前缀；URL 月粒度不足以驱动文件名差异化**） |
| 只知道年（`YYYY`） | `slug.md`（无前缀，年在文件夹里） | `scott-adams-the-day-you-became-a-better-writer.md`（在 `silva/2007/` 里） |

slug 用 lowercase + 连字符 + 描述性（参 `@family/docs/naming-rules.md`）。

根目录的 evergreen 文件：**无日期前缀**，文件名直接是 slug（如 `anthropic-products.md`）。

**实操原则**：粒度不足 8 位时，宁可无前缀也不要填假日（如"用 01 占位"违反"frontmatter / filename 必须诚实"的原则）。同一年同一作者多份 clipping 排序问题靠 `topic:` filter 或编辑器 sort by mtime 解决，不靠假装的 YYYYMMDD。

## 路径永久性

silva 文件一旦放好就永不挪动：

- **不要**因为 status 从 draft 变 stable 就改名 / 改路径——status 进 frontmatter
- **不要**因为 supersede 就 mv 老文件——老文件原地保留，frontmatter 加 `superseded_by:`，新文件正常进 `YYYY/`
- **不要**因为话题大了想拆主题子目录就把文件搬进去——topic 用 frontmatter `topic:` 字段，目录始终 flat under `YYYY/`
- 例外：极少数情况下 user 显式要求结构重组（属 structural change，写到 `history/YYYY/YYYYMMDD_slug.md`）

## 写新 silva 文件的流程

1. **明确文件性质**：own_analysis / summary / tracking（含 Kros 写作）→ 用模板 1；clipping / reference（纯外部）→ 用模板 2。一次性研究 / reading summary / 持续追踪？前两类 → `YYYY/`；只有真正的持续追踪 → 根
2. **确定 `created` 的语义**：模板 1 → 今天；模板 2 → 源材料发表日（粒度按可知信息）
3. **取 final filename**：YYYY = `created` 的年份；filename 前缀按 `created` 粒度（YYYYMMDD / YYYYMM / 无前缀）
4. **写 frontmatter**：至少 `title` + `created` + `updated`，建议补 `status` / `audience` / `topic` / `source_type`；clipping 类必含 `clipped_at` + `source_*` 字段族
5. **写内容**——结构由内容驱动，无固定模板
6. **如内容引用其他 silva / canon 文件**，用相对路径（`../canon/family-trust.md` 或 `./other-file.md` 视位置而定）

## 写 silva 时常踩的坑

- **`audience: family`** 的文件其实该写到 `@family/silva/` 而不是 private silva。判断后**确定家共享性质 → 写到 `@family/silva/`，不要写到这里再贴一份**
- **混合 raw + analysis 的文件**：如果某文件 90% 是原文 + 10% 我的批注，更适合 `resources/YYYY/`（外部原件）而不是 silva（distillation 性质）。回顾自己写的内容比例
- **本应进 canon 的内容写到了 silva**：关于 Kros / 家庭自身事实的"手册式"描述应该去 `../canon/`（first-person 事实），不是 silva（third-person 外部知识）
- **本应进 memory 的事实写到了 silva**：agent 在工作过程中学到的、跨 session 复用的事实（如 advisor 联络方式、家人 LPR 状态）→ `../memory/{topic}/`，不是 silva
- **frontmatter 漏 `created`**：本目录强制 silva-specific 要求，CI / lint 没有但 manual review 时要补
- **clipping 的 `created` 误填成"今天"**：clipping 类的 `created` 是源材料日（不是 Kros clip 的日子），后者进 `clipped_at`。把 Adams 2007 年的文章 created 写成 2026 会让"silva/2026/ 装 2026 内容"这条 model 失真——按源年份归档
- **`source_type` 误归类**：例如把外部 paper 的 1:1 翻译当成 own_analysis；翻译本质仍是 clipping。Kros 的 commentary 必须占文件相当比例（>30%）才升级到 summary / own_analysis
