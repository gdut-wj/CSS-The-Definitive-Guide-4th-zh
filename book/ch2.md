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

### 2.1.1 元素选择器 Element Selectors

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

<div style="margin: 0 auto; width: 50%;">
    <img src='./figure2-1.png' style=""/>
</div>
<p align="center">图 2-1：简单文档的简单样式</p>

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

<div style="margin: 0 auto; width: 50%;">
    <img src='./figure2-2.png' style=""/>
</div>
<p align="center">图 2-把样式从一个元素移到另一个上</p>

### 2.1.2 声明和关键字 Declarations and Keywords

The declaration block contains one or more declarations. A declaration is always formatted as a property followed by a colon and then a value followed by a semicolon. The colon and semicolon can be followed by zero or more spaces. In nearly all cases, a `value` is either a single keyword or a space-separated list of one or more keywords that are permitted for that property. If you use an incorrect property or value in a declaration, the whole rule will be ignored. Thus, the following two declarations would fail:

声明块包含一或多条声明。一条声明的格式总是一个**属性**后面跟着一个冒号，然后一个**值**后面跟着一个分号。冒号和分号后面可以有零或多个空白。几乎所有的值都是单个关键字或者空白分隔的当前属性允许的多个关键字列表。如果在一条声明中使用了错误的属性或值，整条规则都会被忽略。因此，下面这两条声明是无效的：

```css
brain-size: 2cm; /* unknown property 'brain-size' */
color: ultraviolet; /* unknown value 'ultraviolet' */
```

In an instance where you can use more than one keyword for a property’s value, the keywords are usually separated by spaces, with some cases requiring slashes (/) or commas. Not every property can accept multiple keywords, but many, such as the `font` property, can. Let’s say you want to define medium-sized Helvetica for paragraph text, as illustrated in Figure 2-3.

属性值可以使用多个关键字的时候，关键字通常用空白分隔，有些情况下需要斜线（`/`）。很多属性可以接收多个关键字（如`font`属性），但不是全部属性都可以。如果想为段落字体设置中等大小的 Helvetica 字体，就像在图 1-3 中显示的：

<div style="margin: 0 auto; width: 50%;">
    <img src='./figure2-3.png' style=""/>
</div>
<p align="center">图 2-3 属性值包含多个关键字的结果</p>

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

### 2.2.1 Grouping Selectors

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

```
body,table,th,td,h1,h2,h3,h4,p,pre,strong,em,b,i {color: gray;}
```

Grouping allows an author to drastically compact certain types of style assignments, which makes for a shorter stylesheet. The following alternatives produce exactly the same result, but it’s pretty obvious which one is easier to type:

分组允许开发者可以大幅压缩样式分配，从而使样式表更精简。下面两种写法的结果是一样的，哪一种更容易输入是很明显的：

```css
h1 {color: purple;}
h2 {color: purple;}
h3 {color: purple;}
h4 {color: purple;}
h5 {color: purple;}
h6 {color: purple;}

h1,h2,h3,h4,h5,h6 {color: purple;}
.
```

Grouping allows for some interesting choices. For example, all of the groups of rules in the following example are equivalent—each merely shows a different way of grouping both selectors and declarations:

分组允许做出一些有趣的选择，例如下面例子中的写法都是等效的，每个例子展示了一种分组选择器和声明的不同方式：

```css
/* group 1 */
h1 {color: silver; background: white;}
h2 {color: silver; background: gray;}
h3 {color: white; background: gray;}
h4 {color: silver; background: white;}
b {color: gray; background: white;}

/* group 2 */
h1,h2,h4 {color: silver;}
h2,h3 {background: gray;}
h1,h4,b {background: white;}
h3 {color: white;}
b {color: gray;}

/* group 3 */
h1,h4 {color: silver; background: white;}
h2 {color: silver;}
h3 {color: white;}
h2,h3 {background: gray;}
b {color: gray; background: white;}
.
```

Any of these will yield the result shown in Figure 2-4. (These styles use grouped declarations, which are explained in “Grouping Declarations” on page 35.)

每个例子都会生成图 2-4 显示的结果。（这些样式使用的分组声明，将在接下来的“分组声明”中探讨。）

<div style="margin: 0 auto; width: 50%;">
    <img src='./figure2-4.png' style=""/>
</div>
<p align="center">图 2-4 等效样式表的结果</p>

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

### 2.2.2 分组声明 Grouping Declarations

Since you can group selectors together into a single rule, it follows that you can also group declarations. Assuming that you want all `h1` elements to appear in purple, 18-pixel-high Helvetica text on an aqua background (and you don’t mind blinding your readers), you could write your styles like this:

规则中分组选择器，也可以分组声明。假如你想把所有的`h1`元素设置为紫色、18 像素高的 Helvetica 字体显示在水色背景上（你不介意闪瞎用户），你可以把样式写成这样：

```css
h1 {
  font: 18px Helvetica;
}
h1 {
  color: purple;
}
h1 {
  background: aqua;
}
```

But this method is inefficient—imagine creating such a list for an element that will carry 10 or 15 styles! Instead, you can group your declarations together:

但这种方式是低效的——想象一下为每个元素创建一个 10 或 15 个样式的列表！你可以把声明组合在一起来替代前面的写法：

```css
h1 {
  font: 18px Helvetica;
  color: purple;
  background: aqua;
}
```

This will have exactly the same effect as the three-line stylesheet just shown.

这种写法和上面的三行样式表是一样的结果。

Note that using semicolons at the end of each declaration is crucial when you’re grouping them. Browsers ignore whitespace in stylesheets, so the user agent must rely on correct syntax to parse the stylesheet. You can fearlessly format styles like the following:

要注意分组来写的时候每条声明后面的分号至关重要。浏览器会忽略样式表中的空白，因此用户代理要依赖正确的语法来解析样式表。你可以这样格式化样式表：

```css
h1 {
  font: 18px Helvetica;
  color: purple;
  background: aqua;
}
```

You can also minimize your CSS, removing all non-required spaces.

也可以通过移除不必要的空白压缩 CSS：

```
h1{font:18px Helvetica;color: purple;background: aqua;}
```

Ignoring whitespace, the last three are treated equally by the server, but the second one is most human readable, and the recommended method of marking up your CSS during development. (You might choose to minimize your CSS for networkperformance reasons, but this is usually handled by a server-side script, caching network, or other service.)

上例的后三种写法对服务器来说是等效的，但第二种更易于人类阅读，也是 CSS 开发环境中的推荐写法。（也许压缩 CSS 是出于提高网络性能的原因，但通常这应该由服务器端脚本、网络缓存以及其他服务等来完成。）

If the semicolon is omitted on the second statement, the user agent will interpret the stylesheet as follows:

如果第二个例子中漏掉了第二个分号，用户代理会把样式表理解成下面这样：

```css
h1 {
	font: 18px Helvetica;
	color: purple background: aqua;
}
```

Because background: is not a valid value for color, and because color can be given only one keyword, a user agent will ignore the color declaration (including the back ground: aqua part) entirely. You might think the browser would at least render h1s as purple text without an aqua background, but not so. Instead, they will be the default color (which is usually black) with a transparent background (which is also a default). The declaration font: 18px Helvetica will still take effect since it was correctly terminated with a semicolon.

因为`background:`并不是`color`属性的合法值，而且`color`属性只能有一个关键字，因此用户代理会完全忽略`color`声明（包括`background: aqua`的部分）。你可能认为浏览器至少会把`h1`设置成紫色字体但没有水色背景，但是如果浏览器本身的实现是正确的话，你会连紫色的`h1`也看不到，它们会被设置成默认颜色（通常是黑色）和透明背景（默认）。声明`font: 18px Helvetica`将会依然生效，因为它是以一个分号正确结束的。

Although it is not technically necessary to follow the last declaration of a rule with a semicolon in CSS, it is generally good practice to do so. First, it will keep you in the habit of terminating your declarations with semicolons, the lack of which is one of the most common causes of rendering errors. Second, if you decide to add another declaration to a rule, you won’t have to worry about forgetting to insert an extra semicolon. Third, if you ever use a preprocessor like Sass, trailing semicolons are often required for all declarations. Avoid all these problems—always follow a declaration with a semicolon, wherever the rule appears.

_**虽然从技术上来讲，最后一条声明后面的分号并不是必需的，但通常为它加上分号是一个好的实践。首先，丢失分号是渲染错误的最常见的原因之一，遵循这个实践可以使你保持使用分号结束声明的良好习惯；其次，当你为样式规则追加一条声明的时候，不必担心前面的声明后面是否忘了插入分号；第三，如果你曾使用过像 Sass 这样的预处理器，通常尾部的分号对所有声明都是必需的。在每条声明后都跟随一个分号来避免上面的问题。**_

As with selector grouping, declaration grouping is a convenient way to keep your stylesheets short, expressive, and easy to maintain.

分组声明和分组选择器一起使用，可以方便地保持样式表简洁、富有表现力和易于维护。

### 2.2.3 分组的一切 Grouping Everything

You now know that you can group selectors and you can group declarations. By combining both kinds of grouping in single rules, you can define very complex styles using only a few statements. Now, what if you want to assign some complex styles to all the headings in a document, and you want the same styles to be applied to all of them? Here’s how to do it:

选择器和声明都可以分组，在单条样式中使用这两种分组，可以使用很少的声明式定义非常复杂的样式。如果你要把一些复杂样式应用在文档的所有标题上，而且为他们应用相同的样式，应该怎么做呢？下面是做法：

```css
h1,h2,h3,h4,h5,h6 {
  color: gray;
  background: white;
  padding: 0.5em;
  border: 1px solid black;
  font-family: Charcoal, sans-serif;
}
.
```

Here we’ve grouped the selectors, so the styles on the right side of the rule will be applied to all the headings listed; grouping the declarations means that all of the listed styles will be applied to the selectors on the left side of the rule. The result of this rule is shown in Figure 2-5.

因为分组了选择器，右侧的规则会应用在列出的所有标题上；分组声明表明所有列出的样式都会被应用在左侧的选择器上。规则显示的结果如图 2-5。

<div style="margin: 0 auto; width: 50%;">
    <img src='./figure2-5.png' style=""/>
</div>
<p align="center">图 2-5 分组选择器和规则</p>

This approach is preferable to the drawn-out alternative, which would begin with something like this:

这种方案比下面的方案更好：

```css
h1 {color: gray;}
h2 {color: gray;}
h3 {color: gray;}
h4 {color: gray;}
h5 {color: gray;}
h6 {color: gray;}
h1 {background: white;}
h2 {background: white;}
h3 {background: white;}
.
```

and continue for many lines. You can write out your styles the long way, but I wouldn’t recommend it—editing them would be as tedious as using style attributes everywhere!

等等还有许多行。你也**可以**像这样写出长长的样式，但我建议你不要这样做——编辑它们就像到处使用`style`属性一样无聊。

It’s possible to add even more expression to selectors and to apply styles in a way that cuts across elements in favor of types of information. To get something so powerful, you’ll have to do a little work in return, but it’s well worth it.

可以在选择器中加入更多的表达式，并以跨元素的方式应用样式。当然，要得到这么强大的东西需要付出一些工作，但这是值得的。

### 旧浏览器中的新元素 New Elements in Old Browsers

With updates to HTML, such as the HTML5 specification, new elements have come into being. Some browsers predate these newer elements, and so don’t recognize them. Versions of Internet Explorer prior to IE9, for example, did not support selecting elements they did not understand. The solution was to create the element in the DOM, thereby informing the browser that said element exists.

作为 HTML 的升级，HTML5 规范引入了新的元素。比新元素更早的浏览器不能识别它们。例如，IE9 以前的浏览器无法选择它们不支持的元素。解决办法是在 DOM 中创建元素，以此告知浏览器元素的存在。

For example, IE8 does not recognize the `<main>` element. The following JavaScript line informs IE8 of `main’s` existence:

例如，IE8 不能识别`<main>`元素，下面这行 JavaScript 代码告诉 IE8 `main`元素的存在：

```js
document.createElement('main')
```

By running that line of code, older versions of Internet Explorer will recognize the existence of the element, allowing it to be selected and styled.

执行这行代码，旧版本的 IE 浏览器可以识别到这些元素，并允许选择它们以及为它们添加样式。

## 2.3 类和 ID 选择器 Class and ID Selectors

So far, we’ve been grouping selectors and declarations together in a variety of ways, but the selectors we’ve been using are very simple ones that refer only to document elements. Element selectors are fine up to a point, but there are times when you need something a little more specialized.

我们已经以各种方式组合使用了选择器和声明，但我们使用的选择器都非常简单。这些选择器只能用文档元素本身来选择，它们很好用，但有时你需要更专门的选择器。

In addition to raw document elements, there are `class selectors` and `ID selectors`, which let you assign styles in a way that is independent of document elements. These selectors can be used on their own or in conjunction with element selectors. However, they work only if you’ve marked up your document appropriately, so using them generally involves a little forethought and planning.

除了原始的文档元素，还有**类选择器**和 **ID 选择器**，它们允许以独立于文档元素的方式分配样式。这些选择器可以单独使用，也可以与元素选择器结合使用。但是，它们只有在文档被正确标记的时候才能生效，因此使用它们通常需要做一些预想和规划。

For example, say you’re drafting a document that discusses ways of handling plutonium. The document contains various warnings about safely dealing with such a dangerous substance. You want each warning to appear in boldface text so that it will stand out. However, you don’t know which elements these warnings will be. Some warnings could be entire paragraphs, while others could be a single item within a lengthy list or a small section of text. So, you can’t define a rule using element selectors of any kind. Suppose you tried this route:

例如，假设你正在起草一份讨论处理钚的方法的文件。 该文件包含关于安全处理这种危险物质的各种警告。 您希望每个警告都以粗体文本显示以便更突出，但你不知道这些警告将是哪些元素。 一些警告可能是整个段落，而其他警告可能是冗长列表中的单个项目或一小段文本。 因此，你不能使用任何种类的元素选择器定义规则。 假设你尝试这样写：

```css
p {
  font-weight: bold;
  color: red;
}
```

`All` paragraphs would be red and bold, not just those that contain warnings. You need a way to select only the text that contains warnings, or more precisely, a way to select only those elements that are warnings. How do you do it? You apply styles to parts of the document that have been marked in a certain way, independent of the elements involved, by using class selectors.

**所有的**段落都会被加粗，而不仅仅是包含警告的那些。你需要一种方法来选择仅包含警告的文本，或者更准确地说，只选择那些警告元素。怎么做呢？使用类选择器，把样式应用于文档中那些被用特定方式标记出来的部分，而无论是什么元素。

### 2.3.1 类选择器 Class Selectors

The most common way to apply styles without worrying about the elements involved is to use class selectors. Before you can use them, however, you need to modify your actual document markup so that the class selectors will work. Enter the class attribute:

忽略元素类型应用样式的最常用方式，是使用类选择器。但是在使用它们之前需要设置文档标记，以便选择器能够生效。添加`class`属性：

```html
<p class="warning">When handling plutonium, care must be taken to avoid the formation of a critical mass.</p>
<p>
  With plutonium,
  <span class="warning">the possibility of implosion is very real, and must be avoided at all costs</span>. This can be
  accomplished by keeping the various masses separate.
</p>
```

To associate the styles of a class selector with an element, you must assign a `class` attribute the appropriate value. In the previous code block, a `class` value of `warning` was assigned to two elements: the first paragraph and the `span` element in the second paragraph.

要把类选择器和一个元素联系起来，必须为`class`属性设置一个合适的值。在上面的代码中，一个值为`warning`的类被分配给两个元素：第一个段落和第二个段落里的`span`元素。

All you need now is a way to apply styles to these classed elements. In HTML documents, you can use a compact notation where the name of a `class` is preceded by a period (.) and can be joined with an element selector:

现在只需要一种方式把样式应用在这些元素上。在 HTML 文档中，可同`class`名称紧跟一个句点（.），并且可以与元素选择器一起使用：

```css
.warning {
  font-weight: bold;
}
```

When combined with the example markup shown earlier, this simple rule has the effect shown in Figure 2-6. That is, the declaration font-weight: bold will be applied to every element (thanks to the presence of the implicit universal selector) that carries a class attribute with a value of warning.

与前面所示的示例标记集合使用，这个简单规则的效果如图 2-6 所示。亦即，声明`font-weight: bold`会应用在每个（得益于隐含的通配选择器）`class`属性值为`warning`的元素上。

_**通配选择器的符号是`*`，使用 ID、类、属性选择器、伪类选择器以及伪元素选择器等时，如果没有结合元素选择器，它们会隐式地包含通配选择器。**_

<div style="margin: 0 auto; width: 50%;">
    <img src='./figure2-6.png' style=""/>
</div>
<p align="center">图 2-6：使用类选择器</p>

As you can see, the class selector works by directly referencing a value that will be found in the class attribute of an element. This reference is always preceded by a period (.), which marks it as a class selector. The period helps keep the class selector separate from anything with which it might be combined—such as an element selector. For example, you may want boldface text only when an entire paragraph is a warning:

如你所见，类选择器直接通过元素`class`属性中的值来引用元素。引用始终以句点（.）开头，标记它是一个**类选择器**。句点把类选择器和与其组合在一起的其他部分区分开来（例如元素选择器）。假如当只有整个段落是警告时，才设置为粗体：

```css
p.warning {
  font-weight: bold;
}
```

The selector now matches any p elements that have a class attribute containing the word warning, but no other elements of any kind, classed or otherwise. Since the span element is not a paragraph, the rule’s selector doesn’t match it, and it won’t be displayed using boldfaced text.

选择器现在只会匹配任何`class`属性值中包含单词`warning`的`p`元素，而其他类型的元素无论有没有设置`class`值都不会被选中。因为`span`元素不是段落，选择器不会匹配到它，因此它不会显示为粗体文字。

If you did want to assign different styles to the `span` element, you could use the selector `span.warning`:

如果想为`span`元素分配不同的样式，可以使用选择符`span.warning`：

```css
p.warning {
  font-weight: bold;
}
span.warning {
  font-style: italic;
}
```

In this case, the warning paragraph is boldfaced, while the warning `span` is italicized. Each rule applies only to a specific type of element/class combination, so it does not leak over to other elements.

这样，警告段落被设置为粗体，而警告`span`被设置为斜体。每个规则仅应用于特定的元素/类组合，而不会影响到其他元素。

Another option is to use a combination of a general class selector and an elementspecific class selector to make the styles even more useful, as in the following markup:

另一种做法是使用一个一般的类选择器和一个特定元素的类选择器，来让样式更加有用，例如这样：

```css
.warning {
  font-style: italic;
}
span.warning {
  font-weight: bold;
}
```

The results are shown in Figure 2-7.

效果在图 2-7 中。

<div style="margin: 0 auto; width: 50%;">
    <img src='./figure2-7.png' style=""/>
</div>
<p align="center">图 2-7：使用一般和特定选择器联合样式</p>

In this situation, any warning text will be italicized, but only the text within a `span` element with a `class` of `warning` will be both boldfaced and italicized.

这样设置，任何警告文字都被设置成斜体，但只有`class`属性值为`warning`的`span`元素中，文本既是粗体又是斜体。

Notice the format of the general class selector in the previous example: it’s a class name preceded by a period without any element name, and no universal selector. In cases where you only want to select all elements that share a class name, you can omit the universal selector from a class selector without any ill effects.

请注意上例中的一般类选择器，它只包含一个类名和前面的句点，而没有任何元素名称，也没有通配选择器。如果你想选择具有某个类名的所有元素，省略通配选择器不会有任何影响。

### 多个类 Multiple Classes

In the previous section, we dealt with class values that contained a single word. In HTML, it’s possible to have a space-separated list of words in a single class value. For example, if you want to mark a particular element as being both urgent and a warning, you could write:

我们在前面看到了包含单个单词的`class`的属性值。在 HTML 中，使用空白分隔的单词列表可以作为单个`class`的值。例如，如果你想把某个特定元素标记为既是紧急的又是一个警告，可以这样写：

```html
<p class="urgent warning">When handling plutonium, care must be taken to avoid the formation of a critical mass.</p>
<p>
  With plutonium,
  <span class="warning">the possibility of implosion is very real, and must be avoided at all costs</span>. This can be
  accomplished by keeping the various masses separate.
</p>
```

The order of the words doesn’t matter; warning urgent would also suffice and would yield precisely the same results no matter how the CSS class attribute is written.

（`class`值中）单词的顺序没有影响，写成`warning urgent`会产生完全相同的结果。

Now let’s say you want all elements with a class of warning to be boldfaced, those with a class of urgent to be italic, and those elements with both values to have a silver background. This would be written as follows:

假如你想让所有`class`值为`warning`的元素加粗，把`class`值为`urgent`的设为斜体，而同时包含两个值的元素设置银色背景，写法是这样：

```css
.warning {
  font-weight: bold;
}
.urgent {
  font-style: italic;
}
.warning.urgent {
  background: silver;
}
```

By chaining two class selectors together, you can select only those elements that have both class names, in any order. As you can see, the HTML source contains class="urgent warning" but the CSS selector is written .warning.urgent. Regardless, the rule will still cause the “When handling plutonium . . . ” paragraph to have a silver background, as illustrated in Figure 2-8. This happens because the order the words are written in doesn’t matter. (This is not to say the order of classes is always irrelevant, but we’ll get to that later in the book.)

连接两个类选择器，可以选择那些只有同时具有两个类名的元素，无论类名的顺序如何。正如示例，HTML 代码中含有`class="urgent warning"`,但 CSS 选择器却写作`.warning.urgent`。这条规则依然可以把“When handling plutonium . . .”这段设置为银色背景，如图 1-8 所示，这是因为单词书写的顺序并不重要。（但这并不表示类名的顺序总是无关紧要的，我们将会在本书稍后涉及。）

<div style="margin: 0 auto; width: 50%;">
    <img src='./figure2-8.png' style=""/>
</div>
<p align="center">图 2-8：使用多类名选择元素</p>

If a multiple class selector contains a name that is not in the space-separated list, then the match will fail. Consider the following rule:

如果多类选择器里面包含一个不存在于空格分隔列表的类名，匹配将会失败。例如这个规则：

```css
p.warning.help {
  background: red;
}
```

As you would expect, the selector will match only those `p` elements with a `class` containing the words `warning` and `help`. Therefore, it will not match a `p` element with just the words `warning` and `urgent` in its `class` attribute. It would, however, match the following:

你可能期望这个选择器会匹配所有`class`中含有单词`warning`或`help`的`p`元素，然而实际上它不会匹配`class`属性中只有`warning`和`urgent`的`p`元素。它会匹配这样的元素：

```html
<p class="urgent warning help">Help me!</p>
```

### 2.3.3 ID 选择器 ID Selectors

In some ways, ID selectors are similar to class selectors, but there are a few crucial differences. First, ID selectors are preceded by an octothorpe (#)—also known as a pound sign (in the US), hash sign, hash mark, or tic-tac-toe board—instead of a period. Thus, you might see a rule like this one:

从某些方面说，ID 选择器和类选择器类似，但它们有一些重要区别。首先，ID 选择器使用井号（`#`）开头，一条规则可能是这样的：

```css
*#first-para {
  font-weight: bold;
}
```

This rule produces boldfaced text in any element whose `id` attribute has a value of first-para.

这条规则为任意`id`属性值为`first-para`的元素设置文本粗体。

The second difference is that instead of referencing values of the class attribute, ID selectors refer, unsurprisingly, to values found in id attributes. Here’s an example of an ID selector in action:

第二个区别是 ID 选择器（理所当然地）查找`id`属性而不是`class`属性的值。这是一个 ID 选择器生效的例子：

```css
*#lead-para {
  font-weight: bold;
}
```

```html
<p id="lead-para">This paragraph will be boldfaced.</p>
<p>This paragraph will NOT be bold.</p>
```

Note that the value lead-para could have been assigned to any element within the document. In this particular case, it is applied to the first paragraph, but we could have applied it just as easily to the second or third paragraph. Or an unordered list. Or anything.

注意值`lead-para`可以关联给文档中的任意元素。在这个例子中，它只赋给了第一个段落，但是你可以同样赋给第二个、第三个段落。

As with class selectors, it is possible to omit the universal selector from an ID selector. In the previous example, we could also have written:

和类选择器一样，ID 选择器中的通配选择符可以忽略。上例也可以写成这样：

```css
#lead-para {
  font-weight: bold;
}
```

The effect of this selector would be the same.

效果是一样的。

Another similarity between classes and IDs is that IDs can be selected independently of an element. There may be circumstances in which you know that a certain ID value will appear in a document, but you don’t know the element on which it will appear (as in the plutonium-handling warnings), so you’ll want to declare standalone ID selectors. For example, you may know that in any given document, there will be an element with an ID value of `mostImportant`. You don’t know whether that most important thing will be a paragraph, a short phrase, a list item, or a section heading. You know only that it will exist in each document, occur in an arbitrary element, and appear no more than once. In that case, you would write a rule like this:

另一个与类选择器相似的地方是，ID 选择器也可以独立于元素类型。可能有些场景下你知道有一个确定 ID 值会出现在文档中，但不知道会出现在哪个元素上（如在前面的钚处理警告中），因此需要声明独立的 ID 选择器。例如，在任意给定的文档中，有一个元素的 ID 值是`mostImportant`，但不知道这个元素是一个段落、引用、列表还是段落头，只知道这个值会出现在每个文档中的某个随机的元素上，而且在每个文档中仅出现一次。在这种情况下，规则可以这样写：

```css
#mostImportant {
  color: red;
  background: yellow;
}
```

This rule would match any of the following elements (which, as noted before, should not appear together in the same document because they all have the same ID value):

这条规则会匹配下面的每一个元素（正如上面强调的，因为它们有相同的 ID 值，所以任意两个*不应该*同时出现在一个文档中）：

```html
<h1 id="mostImportant">This is important!</h1>
<em id="mostImportant">This is important!</em>
<ul id="mostImportant">
  This is important!
</ul>
```

### 2.3.4 决定使用 Class 还是 ID Deciding Between Class and ID

You may assign classes to any number of elements, as demonstrated earlier; the class name warning was applied to both a p and a span element, and it could have been applied to many more elements. IDs, on the other hand, should be used once, and only once, within an HTML document. Therefore, if you have an element with an id value of lead-para, no other element in that document should have an id value of lead-para.

类可以分配给任意多的元素，类名`warning`可以分配给一个`p`元素或者一个`span`元素，或者更多其他元素。另一方面，ID 在一个 HTML 文档中使用且仅使用一次。因此如果有了一个`id`值为`lead-para`的元素，该文档中的其他元素都不能有`lead-para`的`id`值。

In the real world, browsers don’t always check for the uniqueness of IDs in HTML. That means that if you sprinkle an HTML document with several elements, all of which have the same value for their ID attributes, you’ll probably get the same styles applied to each. This is incorrect behavior, but it happens anyway. Having more than one of the same ID value in a document also makes
DOM scripting more difficult, since functions like `getElementById()` depend on there being one, and only one, element with a given ID value.

_**在实际中，浏览器并不总会检查 HTML 中 ID 的唯一性。如果你为多个元素设置了相同的 ID 属性值，它们可能都会被设置为相同的样式。这是不正确的实现，但这种情况很普遍。在一个文档中存在多个 ID 值相同的元素还会导致 DOM 脚本的问题，因为像`getElementById()`这样的函数依赖于文档中只存在一个 ID 为特定值的元素。**_

Unlike class selectors, ID selectors can’t be combined with other IDs, since ID attributes do not permit a space-separated list of words.

与类选择器不同，ID 选择器不能联合使用，因为 ID 属性不允许使用空白分隔的单词列表。

Another difference between class and id names is that IDs carry more weight when you’re trying to determine which styles should be applied to a given element. This will be explained in greater detail in the next chapter.

`class`和`id`名称的另一个区别是，当决定某个元素应该应用哪个样式时，ID 有更高的权重。这点将在后面详细讨论。

Also note that class and ID selectors may be case-sensitive, depending on the document language. HTML defines class and ID values to be case-sensitive, so the capitalization of your class and ID values must match that found in your documents. Thus, in the following pairing of CSS and HTML, the element’s text will not be boldfaced:

还要注意类和 ID 可能是大小写敏感的，这取决于文档的语言。HTML 语言把类和 ID 定义为大小写敏感的，因此类和 ID 选择器的大小写要和文档中的匹配。在下面的 CSS 和 HTML 中，元素文字不会被设置为粗体：

```css
p.criticalInfo {
  font-weight: bold;
}
```

```html
<p class="criticalinfo">Don't look down.</p>
```

Because of the change in case for the letter i, the selector will not match the element shown.

因为字母`i`的大小写不一致，选择器不会匹配元素。

On a purely syntactical level, the dot-class notation (e.g., `.warning`) is not guaranteed to work for XML documents. As of this writing, the dot-class notation works in HTML, SVG, and MathML, and it may well be permitted in future languages, but it’s up to each language’s specification to decide that. The hash-ID notation (e.g., `#lead`) will work in any document language that has an attribute that enforces uniqueness within a document. Uniqueness can be enforced with an attribute called id, or indeed anything else, as long as the attribute’s contents are defined to be unique within the document.

从纯语法层次来说，点-类标记（例如：`.warning`）不能保证在 XML 文档中生效。在撰写本文时，点-类标记在 HTML、SVG 和 MathML 中有效，它可能在未来被更多语言支持，但这要取决于语言本身的规范。哈希-ID 标记（例如：#lead）在所有强制属性唯一性的语言中都有效。唯一性可以强制使用名为`id`的属性，或者任何其他属性，只要在文档中属性内容被定义为唯一的即可。

## 2.4 属性选择器 Attribute Selectors

When it comes to both class and ID selectors, what you’re really doing is selecting values of attributes. The syntax used in the previous two sections is particular to HTML, XHTML, SVG, and MathML documents (as of this writing). In other markup languages, these class and ID selectors may not be available (as, indeed, those attributes may not be present). To address this situation, CSS2 introduced `attribute selectors`, which can be used to select elements based on their attributes and the values of those attributes. There are four general types of attribute selectors: simple attribute selectors, exact attribute value selectors, partial-match attribute value selectors, and leading-value attribute selectors.

当你使用类和 ID 选择器时，实际上是在选择属性的值。类选择器和 ID 选择器专用于 HTML、XHTML、SVG 和 MathML 文档（到撰写本文时），但在其它的标记语言中，这两个选择器可能是不可用的（属性可能不存在）。因此，CSS2 引入了**属性选择器**，使用元素的任意属性和值来选择元素。属性选择器有四种基本类型：简单属性选择器、准确属性值选择器、部分匹配属性选择器和头值属性选择器。

### 2.4.1 简单属性选择器 Simple Attribute Selectors

If you want to select elements that have a certain attribute, regardless of that attribute’s value, you can use a simple attribute selector. For example, to select all h1 elements that have a class attribute with any value and make their text silver, write:

如果想选择具有某个特定属性的元素，而无论属性的值是什么，可以使用**简单属性选择器**。例如，选择所有具备`class`属性的`h1`元素，然后将其文本设置为银色：

```css
h1[class] {
  color: silver;
}
```

So, given the following markup:

对如下代码：

```html
<h1 class="hoopla">Hello</h1>
<h1>Serenity</h1>
<h1 class="fancy">Fooling</h1>
```

you get the result shown in Figure 2-9.

将得到如图 2-9 的结果：

<div style="margin: 0 auto; width: 50%;">
    <img src='./figure2-9.png' style=""/>
</div>
<p align="center">图 2-9：使用属性选择元素</p>

This strategy is very useful in XML documents, as XML languages tend to have element and attribute names that are specific to their purpose. Consider an XML language that is used to describe planets of the solar system (we’ll call it PlanetML). If you want to select all `pml-planet` elements with a `moons` attribute and make them boldface, thus calling attention to any planet that has moons, you would write:

这种策略对 XML 文档非常有用，因为 XML 语言的元素经常含有表示特定意义的属性名。例如可以想象一种描述太阳系行星的 XML 语言（可以叫它 PlanetML）。如果想要选择所有包含`moons`属性的`pml-planet`元素，把文本设置成粗体，用来突出有月亮的行星，可以这样写：

```css
pml-planet[moons] {
  font-weight: bold;
}
```

This would cause the text of the second and third elements in the following markup fragment to be boldfaced, but not the first:

第二个和第三个元素将会被设置成粗体，第一个则不会：

```html
<pml-planet>Venus</pml-planet>
<pml-planet moons="1">Earth</pml-planet>
<pml-planet moons="2">Mars</pml-planet>
```

In HTML documents, you can use this feature in a number of creative ways. For example, you could style all images that have an alt attribute, thus highlighting those images that are correctly formed:

在 HTML 中可以用一些创新的方式使用这个特性。例如可以为所有包含`alt`属性的图片设置样式，因此突出形式规范的图片：

```css
img[alt] {
  border: 3px solid red;
}
```

(This particular example is generally useful more for diagnostic purposes—that is, determining whether images are indeed correctly marked up—than for design purposes.)

（这个特殊例子更适用于检查而不是设计目的，用来查看图片是否被设置了完全规范的标记。）

If you wanted to boldface any element that includes `title` information, which most browsers display as a “tool tip” when a cursor hovers over the element, you could write:

大部分浏览器在鼠标放到元素上的时候，会显示元素的`title`属性值，称为“tool tip”。如果想把所有包含`title`信息的元素粗体显示，可以这样：

```css
*[title] {
  font-weight: bold;
}
```

Similarly, you could style only those anchors (a elements) that have an href attribute, thus applying the styles to any hyperlink but not to any placeholder anchors.

相似地，可以选择那些包含`href`属性的锚点（`a`）元素，以此为超链接而不是所有锚点元素添加样式。

It is also possible to select based on the presence of more than one attribute. You do this by chaining the attribute selectors together. For example, to boldface the text of any HTML hyperlink that has both an href and a title attribute, you would write:

也可以基于多个属性选择元素，只需简单地并列多个属性选择器即可。例如，把包含`href`和`title`属性的 HTML 超链接设置为粗体：

```css
a[href][title] {
  font-weight: bold;
}
```

This would boldface the first link in the following markup, but not the second or third:

第一个链接会设置为粗体，第二个和第三个不会：

```html
<a href="http://www.w3.org/" title="W3C Home">W3C</a><br />
<a href="http://www.webstandards.org">Standards Info</a><br />
<a name="dead" title="Not a link">dead.letter</a>
```

### 2.4.2 基于准确属性值选择 Selection Based on Exact Attribute Value

You can further narrow the selection process to encompass only those elements whose attributes are a certain value. For example, let’s say you want to boldface any hyperlink that points to a certain document on the web server. This would look something like:

可以进一步缩小选择器范围选择那些某个属性为某个确定值的元素。例如，把指向服务器上某个特定文档的链接设置为粗体：

```css
a[href="http://www.css-discuss.org/about.html"] {
  font-weight: bold;
}
```

This will boldface the text of any a element that has an href attribute with exactly the value http://www.css-discuss.org/about.html. Any change at all, even dropping the www. part or changing to a secure protocol with https, will prevent a match.

所有`href`属性值**准确地**是`http://www.css-discuss.org/about.html`的`a`元素会被设置为粗体。任何修改，即使去掉了`www.`，也会造成无法匹配。

Any attribute and value combination can be specified for any element. However, if that exact combination does not appear in the document, then the selector won’t match anything. Again, XML languages can benefit from this approach to styling. Let’s return to our PlanetML example. Suppose you want to select only those planet elements that have a value of `1` for the attribute `moons`:

任何属性和值的联合都可以定义在任何元素上，然而，如果这个联合没有（准确地）出现在文档中，选择器不会匹配任何东西。XML 语言再次得益于这种方式来设置属性。回到 PlantML 的例子，如果想选择那些`moons`属性值为`1`的`planet`元素：

```css
planet[moons='1'] {
  font-weight: bold;
}
```

This would boldface the text of the second element in the following markup fragment, but not the first or third:

第二个元素的文本将会被设置为粗体，第一个和第三个不会：

```html
<planet>Venus</planet>
<planet moons="1">Earth</planet>
<planet moons="2">Mars</planet>
```

As with attribute selection, you can chain together multiple attribute-value selectors to select a single document. For example, to double the size of the text of any HTML hyperlink that has both an href with a value of http://www.w3.org/ and a title attribute with a value of W3C Home, you would write:

与属性选择一样，使用多个元素-值选择器也可以选择单个文档。例如，将`href`属性值为`http://www.w3.org/`且`title`属性值为`W3C Home`的 HTML 超链接文本设置为两倍尺寸：

```css
a[href="http://www.w3.org/"][title="W3C Home"] {
  font-size: 200%;
}
```

This would double the text size of the first link in the following markup, but not the second or third:

第一个元素会被设置为双倍尺寸字体，第二个和第三个不会：

```html
<a href="http://www.w3.org/" title="W3C Home">W3C</a><br />
<a href="http://www.webstandards.org" title="Web Standards Organization">Standards Info</a><br />
<a href="http://www.example.org/" title="W3C Home">dead.link</a>
```

结果如图 2-10。

<div style="margin: 0 auto; width: 50%;">
    <img src='./figure2-10.png' style=""/>
</div>
<p align="center">图 2-10：使用属性和值选择元素</p>

Again, this format requires an exact match for the attribute’s value. Matching becomes an issue when the selector form encounters values that can in turn contain a space-separated list of values (e.g., the HTML attribute class). For example, consider the following markup fragment:

这种方式需要属性值的**精确**匹配。属性值为多个空白分隔的值列表时，匹配可能会因多个值的顺序不同而产生问题（如 HTML 的属性 `class`）。例如下面的代码片段：

```html
<planet type="barren rocky">Mercury</planet>
```

The only way to match this element based on its exact attribute value is to write:

匹配这个元素的唯一方式是使用准确的属性值：

```css
planet[type='barren rocky'] {
  font-weight: bold;
}
```

If you were to write planet[type="barren"], the rule would not match the example markup and thus would fail. This is true even for the class attribute in HTML. Consider the following:

如果使用`planet[type="barren"]`，规则不会匹配是这个示例。即使是 HTML 中的`class`属性，也会出现这种情况。例如：

```html
<p class="urgent warning">When handling plutonium, care must be taken to avoid the formation of a critical mass.</p>
```

To select this element based on its exact attribute value, you would have to write:

要基于准确属性值选择元素，应该这样：

```css
p[class='urgent warning'] {
  font-weight: bold;
}
```

This is not equivalent to the dot-class notation covered earlier, as we will see in the next section. Instead, it selects any p element whose class attribute has exactly the value "urgent warning", with the words in that order and a single space between them. It’s effectively an exact string match.

我们将在下节看到，这和之前介绍的点-类选择是**不**等同的。这条规则将会选择`class`属性值**精确**地是`urgent warning`的所有`p`元素，单词以相同的顺序，并且中间以单个空格隔开。它实际上是一个精确字符串匹配。

Also, be aware that ID selectors and attribute selectors that target the id attribute are not precisely the same. In other words, there is a subtle but crucial difference between h1#page-title and `h1[id="page-title"]`. This difference is explained in “Specificity” on page 97.

同样地，ID 选择器和使用`id`属性的属性选择器也不是恰好相同的。换句话说，在`h1#page-title`和`h1[id="page-title"]`之间，存在着细微但很重要的区别。这种区别将在章节“特度”解释。

### 2.4.3 基于部分属性值选择 Selection Based on Partial Attribute Values

Odds are that you’ll want to select elements based on portions of their attribute values, rather than the full value. For such situations, CSS actually offers a variety of options for matching substrings in an attribute’s value. These are summarized in Table 2-1.

你可能想基于属性值的一部分而不是整个值来选择元素，这种情况下 CSS 提供了一些选择，匹配属性值中的子串。它们总结在表格 1-1 中。

_表格 1-1：子串匹配属性选择器_

| 类型                | 描述                                                                                             |
| :------------------ | :----------------------------------------------------------------------------------------------- |
| `[foo~="bar"]`      | 选择所有带有`foo`属性、且`foo`属性被空白分隔的单词列表中含有单词`bar`的元素。                    |
| `[foo*="bar"]`      | 选择所有带有`foo`属性、且`foo`属性值中含有子串`bar`的元素。                                      |
| `[foo^="bar"]`      | 选择所有带有`foo`属性、且`foo`属性值以`bar`开头的元素。                                          |
| `[foo$="bar"]`      | 选择所有带有`foo`属性、且`foo`属性值以`bar`结束的元素。                                          |
| `[foo&#124;="bar"]` | 选择所有带有`foo`属性、且`foo`属性值以`bar`开头后接一个短线（`U+002D`）或者属性值是`bar`的元素。 |

### 2.4.4 A Particular Attribute Selection Type 特定的属性选择器

The first of these attribute selectors that match on a partial subset of an element’s attribute value is actually easier to show than it is to describe. Consider the following rule:

基于部分属性值的选择器中的最后一个，展示它的用法比描述它更简单。看下面的规则：

```css
*[lang|='en'] {
  color: white;
}
```

This rule will select any element whose lang attribute is equal to en or begins with en-. Therefore, the first three elements in the following example markup would be selected, but the last two would not:

这条规则会选择任何`lang`属性等于`en`或者以`en-`开头的元素。因此，下面的示例中前三个标签会被选中，而后两个则不会：

```html
<h1 lang="en">Hello!</h1>
<p lang="en-us">Greetings!</p>
<div lang="en-au">G'day!</div>
<p lang="fr">Bonjour!</p>
<h4 lang="cy-en">Jrooana!</h4>
```

In general, the form [att|="val"] can be used for any attribute and its values. Let’s say you have a series of figures in an HTML document, each of which has a filename like figure-1.gif and figure-3.jpg. You can match all of these images using the following selector:

一般来说，`[att|="val"]`的格式可以用于任何属性和属性值。如果 HTML 文档中有一系列图片，文件名都像**“figure-1.gif”**和**“figure-3.jpg”**这样，可以使用这样的选择器匹配所有这样的图片：

```css
img[src|='figure'] {
  border: 1px solid gray;
}
```

Or, if you’re creating a CSS framework or pattern library, instead of creating redundant classes like "btn btn-small btn-arrow btn-active", you can declare "btnsmall-arrow-active", and target the class of elements with:

如果你正在创建一个 CSS 框架或模式库，不必创建许多繁琐的类：`"btn btn-small btn-arrow btn-active"`，你可以声明`"btn-small-arrow-active"`，然后这样匹配元素的类：

```css
*[class|='btn'] {
  border-radius: 5px;
}
```

```html
<button class="btn-small-arrow-active">Click Me</button>
```

The most common use for this type of attribute selector is to match language values, as demonstrated in an upcoming section, “The :lang Pseudo-Class” on page 88.

这个属性选择器最常用的场景是用来匹配语言值，我们将在"`:lang`伪类"章节看到。

#### 匹配空白分隔的列表中的一个单词

For any attribute that accepts a space-separated list of words, it is possible to select elements based on the presence of any one of those words. The classic example in HTML is the class attribute, which can accept one or more words as its value. Consider our usual example text:

任何使用空白分隔单词列表的属性，都可以基于这些单词中的任意一个选择元素。HTML 中最经典的例子是`class`属性，该属性可以使用一或多个单词作为值。看这个常用例子：

```html
<p class="urgent warning">When handling plutonium, care must be taken to avoid the formation of a critical mass.</p>
```

Let’s say you want to select elements whose class attribute contains the word warn ing. You can do this with an attribute selector:

如果要选择`class`属性中包含单词`warning`的元素，可以使用这样的属性选择器：

```css
p[class~='warning'] {
  font-weight: bold;
}
```

Note the presence of the tilde (~) in the selector. It is the key to selection based on the presence of a space-separated word within the attribute’s value. If you omit the tilde, you would have an exact value-matching attribute selector, as discussed in the previous section.

注意选择器中的波浪线（~），这是基于属性值中分离单词进行选择的关键字。如果忽略了波浪线，选择器就变成了前面讨论过的精确值匹配的属性选择器。

This selector construct is equivalent to the dot-class notation discussed in “Deciding Between Class and ID” on page 44. Thus, p.warning and p[class~="warning"] are equivalent when applied to HTML documents. Here’s an example that is an HTML version of the “PlanetML” markup seen earlier:

这个选择器跟“决定使用 Class 还是 ID”中的点-类选择器是等同的。也就是说，用于 HTML 文档时，`p.warning`和`p[class~="warning"]`是相等同的。这是前面提到过的“PlanetML”标记例子的一个 HTML 版本：

```html
<span class="barren rocky">Mercury</span>
<span class="cloudy barren">Venus</span>
<span class="life-bearing cloudy">Earth</span>
```

To italicize all elements with the word barren in their class attribute, you write:

要把所有`class`属性值中包含单词`barren`的元素设置为斜体：

```css
span[class~='barren'] {
  font-style: italic;
}
```

This rule’s selector will match the first two elements in the example markup and thus italicize their text, as shown in Figure 2-11. This is the same result we would expect from writing span.barren {font-style: italic;}.

这个选择器将会匹配例子中的前两个元素并把它们设置为斜体。这和使用`span.barren {font-style: italic;}`是一样的效果。

<div style="margin: 0 auto; width: 50%;">
    <img src='./figure2-11.png' style=""/>
</div>
<p align="center">图 2-11：使用部分属性值选择元素</p>

So why bother with the tilde-equals attribute selector in HTML? Because it can be used for any attribute, not just `class`. For example, you might have a document that contains a number of images, only some of which are figures. You can use a partialmatch value attribute selector aimed at the `title` text to select only those figures:

既然效果相同，为什么还要在 HTML 中使用波浪线-等号属性选择器呢？因为它可被用于任何属性，而不仅仅是`class`。例如：一个文档中包含许多图片，其中一部分是图表，你可以使用匹配部分属性值的选择器选择`title`属性的文字，来选中那些是图表的图片：

```css
img[title~='Figure'] {
  border: 1px solid gray;
}
```

This rule selects any image whose title text contains the word Figure. Therefore, as long as all your figures have title text that looks something like “Figure 4. A baldheaded elder statesman,” this rule will match those images. For that matter, the selector img[title~="Figure"] will also match a title attribute with the value “How to Figure Out Who’s in Charge.” Any image that does not have a title attribute, or whose title value doesn’t contain the word “Figure,” won’t be matched.

这条规则会选择所有`title`文字中包含`Figure`的单词。因此，如果所有的图表的`title`中都有像“Figure 4. A bald- headed elder statesman,”这样的文字，这条规则会匹配所有的图表。同样的，选择器`img[title~="Figure"]`也会匹配`title`属性值是“How to Figure Out Who’s in Charge.”这样内容的图片。所有没有`title`属性的图片，或者`title`值中不包含单词“Figure”的图片，都不会被匹配。

#### 匹配属性值中的子串 Matching a substring within an attribute value

Sometimes you want to select elements based on a portion of their attribute values, but the values in question aren’t space-separated lists of words. In these cases, you can use the form `[att*="val"]` to match substrings that appear anywhere inside the attribute values. For example, the following CSS matches any `span` element whose class attribute contains the substring `cloud`, so both “cloudy” planets are matched, as shown in Figure 2-12:

有时需要匹配属性值的一部分，但并不是空格分隔的单词。这种情况下，可以使用`[att*="val"]`的形式匹配属性值中的任何位置。例如：下面的 CSS 匹配任何`class`属性值中包含子串`cloud`的`span`元素，所以两个“cloudy”的行星都会被匹配，如图 1-12。

```css
span[class*='cloud'] {
  font-style: italic;
}
```

```html
<span class="barren rocky">Mercury</span>
<span class="cloudy barren">Venus</span>
<span class="life-bearing cloudy">Earth</span>
```

<div style="margin: 0 auto; width: 50%;">
    <img src='./figure2-12.png' style=""/>
</div>
<p align="center">图 2-12：基于属性值内子串选择元素</p>

As you can imagine, there are many useful applications for this particular capability. For example, suppose you wanted to specially style any links to the O’Reilly website. Instead of classing them all and writing styles based on that class, you could instead write the following rule:

这种用法有许多有用的场景，例如为所有到 O'Reilly Media 网页的链接添加特殊样式。避免给它们设置类名并基于类添加样式，可以简单地使用下面的规则：

```css
a[href*='oreilly.com'] {
  font-weight: bold;
}
```

You aren’t confined to the class and href attributes. Any attribute is up for grabs here: `title`, `alt`, `src`, `id`…if the attribute has a value, you can style based on a substring within that value. The following rule draws attention to any image with the string `“space”` in its source URL:

选择不限于使用`class`和`href`属性，任何属性都可以。`title`、`alt`、`src`、`id`……可以基于任何属性值的子串添加样式。下面的规则选择所有源文件 URL 中包含字符串“space”的图片：

```css
img[src*='space'] {
  border: 5px solid red;
}
```

Similarly, the following rule draws attention to input elements that have a title tells the user what to, and any other input whose title contains the substring “format” in its title:

类似地，下面的规则关注有标题的`input`元素，标题中包含子串`format`：

```css
input[title*='format'] {
  background-color: #dedede;
}
```

```html
<input type="tel" title="Telephone number should be formatted as XXX-XXX-XXXX" pattern="\d{3}\-\d{3}\-\d{4}" />
```

A common use for the general substring attribute selector is to match a section of a class in pattern library class names. Elaborating on the last example, we can target any class name that starts with `"btn"` followed by a dash, and that contains the substring `“arrow”` preceded by a dash:

属性子串匹配选择器常用来匹配模式库中的类名。在前面的例子中，我们可以匹配以`btn`开始后跟一个短线，并且包含前面有短线的子串`arrow`的类名：

```css
*[class|='btn'][class*='-arrow']:after {
  content: '▼';
}
```

```html
<button class="btn-small-arrow-active">Click Me</button>
```

The matches are exact: if you include whitespace in your selector, then whitespace must also be present in an attribute’s value. The attribute names and values must be case-sensitive only if the underlying document language requires case sensitivity. Class names, titles, URLs, and ID values are all case-sensitive, but HTML attribute keyterm values, such as input types, are not:

这种匹配方式是精确匹配——如果选择器中包含空白，属性值中必须包含空白才能匹配。只有当依赖的文档语言要求区分大小写时，属性名和值才必须区分大小写。类名、标题和 ID 值都是大小写敏感的，但 HTML 的属性关键字值，比如`input`元素的类型，不区分大小写：

```css
input[type='CHeckBoX'] {
  margin-right: 10px;
}
```

```html
<input type="checkbox" name="rightmargin" value="10px" />
```

#### 匹配属性值开头的子串 Matching a substring at the beginning of an attribute value

In cases where you want to select elements based on a substring at the beginning of an attribute value, then the attribute selector pattern `[att^="val"]` is what you’re seeking. This can be particularly useful in a situation where you want to style types of links differently, as illustrated in Figure 2-13.

当需要基于属性值开头的子串选择元素时，可以使用属性选择器模式`[attr^="val"]`。这个匹配模式在给不同类别的链接设置样式时特别有用，如图 2-13 所示：

```css
a[href^='https:'] {
  font-weight: bold;
}
a[href^='mailto:'] {
  font-style: italic;
}
```

<div style="margin: 0 auto; width: 50%;">
    <img src='./figure2-13.png' style=""/>
</div>
<p align="center">图 2-13：基于属性开头的子串选择元素</p>

Another use case is when you want to style all images in an article that are also figures, as in the figures you see throughout this text. Assuming that the alt text of each figure begins with text in the pattern “Figure 5”—which is an entirely reasonable assumption in this case—then you can select only those images as follows:


另一个使用场景是为文档中所有内容是说明的图片添加样式——假定所有的说明图的`alt`属性的文字都以“Figure 5”这样的模式开头——则可以使用这种方式选择这些图片：

```css
img[alt^='Figure'] {
  border: 2px solid gray;
  display: block;
  margin: 2em auto;
}
```

The potential drawback here is that any img element whose alt starts with “Figure”will be selected, whether or not it’s meant to be an illustrative figure. The likeliness of that occurring depends on the document in question.

潜藏的问题是，**任何**`alt`属性值以“Figure”开头的`img`标签都会被选择，而无论它是不是一个说明图。显然，是否产生这个问题是由文档决定的（而不是选择器）。

Another use case is selecting all of the calendar events that occur on Mondays. In this case, let’s assume all of the events have a `title` attribute containing a date in the format “Monday, March 5th, 2012.” Selecting them all is a simple matter of [title^="Monday"].

另一个使用场景是选择所有周一的日程。这种场景中，我们约定所有的事件都有个`title`属性，它以这样的日期格式`Monday,March 5th,2012`开头。选择它们只需要简单地使用`[title^="Monday"]`。

#### 匹配属性值结尾的字串 Matching a substring at the end of an attribute value

The mirror image of beginning-substring matching is ending-substring matching, which is accomplished using the `[att$="val"] `pattern. A very common use for this capability is to style links based on the kind of resource they target, such as separate styles for PDF documents, as illustrated in Figure 2-14.


与开头子串匹配相对应的是结尾子串匹配，使用选择器模式`[att$="val"]`。最常见的使用场景是基于链接的资源类型添加样式，例如图 2-14 所示，为指向 PDF 文档的链接添加特定样式。

```css
a[href$='.pdf'] {
  font-weight: bold;
}
```

<div style="margin: 0 auto; width: 50%;">
    <img src='./figure2-14.png' style=""/>
</div>
<p align="center">图 2-14：基于属性结尾的子串选择元素</p>

Similarly, you could (for whatever reason) select images based on their image format:


类似地，可以（无论因何）基于格式选择图片：

```css
img[src$='.gif'] {
  ...;
}
img[src$='.jpg'] {
  ...;
}
img[src$='.png'] {
  ...;
}
```

To continue the calendar example from the previous section, it would be possible to select all of the events occurring within a given year using a selector like `[title $="2015"]`.

上一节中日程的例子，可以基于给定的年份选择所有事件，使用一个类似这样的选择器`[title$="2015"]`（`title`属性以年份结尾）。

You may have noticed that I’ve quoted all the attribute values in the attribute selectors. Quoting is required if the value includes any special characters, begins with a dash or digit, or is otherwise invalid as an identifier and needs to be quoted as a string. To be safe, I recommend always quoting attribute values in attribute selectors, even though it is only required to makes strings out of invalid identifiers.

_**你可能注意到了，属性选择器中的所有属性值都用了引号包围。当属性值包含任何特殊字符、以短线或数字开头、或其他非法标识符时，需要使用引号把它标记成字符串。为了安全，建议在任何情况下都为属性选择器中的属性值添加引号，尽管只有非法标识符导致它需要被标记成字符串的时候引号才是必需的。**_

### 2.4.5 忽略大小写标识符 The Case Insensitivity Identifier

CSS Selectors level 4 introduces a case-insensitivity option to attribute selectors. Including an i before the closing bracket will allow the selector to match attribute values case-insensitively, regardless of document language rules.

CSS Selectors level 4 为属性选择器引入了忽略大小写选项。在中括号关闭之前使用`i`允许选择器匹配属性值的时候忽略大小写，无视文档语言的规则。

For example, suppose you want to select all links to PDF documents, but you don’t know if they’ll end in .pdf, .PDF, or even .Pdf. Here’s how:

例如，你想选择所有指向 PDF 文档的链接，但并不确定它们以`.pdf`、`.PDF`还是`.Pdf`结束，可以这样：

```css
a[href$='.PDF' i]
```

Adding that humble little i means the selector will match any a element whose href attribute’s value ends in .pdf, regardless of the capitalization of the letters P, D, and F.

添加一个小小的`i`表示选择器匹配任何`href`属性以`.pdf`结束的`a`元素，无论其中是否包含大写的`P`、`D`或`F`。

This case-insensitivity option is available for all attribute selectors we’ve covered. Note, however, that this only applies to the values in the attribute selectors. It does not enforce case insensitivity on the attribute names themselves. Thus, in a case-sensitive language, `planet[type*="rock" i]` will match all of the following.

忽略大小写选项适用于前面涉及的所有属性选择器，但要注意它只用于属性选择器的**值**，而不能用于属性名本身。因此，在大小写敏感的语言中，`planet[type*="rock" i]`可以匹配下面所有的元素：

```html
<planet type="barren rocky">Mercury</planet>
<planet type="cloudy ROCKY">Venus</planet>
<planet type="life-bearing Rock">Earth</planet>
```

It will not match the following element, because the attribute TYPE isn’t matched by type:

但不能匹配下面的元素，因为属性`TYPE`不匹配`type`：

```html
<planet TYPE="dusty rock">Mars</planet>
```

Again, that’s in langauges that enforce case sensitivity in the element and attribute syntax. XHTML was one such. In languages that are case-insensitive, like HTML5, this isn’t an issue.

再次说明，是否在元素和属性语法中强制区分大小写是由语言决定的，XHTML 是这样的语言。在大小写不敏感的语言中没有这样的问题，例如 HTML5。

As of late 2017, Opera Mini, the Android browser, and Edge did not support this capability.

_**至 2017 年底，Opera Mini、Android 浏览器和 Edge 不支持此能力。**_

## 2.5 使用文档结构 Using Document Structure

CSS is powerful because it uses the structure of documents to determine appropriate styles and how to apply them. Yet structure plays a much larger role in the way styles are applied to a document. Let’s take a moment to discuss structure before moving on to more powerful forms of selection.

如前面所说，CSS 之强大在于它利用文档结构决定（元素的）样式和样式作用于元素的方式。结构确实在样式作用于文档时扮演了非常重要的角色，在继续讨论更强大的选择形式之前，我们先来讨论结构。

### 2.5.1 理解父-子关系 Understanding the Parent-Child Relationship

To understand the relationship between selectors and documents, we need to once again examine how documents are structured. Consider this very simple HTML document:

为了理解选择器和文档之间的关系，我们要再次回顾文档结构是如何组织的，看下面这个非常简单的 HTML 文档：

```html
<html>
  <head>
    <base href="http://www.meerkat.web/" />
    <title>Meerkat Central</title>
  </head>
  <body>
    <h1>Meerkat <em>Central</em></h1>
    <p>
      Welcome to Meerkat <em>Central</em>, the
      <strong
        >best meerkat web site on <a href="inet.html">the <em>entire</em> Internet</a></strong
      >!
    </p>
    <ul>
      <li>
        We offer:
        <ul>
          <li><strong>Detailed information</strong> on how to adopt a meerkat</li>
          <li>Tips for living with a meerkat</li>
          <li>
            <em>Fun</em> things to do with a meerkat, including:
            <ol>
              <li>Playing fetch</li>
              <li>Digging for food</li>
              <li>Hide and seek</li>
            </ol>
          </li>
        </ul>
      </li>
      <li>...and so much more!</li>
    </ul>
    <p>Questions? <a href="mailto:suricate@meerkat.web">Contact us!</a></p>
  </body>
</html>
```

CSS 的能力很大程度基于于元素的**父-子关系**。HTML 文档（事实上绝大部分结构化文档）基于元素层级结构，构成文档的“树状”视图（见图 1-15）。在这种层级结构中，每个元素都处在整个文档结构中的某个适当位置上，每个元素都是其他元素的**父**或者**子**，常常既是父又是子。

![图1-15：文档树结构](figure1-15.png)

_图 1-15：文档树结构_

在文档层级结构中，如果一个元素在另一个元素的紧邻的上方，就被称作那个元素的父元素。例如，在图 1-15 中，第一个`p`元素是`em`和`strong`元素的父元素，同时`strong`是一个锚点（`a`）元素的父元素，这个`a`元素又是另一个`em`元素的父元素。反过来，如果在文档层级中，一个元素在另一个元素的紧邻的下方，就被称作那个元素的子元素。因此，图 1-15 中的锚点元素是`strong`元素的子元素，`strong`元素又是`p`元素的子元素，等等。

“父”和“子”是**祖先**和**后代**的特例。它们的区别是：在树状视图中，如果一个元素在另一个元素上面一级，那么它们是父-子关系。如果一个元素到另一个元素的路径有两级或者更多，那么它们是祖先-后代关系，但不是父-子关系。（当然，子也是后代，同时父也是祖先。）在图 1-15 中，第一个`ul`元素是两个`li`元素的父元素，同时也是它的`li`元素所有后代元素的祖先元素，直到嵌套路径最深的`li`元素。

同时，在图 1-15 中，存在一个锚点元素既是`strong`元素的子元素，又是`p`、`body`和`html`元素的后代元素。`body`元素是浏览器默认显示的所有元素的祖先元素，`html`是整个文档中所有其他元素的祖先元素。因此在 HTML 或 XHTML 文档中，`html`元素也被叫做**根元素**。

### 后代选择器 Descendant Selectors

理解文档模型的第一个用处是可以定义**后代选择器**（也叫做**上下文选择器**）。定义后代选择器可以创建只作用于特定结构的规则。例如，如果想要只为那些是`h1`元素的后代的`em`元素设置样式。你可以为`h1`中的`em`元素添加一个`class`属性，但这样做会跟使用`font`标签一样耗费时间。很明显，声明一个只匹配`h1`元素中的`em`元素的规则更加方便。

实现这个规则，可以这样写：

```css
h1 em {
  color: gray;
}
```

这条规则会把所有是`h1`元素后代的`em`元素中的文本设置为灰色。其他的`em`文本，例如在段落（`p`）或引用（`blackquote`）中的`em`元素，不会被这条规则选择。见图 1-16。

![图1-16：基于上下文选择元素](figure1-16.png)

_图 1-16：基于上下文选择元素_

在后代选择器中，选择器由两个或更多空白分隔的选择器组成。选择器之间的空格是一个**组合器**的例子。每个空格组合器都可以被译作“在……中”、“是……的一部分”或“是……的后代”，前提是选择器从右向左读。因此，`h1 em`可以被译作“把样式作用于任何`em`元素，如果它是`h1`元素的后代”。（如果选择器从左向右读，则是：“选择任何`h1`，如果它包含一个`em`元素，规则将会作用于它包含的`em`”）。

可以使用不止两个选择器，例如：

```css
ul ol ul em {
  color: gray;
}
```

在这种情况下，任何`em`文本，如果这个`em`在一个`ul`中，同时`ul`在一个`ol`中，而`ol`又在另一个`ul`中，这个`em`会被设置为灰色,如 1-17 所示。这是一条非常具体的选择规则。

![图1-17：一个非常具体的后代选择器](figure1-17.png)

_图 1-17：一个非常具体的后代选择器_

后代选择器非常有用，它使得 HTML 中（至少是不使用怪异的`font`标签时）办不到的事情变成可能。一个常见的场景是：如果文档中有一个侧边栏和一个主区域，侧边栏的背景是蓝色，而主区域的背景是白色，它们都包含链接。不能把链接设置为蓝色，因为如果这样的话，侧边栏中的链接就看不到了。

解决方法是：后代选择器。在这种情况下，给包含侧边栏的元素（一般是一个`div`）添加一个`class`值`sidebar`，把主区域的`class`命名为`main`，然后使用如下样式：

```css
.sidebar {
  background: blue;
}
.main {
  background: white;
}
.sidebar a:link {
  color: white;
}
.main a:link {
  color: blue;
}
```

图 1-18 显示了样式的结果。

![图1-18：使用后代选择器为同一类型的元素添加不同的样式](figure1-18.png)

_图 1-18：使用后代选择器为同一类型的元素添加不同的样式_

_**`:link`选择那些尚未被访问过的资源链接，我们将在“超链接伪类”中详细讨论。**_

另一个例子是：如果要把所有在`blockquote`和`p`中的`b`元素文本设置为灰色：

```css
blockquote b,
p b {
  color: gray;
}
```

这条样式的结果是在段落或引用段落中的`b`元素中的文本显示为灰色。

后代选择器的一个容易被忽略的地方是，元素和后代元素之间可以间隔无限代其他元素。例如，如果使用规则`ul em`，将会选择`ul`元素后代中的任何`em`元素，无论`em`元素嵌套多么深。因此，对下面的代码，`ul em`会匹配到其中的`em`元素。

```html
<ul>
  <li>
    List item 1
    <ol>
      <li>List item 1-1</li>
      <li>List item 1-2</li>
      <li>
        List item 1-3
        <ol>
          <li>List item 1-3-1</li>
          <li>List item <em>1-3-2</em></li>
          <li>List item 1-3-3</li>
        </ol>
      </li>
      <li>List item 1-4</li>
    </ol>
  </li>
</ul>
```

后代选择器的另一个更微妙的地方是，它没有接近程度的概念。换句话说，文档树中两个元素的紧密程度与是否应用规则无关。这将会在考虑特异性（特度，在后面讨论）和元素规则之间的相互抵消时产生影响。

例如，考虑下面的代码（包含我们将会在本章“否定伪类”中讨论的选择器）：

```html
div:not(.help) span {color: gray;} div.help span {color: red;}

<div class="help">
  <div class="aside">This text contains <span>a span element</span> within.</div>
</div>
```

第一条规则表示“任何`class`中不包含单词`help`的`div`元素中的`span`元素被设置为灰色”，第二条规则表示“任何`class`中包含单词`help`的`div`元素中的`span`元素被设置为红色”。对示例中的 HTML 代码来说，两条规则都会被作用于`span`元素。

因为两条规则有相同的权重，且“红色”规则被写在后面，`span`会被设置为红色。虽然`div class="aside"`比`div class="help"`相比，与`span`元素更“紧密”，但实际上这种紧密程度与规则的选择毫不相关。亦即：后代选择器没有紧密程度的概念。两条规则都匹配了元素，只有一种颜色可以生效，根据 CSS 的工作方式，红色“胜利”了。（下一章讨论）

### 选择子元素 Selecting Children

有时，我们并不想选择全部的后代元素，而是把选择范围控制在元素的子级，例如选择一个是`h1`元素的子元素（而不是任意后代元素）的`strong`元素，这种情况下，可以使用子元素组合器，它是一个大于号（`>`）:

```css
h1 > strong {
  color: red;
}
```

这条规则将会把下面的第一个`h1`元素中的`strong`元素设置为红色，第二个`h1`元素中的`strong`元素则不会被设置为红色。

```html
<h1>This is <strong>very</strong> important.</h1>
<h1>
  This is <em>really <strong>very</strong></em> important.
</h1>
```

从右往左读，选择器`h1 > strong`可以译作“选择任何`strong`元素，如果它是一个`h1`元素的子元素”。子元素组合器两边可以添加空格, 你可以根据自己的爱好添加或省略空格，`h1 > strong`、`h1> strong`和`h1>strong`是完全等价的。

观察文档的树状结构视图，子元素选择器把匹配限制在直接连接的元素上。图 1-19 显示了部分文档树。

![图1-19：一个文档树片段](figure1-19.png)

_图 1-19：一个文档树片段_

在这文档树片段中，可以很清楚的观察到父-子关系。例如，`a`元素是`strong`元素的父元素，同时是`p`元素的子元素。在这个片段中，可以使用`p > a`和`a > strong`选择元素，但无法使用`p > strong`选择元素，因为`strong`是`p`的后代元素但不是子元素。

在同一个选择器中可以结合使用后代选择器和子元素原则器。`table.summary td > p`选择是`td`元素子元素的`p`元素，同时这个`td`元素需要是一个`class`属性值包含`summary`的`table`元素的后代元素。

### 选择相邻兄弟元素 Selecting Adjacent Sibling Elements

假如想要为一个紧跟着标题的段落设置样式，或者给一个紧跟着段落的列表添加一个边距，可以使用**相邻兄弟组合器**来选择在同一个父级元素下紧跟着另一个元素的元素，组合器使用加号（`+`）。就像子级选择器一样，这个符号也可以在两边添加或省略空格。

移除一个紧跟`h1`元素的段落的上边距：

```css
h1 + p {
  margin-top: 0;
}
```

选择器读作：“选择任何紧跟在`h1`元素后面的`p`元素”。

看图 1-20 的文档树片段，更清晰地观察这个选择器是如何生效的：

![图1-20：一个文档树片段](figure1-20.png)

_图 1-20：一个文档树片段_

在这个片段中有两个列表都是`div`元素的后代，一个是有序列表，另一个是无序列表，每个都包含三个列表项。两个列表互为相邻兄弟，每个列表中的列表项也互为相邻兄弟，但第一个列表中的项与第二个列表中的列**不是**相邻兄弟，因为它们没有共同的父元素。（它们最多是表兄弟元素，但 CSS 没有表兄弟元素选择器。）

选择后面的两个相邻兄弟只需要一个组合器符号，如果写作`li + li {font-weight: bold;}`,只有每个列表中的第二项和第三项会被设置为粗体，样式不会对第一项生效。见图 1-21.

![图1-21：选择相邻兄弟元素](figure1-21.png)

_图 1-21：选择相邻兄弟元素_

CSS 的正确性依赖于两个元素的“代码顺序“。在上面的例子中，一个`ol`元素后面紧跟着一个`ul`元素，因此可以使用`ol + ul`选择第二个（`ul`）元素，但不能选择第一个（`ol`）元素。如果想使`ul + ol`匹配，需要一个`ol`元素紧跟在一个`ul`元素后面。

需要记住，两个元素之间的文本内容**不会**影响相邻元素组合器。下面的代码片段，树视图与图 1-19 是一样的：

```html
<div>
  <ol>
    <li>List item 1</li>
    <li>List item 1</li>
    <li>List item 1</li>
  </ol>
  This is some text that is part of the 'div'.
  <ul>
    <li>A list item</li>
    <li>Another list item</li>
    <li>Yet another list item</li>
  </ul>
</div>
```

尽管两个列表之间有文本内容，选择器`ol + ul`依然会匹配第二个列表。因为文本并不包含一个兄弟元素，而是属于父元素`div`的一部分。如果把文本内容用一个段落元素（`p`）包起来，`ol + ul`匹配第二个列表的行为将会被终止。要匹配第二个列表，需要用`ol + p + ul`这样的选择器。

相邻兄弟组合器可以与其他组合器连接使用，例如：

```css
html > body table + ul {
  margin-top: 1.5em;
}
```

这个选择器是指：“选择任何紧跟`table`元素的兄弟`ul`元素，同时这个`table`元素是一个`body`元素的后代，而`body`元素是一个`html`的子元素。”

和所有组合器一样，相邻兄弟选择器可以用于很复杂的选择器中，如`div#content h1 + div ol`。这个选择器是：“选择任何是`div`元素后代的`ol`元素，同时这个`div`元素是一个`h1`元素的紧邻兄弟元素，而这个`h1`元素是一个`id`属性值为`content`的`div`元素的子元素。”

### 选择跟随兄弟元素 Selecting Following Siblings

Selectors Level 3 引入了一个新的兄弟组合器叫做**一般兄弟选择器**。这个组合器允许选择同一个父元素下，跟随（不一定是紧跟随）在某个元素后面的所有元素，使用波浪线符号（`~`）。

如下例，为同一个父元素下跟随在一个`h2`元素后面的任何`ol`元素设置斜体，可以写作`h2 ~ ol {font-style: italic;}`。两个`ol`元素不必都是紧邻兄弟，尽管是紧邻兄弟的话也会被这条规则匹配。效果见图 1-22.

```html
<div>
  <h2>Subheadings</h2>
  <p>
    It is the case that not every heading can be a main heading. Some headings must be subheadings. Examples include:
  </p>
  <ol>
    <li>Headings that are less important</li>
    <li>Headings that are subsidiary to more important headlines</li>
    <li>Headings that like to be dominated</li>
  </ol>
  <p>Let's restate that for the record:</p>
  <ol>
    <li>Headings that are less important</li>
    <li>Headings that are subsidiary to more important headlines</li>
    <li>Headings that like to be dominated</li>
  </ol>
</div>
```

![图1-22：选择跟随兄弟元素](figure1-22.png)

_图 1-22：选择跟随兄弟元素_

如图所示，两个有序列表都是斜体，因为两个`ol`元素都在`h2`元素后面，且它们（三个）共有一个父元素（`div`）。

## 2.6 伪类选择器 Pseudo-Class Selectors

**伪类选择器**非常有趣，它们是一些根据元素状态变化而产生作用的幽灵类。伪类选择器可以根据某些确定元素的状态、文档中的标记模式甚至文档本身的状态选择元素并添加样式。

“幽灵类”的说法可能看起来有点怪，但这个词非常贴切地体现了伪类的工作方式。例如，假如你想要把一个数据表格每隔一行设置为高亮，你可以每隔一行在行元素上加一个`class="even"`，然后写一段 CSS 把`class`值有`even`的行设置为高亮。但是你也可以使用伪类选择器更简便地实现相同的效果，后面会很快看到它的用法。

### 组合伪类 Combining Pseudo-Classes

在开始之前，先提一下“链式”。CSS 允许（链式）组合伪类选择器，例如，当鼠标停留在（`hover`）一个未访问过的链接（`<a>`）上时，将其设置为红色，当鼠标停留在已经访问过的链接上时,将其设置为栗色：

```css
a:link:hover {
  color: red;
}
a:visited:hover {
  color: maroon;
}
```

（伪类的）顺序无关紧要，`a:hover:link`和`a:link:hover`的效果是一样的。同样的，可以为特定语言的不同状态的链接设置不同的样式，例如德语：

```css
a:link:hover:lang(de) {
  color: gray;
}
a:visited:hover:lang(de) {
  color: silver;
}
```

注意不要组合互斥的伪类，例如，一个链接不可能既是访问过的又是没访问过的，所以`a:link:visited`没有任何意义，它并不会匹配任何东西。

### 结构性伪类 Structural Pseudo-Classes

大部分伪类都是结构性的，既它们是与文档的标记结构相关的。大部分伪类由标签内的结构决定，例如某个伪类选择器选择（某个文档片段中的）第三个段落（`p`）。其他一些选择器允许你处理特定类型的元素。所有的伪类都以一个冒号（`:`）开头，没有例外，而且它们可以出现在选择器的任何位置。

在开始之前，关于伪类有一点需要明确：伪类永远只指向他们关联的元素，而不是其他元素。这点似乎非常明显而没有必要特意强调，之所以要明确它，是因为在实际使用中，有一些结构型伪类常常被错误地当成后代元素的描述符。

为了进一步说明这点，我想分享一则我个人的轶事。2003 年，我的大女儿，也是我的第一个孩子，出生了。我在网上公布了这个消息（就像你们会做的一样^\_^）。许多人回复我表示祝贺，并讲了一些 CSS 的小幽默，许多人用了选择器`#ericmeyer:first-child.`。问题是这个选择器选择的是我，而且只有当我是我父母的第一个孩子的时候才会选择我（巧了，我还真是）。如果要选择我的第一个孩子，选择器应该是`#ericmeyer > :first-child`。

这种混淆是可以理解的，这就是为何我会在这里提到它，后面的章节我们会经常想起它。只要记住，伪类的作用是给它们绑定的元素添加一些“影子类”，就不容易犯（前面的）错误了。

### 选择根元素 Dynamic Pseudo-Classes

这是结构简单性的精髓：伪类选择器`:root`选择文档的根元素。在 HTML 中，根元素**永远是**`html`元素。在为 XML 语言添加样式时，这个选择器会非常有用，因为在不同的语言中根元素可能不同。例如，在 RSS 2.0 中，根元素是`rss`。即使在一种语言（甚至是一个文档）里，也可能会使用不止一个根元素。

图 1-23 展示了一个给 HTML 中的根元素添加样式的例子：

```css
:root {
  border: 10px dotted gray;
}
body {
  border: 10px solid black;
}
```

![图1-23：设置根元素样式](figure1-23.png)

_图 1-23：设置根元素样式_

当然，在 HTML 文档中，可以直接选择`html`元素，不需要使用`:root`伪类。这两个选择器在特度方面有差异，我们将在第 3 章讨论。

#### 选择空元素

使用伪类`:empty`，可以选择任何没有子节点的元素——没有任何类型的子元素：**包含**文本节点，包括文字和空白。这有助于筛除 CMS 生成的没有填进任何实际内容的元素。因此，`p:empty {display: none;}`将会让所有空的段落不再显示。

注意，一个元素如果要被`:empty`匹配，它必须（从解析的角度看）是真正空的——没有空白、可见内容，或后代元素。在下面的元素中，只有第一个和最后一个会被`p:empty`匹配。

```html
<p></p>
<p></p>
<p></p>
<p><!—-a comment--></p>
```

第二个和第三个段落不会匹配`:empty`，因为它们不是空的：它们各自包含一个空格和一个换行符，都会被当做文本节点，因此不是空状态。最后一个段落能够匹配，因为注释既不会被当成内容，也不会被当成空白。但是如果在注释的任何一侧添加一个空格或者换行，`p:empty`将不再匹配它。

你可能会试着为所有空元素设置样式，像这样：`*:empty {display: none;}`，但是这里有个潜在的陷阱：`:empty`会匹配 HTML 的空元素，如`img`和`input`，甚至会匹配`textarea`，除非你为`textarea`元素插入了一些默认文本。因此，从匹配元素的角度来说，`img`和`img:empty`是一样的（它们在特度上有区别，我们将在下一章讨论）。

```html
<img src="salmon.png" alt="North Pacific Salmon" />
<br />
<input type="number" min="-1" max="1" step=".01" />
<textarea></textarea>
```

_**到 2017 年底，`:empty`是唯一一个在匹配元素的时候考虑文本节点的 CSS 选择器。所有 Selectors Level 3 的其他选择器都只考虑元素节点，而完全忽略文本节点——例如，前面讨论过的兄弟组合器**_

### UI-State Pseudo-Classes

### The :target Pseudo-Class

### The :lang Pseudo-Class

### The Negation Pseudo-Class

## 2.7 Pseudo-Element Selectors

### Styling the First Letter

### Styling the First Line

### Restrictions on ::first-letter and ::first-line

### Styling (or Creating) Content Before and After Elements

## 2.8 小结 Summary

By using selectors based on the document’s language, authors can create CSS rules that apply to a large number of similar elements just as easily as they can construct rules that apply in very narrow circumstances. The ability to group together both selectors and rules keeps stylesheets compact and flexible, which incidentally leads to smaller file sizes and faster download times.

通过使用基于文档语言的选择器，作者可以创建适用于大量相似元素的 CSS 规则，就像他们可以轻松地构建适用于非常狭窄环境的规则一样。将选择器和规则组合在一起的能力使样式表更紧凑、更灵活，这也顺便带来了更小的文件大小和更快的下载时间。

Selectors are the one thing that user agents usually must get right because the inability to correctly interpret selectors pretty much prevents a user agent from using CSS at all. On the flip side, it’s crucial for authors to correctly write selectors because errors can prevent the user agent from applying the styles as intended. An integral part of correctly understanding selectors and how they can be combined is a strong grasp of how selectors relate to document structure and how mechanisms—such as inheritance and the cascade itself—come into play when determining how an element will be styled.

选择器是用户代理通常必须正确处理的一件事情，因为无法正确解释选择器很大程度上阻碍了用户代理使用 CSS。另一方面，对于作者来说，正确地编写选择器是至关重要的，因为错误可能会阻止用户代理按预期应用样式。正确理解选择器以及如何组合选择器的一个重要部分是深入了解选择器与文档结构的关系，以及在确定元素的样式时如何使用机制(如继承和级联本身)。
