# Matt Pocock Skills

一组由 Claude Code 加载的 agent skill（斜杠命令与行为规范）。Skill 按 bucket（分类目录）组织，由 `/setup-matt-pocock-skills` 为每个仓库生成的配置来消费。

## 术语（Language）

**Issue tracker（问题追踪器）**：
托管一个仓库全部 issue 的工具——GitHub Issues、Linear、本地的 `.scratch/` markdown 约定，或类似东西。`to-tickets`、`to-spec`、`triage`、`qa` 等 skill 都会读写它。
_避免使用_：backlog manager、backlog backend、issue host

**Issue（工作项）**：
**Issue tracker** 中一个被追踪的工作单元——可以是一个 bug、一项任务、一份 spec，或由 `to-tickets` 切出的一个切片。
_避免使用_：ticket（仅在引用外部系统自身的叫法时使用，或用于 **Decision ticket**——见下）

**Decision ticket（决策票）**：
`wayfinder` 的工作单元——`wayfinder:map` 下的一个子 **Issue**，承载一个*问题*，其解决方式是做决策，而不是执行一块构建切片。**decision** 这个限定词用来把它和实现票区分开；`wayfinder` 先引入这个术语，之后简称 "ticket"。

**Triage role（分诊角色）**：
分诊（triage）过程中施加在一个 **Issue** 上的规范化状态机标签（如 `needs-triage`、`ready-for-afk`）。每个角色通过 `docs/agents/triage-labels.md` 映射为 **Issue tracker** 里的真实标签字符串。

## 关系（Relationships）

- 一个 **Issue tracker** 持有多个 **Issue**
- 一个 **Issue** 同一时刻只携带一个 **Triage role**
- 一个 **Decision ticket** 是一个 **Issue**（`wayfinder:map` 的子项）

## 已标记并解决的歧义（Flagged ambiguities）

- "backlog" 曾同时被用来指托管 issue 的*工具*和工具里的*工作集合*——已解决：工具称为 **Issue tracker**；"backlog" 不再作为领域术语使用。
- "backlog backend" / "backlog manager"——已解决：统一并入 **Issue tracker**。

---

<!--
翻译同步信息（勿手动修改）
源文件: CONTEXT.md
源 blob hash: 38f6824216ed1cf487373bc0605474176f1c5d08
源文件最后提交: 7d694b7 (2026-07-13)
校验方法: 运行 `git rev-parse HEAD:CONTEXT.md`，若输出与上面的 blob hash 不一致，说明源文件已更新，需要同步本翻译。
-->
