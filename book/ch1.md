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

Elements are the basis of document structure. In HTML, the most common elements are easily recognizable, such as `p`, `table`, `span`, `a`, and `div`. Every single element in a document plays a part in its presentation.

元素是文档结构的基础。在 HTML 中，最常见的元素很容易识别，如 `p`, `table`, `span`, `a`, 和 `div`。文档中的每个元素都在其表示中起作用。

### 替换和非替换元素 Replaced and Nonreplaced Elements

Although CSS depends on elements, not all elements are created equally. For example, images and paragraphs are not the same type of element, nor are `span` and `div`. In CSS, elements generally take two forms: replaced and nonreplaced.

虽然 CSS 依赖于元素，但并不是所有的元素都是平等创建的。例如，图像和段落不是同一类型的元素，`span` and `div` 也不是。在 CSS 中，元素通常有两种形式:替换和非替换。

#### Replaced elements

Replaced elements are those where the element’s content is replaced by something that is not directly represented by document content. Probably the most familiar HTML example is the img element, which is replaced by an image file external to the document itself. In fact, img has no actual content, as you can see in this simple example:

被替换的元素是那些元素的内容被文档内容没有直接表示的内容所替换的元素。最熟悉的 HTML 示例可能是 img 元素，它被文档本身外部的图像文件所取代。事实上，img 并没有实际的内容，你可以在这个简单的例子中看到:

```html
<img src="howdy.gif" />
```

This markup fragment contains only an element name and an attribute. The element presents nothing unless you point it to some external content (in this case, an image specified by the src attribute). If you point to a valid image file, the image will be placed in the document. If not, it will either display nothing or the browser will show a “broken image” placeholder.

这个标记片段只包含一个元素名和一个属性。元素不会显示任何内容，除非您将其指向某些外部内容(在本例中，是由 src 属性指定的图像)。如果您指向一个有效的图像文件，则图像将被放置在文档中。如果没有，它将不显示任何内容，或者浏览器将显示一个“损坏的图像”占位符。

Similarly, the input element is also replaced—by a radio button, checkbox, or text input box, depending on its type.

类似地，input 元素也可以替换为单选按钮、复选框或文本输入框，这取决于它的类型。

#### Nonreplaced elements

The majority of HTML elements are nonreplaced elements. This means that their content is presented by the user agent (generally a browser) inside a box generated by the element itself. For example, `<span>hi there</span>` is a nonreplaced element, and the text “hi there” will be displayed by the user agent. This is true of paragraphs, headings, table cells, lists, and almost everything else in HTML.

大多数 HTML 元素是不可替换的元素。这意味着它们的内容由用户代理(通常是浏览器)在元素本身生成的框中显示。例如，`<span>hi there</span>` 是一个不可替换的元素，文本“hi there”将由用户代理显示。这适用于 HTML 中的段落、标题、表格单元格、列表和几乎所有其他内容。

### 元素显示角色 Element Display Roles

In addition to replaced and nonreplaced elements, CSS uses two other basic types of elements: block-level and inline-level. There are many more display types, but these are the most basic, and the types to which most if not all other display types refer. The block and inline types will be familiar to authors who have spent time with HTML markup and its display in web browsers. The elements are illustrated in Figure 1-1.

除了替换和非替换元素外，CSS 还使用了其他两种基本类型的元素:块级和行内级。还有更多的显示类型，但这些是最基本的，也是大多数(如果不是所有)其他显示类型所引用的类型。对于那些花时间研究 HTML 标记及其在 web 浏览器中的显示的作者来说，块类型和内联类型是很熟悉的。这些元素如图 1-1 所示。

//

#### 块级元素 Block-level elements

Block-level elements generate an element box that (by default) fills its parent element’s content area and cannot have other elements at its sides. In other words, it generates “breaks” before and after the element box. The most familiar block elements from HTML are p and div. Replaced elements can be block-level elements, but usually they are not.

块级元素生成一个元素框，该元素框(默认情况下)填充其父元素的内容区域，并且不能在其两侧有其他元素。换句话说，它在元素框之前和之后生成“break”。HTML 中最常见的块元素是 p 和 div。被替换的元素可以是块级别的元素，但通常不是。

List items are a special case of block-level elements. In addition to behaving in a manner consistent with other block elements, they generate a marker—typically a bullet for unordered lists and a number for ordered lists—that is “attached” to the element box. Except for the presence of this marker, list items are in all other ways identical to other block elements.

列表项是块级元素的特殊情况。除了以与其他块元素一致的方式工作外，它们还生成一个标记(通常是无序列表的项目符号和有序列表的数字)，该标记被“附加”到元素框中。除了此标记之外，列表项在其他所有方面都与其他块元素相同。

#### 行内元素 Inline-level elements

Inline-level elements generate an element box within a line of text and do not break up the flow of that line. The best inline element example is the a element in HTML. Other candidates are strong and em. These elements do not generate a “break” before or after themselves, so they can appear within the content of another element without disrupting its display.

内联级元素在一行文本中生成一个元素框，并且不会破坏该行的流。最好的内联元素示例是 HTML 中的 a 元素。这些元素不会在它们自己之前或之后生成“break”，因此它们可以出现在另一个元素的内容中，而不会中断它的显示。

Note that while the names “block” and “inline” share a great deal in common with block- and inline-level elements in HTML, there is an important difference. In HTML, block-level elements cannot descend from inline-level elements. In CSS, there is no restriction on how display roles can be nested within each other. To see how this works, let’s consider a CSS property, display.

请注意，虽然“块”和“内联”的名称与 HTML 中的块级和内联级元素有很多相同之处，但它们之间有一个重要的区别。在 HTML 中，块级元素不能从内联级元素派生。在 CSS 中，对于显示角色之间如何嵌套没有限制。为了了解它是如何工作的，让我们考虑一个 CSS 属性 display。

To see how this works, let’s consider a CSS property, display.

为了了解它是如何工作的，让我们考虑一个 CSS 属性 display。

//

You may have noticed that there are a lot of values, only three of which I’ve even come close to mentioning: block, inline, and list-item. Most of these values will be dealt with elsewhere in the book; for example, grid and inline-grid will be covered in a separate chapter about grid layout, and the table-related values are all covered in a chapter on CSS table layout.

For now, let’s just concentrate on block and inline. Consider the following markup:

```html
<body>
  <p>This is a paragraph with <em>an inline element</em> within it.</p>
</body>
```

Here we have two block elements (`body` and `p`) and an inline element (`em`). According to the HTML specification, `em` can descend from `p`, but the reverse is not true. Typically, the HTML hierarchy works out so that inlines descend from blocks, but not the other way around.

CSS, on the other hand, has no such restrictions. You can leave the markup as it is but change the display roles of the two elements like this:

```css
p {
  display: inline;
}
em {
  display: block;
}
```

This causes the elements to generate a block box inside an inline box. This is perfectly legal and violates no part of CSS. You would, however, have a problem if you tried to reverse the nesting of the elements in HTML:

```html
<em><p>This is a paragraph improperly enclosed by an inline element.</p></em>
```

No matter what you do to the display roles via CSS, this is not legal in HTML.

While changing the display roles of elements can be useful in HTML documents, it becomes downright critical for XML documents. An XML document is unlikely to have any inherent display roles, so it’s up to the author to define them. For example, you might wonder how to lay out the following snippet of XML:

```html
<book>
  <maintitle>Cascading Style Sheets: The Definitive Guide</maintitle>
  <subtitle>Third Edition</subtitle>
  <author>Eric A. Meyer</author>
  <publisher>O'Reilly and Associates</publisher>
  <pubdate>November 2006</pubdate>
  <isbn type="print">978-0-596-52733-4</isbn>
</book>
<book>
  <maintitle>CSS Pocket Reference</maintitle>
  <subtitle>Third Edition</subtitle>
  <author>Eric A. Meyer</author>
  <publisher>O'Reilly and Associates</publisher>
  <pubdate>October 2007</pubdate>
  <isbn type="print">978-0-596-51505-8</isbn>
</book>
```

Since the default value of display is inline, the content would be rendered as inline text by default, as illustrated in Figure 1-2. This isn’t a terribly useful display.

//

You can define the basics of the layout with display:

```css
book,
maintitle,
subtitle,
author,
isbn {
  display: block;
}
publisher,
pubdate {
  display: inline;
}
```

We’ve now set five of the seven elements to be block and two to be inline. This means each of the block elements will be treated much as div is treated in HTML, and the two inlines will be treated in a manner similar to span.

This fundamental ability to affect display roles makes CSS highly useful in a variety of situations. We could take the preceding rules as a starting point, add a few other styles for greater visual impact, and get the result shown in Figure 1-3.

//

Before learning how to write CSS in detail, we need to look at how one can associate CSS with a document. After all, without tying the two together, there’s no way for the CSS to affect the document. We’ll explore this in an HTML setting since it’s the most familiar.

## 1.3 将 CSS 和 HTML 结合在一起 Bringing CSS and HTML Together

I’ve mentioned that HTML documents have an inherent structure, and that’s a point worth repeating. In fact, that’s part of the problem with web pages of old: too many of us forgot that documents are supposed to have an internal structure, which is altogether different than a visual structure. In our rush to create the coolest-looking pages on the web, we bent, warped, and generally ignored the idea that pages should contain information with some structural meaning.

That structure is an inherent part of the relationship between HTML and CSS; without it, there couldn’t be a relationship at all. To understand it better, let’s look at an example HTML document and break it down by pieces:

```html
<html>
  <head>
    <title>Eric's World of Waffles</title>
    <meta http-equiv="content-type" content="text/html; charset=utf-8" />
    <link rel="stylesheet" type="text/css" href="sheet1.css" media="all" />
    <style type="text/css">
      /* These are my styles! Yay! */
      @import url(sheet2.css);
    </style>
  </head>
  <body>
    <h1>Waffles!</h1>
    <p style="color: gray;">
      The most wonderful of all breakfast foods is the waffle—a ridged and cratered slab of home-cooked, fluffy goodness
      that makes every child's heart soar with joy. And they're so easy to make! Just a simple waffle-maker and some
      batter, and you're ready for a morning of aromatic ecstasy!
    </p>
  </body>
</html>
```

The result of this markup and the applied styles is shown in Figure 1-4.

//

Now, let’s examine the various ways this document connects to CSS.

### The link Tag

First, consider the use of the link tag:

```html
<link rel="stylesheet" type="text/css" href="sheet1.css" media="all" />
```

The `link` tag is a little-regarded but nonetheless perfectly valid tag that has been hanging around the HTML specification for years, just waiting to be put to good use. Its basic purpose is to allow HTML authors to associate other documents with the document containing the `link` tag. CSS uses it to link stylesheets to the document; in Figure 1-5, a stylesheet called `sheet1.css` is linked to the document.

These stylesheets, which are not part of the HTML document but are still used by it, are referred to as external stylesheets. This is because they’re stylesheets that are external to the HTML document. (Go figure.)

To successfully load an external stylesheet, `link` must be placed inside the `head` element but may not be placed inside any other element. This will cause the web browser to locate and load the stylesheet and use whatever styles it contains to render the HTML document in the manner shown in Figure 1-5. Also shown in Figure 1-5 is the loading of the external `sheet2.css` via the @import declaration. Imports must be placed at the beginning of the stylesheet that contains them, but they are otherwise unconstrained.

// 1.5

And what is the format of an external stylesheet? It’s a list of rules, just like those we saw in the previous section and in the example HTML document; but in this case, the rules are saved into their own file. Just remember that no HTML or any other markup language can be included in the stylesheet—only style rules. Here are the contents of an external stylesheet:

```css
h1 {
  color: red;
}
h2 {
  color: maroon;
  background: white;
}
h3 {
  color: white;
  background: black;
  font: medium Helvetica;
}
```

That’s all there is to it—no HTML markup or comments at all, just plain-and-simple style declarations. These are saved into a plain-text file and are usually given an extension of .css, as in sheet1.css.

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
