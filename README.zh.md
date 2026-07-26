<p>
  <a href="https://www.aihero.dev/s/skills-newsletter">
    <picture>
      <source media="(prefers-color-scheme: dark)" srcset="https://res.cloudinary.com/total-typescript/image/upload/v1777382277/skills-repo-dark_2x.png">
      <source media="(prefers-color-scheme: light)" srcset="https://res.cloudinary.com/total-typescript/image/upload/v1777382277/skill-repo-light_2x.png">
      <img alt="Skills" src="https://res.cloudinary.com/total-typescript/image/upload/v1777382277/skill-repo-light_2x.png" width="369">
    </picture>
  </a>
</p>

# 写给真正工程师的技能（Skills）

[![skills.sh](https://skills.sh/b/mattpocock/skills)](https://skills.sh/mattpocock/skills)

这是我每天用来做真正工程开发的 agent 技能——而不是 vibe coding。

开发真实的应用程序很难。GSD、BMAD、Spec-Kit 这类方法论试图通过接管整个流程来帮助你。但与此同时，它们剥夺了你的控制权，让流程中出现的 bug 变得难以解决。

这些技能被设计得小巧、易于改造、可自由组合。它们适用于任何模型，并且建立在数十年的工程经验之上。随意折腾它们，把它们变成你自己的。祝使用愉快。

如果你想及时了解这些技能的更新，以及我创建的任何新技能，可以和约 6 万名开发者一起订阅我的 newsletter：

[订阅 Newsletter](https://www.aihero.dev/s/skills-newsletter)

## 快速开始（30 秒安装）

1. 运行 skills.sh 安装器：

```bash
npx skills@latest add mattpocock/skills
```

2. 选择你想要的技能，以及你想把它们安装到哪些编码 agent 上。**请务必勾选 `/setup-matt-pocock-skills`**。

3. 在你的 agent 中运行 `/setup-matt-pocock-skills`。它会：
   - 询问你想使用哪个 issue 追踪器（GitHub、Linear 或本地文件）
   - 询问你在分诊（triage）工单时会使用哪些标签（`/triage` 依赖标签）
   - 询问你希望把我们创建的文档保存在哪里

4. 搞定——你可以开始用了。

## 作为 Claude Code 插件安装

更喜欢即插即用、无需手动维护的安装方式？这些技能也以原生 [Claude Code 插件](https://code.claude.com/docs/en/plugins)的形式发布。插件不会把可编辑的文件复制到你的仓库里，而是将整套技能作为一个托管包安装，当我发布新版本时会自动更新——你是订阅，而不是 fork。

在 Claude Code 内：

```
/plugin marketplace add mattpocock/skills
/plugin install mattpocock-skills@mattpocock
```

或在你的 shell 中：

```bash
claude plugin marketplace add mattpocock/skills
claude plugin install mattpocock-skills@mattpocock
```

然后在每个仓库中运行一次 `/setup-matt-pocock-skills`，与上面的快速开始完全相同。

两种安装方式，两种理念：

- **[skills.sh](https://skills.sh/mattpocock/skills)** 会把技能复制进你的项目，方便你随意修改，变成你自己的东西。
- **插件方式** 则把它们保持为一个只读、始终最新的包，你不需要编辑——如果你只想让我这套技能直接可用并跟随它的演进，这是最佳选择。

> 在用 Codex 或其他 agent？[skills.sh 安装器](https://skills.sh/mattpocock/skills)如今已经可以把这些技能安装到 Codex 和其他符合 Agent-Skills 标准的运行环境中。原生 Codex 插件已在路线图上——参见 [`.agents/adr/0002-ship-as-a-claude-code-plugin.md`](./.agents/adr/0002-ship-as-a-claude-code-plugin.md)。

## 这些技能为什么存在

我构建这些技能，是为了修复我在 Claude Code、Codex 及其他编码 agent 上看到的常见失败模式。

### #1：Agent 没有做我想要的事

> "没有人确切知道自己想要什么"
>
> David Thomas & Andrew Hunt，[《程序员修炼之道》（The Pragmatic Programmer）](https://www.amazon.co.uk/Pragmatic-Programmer-Anniversary-Journey-Mastery/dp/B0833F1T3V)

**问题所在**：软件开发中最常见的失败模式是目标错位。你以为开发者知道你想要什么，然后你看到他们做出来的东西——才意识到对方根本没有理解你。

在 AI 时代这一点毫无二致。你和 agent 之间存在沟通鸿沟。解决办法是一场 **grilling session（拷问式访谈）**——让 agent 就你要构建的东西向你提出详细的问题。

**解决方案**是使用：

- [`/grill-me`](./skills/productivity/grill-me/SKILL.md) —— 用于非代码场景
- [`/grill-with-docs`](./skills/engineering/grill-with-docs/SKILL.md) —— 与 [`/grill-me`](./skills/productivity/grill-me/SKILL.md) 相同，但附带更多好东西（见下文）

这是我最受欢迎的技能。它们帮助你在开工前与 agent 对齐，并深入思考你要做的改动。_每次_要做改动时都用它们。

### #2：Agent 太啰嗦了

> 有了通用语言（ubiquitous language），开发者之间的对话和代码中的表达都源自同一个领域模型。
>
> Eric Evans，[《领域驱动设计》（Domain-Driven Design）](https://www.amazon.co.uk/Domain-Driven-Design-Tackling-Complexity-Software/dp/0321125215)

**问题所在**：在项目初期，开发者和软件的服务对象（领域专家）通常说着不同的语言。

我在 agent 身上也感受到了同样的张力。Agent 通常被直接丢进一个项目里，边干边琢磨那些行话。于是它们用 20 个词表达 1 个词就能说清的事。

**解决方案**是一门共享语言。它是一份帮助 agent 解码项目行话的文档。

<details>
<summary>
示例
</summary>

这是一个 [`CONTEXT.md`](https://github.com/mattpocock/course-video-manager/blob/076a5a7a182db0fe1e62971dd7a68bcadf010f1c/CONTEXT.md) 的示例，来自我的 `course-video-manager` 仓库。下面哪个更好读？

- **之前**："课程某一节（section）里的某个课时（lesson）被'落实'（即在文件系统中分配了位置）时出了问题"
- **之后**："物化级联（materialization cascade）出了问题"

这种简洁会在一个又一个会话中持续带来回报。

</details>

这已内置于 [`/grill-with-docs`](./skills/engineering/grill-with-docs/SKILL.md)。它是一场 grilling session，但同时帮你与 AI 建立共享语言，并把难以解释的决策记录到 ADR 中。

它的威力很难用语言说清。这可能是这个仓库里最酷的一项技术。试试看就知道了。

> [!TIP]
> 共享语言除了减少啰嗦之外还有很多其他好处：
>
> - **变量、函数和文件的命名保持一致**，全部使用共享语言
> - 因此，**代码库对 agent 而言更易于导航**
> - agent 还会**在思考上消耗更少的 token**，因为它掌握了一门更简洁的语言

### #3：代码跑不起来

> "永远迈出小而审慎的步子。反馈的速率就是你的速度上限。永远不要接手过大的任务。"
>
> David Thomas & Andrew Hunt，[《程序员修炼之道》（The Pragmatic Programmer）](https://www.amazon.co.uk/Pragmatic-Programmer-Anniversary-Journey-Mastery/dp/B0833F1T3V)

**问题所在**：假设你和 agent 已经就要构建什么达成一致。可如果 agent _仍然_产出垃圾代码怎么办？

这时该审视你的反馈回路了。如果得不到关于代码实际运行情况的反馈，agent 就是在盲飞。

**解决方案**：你需要一整套常规的反馈回路：静态类型、浏览器访问和自动化测试。

对于自动化测试，红-绿-重构循环至关重要。也就是让 agent 先写一个失败的测试，再让测试通过。这为 agent 提供了稳定一致的反馈，从而产出好得多的代码。

我构建了一个 **[`/tdd`](./skills/engineering/tdd/SKILL.md) 技能**，可以放进任何项目。它鼓励红-绿-重构，并为 agent 提供大量关于好测试与坏测试的指导。

对于调试，我还构建了一个 **[`/diagnosing-bugs`](./skills/engineering/diagnosing-bugs/SKILL.md)** 技能，把最佳调试实践包装成一个简单的循环。

### #4：我们造了一坨大泥球

> "_每一天_都要为系统的设计投入。"
>
> Kent Beck，[《解析极限编程》（Extreme Programming Explained）](https://www.amazon.co.uk/Extreme-Programming-Explained-Embrace-Change/dp/0321278658)

> "最好的模块是深的。它们让大量功能可以通过一个简单的接口访问。"
>
> John Ousterhout，[《软件设计的哲学》（A Philosophy Of Software Design）](https://www.amazon.co.uk/Philosophy-Software-Design-2nd/dp/173210221X)

**问题所在**：大多数用 agent 构建的应用都复杂且难以修改。因为 agent 能极大地提升编码速度，它们同样也在加速软件的熵增。代码库正以前所未有的速率变得越来越复杂。

**解决方案**是一种激进的 AI 驱动开发新思路：认真对待代码的设计。

这一点已内置于这些技能的每一层：

- [`/to-spec`](./skills/engineering/to-spec/SKILL.md) 会在创建 spec 之前，先追问你要触碰哪些模块

而最关键的是，[`/improve-codebase-architecture`](./skills/engineering/improve-codebase-architecture/SKILL.md) 能帮你拯救一个已经变成大泥球的代码库。我建议每隔几天就在你的代码库上跑一次。

### 小结

软件工程的基本功比以往任何时候都更重要。这些技能是我把这些基本功浓缩为可重复实践的最大努力，帮助你交付职业生涯中最好的应用。祝使用愉快。

## 参考

这些技能按一个维度划分——谁可以调用它们。**用户调用（User-invoked）**的技能只有你输入命令时才会触达（例如 `/grill-me`）；它们的职责是编排。**模型调用（Model-invoked）**的技能既可以由你调用，_也_可以在任务匹配时被 agent 自动使用；它们承载可复用的纪律。用户调用的技能可以调用模型调用的技能，但永远不会调用另一个用户调用的技能。

### 工程（Engineering）

我每天用于代码工作的技能。

**用户调用**

- **[ask-matt](./skills/engineering/ask-matt/SKILL.md)** —— 询问哪个技能或流程适合你当前的处境。一个覆盖本仓库所有用户调用技能的路由器。
- **[grill-with-docs](./skills/engineering/grill-with-docs/SKILL.md)** —— 一场 grilling session，同时构建你项目的领域模型，打磨术语，并就地更新 `CONTEXT.md` 和 ADR。
- **[triage](./skills/engineering/triage/SKILL.md)** —— 通过一个由分诊角色组成的状态机推进 issue。
- **[improve-codebase-architecture](./skills/engineering/improve-codebase-architecture/SKILL.md)** —— 扫描代码库寻找可"深化"的机会，以可视化 HTML 报告呈现，然后就你选中的那一项展开拷问。
- **[setup-matt-pocock-skills](./skills/engineering/setup-matt-pocock-skills/SKILL.md)** —— 为工程技能配置本仓库（issue 追踪器、分诊标签、领域文档布局）。在使用其他工程技能之前，每个仓库运行一次。
- **[to-spec](./skills/engineering/to-spec/SKILL.md)** —— 把当前对话转化为一份 spec 并发布到 issue 追踪器。不做访谈——只综合你们已经讨论过的内容。
- **[to-tickets](./skills/engineering/to-tickets/SKILL.md)** —— 把任何计划、spec 或对话拆解为一组曳光弹（tracer-bullet）工单，每张工单声明自己的阻塞边——可以写成本地文件里的文本，也可以是真实追踪器上的原生阻塞链接。
- **[implement](./skills/engineering/implement/SKILL.md)** —— 构建 spec 或一组工单所描述的工作，在预先约定的接缝处驱动 `/tdd`，并在提交前以 `/code-review` 收尾。
- **[wayfinder](./skills/engineering/wayfinder/SKILL.md)** —— 规划一大块超出单个 agent 会话容量的工作，将其组织为 issue 追踪器上由调查工单构成的共享地图——逐一解决它们，直到通往目的地的路径清晰为止。

**模型调用**

- **[prototype](./skills/engineering/prototype/SKILL.md)** —— 构建一个用完即弃的原型来回答某个设计问题——针对状态/逻辑问题构建一个可运行的终端应用，或在同一路由下构建若干可切换的、风格迥异的 UI 变体。
- **[diagnosing-bugs](./skills/engineering/diagnosing-bugs/SKILL.md)** —— 针对疑难 bug 和性能退化的纪律化诊断循环：复现 → 最小化 → 假设 → 插桩 → 修复 → 回归测试。
- **[research](./skills/engineering/research/SKILL.md)** —— 依据高可信度的一手来源调查一个问题，并把发现以带引用的 Markdown 文件形式落到仓库中，以后台 agent 方式运行。
- **[tdd](./skills/engineering/tdd/SKILL.md)** —— 带红-绿-重构循环的测试驱动开发。以一次一个垂直切片的方式构建功能或修复 bug。
- **[domain-modeling](./skills/engineering/domain-modeling/SKILL.md)** —— 主动构建并打磨项目的领域模型——对照术语表挑战术语，用边界场景做压力测试，并就地更新 `CONTEXT.md` 和 ADR。
- **[codebase-design](./skills/engineering/codebase-design/SKILL.md)** —— 设计深模块的共享纪律与词汇：大量行为藏在小接口之后，落位于干净的接缝上，并可通过该接口进行测试。
- **[code-review](./skills/engineering/code-review/SKILL.md)** —— 对自某个固定点以来的 diff 做双轴评审：**标准**（是否遵循仓库的编码规范，外加 Fowler 代码坏味道基线？）和 **Spec**（是否忠实实现了源头的 issue/PRD？），以并行子 agent 运行，互不污染。
- **[resolving-merge-conflicts](./skills/engineering/resolving-merge-conflicts/SKILL.md)** —— 逐块（hunk）处理进行中的 git merge 或 rebase 冲突，依据追溯到双方一手来源的意图来解决，然后完成整个操作——绝不 `--abort`。

### 生产力（Productivity）

通用的工作流工具，不限于代码。

**用户调用**

- **[grill-me](./skills/productivity/grill-me/SKILL.md)** —— 就一个计划或设计接受无情的拷问式访谈，直到决策树的每个分支都被敲定。
- **[handoff](./skills/productivity/handoff/SKILL.md)** —— 把当前对话压缩成一份交接文档，让另一个 agent 能继续这项工作。
- **[teach](./skills/productivity/teach/SKILL.md)** —— 以当前目录作为有状态的教学工作区，跨多个会话教用户一项新技能或新概念。
- **[writing-great-skills](./skills/productivity/writing-great-skills/SKILL.md)** —— 写好和改好技能的参考资料：让一个技能行为可预测的词汇与原则。

**模型调用**

- **[grilling](./skills/productivity/grilling/SKILL.md)** —— 就一个计划、决策或想法对用户展开无情访谈，直到决策树的每个分支都被敲定。是 `grill-me` 和 `grill-with-docs` 背后可复用的循环。

---

<!--
翻译同步信息（勿手动修改）
源文件: README.md
源 blob hash: 8cc79099b6932f274c501e58318db3190fd4662a
源文件最后提交: 66898f6 (2026-07-13)
校验方法: 运行 `git rev-parse HEAD:README.md`，若输出与上面的 blob hash 不一致，说明源文件已更新，需要同步本翻译。
-->
