# 下一阶段 Spec Kit 步骤

版本 0.3；更新于 2026-10-14。本轮核对本地初始化配置、技能、模板和工作流：`.specify/init-options.json` 记载 Spec Kit 1.1.2 + Codex 集成，CLI 文件存在；未联网检查版本、未再次 init。会议与 MN01 足以支持业务规格草案；群能力、权限范围、提醒细节、完整评分表及数据政策继续保留待决。技能入口为 `$speckit-…`，在 Codex 对话中使用，不是终端中的同名可执行命令。

## 当前可开始到哪里

| 项目 | 本轮核对结果 | 结论 |
| --- | --- | --- |
| Spec Kit 初始化 | `.specify/`、模板、Codex 技能及 `.tools/spec-kit/bin/specify` 存在 | 不需要重装或重新初始化 |
| 业务材料 | 需求/决策/MVP/验收已同步到 MN01、E15–E19 | 可以开始宪章和业务规格草案，不需重做整套访谈 |
| 宪章 | `.specify/memory/constitution.md` 仍有 `[PROJECT_NAME]` 等占位符 | 先把现有授权原则写成项目宪章；不代填公司批准日期 |
| 正式功能产物 | `specs/` 仅有 README，无功能 spec/plan/tasks | 尚不能直接运行 tasks；本地 tasks 技能明确要求 spec.md 与 plan.md |
| 扩展及工作流 | 未发现 `.specify/extensions.yml`；内置 full workflow 含 implement | 单步执行，并在每次启动前复核新 hook；不运行完整实现链 |

这次完成文档同步与准备度检查，没有执行 constitution/specify/plan/tasks/implement。当前“可以开始”指开始 Spec Kit 文档流程，开始业务代码仍需用户明确指令。

## 推荐顺序

| 步骤 | 命令/动作 | 输入与输出 | 进入后一步的条件 |
| --- | --- | --- | --- |
| 0 | 查看文字复核和当前决策状态 | 已同步 MN01、E15–E19；仅补具体试点/终审人、群边界、权限范围、规则细节和评价首版范围 | 不重问每日/提前一天、被拒警示、未评价零分等已明确口径 |
| 1 | `$speckit-constitution` | 将经确认的范围、质量、权限、安全及验收原则写入 `.specify/memory/constitution.md` | 真实记录版本和批准状态，不伪造 ratified 日期 |
| 2 | `$speckit-specify` | 以“方案部门先试的项目节点跟进闭环”为首个规格，覆盖业务/技术反馈、改期、群协同目标与人工评价条件项 | 区分业务目标、接口可行性和未决细则，保留证据 ID；不照搬参考技术栈 |
| 3 | `$speckit-clarify` | 只追问会议未解决的高优先级问题，答案同步决策日志；群与评价分别对应 D114、D113 | 相关功能定案前，状态、权限、计时、评价、群与 AI 边界无阻塞歧义 |
| 4 | `$speckit-checklist` | 检查范围、需求质量、权限、异常与验收描述是否完整 | checklist 是需求质量检查，不是执行测试 |
| 5 | `$speckit-plan` | 先比较选型理由与替代方案，再按经确认的方向生成技术 `plan.md`、研究、模型、契约及 quickstart | 相关业务歧义和 D108–D111 的设计决定解决；文档研究不要求先连真实环境，接入另按授权；不能借 research 自批安全决策 |
| 6 | `$speckit-tasks` | 按获批 spec/plan 分解任务、测试与依赖 | 任务只覆盖批准范围，不含暗中增加的后置能力 |
| 7 | `$speckit-analyze` | 检查 spec、plan、tasks 与宪章的一致性 | 阻塞性不一致修正并复查 |
| 8 | `$speckit-implement` | 执行批准任务 | 必须收到开始实现的明确指令；本轮禁止 |

`$speckit-converge` 留到有实现后检查与规格的差距；本轮没有可收敛的业务实现。未授权对外建 Issue 时不运行 taskstoissues。

上述顺序以本地已安装的 [constitution 技能](../../.agents/skills/speckit-constitution/SKILL.md)、[specify 技能](../../.agents/skills/speckit-specify/SKILL.md)和 [tasks 技能](../../.agents/skills/speckit-tasks/SKILL.md) 为当前依据；clarify/checklist/analyze 是本项目建议采用的质量步骤。tasks 技能要求先读取当前功能的 spec.md、plan.md，不能用参考 plan.docx 或本准备文档代替。

## 下一轮可直接使用的提示词

```text
按 Spec Kit 单步推进文档准备：先使用 $speckit-constitution，将 AGENTS.md 已有的质量、权限、安全、验收及当前授权边界写入项目宪章，准确标明批准状态。随后使用 $speckit-specify，为方案部门先试的项目节点跟进闭环编写规格草案。
依据 docs/meetings/2026-10-14/review.md、text-comparison.md 和决策日志 v0.3；覆盖业务/技术反馈、成果确认、改期警示、核心管理提醒、群协同目标和人工评价。项目经理及以上全面查看、每日/提前一天、未申请或被拒警示、未评价零分等已有口径不重问；只保留范围、日历/时刻/提交内容、完整评分表等剩余问题。
保持来源与验收关联；普通群读取、外部数据处理和技术栈不得自行定案。全部仍为文档工作，不进入 implement，不编写业务代码；遇到未决业务或安全事项用明确待决项记录，不为通过模板检查而猜测答案。
```

## 执行边界

- 初步项目文档不等于正式 Spec Kit 产物完成；本轮不改宪章占位模板，不创建虚假的已批准 spec/plan/tasks。
- 执行技能时复核扩展 hooks；当前未发现 `.specify/extensions.yml`。本地 specify 技能通过规格目录与 `.specify/feature.json` 定位功能，创建分支是可选 hook；不为了建规格无故切分支。新 hook 若涉及提交、联网或实现，须遵守该次授权边界。
- specify 的提问数量建议不能成为擅自决定业务或安全规则的理由；未决项过多时按优先级澄清、标明草案及质量检查未通过项，不伪造“规格全部通过”。
- 内置 full workflow 包含 implement，本轮不能通过一键工作流绕过准备阶段边界。
- 技术与安全事项未决时可继续收集依据和比较方案，不得为填满技术模板自行批准。
