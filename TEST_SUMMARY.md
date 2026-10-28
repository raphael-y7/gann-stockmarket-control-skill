# Stage 4 压力测试摘要

> 本摘要依据归档目录中的 `审计过程/test-prompts.json`、`审计过程/test-results.md`、`审计过程/PIPELINE_STATE.md` 整理，并对照本仓库实际文件做了一次结构核查。文中「结果」一节是归档里原有的测试记录，**不是本次重新跑出来的评测**。

## 测试范围

- **skill 数量**：16 个能力单元（`bundle/cards/` 16 张能力卡；`single/` 与 `pack/` 各自的 `references/capabilities/` 也是 16 张）。
- **test-prompts 文件**：1 份（`test-prompts.json`，suite 级、入口级用例）。仓库内现有两处同源副本：`evals/test-prompts.json`（原有）与 `single/gann-stockmarket-control-skill/test-prompts.json`（本次按 skill 归位放置），两者内容逐字节一致。
- **用例总数**：11 例，按类型分布：

| 类型 | 例数 | 说明 |
|---|---|---|
| `should_trigger` | 5 | 完整流程过票、持仓年度体检、亏损排障、盯盘节奏整改、建看盘体系 |
| `should_not_trigger` | 3 | 诱饵题：姊妹技能场景（12 条规则列举）、非能力域（财报价值投资）、近邻流派（缠论画笔） |
| `edge_case` | 3 | 单点量价问题（需证据分级）、点位预测（触发判停）、概念查询 vs 流程任务分界 |
| `output_case` | 0 | 本包**未**附带独立命名的 output_case 用例；输出质量以归档中的「实际输出抽检」2 例代表任务记录代替 |

## 结构检查

本次在仓库内实跑的结构核查结果（可复核）：

- **JSON 可解析性**：仓库内 5 个 `.json` 文件全部可被标准 JSON 解析器读入，0 个失败（`evals/test-prompts.json`、`single/…/test-prompts.json`、`single/…/BUILD_MANIFEST.json`、`pack/BUILD_MANIFEST.json`、`pack/capability-destinations.json`）。用例文件的顶层字段为 `skill` / `version` / `test_cases`，每条用例含 `id` / `type` / `prompt` / `expected_behavior` / `notes`。
- **frontmatter**：`single/gann-stockmarket-control-skill/SKILL.md` 与 `pack/gann-stockmarket-control-skill-router/SKILL.md` 均以 `---` 开头的 YAML frontmatter 起始，含 `name` / `description` / `metadata.cangjie.*`（generated-by、variant、bundle-id 等）。
- **六段完整性**：`bundle/cards/` 的 16 张卡均含 R（原文）/ I（自述）/ A1（书中案例）/ A2（触发）/ E（可执行步骤）/ B（边界）六节，缺段 0 张。
- **其他产物**：`bundle/verified.yaml` 可被 YAML 解析，顶层键为 `schema_version` / `bundle_id` / `book` / `entry` / `router_entry` 等。

## 结果

- skills: 16
- test_json: 1（suite 级用例文件 1 份，仓库内 2 处同源副本）
- 通过情况（取自归档 `test-results.md`，测试时间 2026-10-24，方式为独立子代理盲测 + 实际输出抽检）：
  - 触发盲测：11 例最终 **11 / 11 PASS**。其中例 04（盯盘节奏整改）、例 05（建看盘体系）首测被误路由到姊妹技能 `gann-trend-theory-skill`，修复入口 description 后复测通过；诱饵 3 例（例 06 / 07 / 08）无一误触本入口。
  - 输出抽检：2 例代表任务（量价诊断卡、开单检查卡）**2 / 2 达标**，判停条款（缺项先问不猜值、证据分级不喊单、口径差异显式标注）全部生效。
  - 修复记录落在 A2（description），未改动规则本体（E / B 段），故未回炉阶段 2。
  - 说明：以上为归档中原有的评测记录，本仓库未保存逐例的原始执行日志与评分脚本；除这两类记录外，本包没有其他量化通过率数据。

## 可接入 darwin-skill 的后续动作

- 这 11 条用例可直接作为 **回归样本**：任何一次入口 description、路由表或能力卡改写后，重跑这 11 例即可判断触发精度是否回退，尤其是例 04 / 05（曾失败）与例 06 / 07 / 08（诱饵容错 0 要求）。
- 归档 DIGEST 已给出接入命令：`darwin evolve books/gann-stockmarket-control-skill/` —— 用本用例文件做 ratcheting 自动进化。
- 建议补充的方向（当前缺口，非本次交付）：`output_case` 类型用例尚无独立条目，可把归档中的 2 例输出抽检任务固化为可自动判分的 output_case；同时补记逐例原始输出，便于将来对比而不是只依赖结论表。
