# Codex 开发工具

安装目录：`/Users/levine/Desktop/Asistant`。

## Playwright MCP

- 版本：`@playwright/mcp` 0.0.83。
- 项目配置：`.codex/config.toml`，仅对受信任的本项目生效。
- 程序安装在 `.tools/playwright-mcp`，配置使用本机 Node.js 的绝对路径，避免桌面应用未加载 nvm 时找不到命令。
- 使用本机 Google Chrome，显示浏览器窗口，采用独立的临时浏览器上下文；关闭后不保留登录状态。
- 默认截图等输出保存在 `.playwright-mcp/`。

重新打开本项目中的 Codex 任务后，可直接要求：

> 使用 Playwright 打开应用的本地地址，填写任务表单，提交后检查任务是否出现在看板中。

应用需要先启动；权限和审批测试还需要对应角色的测试账号。

检查配置：

```sh
cd /Users/levine/Desktop/Asistant
codex mcp get playwright --json
```

如果更换 Node.js 安装位置或移动项目，需要更新 `.codex/config.toml` 中的绝对路径。

## Spec Kit

- 版本：`specify-cli` 1.1.2。
- 命令行程序：`.tools/spec-kit/bin/specify`。
- Python 环境：项目内独立虚拟环境，基于本机已有的 Python 3.12.2（`/opt/anaconda3/bin/python`）。
- 项目模板、脚本和工作流：`.specify/`。
- Codex 集成：`.agents/skills/`，共 10 个技能。

在 Codex 对话中使用技能，不要将下面的 `$speckit-…` 输入终端：

1. `$speckit-constitution`：制定项目原则。
2. `$speckit-specify`：描述一个明确功能及验收条件。
3. `$speckit-clarify`：澄清需求中的疑点。
4. `$speckit-plan`：制定技术方案。
5. `$speckit-tasks`：拆解开发任务。
6. `$speckit-analyze`：检查规格、方案和任务的一致性。
7. `$speckit-implement`：执行实现。
8. `$speckit-converge`：检查实现与规格的差距。

也可使用 `$speckit-checklist` 和 `$speckit-taskstoissues`。
初始化仅生成模板；项目原则和功能规格仍需结合实际需求填写。

终端检查：

```sh
cd /Users/levine/Desktop/Asistant
.tools/spec-kit/bin/specify version
.tools/spec-kit/bin/specify integration status --json
```

`.tools/`（运行环境和下载缓存）及 `.playwright-mcp/` 已排除在 Git 提交之外。
`.specify/` 和 `.agents/skills/` 可随项目保存。
Context7 已通过应用插件连接，无需在这里重复配置。

## 安装验证

2026-10-08 已确认 Codex 读取并启用项目的 Playwright MCP 配置，MCP 握手和 25 个工具的发现成功。
通过 MCP 启动 Chrome，在临时页面中填写并提交测试表单，最终页面快照显示 `Created: MCP smoke test`；测试窗口已关闭。
Spec Kit 的 `integration status --json` 返回 `ok`，没有缺失、修改或无效的受管理文件。
