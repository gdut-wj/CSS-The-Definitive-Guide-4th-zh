# 第 7 章 基本的视觉格式化 Basic Visual Formatting

This chapter is all about the theoretical side of visual rendering in CSS. Why is that necessary? The answer is that with a model as open and powerful as that contained within CSS, no book could hope to cover every possible way of combining properties and effects. You will undoubtedly go on to discover new ways of using CSS. In exploring CSS, you may encounter seemingly strange behaviors in user agents. With a thorough grasp of how the visual rendering model works, you’ll be better able to determine whether a behavior is a correct (if unexpected) consequence of the rendering engine CSS defines.

本章是关于 CSS 中可视化渲染的理论部分。为什么有这个必要?答案是，有了像 CSS 中所包含的那样开放和强大的模型，没有一本书能够涵盖所有可能的组合属性和效果的方法。毫无疑问，您将继续探索使用 CSS 的新方法。在研究 CSS 时，您可能会在用户代理中遇到一些看似奇怪的行为。通过对可视化呈现模型如何工作的深入了解，您将能够更好地确定一个行为是否是呈现引擎 CSS 定义的正确(如果未预料到)结果。

## 7.1 Basic Boxes

At its core, CSS assumes that every element generates one or more rectangular boxes, called element boxes. (Future versions of the specification may allow for nonrectangular boxes, and indeed there have been proposals to change this, but for now everything is rectangular.) Each element box has a `content area` at its center. This content area is surrounded by optional amounts of padding, borders, outlines, and margins. These areas are considered optional because they could all be set to a width of zero, effectively removing them from the element box. An example content area is shown in Figure 7-1, along with the surrounding regions of padding, borders, and margins.

在其核心，CSS 假设每个元素生成一个或多个矩形框，称为元素框。(规范的未来版本可能允许使用非矩形框，确实有人建议对此进行更改，但目前所有内容都是矩形的。)每个元素框的中心都有一个内容区域。这个内容区域被可选的填充、边框、轮廓和边距包围。这些区域被认为是可选的，因为它们都可以设置为宽度为 0，从而有效地将它们从元素框中移除。图 7-1 显示了一个示例内容区域，以及周围的填充、边框和边距区域。

Each of the margins, borders, and the padding can be set using various side-specific properties, such as `margin-left` or `border-bottom`, as well as shorthand properties such as `padding`. The outline, if any, does not have side-specific properties. The content’s background—a color or tiled image, for example—is applied within the padding by default. The margins are always transparent, allowing the background(s) of any parent element(s) to be visible. Padding cannot have a negative length, but margins can. We’ll explore the effects of negative margins later on.

每个边距、边框和内边距都可以使用各种特定于边的属性进行设置，如左边框或边框-底部，以及内边距等简写属性。大纲(如果有的话)没有特定于边的属性。内容的背景(例如，颜色或平铺图像)默认应用于填充内。页边距总是透明的，允许任何父元素的背景都是可见的。填充不能有负长度，但是空白可以。稍后我们将探讨负边距的影响。

// 7-1

Borders are generated using defined styles, such as `solid` or `inset`, and their colors are set using the `border-color` property. If no color is set, then the border takes on the foreground color of the element’s content. For example, if the text of a paragraph is white, then any borders around that paragraph will be white, `unless` the author explicitly declares a different border color. If a border style has gaps of some type, then the element’s background is visible through those gaps by default. Finally, the width of a border can never be negative.

边框是使用已定义的样式生成的，如实体或 inset，它们的颜色是使用 border-color 属性设置的。如果没有设置颜色，则边框采用元素内容的前景色。例如，如果一个段落的文本是白色的，那么该段落周围的任何边框都是白色的，除非作者明确声明了不同的边框颜色。如果边框样式有某种类型的空白，则默认情况下元素的背景可以通过这些空白显示。最后，边框的宽度不能为负。

The various components of an element box can be affected via a number of proper‐ ties, such as `width` or `border-right`. Many of these properties will be used in this book, even though they aren’t defined here.

一个元件盒的各个部件可以通过一些合适的参数受到影响，如宽度或边界右侧。这些属性中有许多将在本书中使用，尽管它们在这里没有定义。

### 7.1.1 A Quick Refresher

Let’s quickly review the kinds of boxes we’ll be discussing, as well as some important terms that are needed to follow the explanations to come:

让我们快速回顾一下我们将要讨论的方框的类型，以及接下来的解释中需要用到的一些重要术语:

`Normal flow`

This is the left-to-right, top-to-bottom rendering of text in Western languages and the familiar text layout of traditional HTML documents. Note that the flow direction may be changed in non-Western languages. Most elements are in the normal flow, and the only way for an element to leave the normal flow is to be floated, positioned, or made into a flexible box or grid layout element. Remember, the discussions in this chapter cover only elements in the normal flow.

这是西方语言中从左到右、从上到下的文本呈现，是传统 HTML 文档中常见的文本布局。注意，在非西方语言中，流的方向可能会改变。大多数元素都在常规流中，元素离开常规流的惟一方法是浮动、定位或做成一个灵活的盒子或网格布局元素。请记住，本章的讨论只涉及正常流程中的元素。

`Nonreplaced element`

This is an element whose content is contained within the document. For example, a paragraph (`p`) is a nonreplaced element because its textual content is found within the element itself.

这个元素的内容包含在文档中。例如，段落(p)是不可替换的元素，因为它的文本内容是在元素本身中找到的。

`Replaced element`

This is an element that serves as a placeholder for something else. The classic example of a replaced element is the `img` element, which simply points to an image file that is inserted into the document’s flow at the point where the `img` element itself is found. Most form elements are also replaced (e.g., `<input type="radio">`).

这是一个元素，用作其他内容的占位符。被替换元素的典型示例是 img 元素，它简单地指向一个图像文件，该文件被插入到文档流中找到 img 元素本身的地方。大多数表单元素也被替换（例如 `<input type="radio">`）

`Root element`

This is the element at the top of the document tree. In HTML documents, this is the element `html`. In XML documents, it can be whatever the language permits; for example, the root element of RSS files is `rss`.

这是文档树顶部的元素。在 HTML 文档中，这是元素 HTML。在 XML 文档中，它可以是语言允许的任何内容;例如，RSS 文件的根元素是 RSS。

`Block box`

This is a box that an element such as a paragraph, heading, or `div` generates. These boxes generate “new lines” both before and after their boxes when in the normal flow so that block boxes in the normal flow stack vertically, one after another. Any element can be made to generate a block box by declaring `display: block`.

这是一个由段落、标题或 div 等元素生成的框。在正常流中，这些框会在它们的框之前和之后生成“新行”，以便垂直地一个接一个地阻塞正常流堆栈中的框。任何元素都可以通过声明 `display: block` 来生成一个块框。

`Inline box`

This is a box that an element such as `strong` or `span` generates. These boxes do not generate “line breaks” before or after themselves. Any element can be made to generate an inline box by declaring `display: inline`.

这是一个由诸如 strong 或 span 之类的元素生成的方框。这些框不会在它们自己之前或之后生成“换行符”。任何元素都可以通过声明 `display: inline` 来生成内联框。

`Inline-block box`

This is a box that is like a block box internally, but acts like an inline box externally. It acts similar to, but not quite the same as, a replaced element. Imagine picking up a `div` and sticking it into a line of text as if it were an inline image, and you’ve got the idea.

这是一个内部类似于块盒，但在外部充当内联盒的盒子。它的作用与被替换的元素类似，但又不完全相同。想象一下，拿起一个 div，把它插入到一行文本中，就好像它是一个内联图像一样，你就明白了。

There are several other types of boxes, such as table-cell boxes, but they won’t be covered in this book for a variety of reasons—not the least of which is that their complexity demands a book of its own, and very few authors will actually wrestle with them on a regular basis.

有几种其他类型的盒子,例如表格单元框,但他们不会为各种各样的理由不覆盖在这本书中最小的就是它们的复杂性要求自己的一本书,和很少有作者会定期与他们搏斗。

### 7.1.2 The Containing Block

There is one more kind of box that we need to examine in detail, and in this case enough detail that it merits its own section: the containing block.

还有一种类型的 box 需要我们详细地研究，在这种情况下，它有足够的细节值得自己的部分:包含块。

Every element’s box is laid out with respect to its containing block; in a very real way, the containing block is the “layout context” for a box. CSS defines a series of rules for determining a box’s containing block. We’ll cover only those rules that pertain to the concepts covered in this book in order to keep our focus.

每个元素的盒相对于其包含块进行布局;以一种非常真实的方式，包含块是一个框的“布局上下文”。CSS 定义了一系列规则来确定一个框的包含块。我们将只讨论那些与本书所涵盖的概念相关的规则，以保持我们的重点。

For an element in the normal, Western-style flow of text, the containing block forms from the content edge of the nearest ancestor that generated a list item or block box which includes all table-related boxes (e.g., those generated by table cells). Consider the following markup:

对于正常的西式文本流中的元素，包含的块形成于最近的祖先的内容边缘，它生成一个列表项或块框，其中包括所有与表相关的框(例如，由表单元格生成的框)。考虑以下标记:

```html
<body>
  <div>
    <p>This is a paragraph.</p>
  </div>
</body>
```

In this very simple markup, the containing block for the `p` element’s block box is the `div` element’s block box, as that is the closest ancestor element box that is a block or a list item (in this case, it’s a block box). Similarly, the `div`’s containing block is the body’s box. Thus, the layout of the `p` is dependent on the layout of the `div`, which is in turn dependent on the layout of the body element.

在这个非常简单的标记中，p 元素的块框的包含块是 div 元素的块框，因为它是块或列表项最接近的祖先元素框(在本例中，它是块框)。类似地，div 的包含块是主体的框。因此，p 的布局依赖于 div 的布局，而 div 又依赖于 body 元素的布局。

And above that, the layout of the `body` element is dependent on the layout of the `html` element, whose box creates what is called the `initial containing block`. It’s unique in that the viewport—the browser window in screen media, or the printable area of the page in print media—determines its dimensions, not the size of the content of the root element. It’s a subtle distinction, and usually not a very important one, but it does exist.

在此之上，body 元素的布局依赖于 html 元素的布局，html 元素的框创建了所谓的初始包含块。它的独特之处在于视图——屏幕媒体中的浏览器窗口，或打印媒体中页面的可打印区域——决定了它的维数，而不是根元素内容的大小。这是一个微妙的区别，通常不是很重要，但它确实存在。

## 7.2 Altering Element Display

You can affect the way a user agent displays by setting a value for the property `display`. Now that we’ve taken a close look at visual formatting, let’s consider the `display` property and discuss two more of its values using concepts from earlier in the book.

可以通过设置属性显示的值来影响用户代理的显示方式。现在我们已经仔细研究了可视化格式化，让我们考虑 display 属性，并使用本书前面的概念讨论它的另外两个值。

//

We’ll ignore the ruby- and table-related values, since they’re far too complex for this chapter, and we’ll also ignore the value `list-item`, since it’s very similar to block boxes. We’ve spent quite some time discussing block and inline boxes, but let’s spend a moment talking about how altering an element’s display role can alter layout before we look at `inline-block`.

我们将忽略与 ruby 和表相关的值，因为它们对于本章来说太复杂了，我们还将忽略值' list-item '，因为它与块框非常相似。我们已经花了相当多的时间来讨论块和内联框，但是让我们花一点时间来讨论在查看“内联块”之前如何改变元素的显示角色来改变布局。

### 7.2.1 Changing Roles

When it comes to styling a document, it’s handy to be able to change the type of box an element generates. For example, suppose we have a series of links in a `nav` that we’d like to lay out as a vertical sidebar:

在设计文档样式时，可以方便地更改元素生成的框的类型。例如，假设我们在一个导航中有一系列的链接，我们想把它们作为一个垂直的边栏:

```html
<nav>
  <a href="index.html">WidgetCo Home</a>
  <a href="products.html">Products</a>
  <a href="services.html">Services</a>
  <a href="fun.html">Widgety Fun!</a>
  <a href="support.html">Support</a>
  <a href="about.html" id="current">About Us</a>
  <a href="contact.html">Contact</a>
</nav>
```

We could put all the links into table cells, or wrap each one in its own `nav`—or we could just make them all block-level elements, like this:

我们可以把所有的链接放到表格单元格中，或者把每个链接都包装在它自己的导航中，或者我们可以让它们都是块级元素，就像这样:

```css
nav a {
  display: block;
}
```

This will make every a element within the navigation `nav` a block-level element. If we add on a few more styles, we could have a result like that shown in Figure 7-2.

这将使导航导航中的每个元素成为块级元素。如果我们再添加一些样式，就会得到如图 7-2 所示的结果。

// 7-2

Changing display roles can be useful in cases where you want non-CSS browsers to get the navigation links as inline elements but to lay out the same links as block-level elements. With the links as blocks, you can style them as you would `div` or `p` elements, with the advantage that the entire element box becomes part of the link. Thus, if a user’s mouse pointer hovers anywhere in the element box, she can then click the link.

当您希望非 css 浏览器将导航链接作为内联元素，而将相同的链接作为块级元素时，更改显示角色非常有用。将链接作为块，您可以像 div 或 p 元素那样对它们进行样式设置，其优点是整个元素框成为链接的一部分。因此，如果用户的鼠标指针停留在元素框中的任何位置，则可以单击链接。

You may also want to take elements and make them inline. Suppose we have an unordered list of names:

您可能还希望获取元素并使它们内联。假设我们有一个无序的名字列表:

```html
<ul id="rollcall">
  <li>Bob C.</li>
  <li>Marcio G.</li>
  <li>Eric M.</li>
  <li>Kat M.</li>
  <li>Tristan N.</li>
  <li>Arun R.</li>
  <li>Doron R.</li>
  <li>Susie W.</li>
</ul>
```

Given this markup, say we want to make the names into a series of inline names with vertical bars between them (and on each end of the list). The only way to do so is to change their display role. The following rules will have the effect shown in Figure 7-3:

对于这个标记，假设我们想要将这些名称变成一系列内联名称，它们之间有竖线(以及列表的两端)。这样做的唯一方法是改变它们的显示角色。以下规则的效果如图 7-3 所示:

```css
#rollcall li {
  display: inline;
  border-right: 1px solid;
  padding: 0 0.33em;
}
#rollcall li:first-child {
  border-left: 1px solid;
}
```

// 7-3

There are plenty of other ways to use display to your advantage in design. Be creative and see what you can invent!

还有很多其他的方法可以让你在设计中充分利用显示器。要有创意，看看你能发明什么!

Be careful to note, however, that you are changing the display role of elements—not changing their inherent nature. In other words, causing a paragraph to generate an inline box does `not` turn that paragraph into an inline element. In HTML, for example, some elements are block while others are inline. (Still others are “flow” elements, but we’re ignoring them right now.) An inline element can be a descendant of a block element, but the reverse is generally not true. While a `span` can be placed inside a paragraph, a `span` cannot be wrapped around a paragraph. This will hold true no matter how you style the elements in question. Consider the following markup:

但是要注意，您正在更改元素的显示角色—而不是更改它们的固有性质。换句话说，使一个段落生成内联框并不会将该段落转换为内联元素。例如，在 HTML 中，一些元素是块，而另一些元素是内联的。(还有一些是“流”元素，但是我们现在忽略了它们。)内联元素可以是块元素的后代，但通常不是。虽然 span 可以放在段落中，但 span 不能包裹在段落中。这将适用于无论您如何样式的元素的问题。考虑以下标记:

```html
<span style="display: block;">
  <p style="display: inline;">this is wrong!</p>
</span>
```

The markup will not validate because the block element (`p`) is nested inside an inline element (`span`). The changing of display roles does nothing to change this. `display` has its name because it affects how the element is displayed, not because it changes what kind of element it is.

由于块元素(`p`)嵌套在内联元素(`span`)中，所以标记将不会生效。改变显示角色并不能改变这一点。`display` 之所以有它的名字，是因为它影响元素的显示方式，而不是因为它改变了元素的类型。

With that said, let’s get into the details of different kinds of boxes: block boxes, inline boxes, inline-block boxes, and list-item boxes

说到这里，让我们来看看不同类型的框的详细信息:块框、内联框、内联块框和列表项框

### 7.2.2 Block Boxes

Block boxes can behave in sometimes predictable, sometimes surprising ways. The handling of box placement along the horizontal and vertical axes can differ, for example. In order to fully understand how block boxes are handled, you must clearly understand a number of boundaries and areas. They are shown in detail in Figure 7-4.

块盒的行为有时是可预测的，有时是令人惊讶的。例如，沿水平轴和垂直轴放置框的处理可能不同。为了完全理解如何处理块盒，您必须清楚地理解许多边界和区域。它们在图 7-4 中详细显示。

By default, the `width` of a block box is defined to be the distance from the left inner edge to the right inner edge, and the `height` is the distance from the inner top to the inner bottom. Both of these properties can be applied to an element generating a block box.

默认情况下，块框的宽度定义为从左内边到右内边的距离，高度定义为从内顶到内底的距离。这两个属性都可以应用于生成块框的元素。

// 7-4

It’s also the case that we can alter how these properties are treated using the property `box-sizing`.

也可以使用属性 `box-sizing` 属性改变这些属性的处理方式。

//

This property is how you change what the `width` and `height` values actually do. If you declare `width: 400px` and don’t declare a value for `box-sizing`, then the element’s content box will be 400 pixels wide; any padding, borders, and so on will be added to it. If, on the other hand, you declare `box-sizing: border-box`, then the element box will be 400 pixels from the left outer border edge to the right outer border edge; any border or padding will be placed within that distance, thus shrinking the width of the content area. This is illustrated in Figure 7-5.

此属性用于更改宽度和高度值的实际作用。如果您声明 `width: 400px`，而没有声明 `box-sizing` 值，那么元素的内容框将是 400 像素宽;任何内边距、边框等都将被添加到其中。另一方面，如果您声明 `box-sizing: border-box`，则元素框将从左外边框边缘到右外边框边缘的距离为 400 像素;任何边框或填充将被放置在该距离内，从而缩小内容区域的宽度。如图 7-5 所示。

// 7-5

We’re talking about the `box-sizing` property here because, as stated, it applies to “all elements that accept `width` or `height` values.” That’s most often elements generating block boxes, though it also applies to replaced inline elements like images, as well as inline-block boxes.

我们在这里讨论 `box-sizing` 属性，因为如前所述，它适用于“接受宽度或高度值的所有元素”。这是最常见的生成块框的元素，尽管它也适用于像图像这样的被替换的内联元素，以及内联块框。

The various widths, heights, padding, and margins all combine to determine how a document is laid out. In most cases, the height and width of the document are automatically determined by the browser and are based on the available display region, plus other factors. With CSS, you can assert more direct control over the way elements are sized and displayed.

不同的宽度、高度、填充和边距组合在一起决定了文档的布局方式。在大多数情况下，文档的高度和宽度由浏览器自动决定，并基于可用的显示区域和其他因素。使用 CSS，您可以对元素的大小和显示方式进行更直接的控制。

### 7.2.3 Horizontal Formatting

Horizontal formatting is often more complex than you’d think. Part of the complexity has to do with the default behavior of `box-sizing`. With the default value of `content-box`, the value given for width affects the `width` of the content area, `not` the entire visible element box. Consider the following example:

```html
<p style="width: 200px;">wideness?</p>
```

This will make the paragraph’s content 200 pixels wide. If we give the element a background, this will be quite obvious. However, any padding, borders, or margins you specify are `added` to the width value. Suppose we do this:

```html
<p style="width: 200px; padding: 10px; margin: 20px;">wideness?</p>
```

The visible element box is now 220 pixels wide, since we’ve added 10 pixels of padding to the right and left of the content. The margins will now extend another 20 pixels to both sides for an overall element box width of 260 pixels. This is illustrated in Figure 7-6.

// 7-6

If we change the styles to use the border box for box-sizing, then the results would be different. In that case, the visible box would be 200 pixels wide with a content width of 180 pixels, and a total of 40 pixels of margin to the sides, giving an overall box width of 240 pixels, as illustrated in Figure 7-7.

// 7-7

In either case, there is a rule that says that the sum of the horizontal components of a block box in the normal flow always equals the width of the containing block. Let’s consider two paragraphs within a `div` whose margins have been set to be `1em`, and whose `box-sizing` value is the default. The content width (the value of `width`) of each paragraph, plus its left and right padding, borders, and margins, always adds up to the width of the `div`’s content area.

Let’s say the width of the `div` is `30em`. That makes the sum total of the content width, padding, borders, and margins of each paragraph 30 em. In Figure 7-8, the “blank” space around the paragraphs is actually their margins. If the `div` had any padding, there would be even more blank space, but that isn’t the case here.

// 7-8

### 7.2.4 Horizontal Properties

The seven properties of horizontal formatting are `margin-left`, `border-left`, `padding-left`, `width`, `padding-right`, `border-right`, and `margin-right`. These properties relate to the horizontal layout of block boxes and are diagrammed in Figure 7-9.

The values of these seven properties must add up to the width of the element’s containing block, which is usually the value of `width` for a block element’s parent (since block-level elements nearly always have block-level elements for parents).

Of these seven properties, only three may be set to `auto`: the width of the element’s content and the left and right margins. The remaining properties must be set either to specific values or default to a width of zero. Figure 7-10 shows which parts of the box can take a value of auto and which cannot.

// 7-9

// 7-10

`width` must either be set to `auto` or a nonnegative value of some type. When you do use `auto` in horizontal formatting, different effects can occur.

### 7.2.5 Using auto

If you set `width`, `margin-left`, or `margin-right` to a value of `auto`, and give the remaining two properties specific values, then the property that is set to `auto` is set to the length required to make the element box’s width equal to the parent element’s width. In other words, let’s say the sum of the seven properties must equal 500 pixels, no padding or borders are set, the right margin and width are set to `100px`, and the left margin is set to `auto`. The left margin will thus be 300 pixels wide:

```css
div {
  width: 500px;
}
p {
  margin-left: auto;
  margin-right: 100px;
  width: 100px;
} /* 'auto' left margin evaluates to 300px */
```

In a sense, `auto` can be used to make up the difference between everything else and the required total. However, what if all three of these properties are set to `100px` and `none` of them are set to `auto`?

In the case where all three properties are set to something other than `auto`—or, in CSS terminology, when these formatting properties have been `overconstrained`—then `margin-right` is `always` forced to be `auto`. This means that if both margins and the width are set to `100px`, then the user agent will reset the right margin to `auto`. The right margin’s width will then be set according to the rule that one `auto` value “fills in” the distance needed to make the element’s overall width equal that of its containing block. Figure 7-11 shows the result of the following markup:

```css
div {
  width: 500px;
}
p {
  margin-left: 100px;
  margin-right: 100px;
  width: 100px;
} /* right margin forced to be 300px */
```

// 7-11

If both margins are set explicitly, and `width` is set to `auto`, then `width` will be whatever value is needed to reach the required total (which is the content width of the parent element). The results of the following markup are shown in Figure 7-12:

```css
p {
  margin-left: 100px;
  margin-right: 100px;
  width: auto;
}
```

The case shown in Figure 7-12 is the most common case, since it is equivalent to setting the margins and not declaring anything for the `width`. The result of the following markup is exactly the same as that shown in Figure 7-12:

```css
p {
  margin-left: 100px;
  margin-right: 100px;
} /* same as before */
```

// 7-12

You might be wondering what happens if `box-sizing` is set to, say, `padding-box`. The discussion here tends to assume that the default of `content-box` is used, but all the same principles described here apply, which is why this section only talked about `width` and the side margins without introducing any padding or borders. The handling of `width: auto` in this section and the following sections is the same regardless of the value of box-sizing. The details of what gets placed where inside the `box-sizing`-defined box may vary, but the treatment of `auto` values does not, because `box-sizing` determines what `width` refers to, not how it behaves in relation to the margins.

### 7.2.6 More Than One auto

Now let’s see what happens when two of the three properties (`width`, `margin-left`, and `margin-right`) are set to `auto`. If both margins are set to `auto`, as shown in the following code, then they are set to equal lengths, thus centering the element within its parent. This is illustrated in Figure 7-13.

```css
div {
  width: 500px;
}
p {
  width: 300px;
  margin-left: auto;
  margin-right: auto;
}
/* each margin is 100 pixels wide, because (500-300)/2 = 100 */
```

// 7-13

Setting both margins to equal lengths is the correct way to center elements within block boxes in the normal flow. (There are other methods to be found with flexible box and grid layout, but they’re beyond the scope of this text.)

Another way of sizing elements is to set one of the margins and the `width` to `auto`. The margin set to be `auto` is reduced to zero:

```css
div {
  width: 500px;
}
p {
  margin-left: auto;
  margin-right: 100px;
  width: auto;
} /* left margin evaluates to 0; width becomes 400px */
```

The `width` is then set to the value necessary to make the element fill its containing block; in the preceding example, it would be 400 pixels, as shown in Figure 7-14.

// 7-14

Finally, what happens when all three properties are set to `auto`? The answer: both margins are set to zero, and the `width` is made as wide as possible. This result is the same as the default situation, when no values are explicitly declared for margins or the width. In such a case, the margins default to zero and the `width` defaults to `auto`.

Note that since horizontal margins do not collapse, the padding, borders, and margins of a parent element can affect its children. The effect is indirect in that the margins (and so on) of an element can induce an offset for child elements. The results of the following markup are shown in Figure 7-15:

```css
div {
  padding: 50px;
  background: silver;
}
p {
  margin: 30px;
  padding: 0;
  background: white;
}
```

// 7-15

### 7.2.7 Negative Margins

So far, this may all seem rather straightforward, and you may be wondering why I said things could be complicated. Well, there’s another side to margins: the negative side. That’s right, it’s possible to set negative values for margins. Setting negative margins can result in some interesting effects.

Remember that the total of the seven horizontal properties always equals the `width` of the parent element. As long as all properties are zero or greater, an element can never be wider than its parent’s content area. However, consider the following markup, depicted in Figure 7-16:

```css
div {
  width: 500px;
  border: 3px solid black;
}
p.wide {
  margin-left: 10px;
  width: auto;
  margin-right: -50px;
}
```

// 7-16

Yes indeed, the child element is wider than its parent! This is mathematically correct:

```css
10px + 0 + 0 + 540px + 0 + 0 − 50px = 500px
```

The `540px` is the evaluation of `width: auto`, which is the number needed to balance out the rest of the values in the equation. Even though it leads to a child element sticking out of its parent, the specification hasn’t been violated because the values of the seven properties add up to the required total. It’s a semantic dodge, but it’s valid behavior.

Now, let’s add some borders to the mix:

```css
div {
  width: 500px;
  border: 3px solid black;
}
p.wide {
  margin-left: 10px;
  width: auto;
  margin-right: -50px;
  border: 3px solid gray;
}
```

The resulting change will be a reduction in the evaluated width of `width`:

```css
10px + 3px + 0 + 534px + 0 + 3px − 50px = 500px
```

If we were to introduce padding, then the value of `width` would drop even more.

Conversely, it’s possible to have `auto` right margins evaluate to negative amounts. If the values of other properties force the right margin to be negative in order to satisfy the requirement that elements be no wider than their containing block, then that’s what will happen. Consider:

```css
div {
  width: 500px;
  border: 3px solid black;
}
p.wide {
  margin-left: 10px;
  width: 600px;
  margin-right: auto;
  border: 3px solid gray;
}
```

The equation will work out like this:

```css
10px + 3px + 0 + 600px + 0 + 3px − 116px = 500px
```

The right margin will evaluate to `-116px`. Even if we’d given it a different explicit value, it would still be forced to `-116px` because of the rule stating that when an element’s dimensions are overconstrained, the right margin is reset to whatever is needed to make the numbers work out correctly. (Except in right-to-left languages, where the left margin would be overruled instead.)

Let’s consider another example, illustrated in Figure 7-17, where the left margin is set to be negative:

```css
div {
  width: 500px;
  border: 3px solid black;
}
p.wide {
  margin-left: -50px;
  width: auto;
  margin-right: 10px;
  border: 3px solid gray;
}
```

// 7-17

With a negative left margin, not only does the paragraph spill beyond the borders of the `div`, but it also spills beyond the edge of the browser window itself!

Remember that padding, borders, and content widths (and heights) can never be negative. Only margins can be less than zero.

### 7.2.8 Percentages

When it comes to percentage values for the width, padding, and margins, the same basic rules apply. It doesn’t really matter whether the values are declared with lengths or percentages.

Percentages can be very useful. Suppose we want an element’s content to be twothirds the width of its containing block, the right and left padding to be 5% each, the left margin to be 5%, and the right margin to take up the slack. That would be written something like:

```html
<p
  style="width: 67%; padding-right: 5%; padding-left: 5%; margin-right: auto;
 margin-left: 5%;"
>
  playing percentages
</p>
```

The right margin would evaluate to 18% (100% - 67% - 5% - 5% - 5%) of the width of the containing block.

Mixing percentages and length units can be tricky, however. Consider the following example:

```html
<p
  style="width: 67%; padding-right: 2em; padding-left: 2em; margin-right: auto;
 margin-left: 5em;"
>
  mixed lengths
</p>
```

In this case, the element’s box can be defined like this:

```css
5em + 0 + 2 em + 67% + 2 em + 0 + auto = containing block width
```

In order for the right margin’s width to evaluate to zero, the element’s containing block must be 27.272727 em wide (with the content area of the element being 18.272727 em wide). Any wider than that and the right margin will evaluate to a positive value. Any narrower and the right margin will be a negative value.

The situation gets even more complicated if we start mixing length-value unity types, like this:

```html
<p
  style="width: 67%; padding-right: 15px; padding-left: 10px;
 margin-right: auto;
 margin-left: 5em;"
>
  more mixed lengths
</p>
```

And, just to make things more complex, borders cannot accept percentage values, only length values. The bottom line is that it isn’t really possible to create a fully flexible element based solely on percentages unless you’re willing to avoid using borders or use some of the more experimental approaches such as flexible box layout.

### 7.2.9 Replaced Elements

So far, we’ve been dealing with the horizontal formatting of nonreplaced block boxes in the normal flow of text. Block-level replaced elements are a bit simpler to manage. All of the rules given for nonreplaced blocks hold true, with one exception: if `width` is `auto`, then the `width` of the element is the content’s intrinsic width. The image in the following example will be 20 pixels wide because that’s the width of the original image:

```html
<img src="smile.svg" style="display: block; width: auto; margin: 0;" />
```

If the actual image were 100 pixels wide instead, then it would be laid out as 100 pixels wide. It’s possible to override this rule by assigning a specific value to `width`. Suppose wemodify the previous example to show the same image three times, each with a different width value:

```html
<img src="smile.svg" style="display: block; width: 25px; margin: 0;" />
<img src="smile.svg" style="display: block; width: 50px; margin: 0;" />
<img src="smile.svg" style="display: block; width: 100px; margin: 0;" />
```

This is illustrated in Figure 7-18.

Note that the height of the elements also increases. When a replaced element’s `width` is changed from its intrinsic width, the value of `height` is scaled to match, unless `height` has been set to an explicit value of its own. The reverse is also true: if `height` is set, but `width` is left as `auto`, then the width is scaled proportionately to the change in height.

// 7-18

Now that you’re thinking about height, let’s move on to the vertical formatting of normal-flow block box.

### 7.2.10 Vertical Formatting

Like horizontal formatting, the vertical formatting of block boxes has its own set of interesting behaviors. An element’s content determines the default height of an `element`. The width of the content also affects height; the skinnier a paragraph becomes, for example, the taller it has to be in order to contain all of the inline content within it.

In CSS, it is possible to set an explicit height on any block-level element. If you do this, the resulting behavior depends on several other factors. Assume that the specified height is greater than that needed to display the content:

```html
<p style="height: 10em;"></p>
```

In this case, the extra height has a visual effect somewhat like extra padding. But suppose the height is `less` than what is needed to display the content:

```html
<p style="height: 3.33em;"></p>
```

When that happens, the browser is supposed to provide a means of viewing all content without increasing the height of the element box. In a case where the content of an element is taller than the height of its box, the actual behavior of a user agent will depend on the value of the property `overflow`. Two alternatives are shown in Figure 7-19.

Under CSS1, user agents can ignore any value of `height` other than `auto` if an element is not a replaced element (such as an image). In CSS2 and later, the value of `height` cannot be ignored, except in one specific circumstance involving percentage values. We’ll talk about that in a moment.

Just as with `width`, `height` defines the content area’s height by default, as opposed to the height of the visible element box. Any padding, borders, or margins on the top or bottom of the element box are `added` to the value for height, unless the value of `box-sizing` is different than `content-box`.

// 7-19

### 7.2.11 Vertical Properties

As was the case with horizontal formatting, vertical formatting also has seven related properties: `margin-top`, `border-top`, `padding-top`, `height`, `padding-bottom`, `border-bottom`, and `margin-bottom`. These properties are diagrammed in Figure 7-20.

The values of these seven properties must equal the height of the block box’s containing block. This is usually the value of `height` for a block box’s parent (since blocklevel elements nearly always have block-level elements for parents).

Only three of these seven properties may be set to `auto`: the `height` of the element, and the top and bottom margins. The top and bottom padding and borders must be set to specific values or else they default to a width of zero (assuming no `border-style` is declared). If border-style has been set, then the thickness of the borders is set to be the vaguely defined value `medium`. Figure 7-21 provides an illustration for remembering which parts of the box may have a value of `auto` and which may not.

Interestingly, if either `margin-top` or `margin-bottom` is set to `auto` for a block box in the normal flow, they both automatically evaluate to `0`. A value of `0` unfortunately prevents easy vertical centering of normal-flow boxes in their containing blocks. It also means that if you set the top and bottom margins of an element to `auto`, they are effectively reset to `0` and removed from the element box.

The handling of `auto` top and bottom margins is different for positioned elements, as well as flexible-box elements.

// 7-20

`height` must be set to `auto` or to a nonnegative value of some type; it can never be less than zero.

### 7.2.12 Percentage Heights

You already saw how length-value heights are handled, so let’s spend a moment on percentages. If the height of a normal-flow block box is set to a percentage value, then that value is taken as a percentage of the height of the box’s containing block. Given the following markup, the resulting paragraph will be 3 em tall:

```html
<div style="height: 6em;">
  <p style="height: 50%;">Half as tall</p>
</div>
```

Since setting the top and bottom margins to `auto` will give them zero height, the only way to vertically center the element in this particular case would be to set them both to `25%`—and even then, the box would be centered, not the content within it.

// 7-21

However, in cases where the height of the containing block is `not` explicitly declared, percentage heights are reset to `auto`. If we changed the previous example so that the `height` of the `div` is `auto`, the paragraph will now be exactly as tall as the `div` itself:

```html
<div style="height: auto;">
  <p style="height: 50%;">NOT half as tall; height reset to auto</p>
</div>
```

These two possibilities are illustrated in Figure 7-22. (The spaces between the paragraph borders and the `div` borders are the top and bottom margins on the paragraphs.)

// 7-22

Before we move on, take a closer look at the first example in Figure 7-22, the half-astall paragraph. It may be half as tall, but it isn’t vertically centered. That’s because the containing `div` is 6 em tall, which means the half-as-tall paragraph is 3 em tall. It has top and bottom margins of 1 em, so its overall box height is 5 em. That means there is actually 2 em of space between the bottom of the paragraph’s visible box and the `div`’s bottom border, not 1 em. It might seem a bit odd at first glance, but it makes sense once you work through the details.

### 7.2.13 Auto Heights

In the simplest case, a normal-flow block box with `height: auto` is rendered just high enough to enclose the line boxes of its inline content (including text). If an autoheight, normal-flow block box has only block-level children, then its default height will be the distance from the top of the topmost block-level child’s outer border edge to the bottom of the bottommost block-level child’s outer bottom border edge. Therefore, the margins of the child elements will “stick out” of the element that contains them. (This behavior is explained in the next section.)

However, if the block-level element has either top or bottom padding, or top or bottom borders, then its height will be the distance from the top of the outer-top margin edge of its topmost child to the outer-bottom margin edge of its bottommost child:

```html
<div
  style="height: auto;
 background: silver;"
>
  <p style="margin-top: 2em; margin-bottom: 2em;">A paragraph!</p>
</div>
<div
  style="height: auto; border-top: 1px solid; border-bottom: 1px solid;
 background: silver;"
>
  <p style="margin-top: 2em; margin-bottom: 2em;">Another paragraph!</p>
</div>
```

Both of these behaviors are demonstrated in Figure 7-23.

If we changed the borders in the previous example to padding, the effect on the height of the `div` would be the same: it would still enclose the paragraph’s margins within it.

// 7-23

### 7.2.14 Collapsing Vertical Margins

One other important aspect of vertical formatting is the `collapsing` of vertically adjacent margins. Collapsing behavior applies only to margins. Padding and borders,
where they exist, never collapse with anything.

An unordered list, where list items follow one another, is a perfect example of margin collapsing. Assume that the following is declared for a list that contains five items:

```css
li {
  margin-top: 10px;
  margin-bottom: 15px;
}
```

Each list item has a 10-pixel top margin and a 15-pixel bottom margin. When the list is rendered, however, the distance between adjacent list items is 15 pixels, not 25. This happens because, along the vertical axis, adjacent margins are collapsed. In other words, the smaller of the two margins is eliminated in favor of the larger. Figure 7-24 shows the difference between collapsed and uncollapsed margins.

Correctly implemented user agents collapse vertically adjacent margins, as shown in the first list in Figure 7-24, where there are 15-pixel spaces between each list item. The second list shows what would happen if the user agent didn’t collapse margins, resulting in 25-pixel spaces between list items.

Another word to use, if you don’t like “collapse,” is “overlap.” Although the margins are not really overlapping, you can visualize what’s happening using the following analogy.

Imagine that each element, such as a paragraph, is a small piece of paper with the content of the element written on it. Around each piece of paper is some amount of clear plastic, which represents the margins. The first piece of paper (say an `h1` piece) is laid down on the canvas. The second (a paragraph) is laid below it and then slid up until the edge of one of the piece’s plastic touches the edge of the other’s paper. If the first piece of paper has half an inch of plastic along its bottom edge, and the second has a third of an inch along its top, then when they slide together, the first piece’s plastic will touch the top edge of the second piece of paper. The two are now done being placed on the canvas, and the plastic attached to the pieces is overlapping.

// 7-24

Collapsing also occurs where multiple margins meet, such as at the end of a list.Adding to the earlier example, let’s assume the following rules apply:

```css
ul {
  margin-bottom: 15px;
}
li {
  margin-top: 10px;
  margin-bottom: 20px;
}
h1 {
  margin-top: 28px;
}
```

The last item in the list has a bottom margin of 20 pixels, the bottom margin of the `ul` is 15 pixels, and the top margin of a succeeding `h1` is 28 pixels. So once the margins have been collapsed, the distance between the end of the `li` and the beginning of the `h1` is 28 pixels, as shown in Figure 7-25.

// 7-25

Now, recall the examples from the previous section, where the introduction of a border or padding on a containing block would cause the margins of its child elements to be contained within it. We can see this behavior in operation by adding a border to the `ul` element in the previous example:

```css
ul {
  margin-bottom: 15px;
  border: 1px solid;
}
li {
  margin-top: 10px;
  margin-bottom: 20px;
}
h1 {
  margin-top: 28px;
}
```

With this change, the bottom margin of the `li` element is now placed inside its parent element (the `ul`). Therefore, the only margin collapsing that takes place is between the `ul` and the `h1`, as illustrated in Figure 7-26.

// 7-26

### 7.2.15 Negative Margins and Collapsing

Negative margins do have an impact on vertical formatting, and they affect how margins are collapsed. If negative vertical margins are set, then the browser should take the absolute maximum of both margins. The absolute value of the negative margin is then subtracted from the positive margin. In other words, the negative is added to the positive, and the resulting value is the distance between the elements. Figure 7-27 provides two concrete examples.

// 7-27

Notice the “pulling” effect of negative top and bottom margins. This is really no different from the way that negative horizontal margins cause an element to push outside of its parent. Consider:

```css
p.neg {
  margin-top: -50px;
  margin-right: 10px;
  margin-left: 10px;
  margin-bottom: 0;
  border: 3px solid gray;
}
```

```html
<div
  style="width: 420px; background-color: silver; padding: 10px;
 margin-top: 50px; border: 1px solid;"
>
  <p class="neg">
    A paragraph.
  </p>
  A div.
</div>
```

As we see in Figure 7-28, the paragraph has been pulled upward by its negative top margin. Note that the content of the `div` that follows the paragraph in the markup has also been pulled upward 50 pixels. In fact, every bit of normal-flow content that follows the paragraph is also pulled upward 50 pixels.

// 7-28

Now compare the following markup to the situation shown in Figure 7-29:

```css
p.neg {
  margin-bottom: -50px;
  margin-right: 10px;
  margin-left: 10px;
  margin-top: 0;
  border: 3px solid gray;
}
```

```html
<div style="width: 420px; margin-top: 50px;">
  <p class="neg">
    A paragraph.
  </p>
</div>
<p>
  The next paragraph.
</p>
```

// 7-29

What’s really happening in Figure 7-29 is that the elements following the `div` are placed according to the location of the bottom of the `div`. As you can see, the end of the `div` is actually above the visual bottom of its child paragraph. The next element after the `div` is the appropriate distance from the bottom of the `div`. This is expected, given the rules we saw.

Now let’s consider an example where the margins of a list item, an unordered list, and a paragraph are all collapsed. In this case, the unordered list and paragraph are assigned negative margins:

```css
li {
  margin-bottom: 20px;
}
ul {
  margin-bottom: -15px;
}
h1 {
  margin-top: -18px;
}
```

The larger of the two negative margins (`-18px`) is added to the largest positive margin (`20px`), yielding `20px - 18px = 2px`. Thus, there are only two pixels between the bottom of the list item’s content and the top of the `h1`’s content, as we can see in Figure 7-30.

When elements overlap each other due to negative margins, it’s hard to tell which elements are on top. You may also have noticed that none of the examples in this section use background colors. If they did, the background color of a following element might overwrite their content. This is expected behavior, since browsers usually render elements in order from beginning to end, so a normal-flow element that comes later in the document can be expected to overwrite an earlier element, assuming the two end up overlapping.

// 7-30

### 7.2.16 List Items

List items have a few special rules of their own. They are typically preceded by a marker, such as a small dot or a number. This marker isn’t actually part of the list item’s content area, so effects like those illustrated in Figure 7-31 are common.

// 7-31

CSS1 said very little about the placement and effects of these markers with regard to the layout of a document. CSS2 introduced properties specifically designed to address this issue, such as `marker-offset`. However, a lack of implementations and changes in thinking caused this to be dropped from CSS2.1, and work is being done to reintroduce the idea (if not the specific syntax) to CSS. Accordingly, the placement of markers is largely beyond the control of authors, at least as of this writing.

The marker attached to a list item element can be either outside the content of the list item or treated as an inline marker at the beginning of the content, depending on the value of the property `list-style-position`. If the marker is brought inside, then the list item will interact with its neighbors exactly like a block-level element, as illustrated in Figure 7-32.

// 7-32

If the marker stays outside the content, then it is placed some distance from the left content edge of the content (in left-to-right languages). No matter how the list’s styles are altered, the marker stays the same distance from the content edge. Occasionally, the markers may be pushed outside of the list element itself, as we can see in Figure 7-32.

Remember that list-item boxes define containing blocks for their ancestor boxes, just like regular block boxes.

## 7.3 Inline Elements

After block-level elements, inline elements are the most common. Setting box properties for inline elements takes us into more interesting territory than we’ve been so far. Some good examples of inline elements are the `em` tag and the `a` tag, both of which are nonreplaced elements, and images, which are replaced elements.

Note that none of the behavior described in this section applies to table elements. CSS2 introduced new properties and behaviors for handling tables and table content, and these elements behave in ways fairly distinct from either block-level or inline formatting. Table styling is beyond the scope of this book, as it’s surprisingly complicated and exists rather in a world of its own.

Nonreplaced and replaced elements are treated somewhat differently in the inline context, and we’ll look at each in turn as we explore the construction of inline elements.

### 7.3.1 Line Layout

First, you need to understand how inline content is laid out. It isn’t as simple as blocklevel elements, which just generate block boxes and usually don’t allow anything to coexist with them. By contrast, look `inside` a block-level element, such as a paragraph. You may well ask, how did all those lines of text get there? What controls their arrangement? How can I affect it?

In order to understand how lines are generated, first consider the case of an element containing one very long line of text, as shown in Figure 7-33. Note that we’ve put a border around the line by wrapping the entire line in a `span` element and then assigning it a border style:

```css
span {
  border: 1px dashed black;
}
```

// 7-33

Figure 7-33 shows the simplest case of an inline element contained by a block-level element. It’s no different in its way than a paragraph with two words in it. The only differences are that, in Figure 7-34, we have a few dozen words, and most paragraphs don’t contain an explicit inline element such as `span`.

In order to get from this simplified state to something more familiar, all we have to do is determine how wide the element should be, and then break up the line so that the resulting pieces will fit into the content width of the element. Therefore, we arrive at the state shown in Figure 7-34.

// 7-34

Nothing has really changed. All we did was take the single line and break it into pieces, and then stack those pieces on top of each other.

In Figure 7-34, the borders for each line of text also happen to coincide with the top and bottom of each line. This is true only because no padding has been set for the inline text. Notice that the borders actually overlap each other slightly; for example, the bottom border of the first line is just below the top border of the second line. This is because the border is actually drawn on the next pixel (assuming you’re using a monitor) to the `outside` of each line. Since the lines are touching each other, their borders will overlap as shown in Figure 7-34.

If we alter the span styles to have a background color, the actual placement of the lines becomes quite clear. Consider Figure 7-35, which contains four paragraphs, each with a different value of `text-align` and each having the backgrounds of its lines filled in.

As we can see, not every line reaches to the edge of its parent paragraph’s content area, which has been denoted with a dotted gray border. For the left-aligned paragraph, the lines are all pushed flush against the left content edge of the paragraph, and the end of each line happens wherever the line is broken. The reverse is true for the right-aligned paragraph. For the centered paragraph, the centers of the lines are aligned with the center of the paragraph.

In the last case, where the value of `text-align` is `justify`, each line is forced to be as wide as the paragraph’s content area so that the line’s edges touch the content edges of the paragraph. The difference between the natural length of the line and the width of the paragraph is made up by altering the spacing between letters and words in each line. Therefore, the value of `word-spacing` can be overridden when the text is justified. (The value of `letter-spacing` cannot be overridden if it is a length value.)

That pretty well covers how lines are generated in the simplest cases. As you’re about to see, however, the inline formatting model is far from simple.

// 7-35

### 7.3.2 Basic Terms and Concepts

Before we go any further, let’s review some basic terms of inline layout, which will be crucial in navigating the following sections:

`Anonymous text`

This is any string of characters that is not contained within an inline element.
Thus, in the markup `<p> I'm <em>so</em> happy!</p>`, the sequences “ I’m ”
and “ happy!” are anonymous text. Note that the spaces are part of the text since
a space is a character like any other.

`Em box`

This is defined in the given font, otherwise known as the character box. Actual glyphs can be taller or shorter than their em boxes. In CSS, the value of `font-size` determines the height of each em box.

`Content area`

In nonreplaced elements, the content area can be one of two things, and the CSS specification allows user agents to choose which one. The content area can be the box described by the em boxes of every character in the element, strung together; or it can be the box described by the character glyphs in the element. In this book, I use the em box definition for simplicity’s sake. In replaced elements, the content area is the intrinsic height of the element plus any margins, borders, or padding.

`Leading`

Leading is the difference between the values of `font-size` and `line-height`. This difference is actually divided in half and is applied equally to the top and bottom of the content area. These additions to the content area are called, not surprisingly, `half-leading`. Leading is applied only to nonreplaced elements.

`Inline box`

This is the box described by the addition of the leading to the content area. For nonreplaced elements, the height of the inline box of an element will be exactly equal to the value for `line-height`. For replaced elements, the height of the inline box of an element will be exactly equal to the content area, since leading is not applied to replaced elements.

`Line box`

This is the shortest box that bounds the highest and lowest points of the inline boxes that are found in the line. In other words, the top edge of the line box is placed along the top of the highest inline box top, and the bottom of the line box is placed along the bottom of the lowest inline box bottom.

CSS also contains a set of behaviors and useful concepts that fall outside of the bove list of terms and definitions:

- The content area is analogous to the content box of a block box.
- The background of an inline element is applied to the content area plus any pad ding.
- Any border on an inline element surrounds the content area plus any padding and border.
- Padding, borders, and margins on nonreplaced elements have no vertical effect on inline elements or the boxes they generate; that is, they do `not` affect the height of an element’s inline box (and thus the line box that contains the element).
- Margins and borders on replaced elements `do` affect the height of the inline box for that element and, by implication, the height of the line box for the line that contains the element.

One more thing to note: inline boxes are vertically aligned within the line according to their values for the property `vertical-align`.

Before moving on, let’s look at a step-by-step process for constructing a line box, which you can use to see how the various pieces of the line fit together to determine its height.

Determine the height of the inline box for each element in the line by following these steps:

1. Find the values of `font-size` and `line-height` for each inline nonreplaced element and text that is not part of a descendant inline element and combine them. This is done by subtracting the `font-size` from the `line-height`, which yields the leading for the box. The leading is split in half and applied to the top and bottom of each em box.
2. Find the values of `height`, `margin-top`, `margin-bottom`, `padding-top`, `padding-bottom`,`border-top-width`, and `border-bottom-width` for each replaced element and add them together.
3. Figure out, for each content area, how much of it is above the baseline for the overall line and how much of it is below the baseline. This is not an easy task: you must know the position of the baseline for each element and piece of anonymous text and the baseline of the line itself, and then line them all up. In addition, the bottom edge of a replaced element sits on the baseline for the overall line.
4. Determine the vertical offset of any elements that have been given a value for `vertical-align`. This will tell you how far up or down that element’s inline box will be moved, and it will change how much of the element is above or below the baseline.
5. Now that you know where all of the inline boxes have come to rest, calculate the final line box height. To do so, just add the distance between the baseline and the highest inline box top to the distance between the baseline and the lowest inline box bottom.

Let’s consider the whole process in detail, which is the key to intelligently styling inline content.

### 7.3.3 Inline Formatting

First, know that all elements have a `line-height`, whether it’s explicitly declared or not. This value greatly influences the way inline elements are displayed, so let’s give it due attention.

Now let’s establish how to determine the height of a line. A line’s height (or the height of the line box) is determined by the height of its constituent elements and other content, such as text. It’s important to understand that `line-height` actually affects inline elements and other inline content, `not` block-level elements—at least, not directly. We can set a `line-height` value for a block-level element, but the value will have a visual impact only as it’s applied to inline content within that block-level element. Consider the following empty paragraph, for example:

```html
<p style="line-height: 0.25em;"></p>
```

Without content, the paragraph won’t have anything to display, so we won’t see anything. The fact that this paragraph has a `line-height` of any value—be it `0.25em or 25in`—makes no difference without some content to create a line box.

We can certainly set a `line-height` value for a block-level element and have that apply to all of the content within the block, whether or not the content is ontained in any inline elements. In a certain sense, then, each line of text contained within a block-level element is its own inline element, whether or not it’s surrounded by tags. If you like, picture a fictional tag sequence like this:

```html
<p>
  <line>This is a paragraph with a number of</line>
  <line>lines of text which make up the</line>
  <line>contents.</line>
</p>
```

Even though the `line` tags don’t actually exist, the paragraph behaves as if they did—each line of text inherits styles from the paragraph. You only bother to create `line-height` rules for block-level elements so you don’t have to explicitly declare a `line-height` for all of their inline elements, fictional or otherwise.

The fictional `line` element actually clarifies the behavior that results from setting `line-height` on a block-level element. According to the CSS specification, declaring `line-height` on a block-level element sets a `minimum` line box height for the content of that block-level element. Declaring `p.spacious {line-height: 24pt;}` means that the `minimum` heights for each line box is 24 points. Technically, content can inherit this line height only if an inline element does so. Most text isn’t contained by an inline element. If you pretend that each line is contained by the fictional line element, the model works out very nicely.

### 7.3.4 Inline Nonreplaced Elements

Building on your formatting knowledge, let’s move on to the construction of lines that contain only nonreplaced elements (or anonymous text). Then you’ll be in a good position to understand the differences between nonreplaced and replaced elements in inline layout.

### 7.3.5 Building the Boxes

First, for an inline nonreplaced element or piece of anonymous text, the value of `font-size` determines the height of the content area. If an inline element has a `font-size` of `15px`, then the content area’s height is 15 pixels because all of the em boxes in the element are 15 pixels tall, as illustrated in Figure 7-36.

// 7-36

The next thing to consider is the value of `line-height` for the element, and the difference between it and the value of `font-size`. If an inline nonreplaced element has a `font-size` of `15px` and a `line-height` of `21px`, then the difference is six pixels. The user agent splits the six pixels in half and applies half to the top and half to the bottom of the content area, which yields the inline box. This process is illustrated in Figure 7-37.

// 7-37

Let’s assume that the following is true:

```html
<p style="font-size: 12px; line-height: 12px;">
  This is text, <em>some of which is emphasized</em>, plus other text<br />
  which is <strong style="font-size: 24px;">strongly emphasized</strong> and which is<br />
  larger than the surrounding text.
</p>
```

In this example, most of the text has a `font-size` of `12px`, while the text in one inline nonreplaced element has a size of `24px`. However, all of the text has a `line-height` of `12px` since `line-height` is an inherited property. Therefore, the `strong` element’s `line-height` is also `12px`.

Thus, for each piece of text where both the `font-size` and `line-height` are `12px`, the content height does not change (since the difference between `12px` and `12px` is zero), so the inline box is 12 pixels high. For the strong text, however, the difference between `line-height` and `font-size` is `-12px`. This is divided in half to determine the half-leading (`-6px`), and the half-leading is added to both the top and bottom of the content height to arrive at an inline box. Since we’re adding a negative number in both cases, the inline box ends up being 12 pixels tall. The 12-pixel inline box is centered vertically within the 24-pixel content height of the element, so the inline box is actually smaller than the content area.

So far, it sounds like we’ve done the same thing to each bit of text, and that all the inline boxes are the same size, but that’s not quite true. The inline boxes in the second line, although they’re the same size, don’t actually line up because the text is all baseline-aligned (see Figure 7-38).

Since inline boxes determine the height of the overall line box, their placement with respect to each other is critical. The line box is defined as the distance from the top of the highest inline box in the line to the bottom of the lowest inline box, and the top of each line box butts up against the bottom of the line box for the preceding line. The result shown in Figure 7-38 gives us the paragraph shown in Figure 7-39.

// 7-38

// 7-39

As we can see in Figure 7-39, the middle line is taller than the other two, but it still isn’t big enough to contain all of the text within it. The anonymous text’s inline box determines the bottom of the line box, while the top of the strong element’s inline box sets the top of the line box. Because that inline box’s top is inside the element’s content area, the contents of the element spill outside the line box and actually overlap other line boxes. The result is that the lines of text look irregular.

In just a bit, we’ll explore ways to cope with this behavior and methods for achieving consistent baseline spacing.

### 7.3.6 Vertical Alignment

If we change the vertical alignment of the inline boxes, the same height determination principles apply. Suppose that we give the `strong` element a vertical alignment of `4px`:

```html
<p style="font-size: 12px; line-height: 12px;">
  This is text, <em>some of which is emphasized</em>, plus other text<br />
  which is <strong style="font-size: 24px; vertical-align: 4px;">strongly emphasized</strong> and that is<br />
  larger than the surrounding text.
</p>
```

That small change raises the `strong` element four pixels, which pushes up both its content area and its inline box. Because the `strong` element’s inline box top was already the highest in the line, this change in vertical alignment also pushes the top of the line box upward by four pixels, as shown in Figure 7-40.

// 7-40

Let’s consider another situation. Here, we have another inline element in the same line as the strong text, and its alignment is other than the baseline:

```html
<p style="font-size: 12px; line-height: 12px;">
  This is text, <em>some of which is emphasized</em>,<br />
  plus other text that is <strong style="font-size: 24px;">strong</strong> and
  <span style="vertical-align: top;">tall</span> and is<br />
  larger than the surrounding text.
</p>
```

Now we have the same result as in our earlier example, where the middle line box is taller than the other line boxes. However, notice how the “tall” text is aligned in Figure 7-41.

// 7-41

In this case, the top of the “tall” text’s inline box is aligned with the top of the line box. Since the “tall” text has equal values for `font-size` and `line-height`, the content height and inline box are the same. However, consider this:

```html
<p style="font-size: 12px; line-height: 12px;">
  This is text, <em>some of which is emphasized</em>,<br />
  plus other text that is <strong style="font-size: 24px;">strong</strong> and
  <span style="vertical-align: top; line-height: 2px;">tall</span> and is<br />
  larger than the surrounding text.
</p>
```

Since the `line-height` for the “tall” text is less than its `font-size`, the inline box for that element is smaller than its content area. This tiny fact changes the placement of the text itself since the top of its inline box must be aligned with the top of the line box for its line. Thus, we get the result shown in Figure 7-42.

On the other hand, we could set the “tall” text to have a `line-height` that is actually bigger than its `font-size`. For example:

```html
<p style="font-size: 12px; line-height: 12px;">
  This is text, <em>some of which is emphasized</em>, plus other text<br />
  that is <strong style="font-size: 24px;">strong</strong> and
  <span style="vertical-align: top; line-height: 18px;">tall</span> and that is<br />
  larger than the surrounding text.
</p>
```

// 7-42

Since we’ve given the “tall” text a `line-height` of `18px`, the difference between `line-height` and `font-size` is six pixels. The half-leading of three pixels is added to the content area and results in an inline box that is 18 pixels tall. The top of this inline box aligns with the top of the line box. Similarly, the `vertical-align` value `bottom` will align the bottom of an inline element’s inline box with the bottom of the line box.

In relation to the terms we’ve been using in this chapter, the effects of the assorted keyword values of `vertical-align` are:

`top`

Aligns the top of the element’s inline box with the top of the containing line box

`bottom`

Aligns the bottom of the element’s inline box with the bottom of the containing line box

`text-top`

Aligns the top of the element’s inline box with the top of the parent’s content area

`text-bottom`

Aligns the bottom of the element’s inline box with the bottom of the parent’s content area

`middle`

Aligns the vertical midpoint of the element’s inline box with `0.5ex` above the baseline of the parent

`super`

Moves the content area and inline box of the element upward. The distance is not specified and may vary by user agent

`sub`

The same as super, except the element is moved downward instead of upward

`<percentage>`

Shifts the element up or down the distance defined by taking the declared percentage of the element’s value for `line-height`

### 7.3.7 Managing the line-height

In previous sections, we saw that changing the `line-height` of an inline element can cause text from one line to overlap another. In each case, though, the changes were made to individual elements. So how can we affect the `line-height` of elements in a more general way in order to keep content from overlapping?

One way to do this is to use the `em` unit in conjunction with an element whose `font-size` has changed. For example:

```css
p {
  line-height: 1em;
}
big {
  font-size: 250%;
  line-height: 1em;
}
```

```html
<p>
  Not only does this paragraph have "normal" text, but it also<br />
  contains a line in which <big>some big text</big> is found.<br />
  This large text helps illustrate our point.
</p>
```

By setting a `line-height` for the `big` element, we increase the overall height of the line box, providing enough room to display the big element without overlapping any other text and without changing the `line-height` of all lines in the paragraph. We use a value of `1em` so that the `line-height` for the `big` element will be set to the same size as `big`’s font-size. Remember, `line-height` is set in relation to the `font-size` of the element itself, not the parent element. The results are shown in Figure 7-43.

// 7-43

Make sure you really understand the previous sections, because things will get trickier when we try to add borders. Let’s say we want to put five-pixel borders around any hyperlink:

```css
a:link {
  border: 5px solid blue;
}
```

If we don’t set a large enough `line-height` to accommodate the border, it will be in danger of overwriting other lines. We could increase the size of the inline box for unvisited links using `line-height`, as we did for the `big` element in the earlier example; in this case, we’d just need to make the value of `line-height` 10 pixels larger than the value of font-size for those links. However, that will be difficult if we don’t actually know the size of the font in pixels.

Another solution is to increase the `line-height` of the paragraph. This will affect every line in the entire element, not just the line in which the bordered hyperlink appears:

```css
p {
  line-height: 1.8em;
}
a:link {
  border: 5px solid blue;
}
```

Because there is extra space added above and below each line, the border around the hyperlink doesn’t impinge on any other line, as we can see in Figure 7-44.

This approach works here because all of the text is the same size. If there were other elements in the line that changed the height of the line box, our border situation might also change. Consider the following:

```css
p {
  font-size: 14px;
  line-height: 24px;
}
a:link {
  border: 5px solid blue;
}
big {
  font-size: 150%;
  line-height: 1.5em;
}
```

Given these rules, the height of the inline box of a `big` element within a paragraph will be 31.5 pixels (14 × 1.5 × 1.5), and that will also be the height of the line box. In order to keep baseline spacing consistent, we must make the `p` element’s `line-height` equal to or greater than 32px.

// 7-44

#### Baselines and line heights

The actual height of each line box depends on the way its component elements line up with one another. This alignment tends to depend very much on where the baseline falls within each element (or piece of anonymous text) because that location determines how the inline boxes are arranged. The placement of the baseline within each em box is different for every font. This information is built into the font files and cannot be altered by any means other than directly editing the font files.

Consistent baseline spacing tends to be more of an art than a science. If you declare all of your font sizes and line heights using a single unit, such as ems, then you have a reliable chance of consistent baseline spacing. If you mix units, however, that feat becomes a great deal more difficult, if not impossible. As of this writing, there are proposals for properties that would let authors enforce consistent baseline spacing regardless of the inline content, which would greatly simplify certain aspects of online typography. None of these proposed properties have been implemented though, which makes their adoption a distant hope at best.

### 7.3.8 Scaling Line Heights

The best way to set `line-height`, as it turns out, is to use a raw number as the value.
This method is the best because the number becomes the scaling factor, and that fac‐
tor is an inherited, not a computed, value. Let’s say we want the `line-height`'s of all elements in a document to be one and a half times their `font-size`.
We would declare:

```css
body {
  line-height: 1.5;
}
```

This scaling factor of 1.5 is passed down from element to element, and, at each level, the factor is used as a multiplier of the `font-size` of each element. Therefore, the following markup would be displayed as shown in Figure 7-45:

```css
p {
  font-size: 15px;
  line-height: 1.5;
}
small {
  font-size: 66%;
}
big {
  font-size: 200%;
}
```

```html
<p>
  This paragraph has a line-height of 1.5 times its font-size. In addition, any elements within it
  <small>such as this small element</small> also have line-heights 1.5 times their font-size...and that includes
  <big>this big element right here</big>. By using a scaling factor, line-heights scale to match the font-size of any
  element.
</p>
```

In this example, the line height for the `small` element turns out to be 15 pixels, and for the big element, it’s 45 pixels. (These numbers may seem excessive, but they’re in keeping with the overall page design.) Of course, if we don’t want our big text to generate too much extra leading, we can give it a `line-height` value, which will override the inherited scaling factor:

```css
p {
  font-size: 15px;
  line-height: 1.5;
}
small {
  font-size: 66%;
}
big {
  font-size: 200%;
  line-height: 1em;
}
```

// 7-45

Another solution—possibly the simplest of all—is to set the styles such that lines are no taller than absolutely necessary to hold their content. This is where we might use a `line-height` of `1.0`. This value will multiply itself by every `font-size` to get the same value as the `font-size` of every element. Thus, for every element, the inline box will be the same as the content area, which will mean the absolute minimum size necessary is used to contain the content area of each element.

Most fonts still display a little bit of space between the lines of character glyphs because characters are usually smaller than their em boxes. The exception is script (“cursive”) fonts, where character glyphs are usually `larger` than their em boxes.

### 7.3.9 Adding Box Properties

As you’re aware from previous discussions, padding, margins, and borders may all be applied to inline nonreplaced elements. These aspects of the inline element do not influence the height of the line box at all. If you were to apply some borders to a `span` element without any margins or padding, you’d get results such as those shown in Figure 7-46.

The border edge of inline elements is controlled by the `font-size`, not the `line-height`. In other words, if a `span` element has a `font-size` of `12px` and a `line-height` of `36px`, its content area is `12px` high, and the border will surround that content area.

Alternatively, we can assign padding to the inline element, which will push the borders away from the text itself:

```css
span {
  padding: 4px;
}
```

Note that this padding does not alter the actual shape of the content height, and so it will not affect the height of the inline box for this element. Similarly, adding borders to an inline element will not affect the way line boxes are generated and laid out, as illustrated in Figure 7-47.

// 7-46

// 7-47

As for margins, they do not, practically speaking, apply to the top and bottom of an inline nonreplaced element, as they don’t affect the height of the line box. The ends of the element are another story.

Recall the idea that an inline element is basically laid out as a single line and then broken up into pieces. So, if we apply margins to an inline element, those margins will appear at its beginning and end: these are the left and right margins, respectively. Padding also appears at the edges. Thus, although padding and margins (and borders) do not affect line heights, they can still affect the layout of an element’s content by pushing text away from its ends. In fact, negative left and right margins can pull text closer to the inline element, or even cause overlap, as Figure 7-48 shows.

Think of an inline element as a strip of paper with some plastic surrounding it. Displaying the inline element on multiple lines is like slicing up the strip into smaller strips. However, no extra plastic is added to each smaller strip. The only plastic is that which was on the strip to begin with, so it appears only at the beginning and end of the original ends of the paper strip (the inline element). At least, that’s the default behavior, but as we’ll soon see, there is another option.

// 7-48

So, what happens when an inline element has a background and enough padding to cause the lines’ backgrounds to overlap? Take the following situation as an example:

```css
p {
  font-size: 15px;
  line-height: 1em;
}
p span {
  background: #faa;
  padding-top: 10px;
  padding-bottom: 10px;
}
```

All of the text within the `span` element will have a content area 15 pixels tall, and we’ve applied 10 pixels of padding to the top and bottom of each content area. The extra pixels won’t increase the height of the line box, which would be fine, except there is a background color. Thus, we get the result shown in Figure 7-49.

CSS 2.1 explicitly states that the line boxes are drawn in document order: “This will cause the borders on subsequent lines to paint over the borders and text of previous lines.” The same principle applies to backgrounds as well, as Figure 7-49 shows. CSS2, on the other hand, allowed user agents “to ‘clip’ the border and padding areas (i.e., not render them).” Therefore, the results may depend greatly on which specification the user agent follows.

// 7-49

### 7.3.10 Changing Breaking Behavior

In the previous section, we saw that when an inline nonreplaced element is broken across multiple lines, it’s treated as if it were one long single-line element that’s sliced into smaller boxes, one slice per line break. That’s actually just the default behavior, and it can be changed via the property `box-decoration-break`.

//

The default value, `slice`, is what we saw in the previous section. The other value, `clone`, causes each fragement of the element to be drawn as if it were a standalone box. What does that mean? Compare the two examples in Figure 7-50, in which exactly the same markup and styles are treated as either sliced or cloned.

Many of the differences are pretty apparent, but a few are perhaps more subtle. Among the effects are the application of padding to each element’s fragment, including at the ends where the line breaks occurred. Similarly, the border is drawn around each fragment individually, instead of being broken up.

// 7-50

More subtly, notice how the `background-image` positioning changes between the two.
In the sliced version, background images are sliced along with everything else, meaning that only one of the fragments contains the origin image. In the cloned version, however, each background acts as its own copy, so each has its own origin image. This means, for example, that even if we have a nonrepeated background image, it will appear once in each fragment instead of only in one fragment.

The `box-decoration-break` property will most often be used with inline boxes, but itactually applies in any situation where there’s a break in an element—for example, when a page break interrupts an element in paged media. In such a case, each fragment is a separate slice. If we set `box-decoration-break: clone`, then each box fragment will be treated as a copy when it comes to borders, padding, backgrounds, and so on. The same holds true in multicolumn layout: if an element is split by a column break, the value of `box-decoration-break` will affect how it is rendered.

### 7.3.11 Glyphs Versus Content Area

Even in cases where you try to keep inline nonreplaced element backgrounds from overlapping, it can still happen, depending on which font is in use. The problem lies in the difference between a font’s em box and its character glyphs. Most fonts, as it turns out, don’t have em boxes whose heights match the character glyphs.

That may sound very abstract, but it has practical consequences. In CSS2.1, we find the following: “the height of the content area should be based on the font, but this specification does not specify how. A user agent may…use the em box or the maximum ascender and descender of the font. (The latter would ensure that glyphs with parts above or below the em box still fall within the content area, but leads to differently sized boxes for different fonts.)”

In other words, the “painting area” of an inline nonreplaced element is left to the user agent. If a user agent takes the em box to be the height of the content area, then the background of an inline nonreplaced element will be equal to the height of the em box (which is the value of `font-size`). If a user agent uses the maximum ascender and descender of the font, then the background may be taller or shorter than the em box. Therefore, you could give an inline nonreplaced element a `line-height` of `1em` and still have its background overlap the content of other lines.

### 7.3.12 Inline Replaced Elements

Inline replaced elements, such as images, are assumed to have an intrinsic height and width; for example, an image will be a certain number of pixels high and wide. Therefore, a replaced element with an intrinsic height can cause a line box to become taller than normal. This does `not` change the value of `line-height` for any element in the line, including the replaced element itself. Instead, the line box is made just tall enough to accommodate the replaced element, plus any box properties. In other words, the entirety of the replaced element—content, margins, borders, and padding—is used to define the element’s inline box. The following styles lead to one such example, as shown in Figure 7-51:

```css
p {
  font-size: 15px;
  line-height: 18px;
}
img {
  height: 30px;
  margin: 0;
  padding: 0;
  border: none;
}
```

Despite all the blank space, the effective value of `line-height` has not changed, either for the paragraph or the image itself. `line-height` has no effect on the image’s inline box. Because the image in Figure 7-51 has no padding, margins, or borders, its inline box is equivalent to its content area, which is, in this case, 30 pixels tall.

Nonetheless, an inline replaced element still has a value for `line-height`. Why? In the most common case, it needs the value in order to correctly position the element if it’s been vertically aligned. Recall that, for example, percentage values for verticalalign are calculated with respect to an element’s `line-height`. Thus:

```css
p {
  font-size: 15px;
  line-height: 18px;
}
img {
  vertical-align: 50%;
}
```

```html
<p>the image in this sentence <img src="test.gif" alt="test image" /> will be raised 9 pixels.</p>
```

// 7-51

The inherited value of `line-height` causes the image to be raised nine pixels instead of some other number. Without a value for `line-height`, it wouldn’t be possible to perform percentage-value vertical alignments. The height of the image itself has no relevance when it comes to vertical alignment; the value of `line-height` is all that matters.

However, for other replaced elements, it might be important to pass on a `line-height` value to descendant elements within that replaced element. An example would be an SVG image, which uses CSS to style any text found within the image.

### 7.3.13 Adding Box Properties

After everything we’ve just been through, applying margins, borders, and padding to inline replaced elements almost seems simple.

Padding and borders are applied to replaced elements as usual; padding inserts space around the actual content and the border surrounds the padding. What’s unusual about the process is that these two things actually influence the height of the line box because they are part of the inline box of an inline replaced element (unlike inline nonreplaced elements). Consider Figure 7-52, which results from the following styles:

```css
img {
  height: 50px;
  width: 50px;
}
img.one {
  margin: 0;
  padding: 0;
  border: 3px dotted;
}
img.two {
  margin: 10px;
  padding: 10px;
  border: 3px solid;
}
```

Note that the first line box is made tall enough to contain the image, whereas the second is tall enough to contain the image, its padding, and its border.

// 7-52

Margins are also contained within the line box, but they have their own wrinkles. Setting a positive margin is no mystery; it will make the inline box of the replaced element taller. Setting negative margins, meanwhile, has a similar effect: it decreases the size of the replaced element’s inline box. This is illustrated in Figure 7-53, where we can see that a negative top margin is pulling down the line above the image:

```css
img.two {
  margin-top: -10px;
}
```

Negative margins operate the same way on block-level elements, of course. In this case, the negative margins make the replaced element’s inline box smaller than ordinary. Negative margins are the only way to cause inline replaced elements to bleed into other lines, and it’s why the boxes that replaced inline elements generate are often assumed to be inline-block.

// 7-53

### 7.3.14 Replaced Elements and the Baseline

You may have noticed by now that, by default, inline replaced elements sit on the baseline. If you add bottom padding, a margin, or a border to the replaced element, then the content area will move upward (assuming `box-sizing: content-box`). Replaced elements do not have baselines of their own, so the next best thing is to align the bottom of their inline boxes with the baseline. Thus, it is actually the bottom outer margin edge that is aligned with the baseline, as illustrated in Figure 7-54.

// 7-54

This baseline alignment leads to an unexpected (and unwelcome) consequence: an image placed in a table cell all by itself should make the table cell tall enough to contain the line box containing the image. The resizing occurs even if there is no actual text, not even whitespace, in the table cell with the image. Therefore, the common sliced-image and spacer-GIF designs of years past can fall apart quite dramatically in modern browsers. (I know that you don’t create such things, but this is still a handy context in which to explain this behavior.) Consider the simplest case:

```css
td {
  font-size: 12px;
}
```

```html
<td><img src="spacer.gif" height="1" width="10" /></td>
```

Under the CSS inline formatting model, the table cell will be 12 pixels tall, with the image sitting on the baseline of the cell. So there might be three pixels of space below the image and eight above it, although the exact distances would depend on the font family used and the placement of its baseline.

This behavior is not confined to images inside table cells; it will also happen in any situation where an inline replaced element is the sole descendant of a block-level or table-cell element. For example, an image inside a `div` will also sit on the baseline.

The most common workaround for such circumstances is to make images in table cells block-level so that they do not generate a line box. For example:

```css
td {
  font-size: 12px;
}
img.block {
  display: block;
}
```

```html
<td><img src="spacer.gif" height="1" width="10" class="block" /></td>
```

Another possible fix would be to make the `font-size` and `line-height` of the enclosing table cell `1px`, which would make the line box only as tall as the one-pixel image within it.

As of this writing, many browsers can ignore this CSS inline formatting model in this context. See the article `“Images, Tables, and Mysterious Gaps”` for more information.

Here’s another interesting effect of inline replaced elements sitting on the baseline: if we apply a negative bottom margin, the element will actually get pulled downward because the bottom of its inline box will be higher than the bottom of its content area. Thus, the following rule would have the result shown in Figure 7-55:

```css
p img {
  margin-bottom: -10px;
}
```

// 7-55

This can easily cause a replaced element to bleed into following lines of text, as Figure 7-55 shows.

Inline with History

The CSS inline formatting model may seem needlessly complex and, in some ways, even contrary to author expectations. Unfortunately, the complexity is the result of creating a style language that is both backward-compatible with pre-CSS web browsers and leaves the door open for future expansion into more sophisticated territory—an awkward blend of past and present. It’s also the result of making some sensible decisions that avoid one undesirable effect while causing another.

For example, the “spreading apart” of lines of text by image and vertically aligned text owes its roots to the way Mosaic 1.0 behaved. In that browser, any image in a paragraph would push open enough space to contain the image. That’s a good behavior, since it prevents images from overlapping text in other lines. So when CSS introduced ways to style text and inline elements, its authors endeavored to create a model that did not (by default) cause inline images to overlap other lines of text. However, the same model also meant that a superscript element (`sup`), for example, would likely also push apart lines of text.

Such effects annoy some authors who want their baselines to be an exact distance apart and no further, but consider the alternative. If `line-height` forced baselines to be exactly a specified distance apart, we’d easily end up with inline replaced and vertically shifted elements that overlap other lines of text—which would also annoy authors. Fortunately, CSS offers enough power to create your desired effect in one way or another, and the future of CSS holds even more potential.

### 7.3.15 Inline-Block Elements

As befits the hybrid look of the value name `inline-block`, inline-block elements are indeed a hybrid of block-level and inline elements. This display value was introduced in CSS2.1.

An inline-block element relates to other elements and content as an inline box. In other words, it’s laid out in a line of text just as an image would be, and in fact, inlineblock elements are formatted within a line as a replaced element. This means the bottom of the inline-block element will rest on the baseline of the text line by default and will not line break within itself.

Inside the inline-block element, the content is formatted as though the element were block-level. The properties `width` and `height` apply to it (and thus so does `box-sizing`), as they do to any block-level or inline replaced element, and those properties will increase the height of the line if they are taller than the surrounding content.

Let’s consider some example markup that will help make this clearer:

```html
<div id="one">
  This text is the content of a block-level level element. Within this block-level element is another block-level
  element.
  <p>Look, it's a block-level paragraph.</p>
  Here's the rest of the DIV, which is still block-level.
</div>
<div id="two">
  This text is the content of a block-level level element. Within this block-level element is an inline element.
  <p>Look, it's an inline paragraph.</p>
  Here's the rest of the DIV, which is still block-level.
</div>
<div id="three">
  This text is the content of a block-level level element. Within this block-level element is an inline-block element.
  <p>Look, it's an inline-block paragraph.</p>
  Here's the rest of the DIV, which is still block-level.
</div>
```

To this markup, we apply the following rules:

```css
div {
  margin: 1em 0;
  border: 1px solid;
}
p {
  border: 1px dotted;
}
div#one p {
  display: block;
  width: 6em;
  text-align: center;
}
div#two p {
  display: inline;
  width: 6em;
  text-align: center;
}
div#three p {
  display: inline-block;
  width: 6em;
  text-align: center;
}
```

The result of this stylesheet is depicted in Figure 7-56.

// 7-56

Notice that in the second `div`, the inline paragraph is formatted as normal inline content, which means `width` and `text-align` get ignored (since they do not apply to inline elements). For the third `div`, however, the inline-block paragraph honors both properties, since it is formatted as a block-level element. That paragraph’s margins also force its line of text to be much taller, since it affects line height as though it were a replaced element.

If an inline-block element’s `width` is not defined or explicitly declared `auto`, the element box will shrink to fit the content. That is, the element box is exactly as wide as necessary to hold the content, and no wider. Inline boxes act the same way, although they can break across lines of text, whereas inline-block elements cannot. Thus, we have the following rule, when applied to the previous markup example:

```css
div#three p {
  display: inline-block;
  height: 4em;
}
```

will create a tall box that’s just wide enough to enclose the content, as shown in Figure 7-57.

// 7-57

Inline-block elements can be useful if, for example, we have a set of five hyperlinks that we want to be equal width within a toolbar. To make them all 20% the width of their parent element, but still leave them inline, declare:

```css
nav a {
  display: inline-block;
  width: 20%;
}
```

Flexible-box layout is another way to achieve this effect, and is probably better suited to it in most if not all cases.

### 7.3.16 Flow Display

The values `flow` and `flow-root` deserve a moment of explanation. Declaring an element to be laid out using display: flow means that it should use block-and-inline layout, the same as normal. That is, unless it’s combined with inline, in which case it generates an inline box.

In other words, the first two of the following rules will result in a block box, whereas the third will yield an inline box.

```css
#first {
  display: flow;
}
#second {
  display: block flow;
}
#third {
  display: inline flow;
}
```

The reason for this pattern is that CSS is moving to a system where there are two kinds of display: the `outer display type` and the `inner display typ`e. Value keywords like `block` and `inline` represent the outer display type, which provides how the display box interacts with its surroundings. The inner display, in this case `flow`, describes what should happen inside the element.

This approach allows for declarations like display: inline table to indicate an element should generate a table formatting context within, but relate to its surrounding content as an inline element. (The legacy value `inline-table` has the same effect.)

`display: flow-root`, on the other hand, always generates a block box, with a new block formatting context inside itself. This is the sort of thing that would be applied to the root element of a document, like `html`, to say “this is where the formatting root lies.”

The old `display` values you may be familiar with are still available. Table 7-1 shows how the old values will be represented using the new values.

//

As of late 2017, `flow` and `flow-root` were supported by Firefox and Chrome, but no other browsers.

### 7.3.17 Contents Display

There is one fascinating new addition to `display`, which is the value `contents`. When applied to an element, `display: contents` causes the element to be removed from page formatting, and effectively “elevates” its child elements to its level. As an example, consider the following simple CSS and HTML.

```css
ul {
  border: 1px solid red;
}
li {
  border: 1px solid silver;
}
```

```html
<ul>
  <li>The first list item.</li>
  <li>List Item II: The Listening.</li>
  <li>List item the third.</li>
</ul>
```

That will yield an unordered list with a red border, and three list items with silver borders.

If we then apply `display: contents` to the `ul` element, the user agent will render things as if the `<ul>` and `</ul>` lines had been deleted from the document source. The difference in the regular result and the `contents` result is shown in Figure 7-58.

// 7-58

The list items are still list items, and act like them, but visually, the `ul` is gone, as if had never been. The means not only does its border go away, but also the top and bottom margins that usually separate the list from surrounding content. This is why the second list in Figure 7-58 appears higher up than the first.

As of late 2017, only Firefox browsers supported `display: contents`. At the time, implementation work was being done for the Chrome/Blink line of browsers.

### 7.3.18 Other Display Values

There are a great many more display values we haven’t covered in this chapter, and won’t. The various table-related values will come up in a later chapter devoted to table layout, and we’ll talk about list items again in the chapter on counters and generated content.

Values we won’t really talk about are the ruby-related values, which need their own book and are poorly supported as of late 2017; and `run-in`, which never caught on and will either be dropped from CSS, or will return with a new definition.

### 7.3.19 Computed Values

The computed value of `display` can change if an element is floated or positioned. It can also change when declared for the root element. In fact, the values `display`, `position`, and `float` interact in interesting ways.

If an element is absolutely positioned, the value of `float` is set to `none`. For either floated or absolutely positioned elements, the computed value of `display` is determined by the declared value, as shown in Table 7-2.

//

In the case of the root element, declaring either of the values `inline-table` or `table` results in a computed value of `table`, whereas declaring `none` results in the same computed value. All other display values are computed to be block.

## 7.4 Summary

Although some aspects of the CSS formatting model may seem counterintuitive at first, they begin to make sense the more one works with them. In many cases, rules that seem nonsensical or even idiotic turn out to exist in order to prevent bizarre or otherwise undesirable document displays. Block-level elements are in many ways easy to understand, and affecting their layout is typically a simple task. Inline elements, on the other hand, can be trickier to manage, as a number of factors come into play, not least of which is whether the element is replaced or nonreplaced.
