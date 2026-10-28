<h1 align="center">江恩股市操盘术 Skill</h1>

<p align="center">中文 | <a href="README.en.md">English</a></p>

一套可直接使用的 AI skill 工具包——把威廉·D. 江恩《江恩股市操盘术》里的操盘流程，蒸馏成 16 张按流程阶段排列的能力卡：从入市准备、看盘节奏、三图体系，一路走到开单闸门、止损执行、金字塔加仓、持仓体检和亏损排障。

它不是原书摘要，也不是读后感，而是把书中可复用的方法论拆成可触发、可执行、可测试的 skill 模块。

## 这套 skills 能解决什么问题

- 盯盘盯到心态崩、一年交易几十次，却说不清自己到底该按什么节奏看盘、一年该做几笔
- "放量滞涨""缩量下跌"字面都懂，但判断不了这波量到底是主力在吸筹还是在派发，也不知道该等什么信号才算确认
- 想选强势股，手上只有涨跌幅和感觉，缺一条可复现的强弱判定链，也没有"突破上年高点"这种能落成名单的选股法
- 分不清"最终顶部"和"中期调整"，突破多年高点时不知道该追、该等回抽，还是该怀疑是假突破
- 开单前没有闸门：止损随手撤、浮亏越补越多、目标价越设越高，事后只能说一句"当时该按规则来"
- 持仓拿了两三年，说不出该继续拿还是该走的客观信号，只能等消息或等别人喊

## 蒸馏了什么

16 张能力卡，按"先准入、再诊断、后执行"的流程顺序组织：

- **入市与看盘地基**：`readiness-gate`（入市准备与看盘节奏，流程第0步）、`tape-reading-workflow`（看盘纪律与月/周/日三图体系，第1步）
- **供求与阶段诊断**：`volume-supply-diagnosis`（成交量供求诊断，第2步）、`seven-zone-positioning`（七区域阶段定位与极端反向，第3步）
- **选股与位置语境**：`stock-type-filter`（标的类型过滤与轮动，第4步）、`stock-habits-profile`（个股习性档案与安全位置，第5步）、`strength-weakness-ranking`（强弱判定与年度名单，第6步·选股核心）
- **顶底与特殊结构**：`final-top-bottom`（最终顶底判定，第7步）、`low-price-accumulation`（低价吸筹股生命周期，第7b步·特殊结构）
- **开单与执行**：`pretrade-checklist`（开单前12条规则检查，第8步·开单闸门）、`capital-stop-loss`（资金与止损管理，第9步）、`breakout-execution`（突破买卖执行，第10步）、`pyramid-plan`（金字塔顺势递减加仓计划，第11步）
- **持有与纠错**：`event-news-reaction`（消息贴现判定与事件反应，第12步）、`portfolio-annual-checkup`（持仓年度体检与征兆即卖，第13步）、`failure-mode-triage-skill`（失败模式排障与运作方法辨析，第14步·纠错回路）

16 张卡的重要度分布：critical 7 张、high 8 张、medium 1 张。完整对照表（capability_id、slug、重要度、去向、`also_read` 依赖）见 [INDEX.md](./INDEX.md)。

## 两种打包模式：single 与 pack

同一套 16 张能力卡，按两种形态各编译了一次。能力内容完全一致，区别在入口的命名与目录形态。

| | single（单一入口） | pack（compact pack，来源路由入口） |
|---|---|---|
| 可发现入口 | **1 个**：`gann-stockmarket-control-skill` | **1 个**：`gann-stockmarket-control-skill-router` |
| 16 张能力卡放在哪 | 全部在入口的 `references/capabilities/` 里，由入口按路由表按需加载 1–2 张 | 同样全部在 router 的 `references/capabilities/` 里 |
| 晋级为独立 skill 的卡 | 0 张（全部走路由表） | **0 张**——本次编译 16 张全部留在 router 内 |
| 触发方式 | 入口 description 参与匹配，进入后靠路由表分流 | 同左，router 的 description 明确标注为"pack 来源路由入口" |
| 升级维护 | 替换 1 个目录 | 替换 1 个目录 |
| 附带编译清单 | `BUILD_MANIFEST.json` | `BUILD_MANIFEST.json` + `capability-destinations.json` |

> 关于"为什么 pack 没有晋级独立 skill"：本 Bundle 的晋级预算虽为 8，但编译决策把 16 张卡全部判为 router 去向（`promoted_count: 0`），因此两版的可发现入口数实际相同。pack 的价值在分发形态——它额外保留了 `capability-destinations.json`（每张卡的去向裁决），便于团队按需拆分或二次晋级。

### 该装哪一种

按你的工作方式选，**只装一种**：

| 你的工作方式 | 推荐 | 原因 |
|---|---|---|
| 用 DSH / Codex / Claude Code 等有 skills 目录，希望列表干净 | single | 入口名最直白，只占 1 个槽位 |
| 要审阅"这张卡为什么进 router 而不是独立成 skill" | pack | 附带 `capability-destinations.json` 的去向裁决记录 |
| 要分发给多个 agent 或团队，后续可能二次晋级 | pack | 目录形态与分发口径一致，便于按卡拆分 |
| 只想装一次、不想维护多个目录 | single | 升级时只替换 1 个目录 |

> 两版由同一个 Bundle 编译，能力内容一致。**同时安装会重复触发**，请只装一种。

## 效果示例

### 示例 1：连续三周高换手却涨不动，是不是要拉了

**用户问题**

"这只票流通盘 2 亿股，连续三周周换手 8%、12%、15%，股价才涨 2%，量都堆在这儿了，是不是要拉了？"

**skill 如何判断**

- 先过 `volume-supply-diagnosis`：绝对成交量没有意义，必须先换算成换手率口径（成交量 ÷ 流通股本），再看这个量级相对该股常态落在什么分位
- 走量价四象限：放量却推不动价格，落在"高位放量滞涨"格，对应派发预警
- 叠加位置：同一组量价在高位是派发预警，在多年低位可能只是吸筹活跃——这一步要 `seven-zone-positioning` 给位置语境，本卡自己不下结论
- 天量与区间计数：三周累计换手约 17.5%，若股价仍在同一箱体内 5% 级震荡且上下沿未破，标注"吸筹或派发进行中"
- 输出只有"证据强度"，最终确认点交给突破方向

**最终回答示例**

> 先把它换成换手口径看：三周累计约 17.5%，对 2 亿流通盘来说这是很重的量，而股价只走了 2%——典型的"大换手推不动价"，命中高位放量滞涨，方向上是派发预警。但请注意这是**预警**，不是判词：吸筹和派发的最终确认必须等区间突破，光凭量不能定案。另外两个口径要写清楚：单日换手超过 7% 就该警觉，这是点评里引用的经验值，有的股票 7% 就深调、有的 15% 还在涨，得按你手里这只票磨合；"周换手 8/12/15%"和"单日 7%"是两个时间口径，不要混着用。所以现在的动作不是追进去，而是把区间上下沿标出来，等它突破哪边再决定：向上突破且量能跟上才谈进场，向下跌破就按派发处理。

### 示例 2：这笔交易能不能做

**用户问题**

"20 万本金，想 30 元买 2000 股，现在浮盈 5% 了，我打算直接加到满仓，你看行不行？"

**skill 如何判断**

- 进 `pretrade-checklist`，先查输入契约：本金有了、标的和数量有了、入场价有了，但**没有止损价**——缺项先补齐再过闸，不猜值
- 12 关逐条二值判定：规则 1 资本量（单笔最大亏损 ≤ 本金 3~5%，即 6000~10000 元，按现有信息无法核算，因为止损价缺失）；规则 2 止损预设（无止损价 = 不过）；规则 4 浮盈保护（已浮盈 5%，止损该提到保本位）；规则 8 分摊（资金 < 50 万可按点评口径豁免）；规则 9 目标价（若心里已设卖点，删掉，改为看走势变化退出）；规则 10 卖点四问
- 输出只有"通过"或"不通过 + 整改项"，不给"部分通过"

**最终回答示例**

> 先停一步：你没有给止损价，而"没有止损价"在第 2 关就是直接不过，不存在"这次特殊"。先把止损补上，我们再往下走——顺带算一下规则 1：单笔最大亏损要压在 6000~10000 元（本金的 3~5%，这是把原书的 3~5 点换算成 A 股口径的整理者补丁，不是原书原话），按 30 元买 2000 股共 6 万，止损距离最多只能给到 5%~8%，超了就得减数量，而不是放宽止损。第二件事，"加到满仓"这个动作本身要否掉：规则 8 讲的是等量分摊而不是单票打满，浮盈 5% 时正确动作是把止损提到保本位，不是加仓——加仓序列归 `pyramid-plan`，它只允许顺着浮盈方向递减加码，且吸筹/派发区和接近顶底 10% 的区域禁止加。第三，A 股 T+1 下"买入当天止损"不可执行，风险口径要按隔日跳空放宽。所以结论是不通过：先补止损价 → 降数量到风险额度内 → 止损提到保本位，再回来过一遍闸门。

## 这些 skill 是怎么生成出来的

这套 skill 使用 **[cangjie-skill](https://github.com/kangarooking/cangjie-skill)** 的 RIA-TV++ 流水线生成，整个流程分六个阶段：

1. **整书理解（Adler 分析）**——用 Mortimer Adler 的分析阅读法，对全书做结构、解释、批判、应用四步拆解，产出 `BOOK_OVERVIEW.md`
2. **并行提取**——同时派多个专项提取器（框架、原则、案例、反例、术语），从原文中提取候选方法论单元
3. **三重验证筛选**——每个候选必须通过三项检验：书内至少有 2 处独立佐证（V1 来源充分）、能落到可执行步骤（V2 可执行）、能带来任务增益（V3 任务增益）
4. **RIA++ 构造**——按 R（原文引用）/ I（用自己的话重写）/ A1（书中案例）/ A2（未来触发场景）/ E（可执行步骤）/ B（边界与盲点）六个维度结构化
5. **Zettelkasten 链接**——找出能力卡之间的依赖、对比、组合关系，生成能力索引与路由表
6. **触发与输出测试**——为入口设计触发盲测题（含诱饵题：该触发时要触发，不该触发时要沉默或路由走）与输出抽检场景，未通过的回炉重做，回炉后再做回归验证

本次蒸馏有一条特别的约束：本书与已发布的《江恩股市趋势理论》是同一原著的不同中文译本，32 章逐章对应、案例数字相同。因此本书被刻意组织成"操盘全流程 SOP"（按流程步号推进），与那套"按能力域查询"的工具箱区分开，两者互为近邻负例——问"12 条规则是哪 12 条"应路由到那边，问"帮我检查这单"才进这里。

## 测试与验证

本仓库连生成过程的测试材料一起发布：入口级触发与边界用例在各 skill 目录下的 `test-prompts.json` 里（`single/gann-stockmarket-control-skill/test-prompts.json`、`pack/gann-stockmarket-control-skill-router/test-prompts.json`），逐项评分结果见仓库根目录的 [`test-results.md`](./test-results.md)——包含失败与回炉修复的完整过程，不是只留通过记录。

- **触发盲测**：11 例（5 例 should_trigger、3 例 should_not_trigger、3 例 edge），最终 11 / 11 PASS
- **诱饵容错**：3 例跨技能混淆 / 近邻流派 / 非能力域全部正确拦截或路由，无一误触本入口
- **修复记录**：例 04（盯盘节奏整改）、例 05（建看盘体系）首测被误路由到姊妹技能，原因是入口 description 缺情境例句、且与对方"看盘复盘工作流"字面重叠；修复方式是改写入口 description（补情境例句 + 把分工边界细化为"某条规则**是什么**→对方；**建体系、走流程、做体检、按我的情况整改**→本技能），复测两例均正确路由。修复落在 A2 段（description），未改动规则本体（E / B 段），因此无需回炉第二阶段
- **输出抽检**：2 例代表任务（量价诊断卡、开单检查卡）均达标；缺项先问不猜值、证据分级不喊单、口径差异显式标注三项判停条款全部生效

## 仓库结构

```text
gann-stockmarket-control-skill/
├── README.md              ← 你正在看的
├── README.en.md           ← English version
├── LICENSE                ← MIT
├── BOOK_OVERVIEW.md       ← 阶段 0 产出：全书 Adler 分析
├── INDEX.md               ← 阶段 3 产出：skill 总览 + 依赖关系
├── verified.md            ← 通过三重验证的 16 个单元
├── TEST_SUMMARY.md        ← 阶段 4 产出：压力测试摘要
├── CANGJIE_ADAPTATION.md  ← 仓颉适配说明
├── GITHUB_REPO.md         ← 仓库元数据
├── test-results.md        ← 测试结果记录
├── candidates/            ← 阶段 1 产出：原始候选池
│   ├── frameworks.md      ← 框架与方法候选
│   ├── principles.md      ← 原则 / 规则 / 计算候选
│   ├── cases.md           ← 书中案例候选
│   ├── counter-examples.md← 反例与边界候选
│   └── glossary.md        ← 术语候选
├── rejected/              ← 阶段 1.5 产出：被淘汰的单元 + 原因
├── bundle/                ← 编译事实源
│   ├── verified.yaml      ← 能力元数据、判据与去向
│   ├── cards/             ← 能力卡源文件（六段结构）
│   └── book/              ← overview.md + glossary.md
├── single/                ← single 模式（1 个入口 + 全部能力卡）
│   └── gann-stockmarket-control-skill/SKILL.md  ← 入口：触发 + 路由表 + 加载规则
└── pack/                  ← pack 模式（1 个路由入口 + 0 个晋级 skill）
    └── */SKILL.md         ← 1 个 skill（router 入口），附带 test-prompts.json
```

## 如何使用

先把仓库克隆下来：

```bash
git clone https://github.com/raphael-y7/gann-stockmarket-control-skill.git
```

### 装 single（推荐先试这个）

```bash
# macOS / Linux
cp -r gann-stockmarket-control-skill/single/gann-stockmarket-control-skill ~/.agents/skills/
```

```powershell
# Windows
Copy-Item -Recurse .\gann-stockmarket-control-skill\single\gann-stockmarket-control-skill "$env:USERPROFILE\.agents\skills\"
```

### 装 pack

只复制含 `SKILL.md` 的目录，不要把 `pack/` 下的两个 json 一起拷进 skills 目录：

```bash
# macOS / Linux
cd gann-stockmarket-control-skill/pack
cp -r gann-stockmarket-control-skill-router ~/.agents/skills/
```

```powershell
# Windows
$pack = ".\gann-stockmarket-control-skill\pack"
$dest = "$env:USERPROFILE\.agents\skills"
Copy-Item -Recurse -LiteralPath (Join-Path $pack "gann-stockmarket-control-skill-router") -Destination $dest
```

> `~/.agents/skills` 是 DSH 的 skill 目录；用别的 agent 时换成它自己的 skills 目录即可（例如 Claude Code 是 `~/.claude/skills`）。

### 怎么确认装好了

装完问一句"帮我按江恩的 12 条规则检查一下这单能不能做"，看 agent 是否直接进入开单闸门的逐关判定（资本量、止损预设、频率、保本位……），而不是给你一段泛泛的风险提示。装的是 single 时，它会先读入口再按路由表进 `pretrade-checklist` 卡；装的是 pack 时，router 入口做同样的事。

## 来源

- 《江恩股市操盘术》威廉·D. 江恩 著
- 全书 32 章蒸馏为 16 张能力卡

## 声明

本仓库只发布蒸馏后的 skill、索引与规则速查材料，不包含原书 PDF、EPUB、OCR 文件、截图或全书转写稿。能力卡中出现的原文引用仅用于标注方法论出处和保持可审计性。

书中所有数字判据（单笔 3~5 点、换手率 7%、金字塔 100→50→30→20→10、突破外 3 点止损等）都是案例与经验归纳，原书未提供统计回测背书，且多为 1920 年代美股的绝对点数口径，用于 A 股前必须换算为百分比或波动率口径，并在使用时就所用口径作出声明。本仓库内容不构成投资建议。

## License

[MIT](./LICENSE)
