# coverage-audit.md — 原书关键任务 → 候选 → 判定 → 实际交付去向

> 基准：BOOK_OVERVIEW.md「原书关键任务清单」（独立于旧 verified 制定）
> 审计轮次：阶段 1.5 完成后（2026-10-24）

| task_id | 读者任务 | 候选来源 | 判定 | 最终去向 |
|---|---|---|---|---|
| task-01 | 入市准备与看盘节奏 | f01~f06, p001~p004/016/017, c11/c12, x30/x35 | verified | cap-01 readiness-gate |
| task-02 | 开单前全套规划（12条规则） | f07/f08, p018~p035/046, c13~c15, x01/x02/x25/x29/x37 | verified | cap-02 pretrade-checklist |
| task-03 | 止损与单笔风险上限 | f09/f10, p015/019~p023/123/124, c13, x02/x03 | verified | cap-03 capital-stop-loss |
| task-04 | 金字塔加仓计划 | f12/f13, p039/p040/133/141, c81, x24 | verified | cap-04 pyramid-plan（方法辨析部分归 cap-16） |
| task-05 | 成交量供求诊断 | f23~f25, p005/048/049/062/095/096/147, c24~c26/c33~c35/c60/c88 | verified | cap-05 volume-supply-diagnosis |
| task-06 | 七区域阶段定位 | f27/f28, p050~p053/136/137, c27/c28/c84 | verified | cap-06 seven-zone-positioning |
| task-07 | 个股习性档案与安全位置 | f29, p054~p061/080/081, c29/c30/c32/c41, x26/x39 | verified | cap-07 stock-habits-profile |
| task-08 | 标的类型过滤 | f30/f31, p029/065~p077/088/089, c36~c38/c42/c43/c55, x14/x15/x36 | verified | cap-08 stock-type-filter |
| task-09 | 强弱判定与年度名单 | f32~f35, p078~p086/106~109, c46/c47/c52/c67/c68, x31 | verified | cap-09 strength-weakness-ranking |
| task-10 | 最终顶底判定 | f36~f38/f40, p087~p092/104/105/110~115/144, c48/c49/c56~c58/c69/c70, x13/x19/x32 | verified | cap-10 final-top-bottom |
| task-11 | 突破买卖执行 | f41/f42, p061/093/099/100/112/144/145, c59~c63, x16/x23/x27 | verified | cap-11 breakout-execution |
| task-12 | 消息与事件反应 | f43~f45, p007~p014/101~104/132/135, c04~c08/c10/c19/c64/c65/c71, x20/x21/x22 | verified | cap-12 event-news-reaction；周一节律(f46/p008/p011部分)降为 reference（时代参照，点评明示勿套用） |
| task-13 | 低价吸筹生命周期 | f39, p114~p116, c59, x16 | verified | cap-13 low-price-accumulation |
| task-14 | 看盘纪律与三图体系 | f20~f22, p004/046/047/071~075/131/142/143, c02/c44, x12/x13 | verified | cap-14 tape-reading-workflow |
| task-15 | 持仓年度体检 | f47, p117~p121/044部分, c74~c77, x34 | verified | cap-15 portfolio-annual-checkup |
| task-16 | 失败模式诊断 | f11/f13/f14/f19, p024/036/037/038/041~p045/122, x01~x09/x11/x17/x24/x26/x28/x29/x37/x38, c16~c18/c21/c22/c80 | verified | cap-16 failure-mode-triage-skill |
| task-17 | 期货专用细则（降权） | f49/f50, p125~p130/p134/p135(部分)/p138~p141/p147/p148, c79/c82~c89 | reference | Bundle book/overview 参考区 + DIGEST 期货节选；不出能力卡 |

## 覆盖结论

- 17 项任务全部有去向；critical 级（task-01~05/09/10/11/16）逐项复核候选与原文位置，无缺口。
- 姊妹书差异化核对：gann-trend-theory-skill 已覆盖主题（止损/吸筹派发/七区域/强弱/12规则/金字塔/消息贴现/看盘工作流/失败排障/年度体检）在本书中以"流程阶段卡 + 张艺博A股适配 + 本版译笔参数"呈现，编译为 single 单入口（阶段 1.6 决定），两入口互为近邻负例（见 destinations.json 与 A2 边界）。
- 原文疑误处（"1930年工业股""1898—1960年""11美元"等 (?原文如此)）未作为规则依据使用。
