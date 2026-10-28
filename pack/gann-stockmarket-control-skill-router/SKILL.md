---
name: gann-stockmarket-control-skill-router
description: |
  《江恩股市操盘术（专业解读版）》（Truth of the Stock Tape, 1923）pack 来源路由入口：当用户要按江恩操盘术的完整流程做股票投资分析与操盘时使用——建看盘与交易体系、按流程把个股从头过一遍、持仓年度体检、失败模式排查，以及入市准备节奏、三图体系、量价供求诊断、七区域定位、标的类型过滤、个股习性档案、强弱名单选股、最终顶底判定、低价吸筹生命周期、12条规则开单闸门、资金止损、突破执行、金字塔加仓、消息事件反应等 16 个流程阶段（每步内嵌张艺博点评的A股适配）。不适用于：单点概念与单条规则查询（优先路由姊妹技能 gann-trend-theory-skill）、基本面估值建模、日内高频执行、具体点位预测、期货专用细则。
metadata:
  cangjie.generated-by: cangjie-tools v2.5.0
  cangjie.variant: router
  cangjie.bundle-id: bundle.gann-stockmarket-control-skill
  cangjie.capability-count: 16
  cangjie.entrypoint-count: 1
---
# 江恩股市操盘术（专业解读版） — 来源路由入口（compact pack）

## 触发与不触发

**适用**：与本书能力域相关的咨询与任务（见下方路由表的意图列）。
**不适用**：
- 教科书式单点概念问答与基本面估值建模（原书否定账面价值路线）
- 日内高频交易执行与具体未来点位预测（时间周期算法原书未公开且不可检验）
- 期货专有操作细则（棉花/小麦/玉米参数仅作参考域，见 references）
- 姊妹技能 gann-trend-theory-skill 已按能力域覆盖的单点查询场景（本入口承接流程型任务）

## 核心原则（常驻速览，概览类问题读到这里即可回答）

1. 价格由供求决定，量必须相对股本衡量（换手率口径）；大行情前必有长时间吸筹或派发，幅度越大准备时间越长。
2. 趋势=累进的高低序列；月图定位置、周图定主流、日图只择时且警惕假行情。
3. 一单未下先过12条规则：单笔风险3~5点（换算3~5%）、止损单必设不取消不上移、不逆势、有疑虑就退出、不预设目标价。
4. 三大致命错误=过度交易、不下止损单、摊薄亏损；盯盘两年改主意1200次90%是错的——远离市场，紧盯趋势。
5. 卖出弱势股买进强势股；突破上年高点名单法选股；二次新高比首次更安全；突破确立区间+原底（顶）外3点止损。
6. 金字塔只顺浮盈方向递减加码（100→50→30→20→10），趋势启动初期才加，吸筹/派发区与顶底10%区禁加。
7. 消息几乎已被贴现：利好出而价跌=已贴现；消息与图抵触时信图；突发利空先退出现望半小时再定。
8. 1920年代绝对点数参数用于A股前必须归一化；点评A股适配（换手7%警觉、永不满仓、弱势股屏蔽）为本版特色内容。

## 能力路由（先读本表，按意图加载 1 张能力卡）

| 用户意图 | 先读 | 补读/备注 |
|---|---|---|
| 评估自己适不适合入市/有没有资格做交易；我该天天盯盘吗，多久看一次盘合适；帮我制定交易节奏和休整计划 | references/capabilities/readiness-gate-skill.md | references/capabilities/tape-reading-workflow-skill.md、references/capabilities/failure-mode-triage-skill.md |
| 建立江恩式的看盘与记录流程；月线周线日线图各自看什么、以哪个为准；怎样不被盘中波动洗出来 | references/capabilities/tape-reading-workflow-skill.md | references/capabilities/volume-supply-diagnosis-skill.md、references/capabilities/readiness-gate-skill.md |
| 这只票放量不涨/放量滞涨是什么意思；缩量下跌是不是跌不动了；换手率多高算异常；用成交量判断主力在吸筹还是出货 | references/capabilities/volume-supply-diagnosis-skill.md | references/capabilities/seven-zone-positioning-skill.md、references/capabilities/final-top-bottom-skill.md |
| 现在市场处于什么阶段，高位还是低位；是不是过热了该清仓/是不是跌透了能抄底；无消息突然跳空低开说明什么 | references/capabilities/seven-zone-positioning-skill.md | references/capabilities/volume-supply-diagnosis-skill.md、references/capabilities/final-top-bottom-skill.md |
| 次新股能不能买；老蓝筹很多年不动能碰吗；低价股是不是跌不动更安全；怎么跟踪板块轮动选类型 | references/capabilities/stock-type-filter-skill.md | references/capabilities/strength-weakness-ranking-skill.md、references/capabilities/stock-habits-profile-skill.md |
| 帮我给这只票建个研究档案；现在这个价位买安全吗；这只票的历史支撑阻力位在哪 | references/capabilities/stock-habits-profile-skill.md | references/capabilities/final-top-bottom-skill.md、references/capabilities/breakout-execution-skill.md |
| 怎么选出最强的股票；我的票大盘涨它不涨算弱势吗，该不该换；用突破上年高点做一份候选名单 | references/capabilities/strength-weakness-ranking-skill.md | references/capabilities/stock-type-filter-skill.md、references/capabilities/final-top-bottom-skill.md |
| 这是最终顶部还是中期调整；是不是历史大底，能重仓抄底吗；突破十年高点意味着什么；帮我复盘指数的大结构 | references/capabilities/final-top-bottom-skill.md | references/capabilities/strength-weakness-ranking-skill.md、references/capabilities/breakout-execution-skill.md、references/capabilities/seven-zone-positioning-skill.md |
| 长期横盘的低价股突然放量突破多年高点能追吗；怎么跟踪底部吸筹的大牛股生命周期 | references/capabilities/low-price-accumulation-skill.md | references/capabilities/final-top-bottom-skill.md、references/capabilities/volume-supply-diagnosis-skill.md |
| 帮我按江恩12条规则检查这笔交易能不能做；开仓前需要检查哪些事项；我总管不住手乱开仓怎么办 | references/capabilities/pretrade-checklist-skill.md | references/capabilities/capital-stop-loss-skill.md、references/capabilities/pyramid-plan-skill.md |
| 这笔该用多少仓位、我能承受多大亏损；止损单怎么设、挂了能不能撤；浮盈怎么保护不成亏损 | references/capabilities/capital-stop-loss-skill.md | references/capabilities/pretrade-checklist-skill.md、references/capabilities/pyramid-plan-skill.md |
| 突破了该追吗、买点止损点设哪；假突破怎么防；首次新高和二次新高买哪个 | references/capabilities/breakout-execution-skill.md | references/capabilities/final-top-bottom-skill.md、references/capabilities/capital-stop-loss-skill.md |
| 浮盈了怎么加仓、每次加多少；金字塔加码和摊平有什么区别；什么情况下不能加仓 | references/capabilities/pyramid-plan-skill.md | references/capabilities/capital-stop-loss-skill.md、references/capabilities/failure-mode-triage-skill.md |
| 这个利好/利空消息该买还是该卖；突发利空跳空低开怎么应对；股票分红调整/增发怎么看；财报出来不涨反跌为什么 | references/capabilities/event-news-reaction-skill.md | references/capabilities/volume-supply-diagnosis-skill.md、references/capabilities/seven-zone-positioning-skill.md |
| 帮我的持仓做年度体检；拿了两年了什么时候该卖；高股息/高收益产品安全吗 | references/capabilities/portfolio-annual-checkup-skill.md | references/capabilities/final-top-bottom-skill.md、references/capabilities/event-news-reaction-skill.md |
| 我又亏了，帮我排查错在哪；越跌越补对不对；买断拿长期/对冲两只票行不行；盯盘盯得心态崩了怎么办 | references/capabilities/failure-mode-triage-skill.md | references/capabilities/pretrade-checklist-skill.md、references/capabilities/capital-stop-loss-skill.md、references/capabilities/pyramid-plan-skill.md |

**非能力类查询**：
- 书名/作者/章节/整书概览 → references/overview.md
- 术语解释 → references/glossary.md
- 决策规则速查（不需要原文依据时） → references/cheatsheet.md
- 完整意图与关键词索引（本表未覆盖的意图先查这里） → references/capability-index.md

## 加载规则

- 每次任务先读本文件，再按路由表加载 **1** 张能力卡；任务明确跨域时最多加载 2 张。
- 概览/书名类问题不加载能力卡，用「核心原则」与 overview.md 回答。
- 路由表与 capability-index.md 都无法命中的意图，明确告知超出本书范围，不要硬套。

## 边界与判停

- 用户要求保证盈利或确定点位时：声明本方法论无统计检验、作者自述预测不可证伪，不提供保证。
- 拒绝把1920年代固定点数直接套用于A股；引用时必须标注换算口径为整理者补丁（点评背书）。
- 吸筹/派发判定只作证据强度评估，不得当作确定结论；原文疑误处（(?原文如此)）不得作为规则依据。
- 路由顺序：先查 out_of_scope，再按流程阶段定位加载对应阶段卡；复合任务按"流程走到哪一步"裁决主卡，单次最多加载2张。
