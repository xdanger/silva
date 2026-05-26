---
title: Recursive — 递归自我改进 AI Lab
created: 2026-04-25
updated: 2026-04-25
status: stable
audience: kros-only
topic: [ai, investment, recursive-self-improvement]
source_type: [own_analysis, summary]
source: 和暄资本《Recursive 研究报告》2026-04-17 内部投资备忘录（26 页 PDF，uploads/Recursive研究报告_20260417.pdf）
stance: critical-reading-of-a-bullish-memo（对看多报告的批判性解读）
---

# Recursive — 递归自我改进 AI Lab

## 1. 公司一句话画像

美国前沿 AI 初创公司，首轮融资投前估值 **40 亿美元**，预计本轮融资 **5 亿美元**，**NVIDIA、Google Ventures、AMD** 已确认参投。核心主张是做 **Recursive Self-Improvement（RSI，递归自我改进）**——让 AI 系统在无需人类反馈的前提下自主迭代自身算法、权重、代码与架构。

和暄资本 2026-04 内部报告将其定性为"极具赔率的左侧布局点（high-conviction left-side bet，高确信度的左侧建仓机会）"。本 KB 文件是对该报告的批判性解读（critical reading），不是原文摘要。

## 2. 核心技术叙事

### 2.1 RSI 解决的痛点

当前 LLM 面临两堵墙：
- **人类先验天花板**：模型接近人类水平后，RLHF 提供的信号越来越弱
- **高质量训练数据枯竭（data exhaustion）**：互联网公开高质量文本接近耗尽

静态模型（static model）在部署后无法从交互经验中学习，工具库被预定义 API 锁死，架构在设计期固化——这三重静态性构成当前 AI 能力天花板。

### 2.2 RSI 的四个进化位点（evolutionary loci）

| 维度 | 含义 | 代表技术 |
|---|---|---|
| **模型（Models）** | 权重参数自主更新 | 自我奖励、RAGEN |
| **上下文（Context）** | 记忆 + 提示词 | Mem0、SAGE、PromptBreeder、SPO |
| **工具（Tools）** | 从工具使用者升级为工具创造者 | Voyager、Alita、ToolGen |
| **架构（Architecture）** | 重写工作流 + 多智能体编排 | — |

### 2.3 关键技术主张：新型 Test-Time Scaling Law

报告最核心的技术叙事——区别于 OpenAI o1 的推理时扩展（算力消耗完即止，模型不变），Recursive 主张算力应转化为 **永久性的知识沉淀**（persistent knowledge accretion），形成飞轮（flywheel）效应。

| 维度 | 经典 Test-Time Scaling（如 o1） | 新型 Test-Time Scaling（Recursive） |
|---|---|---|
| 算力目标 | 探索推理树、找单次答案 | 持续沉淀知识与经验 |
| 底层影响 | 权重/代码冻结 | 递归优化提示词、权重、代码、基础设施 |
| 时间收益 | 算力消耗完即止 | 飞轮效应，系统持续自我进化 |

## 3. 创始团队（全球 RSI 最高密度人才集群）

这是报告里**最硬**的部分。八位联合创始人每人在 RSI 技术栈都有清晰的学术定义权：

| 成员 | 背景 | 关键贡献 |
|---|---|---|
| Richard Socher | 前 Salesforce CSO、You.com CEO、AIX Ventures | 词向量、prompt engineering 发明人之一；NLP 被引前五 |
| Tim Rocktäschel | Google DeepMind Director | **RAG 共同发明人**、Promptbreeder、Genie 1-3 |
| Tim Shi | OpenAI 早期成员、Cresta 创始人 | **RLHF 奠基论文**作者、World of Bits |
| Yuandong Tian（田渊栋） | 前 Meta FAIR Research Director | Llama 4 Reasoning 负责人、AdvPrompter、coconut |
| Jeff Clune | 前 OpenAI 研究团队负责人、DeepMind 顾问 | **Darwin-Gödel Machines**、AI Scientist、Go-Explore 共同发明人 |
| Caiming Xiong | Salesforce AI Research 联合创始人 | CTRL、BLIP、Codegen、xLAM、ProGen |
| Alexey Dosovitskiy | 前 Google Brain / DeepMind | **Vision Transformer (ViT)** 领导者 |
| Josh Tobin | 前 OpenAI Agents 负责人 | Deep Research、ChatGPT Agent、Codex v1；Sim2Real |

**最值得留意的组合**：**Jeff Clune + Tim Rocktäschel**——开放式进化（open-endedness）和 Darwin-Gödel Machines 方向的真正学术源头。Recursive 的技术叙事不是 pitch 编出来的，而是**把这两位实验室的研究做商业化延伸**。

另有 13 位顶尖实验室/高校背景的创始成员。

## 4. 商业模式（远期憧憬，无 PMF 证据）

报告罗列三条变现路径：
1. **AI Drop-in Employees**：交付数字员工，直接替代软件开发岗位
2. **模型 API 服务**：对开源权重模型快速强化后通过 API 外售
3. **底层 RSI 算法 API**：把 RSI 算法本身作为 API 出售

现阶段三条都是远期愿景（distant aspirations），没有收入轨迹。

## 5. 批判性分析（报告没说透的几点）

作为推荐材料写得非常漂亮，但作为投资判断需要警惕：

**1. RSI 在工程上仍高度未验证。** Darwin-Gödel Machines、AI Scientist 等学术成果大多还是玩具规模（toy-scale）实验，从 arXiv paper 到 $4B 估值之间没有产品中间态，没有在生产环境做出过可持续、可审计的自我改进循环。

**2. 与大厂差距被低估。** 报告承认 OpenAI/Anthropic/DeepMind 已有 Codex、Claude Code、AlphaEvolve，然后用"结构性空白"论证机会。但 RSI 最吃算力+数据+基础设施，而这三样恰恰是大厂的绝对优势。$500M 烧算力烧自动化 GPU 调优的模型，消耗是指数级的。

**3. 商业化路径讲得虚。** 三条变现路径都是愿景，估值完全建立在"团队 × 叙事"而非收入轨迹。

**4. 估值锚点存在幸存者偏差（survivorship bias）。** 报告拿 OpenAI/Anthropic/xAI 做对标，说"12-18 个月数倍回报"。但同类"豪华团队+顶级资本"的降估值/失败案例（**Inflection、Adept、Character.AI**）没有被对称列出。

**5. 投资人组合暗藏利益冲突。** NVIDIA + Google + AMD 是**芯片/云的供给方**，它们投 AI Lab 往往是战略性锁定 GPU/TPU 消费方，与纯财务投资人（a16z、红杉）的估值锚定逻辑不完全对齐——Recursive 拿到的不一定是最严苛的市场价。

## 6. 结论

剥开营销语言，真实信号是：

> **Recursive 是一次"以人才密度定价"的赌注**——赌点不是产品、不是收入、不是护城河，而是"一组全球 RSI 方向最顶尖的科学家愿意一起创业"这件事本身的稀缺性。

这种赌法在 AI 超级周期里历史回报率的确极高（OpenAI/Anthropic 是模板），但也意味着：**如果团队分裂、如果大厂挖走任何核心人、或如果 RSI 范式本身被证伪，$4B 估值会迅速崩塌**，因为底下没有收入垫（no revenue cushion）。

**定性**：高赔率、高方差、团队即资产的早期船票（early-stage ticket）。适合配置里能承受归零的头寸，不适合作为稳健仓位。

## 7. 追踪指标（future signals to watch）

- Recursive 是否发布首个可公开验证的自我改进闭环 demo（不是 paper）
- 八位联合创始人是否保持全员在岗（任何一位离开都是重大信号）
- 大厂是否以具体产品形态追赶（OpenAI/Anthropic 的下一代 agent 是否朝 RSI 收敛）
- NVIDIA/Google/AMD 的后续追投行为（战略投资方下一轮跟投 vs 转为纯财务观望）
- 同代 AI Lab（AMI Labs、World Labs、Thinking Machines）估值走势的对标参照
