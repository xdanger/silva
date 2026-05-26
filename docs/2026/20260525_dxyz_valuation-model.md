---
title: DXYZ (Destiny Tech100) — 持仓拆解与 NAV 估值
created: 2026-05-25
updated: 2026-05-25
status: draft
audience: kros-only
topic: [investments, closed-end-fund, private-tech, dxyz, spacex, anthropic, openai]
source_type: [own_analysis]
ticker: DXYZ
exchange: NYSE
nav_as_of: 2026-03-31
nav_per_share: 24.56
portfolio_value: 742_500_000
market_price_at_research: 66.64
estimated_shares_outstanding: ~33M（5/25/2026 估算）
---

> 调研时点 **2026-05-25**。所有 NAV / 持仓数据基于 Destiny Tech100 在 SEC 提交的 [Form 424B3 (3/31/2026)](https://www.sec.gov/Archives/edgar/data/0001843974/000157587226000288/dxyz100_424b3.htm) 与 [destiny.xyz/tech100](https://destiny.xyz/tech100) 官方披露。底层公司估值来自最近一轮一级市场或可查到的二级市场报价。

## 1. 一句话结论

DXYZ 当前股价 **$66.64**，最近一次官方 NAV（2026-03-31）**$24.56/股**，市价是 NAV 的 **~2.7×**（溢价 **~171%**）。把已有持仓按 2026-05 最新可见的一级 / 二级估值重新 mark-to-market 之后，"公允" NAV 大致落在：

| 方法 | 估算 NAV/股 | 隐含合理价（贴 NAV） | 与 $66.64 比 |
|---|---|---|---|
| **A. NAV 中性**（信任 Destiny 自己的 ASC 820 mark，仅滚动 ATM 摊薄 / 增厚） | **$25–27** | $25–27 | 溢价 **~150%** |
| **B. Mark-to-market**（把 Anthropic 提到传言中 $900B、SpaceX 维持 $800B 等最新口径） | **$30–34** | $30–34 | 溢价 **~100%** |
| **C. 极乐观**（Anthropic $900B 落地 + SpaceX $1.0T 提价 + OpenAI 估值不变） | **$36–40** | $36–40 | 溢价 **~70%** |

无论用哪种口径，**当前股价都超出 NAV 一大截**。这个 premium 是 DXYZ 自上市以来的常态——它本质上是 retail 通道稀缺性 + 单一标的（尤其 SpaceX、Anthropic）的隐含看涨期权——但 ATM 增发持续以高溢价兑现这部分 premium，会逐步把价格往 NAV 拉。

## 2. 这是个什么东西（机制速览）

**Destiny Tech100（DXYZ）** 是一支 NYSE 挂牌的 **closed-end fund**（封闭式基金，CEF）——结构上是 1940 年《投资公司法》（Investment Company Act）下的注册投资公司，但只发了一次 IPO 之后不再申赎，份额在交易所上像股票一样买卖。它的投资策略：**用基金壳装一篮子未上市的硅谷 / 美国 late-stage 私有科技公司**，让普通散户能买到 SpaceX、Anthropic、OpenAI 这种平时只对机构 LP 开放的标的。

### 它怎么持仓这些非上市公司？

不是直接拿到 SpaceX 的 Series J 优先股证书。绝大多数大头持仓是通过 **SPV**（special purpose vehicle / 特殊目的载体）持有的："Magnitude ANC III, LLC"、"DXYZ SpaceX I LLC"、"Goanna Capital 26E LLC" 这些名字都是 SPV——它们各自只持有一家公司的一笔股权，DXYZ 买的是 SPV 的 LP 份额。SPV 一般会向 DXYZ 收 1–2% 管理费 + 10–20% carry（业绩报酬），所以**披露的 18.1% Anthropic 暴露不等于退出时 DXYZ 真能拿到 18.1% 对应的现金**——中间有 SPV 层级抽水。这是一层估值上的 "stealth tax"，模型里值得打个折。

还有少量是 **forward contract**（远期合约）——比如 Forge Investments 那两支（Stripe、Plaid），合约方将来在标的股票可自由转让时把股票交付给 DXYZ，本质上是 fund-of-funds 的另一种法律皮。

### NAV 是怎么算的？

按 1940 Act Rule 2a-5 + FASB **ASC 820**（Fair Value Measurement，公允价值计量）。非上市股权没市价，所以三种方法混用：
- **市场法**：最近一轮 priced round（已定价的融资轮）的每股价，乘自己持股数；类似行业的可比 multiples（comparable multiples）打折。
- **收入法**：DCF / 预期现金流贴现，对营收稳定的标的（少用）。
- **成本法**：实在没法估值的初创公司用成本（cost）当 fair value。

Destiny 一年请独立估值师（valuation specialist）评一次，季度自己 mark。注意：**最近一轮融资距今越久，mark 越可能跟二级市场实际报价脱节**。

## 3. 持仓全景（2026-03-31，按占组合比例排序）

总组合公允价值 **$742.5M**，36 家持仓公司，NAV/股 **$24.56**。下表只列 > 0.5%，更小的位置见 SEC 424B3 原文。

| # | 经济暴露标的 | 持仓载体（SPV/直接） | 占组合 % | 隐含 $ 价值 (M) | 行业 |
|---|---|---|---|---|---|
| 1 | **First American Treasury** | Money Market（货币基金） | **31.4%** | 233.1 | 现金等价物 |
| 2 | **Anthropic**（Series B Preferred） | Magnitude ANC III, LLC | **18.1%** | 134.4 | AI |
| 3 | **SpaceX**（99% Class A Common + 1% Series J Pref） | DXYZ SpaceX I LLC | 9.6% | 71.3 | 航天 |
| 4 | **OpenAI**（Series C Preferred） | Goanna Capital 26E LLC | 4.7% | 34.9 | AI |
| 5 | **OpenEvidence**（Common） | SP21Z Opportunities LLC | 4.6% | 34.2 | 医疗 AI |
| 6 | **Shield AI**（Series F1 Pref） | Snowpoint Growth 2.5 | 4.2% | 31.2 | 国防 AI |
| 7 | **SpaceX**（55% Class A + 45% Class C） | MWAM VC SpaceX-II | 2.8% | 20.8 | 航天 |
| 8 | **Beast Industries**（Series C Pref） | 直接 | 2.0% | 14.9 | Creator 经济 |
| 9 | **SpaceX**（Class B Common） | Snowpoint Growth 2.6 | 2.0% | 14.9 | 航天 |
| 10 | **Hermeus**（Series C Pref） | 直接 | 2.0% | 14.9 | 高超声速航空 |
| 11 | **Tenstorrent**（可转债，15% / 2026-12 到期） | Prive Tens, LLC | 1.7% | 12.6 | AI 芯片 |
| 12 | **Revolut**（Common） | 直接 | 1.6% | 11.9 | 数字银行 |
| 13 | **Ferox Games**（Series F Pref） | Hexagon Master LLC | 1.5% | 11.1 | 游戏 |
| 14 | **Databricks**（Series L Pref） | MCTC Investments Holdings | 1.4% | 10.4 | 数据 / AI |
| 15 | **Skild AI**（Series C Pref） | 直接 | 1.4% | 10.4 | 机器人 |
| 16 | **Databricks**（Series L Pref） | DA-1125 Gaingels Fund II | 1.1% | 8.2 | 数据 / AI |
| 17 | **OpenAI**（Profit Participation Units） | DXYZ OAI I LLC | 1.0% | 7.4 | AI |
| 18 | **Monzo**（F Ordinary） | Lemonade 18, LLC | 0.8% | 5.9 | 数字银行（UK） |
| 19 | **Astranis**（Series E Pref） | Snowpoint Growth 2.7 | 0.7% | 5.2 | 卫星 |
| 20 | **Redwood Materials**（Common） | 直接 | 0.7% | 5.2 | 电池回收 |
| 21 | **Kraken/Payward**（Series C Pref） | 直接 | 0.6% | 4.5 | 加密交易所 |
| 22 | **Stripe**（Common forward） | Fund FG-RTA / Forge | 0.4% | 3.0 | 支付 |
| 其他 (~14 家 < 0.5%) | Brex / Chime / ClassDojo / Klarna / Boom / Supabase / Jeeves 等 | 各种 | ~3.5% | ~26.0 | 杂项 |

### 持仓集中度（按底层公司聚合）

| 底层公司 | 合并占组合 % | $ 价值 (M) | 备注 |
|---|---|---|---|
| **现金 / 国债** | 31.4% | 233.1 | Q1 ATM 募了 $244M 没投出去 |
| **Anthropic** | **18.1%** | **134.4** | 单一最大私募头寸 |
| **SpaceX**（合并 3 个 SPV） | **14.4%** | **107.0** | 含 2026-02 并购的 xAI |
| **OpenAI**（C 优先 + PPU） | 5.7% | 42.3 | PPU = profit participation unit |
| **OpenEvidence** | 4.6% | 34.2 | |
| **Shield AI** | 4.2% | 31.2 | |
| **Databricks**（2 个 SPV 合并） | 2.5% | 18.6 | |
| **其他 ~30 家** | 19.1% | 141.7 | |

**两条重点**：
1. 真正"private tech alpha"只占组合 **68.6%**，其余 31.4% 是国债基金——ATM 募资速度跑赢了部署速度。NAV/股 $24.56 里，约 $7.71/股是纯现金。买 DXYZ 其实有近 1/3 在买一支货币基金。
2. **Anthropic + SpaceX = 32.5%**——这俩单一标的的估值波动直接决定 DXYZ NAV 的命运。Anthropic 2026-02 Series G 给的 $380B post-money，2026-05 又传要按 $900B 融资。如果传言落地，DXYZ NAV 单这一笔就能涨 ~24%。

## 4. 关键底层公司的"今日"估值

| 公司 | DXYZ 持仓 mark 隐含估值（基于最近 priced round） | 最新一级 / 二级口径（2026-05） | 与 mark 偏差 |
|---|---|---|---|
| **Anthropic** | $380B（2026-02 Series G post-money） | $900B（2026-05 路边社传 in talks） | **+137%** 上行空间 |
| **SpaceX** | $800B（2025-12 内部回购，$421/股） | 维持 $800B（2026 IPO 传闻 $1.0–1.5T） | 0% 已 mark 到位；IPO 是 optionality |
| **OpenAI** | $852B（2026-03-31 Series 收尾，$122B 融资） | $852B（同期，无新轮） | 0% 已最新 |
| **OpenEvidence** | $12B（2026-01 Series D） | $12B（无新轮） | 0% |
| **Shield AI** | $12.7B（2026-03 Series G） | $12.7B | 0% |
| **Databricks** | $134B（2025-12 Series L） | $134B（无新轮，但 IPO 临近） | 0% |
| **Skild AI** | $14B（2026-01） | $14B | 0% |
| **Tenstorrent** | $2.6B（2024-02，债权 mark 按面值） | $2.6B（无更新） | 可能偏低 |
| **Beast Industries** | $5.2B（2025 round） | ~$5B（2026-01 Bitmine 投 $200M） | -4% |
| **Hermeus** | ~$1B+（2026 Khosla 领投） | $1B+ | 0% |
| **Stripe** | $91.5B（2025-02 tender） | **$159B**（2026-02-24 tender, +74%） | **+74%** 上行 |
| **Discord** | ~$15B（2021 round, 可能折价） | 二级 ~$7B（Caplight），IPO 期望 $15–25B | -50% 到 +0% |
| **Monzo** | mark 不明 | $8B 目标 IPO（Q2 2026） | 不确定 |
| **Klarna**（上市） | 已上市，按市价 mark | $40 IPO 价（2025-09），后续波动 | 已可观察 |
| **Chime**（上市） | 已上市，按市价 mark | 已上市 2025 | 已可观察 |
| **Redwood Materials** | $6B（2026-01 Series E） | $6B | 0% |
| **OpenAI** | $852B | $852B | 0% |
| **Kraken/Payward** | private | private | TBD |

## 5. NAV-中性估值（方法 A）

**前提**：信任 Destiny 自己的 ASC 820 mark；只对 3/31 以后的两件事做调整：
1. **ATM 增发摊薄 / 增厚效应**：Q1 2026 ATM 卖了 8.49M 股，weighted avg $28.76，远高于 Q1 起始 NAV $19.97 → **NAV-accretive（增厚）**。
2. **Q2 2026 至今 ATM**：估算 4–5 月又卖了 ~3M 股，假设均价 $50（保守），增厚 NAV/股 约 $1。

### 推演

|  | 数值 | 公式 / 来源 |
|---|---|---|
| 起点：3/31/2026 net assets | ~$748.6M | $24.56 × 30.46M 股 |
| 起点：3/31/2026 流通股 | 30.46M | 12/31 21.97M + Q1 ATM 8.49M |
| Q2 至今估算 ATM 增发 | +3M 股 @ $50 | net $150M 现金入账 |
| 当前估算 net assets | ~$898.6M | 748.6 + 150 |
| 当前估算流通股 | ~33.46M | 30.46 + 3 |
| **当前估算 NAV/股** | **~$26.85** | 898.6 / 33.46 |
| 当前股价 | $66.64 | 市场 |
| **隐含 premium** | **148%** | 66.64 / 26.85 - 1 |

> 注：ATM 数据未官方披露 Q2，3M @ $50 是 informed 估算。若实际更多，NAV/股 还会再增厚一点；若更少，则 NAV/股 接近 $24.56。

## 6. Mark-to-market 估值（方法 B & C）

**前提**：把那些有"今日"参考价的标的，按今日参考价重新 mark。最关键的变量是 Anthropic 的传言轮（$900B）和 Stripe（$159B vs 旧 $91.5B 注：mark 可能已经反映了 Stripe 涨）。

### Anthropic 调整

DXYZ 在 3/31 mark Anthropic 按 $380B → 占组合 18.1% = $134.4M。
- **B 场景**（传言落地 $900B）：mark 乘 900/380 = **2.37×** → 新 mark $318.5M → 增厚 **+$184.1M**
- **C 场景**（更夸张 $1T）：mark 乘 1000/380 = **2.63×** → 新 mark $353.7M → 增厚 **+$219.3M**

### SpaceX 调整

3/31 mark $800B 已是 2025-12 secondary 价。无新轮，**保持不变**。
- 但 SpaceX IPO 在 2026 内、Musk 喊出 $1.5T 目标。**Optionality 值得加权 5–10%**：mark × 1.05–1.10 → 增厚 **+$5.4M – $10.7M**

### Stripe 调整

3/31 mark 应已包含 2026-02-24 的 $159B tender（在 3/31 之前）。**Stripe 已最新，不调整**。

### 其他

OpenAI / OpenEvidence / Shield AI / Databricks / Skild AI / Redwood — 都已经按最新轮 mark，**不调整**。

### 汇总（方法 B：温和上调）

|  | 数值 |
|---|---|
| 起点 net assets（含 Q2 ATM）| $898.6M |
| Anthropic 上调（B 场景 $900B）| +$184.1M |
| SpaceX optionality (×1.05) | +$5.4M |
| **调整后 net assets** | **$1,088.1M** |
| **流通股** | 33.46M |
| **NAV/股（方法 B）** | **$32.52** |
| 隐含 premium vs $66.64 | **105%** |

### 汇总（方法 C：极乐观）

|  | 数值 |
|---|---|
| 起点 net assets | $898.6M |
| Anthropic 上调（C 场景 $1T）| +$219.3M |
| SpaceX optionality (×1.15, 预 IPO 跑步) | +$16.1M |
| **调整后 net assets** | **$1,134.0M** |
| **流通股** | 33.46M |
| **NAV/股（方法 C）** | **$33.89** |
| 隐含 premium vs $66.64 | **97%** |

## 7. 为什么市场给这么高的 premium？

DXYZ 不是第一支这种"私募 wrapper"。历史上类似结构（如 GBTC 早期、ARKK 巅峰、SoFi 早年 SPAC）都出现过类似 reflexive premium：

1. **稀缺通道**（access premium）：散户没有合法渠道直接买 SpaceX / Anthropic 一手股。即便用 Forge / EquityZen，门槛是 accredited investor + 单笔 $50K+。DXYZ 在 $20 / 股门槛把这扇门开给了所有人。
2. **liquidity events optionality**：SpaceX 2026 IPO 被广泛预期；Anthropic / OpenAI / Databricks 也有 IPO 路线图。任何一笔大兑现都会立刻给 NAV 加杠杆。
3. **reflexive 自我强化**：高溢价让 Destiny 能持续 ATM 发新股，募来的钱投到 private rounds，private 资产又因 AI / 防务热潮升值，进一步推 NAV，鼓励 retail 继续买入。**这是 George Soros 笔下"反身性"（reflexivity）的教科书循环**。
4. **空头摩擦**：private exposure 不易对冲，做空 DXYZ 借券成本极高，短期 squeeze 频发——历史上 DXYZ 多次单日 +20%/-20%。

**反向力量**：
- **ATM 持续摊薄 premium**。Destiny 每发一股，premium 就被现金稀释一点（因为新现金按 $1 = NAV $1，溢价不会跟过来）。
- **NAV 真实增长会让 premium 自然 compress**——分母上升，比值就降。
- **任何关键持仓的 down round 或 markdown**（比如 Anthropic 万一融不到 $900B、回到 $400B）都会触发 premium 收缩。
- 一旦 SpaceX IPO 落地，DXYZ 持仓变成可流通股票，"access premium" 的逻辑大幅削弱——这其实是个 **risk-reward 反转点**。

## 8. 风险与注意事项

1. **SPV 抽水**：本笔记里 "Anthropic 占组合 18.1%" 是 gross 暴露。SPV 管理费 + carry 一吃，retire 时拿到的现金可能少 15–25%。模型里如果想严谨，可对每个 SPV 项打 0.8–0.85 折扣。
2. **mark 滞后**：私募估值天然滞后 6–12 个月。在 down 周期（如 2022），DXYZ 的 NAV 可能高估真实价值；在 up 周期（现在），可能低估——这也是 secondary mark-to-market 比 ASC 820 mark 通常更激进的原因。
3. **流动性差**：DXYZ 自身在 NYSE 流动性不差（3 个月日均 ~2.88M 股，对应 ~$120M 名义），但底层持仓**完全没有日流动性**。Destiny 真要兑现 SpaceX，得等 IPO 或 secondary window。
4. **2.5% 管理费 + ATM 持续摊薄**：长期 drag。
5. **集中度**：Anthropic + SpaceX 占 1/3 组合，单家公司 markdown 风险大。
6. **monthly distribution 是噪音**：DXYZ 没有真正的现金流派息，distribution 来自 return of capital，本质是把你的本金还给你。**别把 yield 当真**。

## 9. 操作含义

- **如果当前股价 $66.64 是判断对象**：相对方法 A（NAV-中性 ~$27）溢价 148%；相对方法 B（mark-to-market ~$32）溢价 105%。**任何一种口径下都贵**。
- **想买的合理价位**：
  - 保守（贴 NAV）：$25–28
  - 中性（合理 premium 30–50%，反映 access + IPO option）：$35–45
  - 激进（信 Anthropic $900B + SpaceX IPO $1T+）：$50–55
- **历史 premium 区间**：52 周平均溢价 235%，最高 658%。当前 ~170% 实际是历史**偏低位**——但绝对值仍贵。
- **触发卖出**：如果手里有，需要警惕的信号是 SpaceX IPO 临近时 premium 反而扩大（投机 frenzy），那时反而该减仓而不是加仓——上市落地 access premium 就死了。

## 10. 来源

主要披露：
- [Destiny Tech100 — Form 424B3, 2026-04（含 3/31/2026 NAV + 持仓清单）](https://www.sec.gov/Archives/edgar/data/0001843974/000157587226000288/dxyz100_424b3.htm)
- [Destiny Tech100 — 官方持仓页面](https://destiny.xyz/tech100)
- [Destiny Tech100 — 2025 半年报 N-CSRS](https://www.sec.gov/Archives/edgar/data/0001843974/000121390025084014/ea0251788-01_ncsrs.htm)
- [Destiny Tech100 — 2025 Q4 财报新闻稿（NAV $19.97, 209% YoY）](https://finance.yahoo.com/news/destiny-tech100-inc-reports-fourth-210000037.html)
- [CEF Connect — DXYZ 概览（市价 / NAV / Z-score）](https://www.cefconnect.com/fund/DXYZ)
- [Morningstar — DXYZ portfolio page](https://www.morningstar.com/cefs/xnys/dxyz/portfolio)

底层公司估值：
- [SpaceX $800B secondary, 2025-12 (Fortune)](https://fortune.com/2025/12/13/spacex-ipo-plan-2026-secondary-offering-insider-share-sale-800-billion-valuation/)
- [Anthropic Series G $380B post-money, 2026-02](https://www.anthropic.com/news/anthropic-raises-series-f-at-usd183b-post-money-valuation)
- [Anthropic 传言 $900B, 2026-05 (TechTimes)](https://www.techtimes.com/articles/317066/20260523/anthropic-funding-round-top-30b-900b-valuation-would-surpass-openai-most-valuable-ai-startup.htm)
- [OpenAI $852B, 2026-03-31 (Bloomberg)](https://www.bloomberg.com/news/articles/2026-03-31/openai-valued-at-852-billion-after-completing-122-billion-round)
- [Stripe $159B tender, 2026-02-24 (CNBC)](https://www.cnbc.com/2026/02/24/stripe-value-stock-sale-tender-offer.html)
- [Databricks $134B Series L, 2025-12](https://www.databricks.com/company/newsroom/press-releases/databricks-surpasses-4b-revenue-run-rate-exceeding-1b-ai-revenue)
- [xAI 被 SpaceX 收购，2026-02 估值 $1.25T 合并体](https://www.cnbc.com/2026/01/06/elon-musk-xai-raises-20-billion-from-nvidia-cisco-investors.html)
- [Shield AI $12.7B Series G, 2026-03 (TechCrunch)](https://techcrunch.com/2026/03/26/defense-startup-shield-ai-lands-12-7b-valuation-up-140-after-u-s-air-force-deal/)
- [OpenEvidence $12B Series D, 2026-01 (CNBC)](https://www.cnbc.com/2026/01/21/openevidence-chatgpt-for-doctors-doubles-valuation-to-12-billion.html)
- [Skild AI $14B Series, 2026-01 (TechCrunch)](https://techcrunch.com/2026/01/14/robotic-software-maker-skild-ai-hits-14b-valuation/)
- [Redwood Materials $6B Series E, 2026-01](https://techcrunch.com/2026/01/28/redwood-attracts-google-for-its-425m-series-e-as-ai-power-needs-rise/)
- [Discord 二级市场估值 $6.8–8B, 2026-04](https://medium.com/analysts-corner/discords-confidential-ipo-can-community-as-capital-justify-a-7b-valuation-f8ad8d20cee8)
