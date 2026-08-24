Skill 按 bucket（分类目录）组织在 `skills/` 下：

- `engineering/` —— 日常代码工作
- `productivity/` —— 日常非代码工作流工具
- `misc/` —— 保留但很少使用，不晋升（not promoted）
- `personal/` —— 绑定作者个人环境，不晋升
- `in-progress/` —— 尚未达到发布标准的草稿
- `deprecated/` —— 已不再使用

`engineering/` 或 `productivity/`（即**已晋升** bucket）中的每个 skill，都必须在顶层 `README.md` 中有一条引用，并在 `.claude-plugin/plugin.json` 的 `skills` 数组中有一条登记（Claude Code 插件恰好发布已晋升的这套集合）。`misc/`、`personal/`、`in-progress/`、`deprecated/` 中的 skill 不得出现在这两处中的任何一处。

本仓库同时也是自己的单插件 Claude Code marketplace：`.claude-plugin/marketplace.json` 只列出 `mattpocock-skills` 这一个插件。提升发布版本号时，要让 `.claude-plugin/plugin.json` 的 `version` 与 `package.json` 保持同步——Claude 依据插件的 `version` 判断已安装用户何时能看到更新。改动任一清单文件后，运行 `claude plugin validate . --strict`。为什么发 Claude 插件而（暂时）不发 Codex 插件，见 [.agents/adr/0002-ship-as-a-claude-code-plugin.md](./.agents/adr/0002-ship-as-a-claude-code-plugin.md)。

顶层 `README.md` 中每个 skill 条目都必须把 skill 名链接到它的 `SKILL.md`。

每个 bucket 目录各有一个 `README.md`，用一句话描述列出该 bucket 的每个 skill，并将 skill 名链接到它的 `SKILL.md`。已晋升 bucket 的 `README.md` 和顶层 `README.md` 把条目分为**用户调用（User-invoked）**和**模型调用（Model-invoked）**两组；非晋升 bucket 的 `README.md`（`misc/`、`personal/`）使用平铺列表。

`engineering/` 和 `productivity/` 中的 skill 还有一个面向人类的文档页，位于 `docs/<bucket>/<skill-name>.md`（docs 目录树镜像 `skills/` 下这两个 bucket 的结构）。发布的 URL 统一是 `https://aihero.dev/skills-<skill-name>`，与 bucket 无关——docs 路径仅为仓库内部组织方式。当你新增、重命名或改变 `engineering/`、`productivity/` 中某个 skill 的行为时，按照 [.agents/writing-docs.md](./.agents/writing-docs.md) 创建或重新同步它的文档页。非晋升 bucket（`misc/`、`personal/`、`in-progress/`、`deprecated/`）中的 skill **不**配文档页。

每个 `SKILL.md` 要么是用户调用（frontmatter 设 `disable-model-invocation: true`，且 `agents/openai.yaml` 中设 `policy.allow_implicit_invocation: false`，仅人类可触达），要么是模型调用（模型和用户均可触达）。见 [.agents/invocation.md](./.agents/invocation.md)。

[`ask-matt`](./skills/engineering/ask-matt/SKILL.md) 是路由器，映射了每个用户可触达的 skill 以及它们之间的关系。文档页的同步触发条件对它同样适用：每当你新增、重命名、移除一个用户可触达的 skill，或改变它在各流程中的位置时，重新阅读 `ask-matt` 的 `SKILL.md` 并更新它，让地图保持准确——一个它从未提及的新 skill，或一个它仍在路由的旧 skill，就是一个说谎的路由器。

要把所有 skill（重新）链接进本地 harness 的 skill 目录（`~/.claude/skills`、`~/.agents/skills`），运行 `scripts/link-skills.sh`。每个条目都是指回本仓库的符号链接，所以 `git pull` 就能让已安装的 skill 保持最新；新增、移除或重命名 skill 后要重新运行该脚本。

---

<!--
翻译同步信息（勿手动修改）
源文件: AGENTS.md
源 blob hash: 681311eb9cf453d0faddf3aacaec7357e97ba8e9
源文件最后提交: 697d4ce (2026-07-13)
校验方法: 运行 `git rev-parse HEAD:AGENTS.md`，若输出与上面的 blob hash 不一致，说明源文件已更新，需要同步本翻译。
-->
