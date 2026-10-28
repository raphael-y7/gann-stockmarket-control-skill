# Skill 地图 — 江恩股市操盘术（专业解读版）

一张表看清 16 张能力卡各自管哪一步流程、彼此依赖谁、该按什么顺序加载；本文件由 `bundle/verified.yaml` 生成，卡片本体在 `bundle/cards/`。

## 能力总表

| capability_id | slug | 中文标题 | 重要度 | 去向（promoted→独立 skill / router→路由入口） |
|---|---|---|---|---|
| cap.gann-stockmarket-control-skill.readiness-gate | `readiness-gate` | 入市准备与看盘节奏（流程第0步） | high | router → 路由入口 |
| cap.gann-stockmarket-control-skill.tape-reading-workflow | `tape-reading-workflow` | 看盘纪律与月/周/日三图体系（流程第1步） | high | router → 路由入口 |
| cap.gann-stockmarket-control-skill.volume-supply-diagnosis | `volume-supply-diagnosis` | 成交量供求诊断（流程第2步） | critical | router → 路由入口 |
| cap.gann-stockmarket-control-skill.seven-zone-positioning | `seven-zone-positioning` | 七区域阶段定位与极端反向（流程第3步） | high | router → 路由入口 |
| cap.gann-stockmarket-control-skill.stock-type-filter | `stock-type-filter` | 标的类型过滤与轮动（流程第4步） | high | router → 路由入口 |
| cap.gann-stockmarket-control-skill.stock-habits-profile | `stock-habits-profile` | 个股习性档案与安全位置（流程第5步） | high | router → 路由入口 |
| cap.gann-stockmarket-control-skill.strength-weakness-ranking | `strength-weakness-ranking` | 强弱判定与年度名单（流程第6步·选股核心） | critical | router → 路由入口 |
| cap.gann-stockmarket-control-skill.final-top-bottom | `final-top-bottom` | 最终顶底判定（流程第7步） | critical | router → 路由入口 |
| cap.gann-stockmarket-control-skill.low-price-accumulation | `low-price-accumulation` | 低价吸筹股生命周期（流程第7b步·特殊结构） | medium | router → 路由入口 |
| cap.gann-stockmarket-control-skill.pretrade-checklist | `pretrade-checklist` | 开单前12条规则检查（流程第8步·开单闸门） | critical | router → 路由入口 |
| cap.gann-stockmarket-control-skill.capital-stop-loss | `capital-stop-loss` | 资金与止损管理（流程第9步） | critical | router → 路由入口 |
| cap.gann-stockmarket-control-skill.breakout-execution | `breakout-execution` | 突破买卖执行（流程第10步） | critical | router → 路由入口 |
| cap.gann-stockmarket-control-skill.pyramid-plan | `pyramid-plan` | 金字塔顺势递减加仓计划（流程第11步） | high | router → 路由入口 |
| cap.gann-stockmarket-control-skill.event-news-reaction | `event-news-reaction` | 消息贴现判定与事件反应（流程第12步） | high | router → 路由入口 |
| cap.gann-stockmarket-control-skill.portfolio-annual-checkup | `portfolio-annual-checkup` | 持仓年度体检与征兆即卖（流程第13步） | high | router → 路由入口 |
| cap.gann-stockmarket-control-skill.failure-mode-triage-skill | `failure-mode-triage-skill` | 失败模式排障与运作方法辨析（流程第14步·纠错回路） | critical | router → 路由入口 |

**汇总**：16 张能力卡，全部去向为 router（无 promoted 独立 skill）。重要度分布：critical 7 张、high 8 张、medium 1 张。

## 依赖关系

下表取自 `verified.yaml` 的 `also_read` 字段：主卡判定之后，若任务跨域则按此补读 1 张（最多 2 张）。

| 主卡（先读） | 补读（also_read） |
|---|---|
| `readiness-gate` | `tape-reading-workflow`、`failure-mode-triage-skill` |
| `tape-reading-workflow` | `volume-supply-diagnosis`、`readiness-gate` |
| `volume-supply-diagnosis` | `seven-zone-positioning`、`final-top-bottom` |
| `seven-zone-positioning` | `volume-supply-diagnosis`、`final-top-bottom` |
| `stock-type-filter` | `strength-weakness-ranking`、`stock-habits-profile` |
| `stock-habits-profile` | `final-top-bottom`、`breakout-execution` |
| `strength-weakness-ranking` | `stock-type-filter`、`final-top-bottom` |
| `final-top-bottom` | `strength-weakness-ranking`、`breakout-execution`、`seven-zone-positioning` |
| `low-price-accumulation` | `final-top-bottom`、`volume-supply-diagnosis` |
| `pretrade-checklist` | `capital-stop-loss`、`pyramid-plan` |
| `capital-stop-loss` | `pretrade-checklist`、`pyramid-plan` |
| `breakout-execution` | `final-top-bottom`、`capital-stop-loss` |
| `pyramid-plan` | `capital-stop-loss`、`failure-mode-triage-skill` |
| `event-news-reaction` | `volume-supply-diagnosis`、`seven-zone-positioning` |
| `portfolio-annual-checkup` | `final-top-bottom`、`event-news-reaction` |
| `failure-mode-triage-skill` | `pretrade-checklist`、`capital-stop-loss`、`pyramid-plan` |

几条成对强依赖值得注意：`volume-supply-diagnosis` ↔ `seven-zone-positioning`（量价证据必须叠位置才能定性）、`pretrade-checklist` ↔ `capital-stop-loss`（闸门与止损挂法互为前后手）、`final-top-bottom` ↔ `breakout-execution`（结构定方向、突破定执行）。

## 加载顺序

1. **先读入口** `single/gann-stockmarket-control-skill/SKILL.md`（pack 模式下读 `pack/gann-stockmarket-control-skill-router/SKILL.md`）。入口里有常驻核心原则与完整路由表，多数概览类问题读到这里就能答。
2. **按路由表定位主卡**：用用户意图匹配入口路由表的"用户意图"列，加载 `references/capabilities/` 下的 1 张主卡（对应本表 slug）。
3. **需要时补读 1 张**：主卡判完发现任务跨域，按上表 `also_read` 补读 1 张；单次任务最多加载 2 张卡，不要一次把 16 张全读进来。
4. **卡片内按 R/I/A1/A2/E/B 六段读**：E（可执行步骤）与 B（边界）是行动依据，R（原文）只用于核对出处。

流程型复合任务（"帮我把这只票从头到尾过一遍"）按流程步号走：第0步 → 第14步逐段推进，每段只加载当段卡，不要跳步。
