# 第 1 章 CSS 和 Documents CSS and Documents

Cascading Style Sheets (CSS) is a powerful tool that transforms the resentation of a document or a collection of documents, and it has spread to nearly every corner of the web and into many ostensibly non-web environments. For example, Gecko-based browsers use CSS to affect the presentation of the browser chrome itself, many RSS clients let you apply CSS to feeds and feed entries, and some instant message clients use CSS to format chat windows. Aspects of CSS can be found in the syntax used by JavaScript frameworks, and even in JavaScript itself. It’s everywhere!

层叠样式表(Cascading Style Sheets, CSS)是一种强大的工具，它可以转换文档或文档集合的格式，而且它已经扩展到 web 的几乎每个角落，并进入许多表面上没有 web 的环境。例如，基于 gecko 的浏览器使用 CSS 来影响浏览器 chrome 本身的表现，许多 RSS 客户端允许您将 CSS 应用于提要和提要条目，一些即时消息客户端使用 CSS 来格式化聊天窗口。CSS 的各个方面可以在 JavaScript 框架使用的语法中找到，甚至在 JavaScript 本身中也可以找到。到处都是!

## 1.1 Web 风格的简史 A Brief History of (Web) Style

CSS was first proposed in 1994, just as the web was beginning to really catch on. At the time, browsers gave all sorts of styling power to the user—the presentation preferences in Mosaic, for example, permitted all manner of font family, size, and color to be defined by the user on a per-element basis. None of this was available to document authors; all they could do was mark a piece of content as a paragraph, as a heading of some level, as preformatted text, or one of a handful of other element types. If a user configured his browser to make all level-one headings tiny and pink and all level-six headings huge and red, well, that was his lookout.

CSS 最初是在 1994 年提出的，当时 web 刚刚开始流行。当时，浏览器为用户提供了各种样式设置功能——例如，Mosaic 中的表示首选项允许用户在每个元素的基础上定义各种字体、大小和颜色。这些对文档作者都是不可用的;他们所能做的就是将一段内容标记为段落、某个级别的标题、预先格式化的文本或少数其他元素类型之一。如果一个用户配置他的浏览器使所有一级的标题都是小的和粉红色的，而所有六级的标题都是大的和红色的，那么，这就是他的问题了。

It was into this milieu that CSS was introduced. Its goal was to provide a simple, declarative styling language that was flexible for authors and, most importantly, provided styling power to authors and users alike. By means of the “cascade,” these styles could be combined and prioritized so that both authors and readers had a say—though readers always had the last say.

CSS 就是在这种环境中引入的。它的目标是提供一种简单的、声明式的样式语言，这种语言对作者来说是灵活的，最重要的是，它为作者和用户都提供了样式功能。通过“级联”的方式，这些风格可以被组合在一起并按优先级排列，这样作者和读者都有发言权——尽管读者总是拥有最后的发言权。

Work quickly advanced, and by late 1996, CSS1 was finished. While the newly established CSS Working Group moved forward with CSS2, browsers struggled to implement CSS1 in an interoperable way. Although each piece of CSS was fairly simple on its own, the combination of those pieces created some surprisingly complex behaviors. There were also some unfortunate missteps in early implementations, such as the infamous discrepancy in box model implementations. These problems threatened to derail CSS altogether, but fortunately some clever proposals were implemented, and browsers began to harmonize. Within a few years, thanks to increasing interoperability and high-profile developments such as the CSS-based redesign of Wired magazine and the CSS Zen Garden, CSS began to catch on.

工作进展迅速，到 1996 年年底，CSS1 已经完成。当新成立的 CSS 工作组推进 CSS2 时，浏览器却难以以互操作的方式实现 CSS1。尽管每个 CSS 片段本身相当简单，但是这些片段的组合创建了一些令人惊讶的复杂行为。在早期的实现中也有一些不幸的失误，比如 box 模型实现中臭名昭著的差异。这些问题威胁着 CSS 的发展，但幸运的是，一些聪明的建议得以实施，浏览器开始协调起来。在几年之内，由于增强的互操作性和引人注目的发展，例如基于 CSS 的 Wired 杂志的重新设计和 CSS Zen Garden, CSS 开始流行起来。

Before all that happened, though, the CSS Working Group had finalized the CSS2 specification in early 1998. Once CSS2 was finished, work immediately began on CSS3, as well as a clarified version of CSS2 called CSS2.1. In keeping with the spirit of the times, CSS3 was constructed as a series of (theoretically) standalone modules instead of a single monolithic specification. This approach reflected the then-active XHTML specification, which was split into modules for similar reasons.

然而，在这一切发生之前，CSS 工作组已经在 1998 年初确定了 CSS2 规范。CSS2 完成后，立即开始 CSS3 的工作，并将 CSS2 的一个明确版本称为 CSS2.1。为了顺应时代精神，CSS3 被构建为一系列(理论上)独立的模块，而不是单一的单一规范。这种方法反映了当时处于活动状态的 XHTML 规范，出于类似的原因，该规范被划分为多个模块。

The rationale for modularizing CSS3 was that each module could be worked on at its own pace, and particularly critical (or popular) modules could be advanced along the W3C’s progress track without being held up by others. Indeed, this has turned out to be the case. By early 2012, three CSS3 modules (along with CSS1 and CSS 2.1) had reached full Recommendation status—CSS Color Level 3, CSS Namespaces, and Selectors Level 3. At that same time, seven modules were at Candidate Recommenda‐tion status, and several dozen others were in various stages of Working Draft-ness. Under the old approach, colors, selectors, and namespaces would have had to wait for every other part of the specification to be done or cut before they could be part of a completed specification. Thanks to modularization, they didn’t have to wait.

模块化 CSS3 的基本原理是，每个模块都可以按照自己的速度工作，而且特别重要的(或流行的)模块可以按照 W3C 的进度前进，而不会受到其他模块的阻碍。事实上，事实就是如此。到 2012 年初，三个 CSS3 模块(以及 CSS1 和 CSS 2.1)已经达到了完全推荐状态——CSS 颜色级别 3、CSS 名称空间和选择器级别 3。与此同时，有 7 个模块处于候选推荐状态，其他几十个模块处于不同的工作草拟阶段。在旧的方法下，颜色、选择器和名称空间必须等到规范的其他部分完成或删除之后才能成为完整规范的一部分。由于模块化，他们不必等待。

The flip side of that advantage is that it’s hard to speak of a single “CSS3 specification.” There isn’t any such thing, nor can there be. Even if every other CSS module had reached level 3 by, say, late 2016 (they didn’t), there was already a Selectors Level 4 in process. Would we then speak of it as CSS4? What about all the “CSS3” features still coming into play? Or Grid Layout, which had not then even reached Level 1?

这种优势的另一面是，很难谈论一个“CSS3 规范”。“没有这种东西，也不可能有。即使其他所有的 CSS 模块在 2016 年末达到了第 3 级(他们没有)，已经有了第 4 级的选择器。我们会把它称为 CSS4 吗?还有哪些“CSS3”特性仍在发挥作用?或者网格布局，甚至还没有达到一级?

So while we can’t really point to a single tome and say, “There is CSS3,” we can talk of features by the module name under which they are introduced. The flexibility modules permit more than makes up for the semantic awkwardness they sometimes create. (If you want something approximating a single monolithic specification, the CSS Working Group publishes yearly “Snapshot” documents.)

因此，虽然我们不能指着一本大部头说“有 CSS3”，但我们可以通过介绍这些功能的模块名称来谈论它们。这些灵活性模块不仅弥补了它们有时造成的语义上的尴尬。(如果你想要一个近似于单一规范的东西，CSS 工作组每年都会发布“快照”文档。)

With that established, we’re almost ready to start understanding CSS. First though, we must go over markup.

有了这些，我们就可以开始理解 CSS 了。不过，我们必须先检查一下标记。

## 1.2 元素 Elements

### Replaced and Nonreplaced Elements

### Element Display Roles

## 1.3 Bringing CSS and HTML Together

### The link Tag

### The style Element

### The @import Directive

### HTTP Linking

### Inline Styles

## 1.4 Stylesheet Contents

### Markup

### Rule Structure

### Vendor prefixing

### Whitespace Handling

### CSS Comments

## 1.5 Media Queries

### Usage

### Simple Media Queries

### Media Types

### Media Descriptors

### Media Feature Descriptors and Value Types

## 1.6 Feature Queries

## 1.7 Summary
