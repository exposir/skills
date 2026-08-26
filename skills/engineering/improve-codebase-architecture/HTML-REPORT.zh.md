# HTML 报告格式

架构审视渲染为一个自包含的 HTML 文件，放在操作系统临时目录。Tailwind 和 Mermaid 都从 CDN 加载。Mermaid 可靠地处理图状图表；手工 div 和内联 SVG 处理更编辑性的视觉（质量图、横截面）。两者混合使用：不要什么都靠 Mermaid，会显得千篇一律。

## 脚手架

```html
<!doctype html>
<html lang="zh-CN">
  <head>
    <meta charset="utf-8" />
    <title>{{仓库名}} 架构审视</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <script type="module">
      import mermaid from "https://cdn.jsdelivr.net/npm/mermaid@11/dist/mermaid.esm.min.mjs";
      mermaid.initialize({ startOnLoad: true, theme: "neutral", securityLevel: "loose" });
    </script>
    <style>
      /* 小型自定义层，处理 Tailwind 不方便覆盖的东西：
         虚线接缝线、手绘感箭头等 */
      .seam { stroke-dasharray: 4 4; }
      .leak { stroke: #dc2626; }
      .deep { background: linear-gradient(135deg, #0f172a, #1e293b); }
    </style>
  </head>
  <body class="bg-stone-50 text-slate-900 font-sans">
    <main class="max-w-5xl mx-auto px-6 py-12 space-y-12">
      <header>...</header>
      <section id="candidates" class="space-y-10">...</section>
      <section id="top-recommendation">...</section>
    </main>
  </body>
</html>
```

## 页头

仓库名、日期，以及一个紧凑的图例：实线框 = 模块，虚线 = 接缝，红色箭头 = 泄漏，粗黑框 = 深模块。不需要引言段落。直接进入候选。

## 候选卡片

图表承担分量。文字稀疏、朴素，使用（来自 `/codebase-design` skill 的）术语表词汇，不刻意。

每个候选是一个 `<article>`：

- **标题**：简短，命名这次深化（如"折叠 Order 入口管线"）。
- **徽章行**：推荐强度（`Strong` = 翠绿，`Worth exploring` = 琥珀，`Speculative` = 石板灰），外加依赖类别的标签（`in-process`、`local-substitutable`、`ports & adapters`、`mock`）。
- **文件**：等宽字体列表，`font-mono text-sm`。
- **前后对照图**：核心。两列，并排。见下方图表模式。
- **问题**：一句话。哪里疼。
- **解决方案**：一句话。变什么。
- **收益**：子弹列表，每条 ≤6 个字。如"测试只对一个接口"、"定价逻辑不再泄漏"、"删掉 4 个浅包装器"。
- **ADR 标注**（如果适用）：一行，琥珀色框。

不需要解释性段落。如果图表需要一段话来理解，重新画图。

## 图表模式

选适合候选的模式。混合使用。不要每张图看起来一样。多样性本身就是要点。

### Mermaid 图（依赖/调用流的工兵）

当要点是"X 调 Y 调 Z，看这有多乱"时，用 Mermaid 的 `flowchart` 或 `graph`。把它包在 Tailwind 风格的卡片里，让它不像是从天上掉下来的。用 classDef 把泄漏边染红，深模块染黑。序列图适合"before：6 次往返；after：1 次"。

```html
<div class="rounded-lg border border-slate-200 bg-white p-4">
  <pre class="mermaid">
    flowchart LR
      A[OrderHandler] --> B[OrderValidator]
      B --> C[OrderRepo]
      C -.leak.-> D[PricingClient]
      classDef leak stroke:#dc2626,stroke-width:2px;
      class C,D leak
  </pre>
</div>
```

### 手工框和箭头（Mermaid 布局不好使的时候）

模块用带边框和标签的 `<div>` 表示。箭头用绝对定位在相对容器上的内联 SVG `<line>` 或 `<path>` 元素。当你想让"after"图感觉像一个粗边框的深模块、内部变灰时用这个，因为 Mermaid 画不出那种分量。

### 横截面（适合分层浅度）

堆叠水平条（`h-12 border-l-4`）来展示一个调用经过的层级。Before：6 个薄层，每层什么都没做。After：1 个粗条，标注合并后的职责。

### 质量图（适合"接口和实现一样宽"）

每个模块两个矩形：一个表示接口面积，一个表示实现。Before：接口矩形几乎和实现矩形一样高（浅）。After：接口矩形短，实现矩形长（深）。

### 调用图折叠

Before：一组嵌套框表示的函数调用树。After：同一棵树折叠成一个框，现在内部化的调用在框内变淡显示。

## 样式指南

- 偏编辑感，不是企业仪表盘。宽裕的留白。标题可选衬线体（`font-serif` 配合 stone/slate 效果好）。
- 颜色克制：一种强调色（翠绿或靛蓝），加上红色标泄漏、琥珀色标警告。
- 图表控制在约 320px 高，这样 before/after 能舒适地并排，不需要滚动。
- 图表内的模块标签用 `text-xs uppercase tracking-wider`，让它们读起来像示意图，不是 UI。
- 唯一脚本是 Tailwind CDN 和 Mermaid ESM 导入。除此之外报告是静态的：没有应用代码，除了 Mermaid 自身的渲染外没有交互。

## 首要推荐部分

一张更大的卡片。候选名，一句话说为什么，锚链接指向它的卡片。就这些。

## 语气

朴素英语，简洁，但架构名词和动词直接从 `/codebase-design` skill 来。简洁不是偏离术语的借口。

**精确使用：** 模块、接口、实现、深度、深、浅、接缝、适配器、杠杆、局部性。

**绝不替代：** 组件、服务、单元（代替模块）· API、签名（代替接口）· 边界（代替接缝）· 层、包装器（代替模块，当你的意思是模块时）。

**符合风格的措辞：**

- "Order 入口模块浅：接口几乎匹配实现。"
- "定价跨接缝泄漏。"
- "深化：一个接口，一个测试的地方。"
- "两个适配器为接缝提供了理由：生产用 HTTP，测试用内存。"

**收益子弹**用术语表词汇说出增益：*"局部性：bug 集中在一个模块里"*、*"杠杆：一个接口，N 个调用点"*、*"接口缩小；实现吸收了包装器"*。不要写*"更容易维护"*或*"代码更干净"*，因为那些词不在术语表里，也不值得占位置。

不要模棱两可，不要铺垫，不要"值得注意的是……"。如果一个句子可以变成子弹，就变成子弹。如果一个子弹可以砍掉，就砍掉。如果一个词不在 `/codebase-design` 术语表里，在发明新词之前先用一个在的。