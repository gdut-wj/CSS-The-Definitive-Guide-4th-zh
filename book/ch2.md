# 第 2 章 选择器 Selectors

One of the primary advantages of CSS is its ability to easily apply a set of styles to all elements of the same type. Unimpressed? Consider this: by editing a single line of CSS, you can change the colors of all your headings. Don’t like the blue you’re using? Change that one line of code, and they can all be purple, yellow, maroon, or any other color you desire. That lets you, the designer, focus on design, rather than grunt work. The next time you’re in a meeting and someone wants to see headings with a different shade of green, just edit your style and hit Reload. `Voilà!` The results are accomplished in seconds and there for everyone to see.

CSS 的一个主要优势——尤其对设计者而言——是它能够轻松地把一组样式应用到同一类型的所有元素。印象不够深刻？想象这样的场景：通过编辑单行 CSS，你可以修改所有标题的颜色。不喜欢正在使用的蓝色？修改一行代码，把它们都变成紫色、黄色、栗色等等任何想要的颜色。这可以让你，设计师，专注于设计而不是繁琐的工作。下次会议中，有人想看绿色标题，你只需要编辑样式然而点击重新加载。瞧!几秒钟就完成了，每个人都可以看到。

CSS can’t solve all your problems—you can’t use it to change the colorspace of your PNGs, for example, at least not yet—but it can make some global changes much easier. So let’s begin with selectors and structure.

当然，CSS 不能解决所有问题——比如，它不能用来改变 PNG 图片的颜色空间，至少现在还不能——但它确实让全局修改变得容易多了。我们先从选择器和结构开始。

## 2.1 基本样式规则 Basic Style Rules

As stated, a central feature of CSS is its ability to apply certain rules to an entire set of element types in a document. For example, let’s say that you want to make the text of all `h2` elements appear gray. Using old-school HTML, you’d have to do this by inserting `<font color="gray">…</font>` tags inside all your `h2` elements. Using the `style` attribute, which is also bad practice, would require you to include `style="color: gray;"` in all your h2 elements, like this:

如上所述，CSS 的核心特性是将某些样式应用于文档中的整个元素类型的能力。例如，如果你想把所有`h2`元素的文本显示为灰色，使用老套的 HTML，你必须在所有的`h2`元素中插入`<font color="gray">…</font>`标签；使用`style`属性也不好，这需要你在所有的`h2`元素上添加`style="color: gray;"`:

```html
<h2><font color="gray">This is h2 text</font></h2>
<h2 style="color: gray;">This is h2 text</h2>
```

This will be a tedious process if your document contains a lot of `h2` elements. Worse, if you later decide that you want all those `h2`s to be green instead of gray, you’d have to start the manual tagging all over again. (Yes, this is really how it used to be done!)

显然，如果你的文档里面有许多`h2`元素，修改过程将是乏味的。更糟糕的是，如果你之后又想把所有的`h2`从灰色变成绿色，你又得重新开始手动设置一遍便签。（没错，以前就是这么干的！）

CSS allows you to create rules that are simple to change, edit, and apply to all the text elements you define (the next section will explain how these rules work). For example, you can write this rule once to make all your `h2` elements gray:

CSS 让你可以创建易于编辑的规则，并把它们应用于所有你定义的文本元素（下一部分将解释规则如何生效）。例如，简单地写一次下面的规则，把所有的`h2`元素都变成灰色：

```css
h2 {
  color: gray;
}
```

If you want to change all `h2` text to another color—say, silver—just alter the value:

如果你想把所有`h2`的文本变成另一种颜色——比如银色——只要简单地选择（属性）值：

```css
h2 {
  color: silver;
}
```

### 元素选择器 Element Selectors

An element selector is most often an HTML element, but not always. For example, if a CSS file contains styles for an XML document, the element selectors might look something like this:

元素选择器通常都是 HTML 元素，但也有例外。例如，如果 CSS 文件的样式是用于 XML 文档的，元素选择器可能会是这样：

```css
quote {
  color: gray;
}
bib {
  color: red;
}
booktitle {
  color: purple;
}
myElement {
  color: red;
}
```

In other words, the elements of the document serve as the most basic selectors. In XML, a selector could be anything, since XML allows for the creation of new markup languages that can have just about anything as an element name. If you’re styling an HTML document, on the other hand, the selector will generally be one of the many HTML elements such as `p`, `h3`, `em`, `a`, or even `html` itself. For example:

换句话说，文档的元素被用作最基本的选择器。在 XML 中，选择器可以是任何东西，因为 XML 允许创建新的标记语言，任何东西都可以作为元素名称。另一方面，如果为 HTML 文档添加样式，选择器一般是许多 HTML 元素之一，如`p`，`h3`，`em`，`a`,甚至`html`元素本身。例如：

```css
html {
  color: black;
}
h1 {
  color: gray;
}
h2 {
  color: silver;
}
```

样式表的结果在图 1-1 中展示：

![图1-1：简单文档的简单样式](figure1-1.png)

_图 1-1：简单文档的简单样式_

Once you’ve globally applied styles directly to elements, you can shift those styles from one element to another. Let’s say you decide that the paragraph text, not the `h1` elements, in Figure 2-1 should be gray. No problem. Just change the `h1` selector to `p`:

当你直接全局地给元素设置了样式，你可以把样式从一个样式移到另一个样式上。如果你想要图 1-1 中的段落文本而不是`h1`元素是灰色，没问题，只要把`h1`选择器换成`p`就行了;

```css
html {
  color: black;
}
p {
  color: gray;
}
h2 {
  color: silver;
}
```

结果在图 1-2 中展示:

![图1-2：把样式从一个元素移到另一个上](figure1-2.png)

图 1-2：把样式从一个元素移到另一个上

### 声明和关键字 Declarations and Keywords

The declaration block contains one or more declarations. A declaration is always formatted as a property followed by a colon and then a value followed by a semicolon. The colon and semicolon can be followed by zero or more spaces. In nearly all cases, a `value` is either a single keyword or a space-separated list of one or more keywords that are permitted for that property. If you use an incorrect property or value in a declaration, the whole rule will be ignored. Thus, the following two declarations would fail:

声明块包含一或多条声明。一条声明的格式总是一个**属性**后面跟着一个冒号，然后一个**值**后面跟着一个分号。冒号和分号后面可以有零或多个空白。几乎所有的值都是单个关键字或者空白分隔的当前属性允许的多个关键字列表。如果在一条声明中使用了错误的属性或值，整条规则都会被忽略。因此，下面这两条声明是无效的：

```css
brain-size: 2cm; /* unknown property 'brain-size' */
color: ultraviolet; /* unknown value 'ultraviolet' */
```

In an instance where you can use more than one keyword for a property’s value, the keywords are usually separated by spaces, with some cases requiring slashes (/) or commas. Not every property can accept multiple keywords, but many, such as the `font` property, can. Let’s say you want to define medium-sized Helvetica for paragraph text, as illustrated in Figure 2-3.

属性值可以使用多个关键字的时候，关键字通常用空白分隔，有些情况下需要斜线（`/`）。很多属性可以接收多个关键字（如`font`属性），但不是全部属性都可以。如果想为段落字体设置中等大小的 Helvetica 字体，就像在图 1-3 中显示的：

![图1-3：属性值包含多个关键字的结果](figure1-3.png)

_图 1-3：属性值包含多个关键字的结果_

The rule would read as follows:

规则将是这样：

```css
p {
  font: medium Helvetica;
}
```

Note the space between medium and Helvetica, each of which is a keyword (the first is the font’s size and the second is the actual font name). The space allows the user agent to distinguish between the two keywords and apply them correctly. The semicolon indicates that the declaration has been concluded.

注意两个关键字`medium`和`Helvetica`之间的空白（第一个是字体大小，第二个是字体名称）。空白使用户代理可以分辨出两个关键字并正确地使用它们。分号指明当前声明已经结束。

These space-separated words are referred to as keywords because, taken together, they form the value of the property in question. For instance, consider the following fictional rule:

这些空白分隔的词被称为**关键字**，因为它们在一起组成了属性的值。例如下面这个虚拟的规则：

```css
rainbow: red orange yellow green blue indigo violet;
```

There is no such property as `rainbow`, but the example is useful for illustrative purposes. The value of `rainbow` is red orange yellow green blue indigo violet, and the seven keywords add up to a single, unique value. We can redefine the value for `rainbow` as follows:

当然不存在`rainbow`这个属性，它只是被当做例子来进行说明。`rainbow`的值是`red orange yellow green blue indigo violet`，这 7 个关键字放在一起组成了一个唯一的值。我们可以像下面这样重新定义`rainbow`的值：

```css
rainbow: infrared red orange yellow green blue indigo violet ultraviolet;
```

Now we have a new value for `rainbow` composed of nine keywords instead of seven. Although the two values look mostly the same, they are as unique and different as zero and one. This may seem an abstract point, but it’s critical to understanding some of the subtler effects of specificity and the cascade (covered in later in this book).

现在我们有了一个由 9 个而不是 7 个关键字组成的新值。虽然这两个值看起来很像，但他们就像 0 和 1 一样是不同而且唯一的。这里好像有点抽象，但它对理解一些特性和层叠（在本书后面部分讨论）的微妙影响是至关重要的。

As we’ve seen, CSS keywords are usually separated by spaces. In CSS2.1 there was one exception: in the CSS property `font`, there is exactly one place where a forward slash (/) could be used to separate two specific keywords. Here’s an example:

如我们所见。CSS 关键字通常使用空白分隔。在 CSS2.1 中有个例外：`font`属性值可以使用正斜杠（`/`）分隔两个特殊的关键字，例如：

```css
h2 {
  font: large/150% sans-serif;
}
```

The slash separates the keywords that set the element’s font size and line height. This is the only place the slash is allowed to appear in the `font` declaration. All of the other keywords allowed for `font` are separated by spaces.

斜线分隔的关键字设置元素的字体大小和行高，这是`font`声明中唯一允许使用斜线的地方，`font`的所有其他关键字都使用空白分隔。

The slash has since worked its way into a number of other properties’ values. These include, but may not always be limited to the following:

斜线已经可以使用在其他一些属性值中，包括可能不限于下面的属性：

- `background`
- `border-image`
- `border-radius`
- `grid`
- `grid-area`
- `grid-column`
- `grid-row`
- `grid-template`
- `mask-border`

There are also some keywords that are separated by commas. When declaring multiple values, such as multiple background images, transition properties, and shadows, the declarations are separated with commas. Additionally, parameters in functions, such as linear gradients and transforms, are comma separated, as the following example shows:

还有些关键字使用逗号分隔。声明多个值时，例如多背景图片、变换属性和阴影，声明使用逗号分隔。另外函数参数，如`linear gradiennts`和`transform`等，也使用逗号分隔，示例：

```css
.box {
  box-shadow: inset -1px -1px white, 3px 3px 3px rgba(0, 0, 0, 0.2);
  background-image: url(myimage.png), linear-gradient(180deg, #fff 0%, #000 100%);
  transform: translate(100px, 200px);
}
a:hover {
  transition: color, background-color 200ms ease-in 50ms;
}
```

Those are the basics of simple declarations, but they can get much more complex. The next section begins to show you just how powerful CSS can be.

这些是基础的简单声明，但它们也可以变得非常复杂。下一部分我们将要展示 CSS 有多么强大。

## 2.2 分组 Grouping

So far, we’ve seen fairly simple techniques for applying a single style to a single selector. But what if you want the same style to apply to multiple elements? If that’s the case, you’ll want to use more than one selector or apply more than one style to an element or group of elements.

如我们所见，把一个简单样式应用在一个简单选择器上是非常简单的，但是如果你想把相同的样式引用在多个元素上应该怎么做呢？这种场景下，你会想要把多个选择器或多个样式应用在一个或一组元素上。

### Grouping Selectors

Let’s say you want both `h2` elements and paragraphs to have gray text. The easiest way to accomplish this is to use the following declaration:

如果你想让`h2`元素和段落都显示灰色文本，最简单的方式是使用下面的声明：

```css
h2,
p {
  color: gray;
}
```

By placing the `h2` and `p` selectors on the left side of the rule and separating them with a comma, you’ve defined a rule where the style on the right (color: gray;) applies to the elements referenced by both selectors. The comma tells the browser that there are two different selectors involved in the rule. Leaving out the comma would give the rule a completely different meaning, which we’ll explore in “Descendant Selectors” on page 56.

把`h2`和`p`选择器放置在规则左边并用逗号分隔，这种方式定义了一条把右边样式（`color: gray;`）应用于两个选择器的规则。逗号告诉浏览器规则里面是两个不同的选择器，如果去掉逗号，会使语句变成另外一条含义完全不同的规则。（参见后面的章节“后代选择器”。）

There are really no limits to how many selectors you can group together. For example, if you want to display a large number of elements in gray, you might use something like the following rule:

分组的选择器数目没有限制，例如，如果你想把一大堆元素都设置成灰色，你可以用这样的规则：

```css
body,
table,
th,
td,
h1,
h2,
h3,
h4,
p,
pre,
strong,
em,
b,
i {
  color: gray;
}
```

Grouping allows an author to drastically compact certain types of style assignments, which makes for a shorter stylesheet. The following alternatives produce exactly the same result, but it’s pretty obvious which one is easier to type:

分组允许开发者可以大幅压缩样式分配，从而使样式表更精简。下面两种写法的结果是一样的，哪一种更容易输入是很明显的：

```css
h1 {
  color: purple;
}
h2 {
  color: purple;
}
h3 {
  color: purple;
}
h4 {
  color: purple;
}
h5 {
  color: purple;
}
h6 {
  color: purple;
}

h1,
h2,
h3,
h4,
h5,
h6 {
  color: purple;
}
```

Grouping allows for some interesting choices. For example, all of the groups of rules in the following example are equivalent—each merely shows a different way of grouping both selectors and declarations:

分组允许做出一些有趣的选择，例如下面例子中的写法都是等效的，每个例子展示了一种分组选择器和声明的不同方式：

```css
/* group 1 */
h1 {
  color: silver;
  background: white;
}
h2 {
  color: silver;
  background: gray;
}
h3 {
  color: white;
  background: gray;
}
h4 {
  color: silver;
  background: white;
}
b {
  color: gray;
  background: white;
}

/* group 2 */
h1,
h2,
h4 {
  color: silver;
}
h2,
h3 {
  background: gray;
}
h1,
h4,
b {
  background: white;
}
h3 {
  color: white;
}
b {
  color: gray;
}

/* group 3 */
h1,
h4 {
  color: silver;
  background: white;
}
h2 {
  color: silver;
}
h3 {
  color: white;
}
h2,
h3 {
  background: gray;
}
b {
  color: gray;
  background: white;
}
```

Any of these will yield the result shown in Figure 2-4. (These styles use grouped declarations, which are explained in “Grouping Declarations” on page 35.)

每个例子都会生成图 1-4 显示的结果。（这些样式使用的分组声明，将在接下来的“分组声明”中探讨。）

![图4：等效样式表的结果](figure1-4.png)

_图 4：等效样式表的结果_

#### 通配选择器 The universal selector

CSS2 introduced a new simple selector called the universal selector, displayed as an asterisk (\*). This selector matches any element at all, much like a wildcard. For example, to make every single element in a document red, you would write:

CSS2 引入了一个新的简单选择器叫做**通配选择器**，使用星号（`*`）标注。这个选择器就像一张百搭牌，可以匹配所有元素。例如，要把文档中的每个元素（文本）都设置成红色，可以这样写：

```css
* {
  color: red;
}
```

This declaration is equivalent to a grouped selector that lists every single element contained within the document. The universal selector lets you assign the `color` value `red` to every element in the document in one efficient stroke. Beware, however: although the universal selector is convenient, with a specificity on 0-0-0; and because it targets everything within its declaration scope, it can have unintended consequences, which are discussed later in this book.

此声明等效于一个列出文档中所有元素的分组选择器。通配选择器允许你以一种有效的方式为文档中每个元素的`color`属性设置一个值`red`。但是，要注意，虽然通配选择器很方便，它的特度是 0-0-0，但因为会匹配所有元素，它可能带来意外的后果，我们将在本书后面的部分讨论。

### Grouping Declarations

### Grouping Everything

### New Elements in Old Browsers

## 2.3 Class and ID Selectors

### Class Selectors

### Multiple Classes

### ID Selectors

### Deciding Between Class and ID

## 2.4 Attribute Selectors

### Simple Attribute Selectors

### Selection Based on Exact Attribute Value

### Selection Based on Partial Attribute Values

### A Particular Attribute Selection Type

### The Case Insensitivity Identifier

## 2.5 Using Document Structure

### Understanding the Parent-Child Relationship

### Descendant Selectors

### Selecting Children

### Selecting Adjacent Sibling Elements

### Selecting Following Siblings

## 2.6 Pseudo-Class Selectors

### Combining Pseudo-Classes

### Structural Pseudo-Classes

### Dynamic Pseudo-Classes

### UI-State Pseudo-Classes

### The :target Pseudo-Class

### The :lang Pseudo-Class

### The Negation Pseudo-Class

## 2.7 Pseudo-Element Selectors

### Styling the First Letter

### Styling the First Line

### Restrictions on ::first-letter and ::first-line

### Styling (or Creating) Content Before and After Elements

## 2.8 Summary
