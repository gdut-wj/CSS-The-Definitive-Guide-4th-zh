# 第 3 章 特异性和级联 Specificity and the Cascade

Chapter 2 showed how document structure and CSS selectors allow you to apply a wide variety of styles to elements. Knowing that every valid document generates a structural tree, you can create selectors that target elements based on their ancestors, attributes, sibling elements, and more. The structural tree is what allows selectors to function and is also central to a similarly crucial aspect of CSS: inheritance.

Inheritance is the mechanism by which some property values are passed on from an element to its descendants. When determining which values should apply to an element, a user agent must consider not only inheritance but also the specificity of the declarations, as well as the origin of the declarations themselves. This process of consideration is what’s known as the cascade. We will explore the interrelation between these three mechanisms—specificity, inheritance, and the cascade—in this chapter, but the difference between the latter two can be summed up this way: choosing the result of h1 {color: red; color: blue;} is the cascade; making a span inside the h1 blue is inheritance.

Above all, regardless of how abstract things may seem, keep going! Your perseverance will be rewarded.

## 3.1 Specificity

You know from Chapter 2 that you can select elements using a wide variety of means. In fact, it’s possible that the same element could be selected by two or more rules, each with its own selector. Let’s consider the following three pairs of rules. Assume that each pair will match the same element:

```css
h1 {
  color: red;
}
body h1 {
  color: green;
}
h2.grape {
  color: purple;
}
h2 {
  color: silver;
}
html > body table tr[id='totals'] td ul > li {
  color: maroon;
}
li#answer {
  color: navy;
}
```

Only one of the two rules in each pair can win out, since the matched elements can be only one color or the other. How do we know which one will win?
The answer is found in the specificity of each selector. For every rule, the user agent evaluates the specificity of the selector and attaches it to each declaration in the rule.When an element has two or more conflicting property declarations, the one with the highest specificity will win out.

This isn’t the whole story in terms of conflict resolution. All style conflict resolution (including specificity) is handled by the cascade, which has its own section later in this chapter (“The Cascade” on page 106).

A selector’s specificity is determined by the components of the selector itself. A specificity value can be expressed in four parts, like this: 0,0,0,0. The actual specificity of a selector is determined as follows:

- For every ID attribute value given in the selector, add 0,1,0,0.
- For every class attribute value, attribute selection, or pseudo-class given in the selector, add 0,0,1,0.
- For every element and pseudo-element given in the selector, add 0,0,0,1. CSS2 contradicted itself as to whether pseudo-elements had any specificity at all, but CSS2.1 made it clear that they do, and this is where they belong.
- Combinators and the universal selector do not contribute anything to the specificity.

For example, the following rules’ selectors result in the indicated specificities:

```css
h1 {
  color: red;
} /* specificity = 0,0,0,1 */
p em {
  color: purple;
} /* specificity = 0,0,0,2 */
.grape {
  color: purple;
} /* specificity = 0,0,1,0 */
*.bright {
  color: yellow;
} /* specificity = 0,0,1,0 */
p.bright em.dark {
  color: maroon;
} /* specificity = 0,0,2,2 */
#id216 {
  color: blue;
} /* specificity = 0,1,0,0 */
div#sidebar *[href] {
  color: silver;
} /* specificity = 0,1,1,1 */
```

Given a case where an em element is matched by both the second and fifth rules in this example, that element will be maroon because the fifth rule’s specificity outweighs the second’s.

As an exercise, let’s return to the pairs of rules from earlier in the section and fill in the specificities:

```css
h1 {
  color: red;
} /* 0,0,0,1 */
body h1 {
  color: green;
} /* 0,0,0,2 (winner)*/
h2.grape {
  color: purple;
} /* 0,0,1,1 (winner) */
h2 {
  color: silver;
} /* 0,0,0,1 */
html > body table tr[id='totals'] td ul > li {
  color: maroon;
} /* 0,0,1,7 */
li#answer {
  color: navy;
} /* 0,1,0,1
 (winner) */
```

I’ve indicated the winning rule in each pair; in each case, it’s because the specificity is higher. Notice how they’re sorted. In the second pair, the selector h2.grape wins because it has an extra 1: 0,0,1,1 beats out 0,0,0,1. In the third pair, the second rule wins because 0,1,0,1 wins out over 0,0,1,7. In fact, the specificity value 0,0,1,0 will win out over the value 0,0,0,13.

This happens because the values are sorted from left to right. A specificity of 1,0,0,0 will win out over any specificity that begins with a 0, no matter what the rest of the numbers might be. So 0,1,0,1 wins over 0,0,1,7 because the 1 in the first value’s second position beats out the 0 in the second value’s second position.

### 3.1.1 Declarations and Specificity

Once the specificity of a selector has been determined, the specificity value will be conferred on all of its associated declarations. Consider this rule:

```css
h1 {
  color: silver;
  background: black;
}
```

For specificity purposes, the user agent must treat the rule as if it were “ungrouped” into separate rules. Thus, the previous example would become:

```css
h1 {
  color: silver;
}
h1 {
  background: black;
}
```

Both have a specificity of 0,0,0,1, and that’s the value conferred on each declaration. The same splitting-up process happens with a grouped selector as well. Given the rule:

```css
h1,
h2.section {
  color: silver;
  background: black;
}
```

the user agent treats it if it were the following:

```css
h1 {
  color: silver;
} /* 0,0,0,1 */
h1 {
  background: black;
} /* 0,0,0,1 */
h2.section {
  color: silver;
} /* 0,0,1,1 */
h2.section {
  background: black;
} /* 0,0,1,1 */
```

This becomes important in situations where multiple rules match the same element and some of the declarations clash. For example, consider these rules:

```css
h1 + p {
  color: black;
  font-style: italic;
} /* 0,0,0,2 */
p {
  color: gray;
  background: white;
  font-style: normal;
} /* 0,0,0,1 */
*.aside {
  color: black;
  background: silver;
} /* 0,0,1,0 */
```

When applied to the following markup, the content will be rendered as shown in Figure 3-1:

```html
<h1>Greetings!</h1>
<p class="aside">
  It's a fine way to start a day, don't you think?
</p>
<p>
  There are many ways to greet a person, but the words are not as important as the act of greeting itself.
</p>
<h1>Salutations!</h1>
<p>
  There is nothing finer than a hearty welcome from one's fellow man.
</p>
<p class="aside">
  Although a thick and juicy hamburger with bacon and mushrooms runs a close second.
</p>
```

// 3-1

In every case, the user agent determines which rules match a given element, calculates all of the associated declarations and their specificities, determines which rules win out, and then applies the winners to the element to get the styled result. These machinations must be performed on every element, selector, and declaration. Fortunately, the user agent does it all automatically. This behavior is an important component of the cascade, which we will discuss later in this chapter.

### 3.1.2 Universal Selector Specificity

The universal selector does not contribute to specificity. In other words, it has a specificity of 0,0,0,0, which is different than having no specificity (as we’ll discuss in “Inheritance” on page 103). Therefore, given the following two rules, a paragraph descended from a div will be black, but all other elements will be gray:

```css
div p {
  color: black;
} /* 0,0,0,2 */
* {
  color: gray;
} /* 0,0,0,0 */
```

As you might expect, this means the specificity of a selector that contains a universal selector along with other selectors is not changed by the presence of the universal selector. The following two selectors have exactly the same specificity:

```css
div p /* 0,0,0,2 */
body * strong /* 0,0,0,2 */
```

Combinators, by comparison, have no specificity at all—not even zero specificity. Thus, they have no impact on a selector’s overall specificity.

### 3.1.3 ID and Attribute Selector Specificity

It’s important to note the difference in specificity between an ID selector and an attribute selector that targets an id attribute. Returning to the third pair of rules in the example code, we find:

```css
html > body table tr[id='totals'] td ul > li {
  color: maroon;
} /* 0,0,1,7 */
li#answer {
  color: navy;
} /* 0,1,0,1 (wins) */
```

The ID selector (#answer) in the second rule contributes 0,1,0,0 to the overall specificity of the selector. In the first rule, however, the attribute selector ([id="totals"]) contributes 0,0,1,0 to the overall specificity. Thus, given the following rules, the element with an id of meadow will be green:

```css
#meadow {
  color: green;
} /* 0,1,0,0 */
*[id='meadow'] {
  color: red;
} /* 0,0,1,0 */
```

### 3.1.4 Inline Style Specificity

So far, we’ve only seen specificities that begin with a zero, so you may be wondering why it’s there at all. As it happens, that first zero is reserved for inline style declarations, which trump any other declaration’s specificity. Consider the following rule and markup fragment:

```css
h1 {
  color: red;
}
```

```html
<h1 style="color: green;">The Meadow Party</h1>
```

Given that the rule is applied to the h1 element, you would still probably expect the text of the h1 to be green. This happens because every inline declaration has a specificity of 1,0,0,0.

This means that even elements with id attributes that match a rule will obey the inline style declaration. Let’s modify the previous example to include an id:

```css
h1#meadow {
  color: red;
}
```

```html
<h1 id="meadow" style="color: green;">The Meadow Party</h1>
```

Thanks to the inline declaration’s specificity, the text of the h1 element will still be green.

### 3.1.5 Importance

Sometimes, a declaration is so important that it outweighs all other considerations. CSS calls these important declarations (for hopefully obvious reasons) and lets you mark them by inserting !important just before the terminating semicolon in a declaration:

```css
p.dark {
  color: #333 !important;
  background: white;
}
```

Here, the color value of #333 is marked !important, whereas the background value of white is not. If you wish to mark both declarations as important, each declaration needs its own !important marker:

```css
p.dark {
  color: #333 !important;
  background: white !important;
}
```

You must place !important correctly, or the declaration may be invalidated. !important always goes at the end of the declaration, just before the semicolon. This placement is especially important—no pun intended—when it comes to properties that allow values containing multiple keywords, such as font:

```css
p.light {
  color: yellow;
  font: smaller Times, serif !important;
}
```

If !important were placed anywhere else in the font declaration, the entire declaration would likely be invalidated and none of its styles applied.

I realize that to those of you who come from a programming background, the syntax of this token instinctively translates to “not important.” For whatever reason, the bang (!) was chosen as the delimiter for important tokens, and it does not mean “not” in CSS, no matter how many other languages give it that very meaning. This association is unfortunate, but we’re stuck with it.

Declarations that are marked !important do not have a special specificity value, but are instead considered separately from non-important declarations. In effect, all !important declarations are grouped together, and specificity conflicts are resolved relatively within that group. Similarly, all non-important declarations are considered together, with any conflicts within the non-important group are resolved using specificity. Thus, in any case where an important and a non-important declaration conflict, the important declaration always wins.

Figure 3-2 illustrates the result of the following rules and markup fragment:

```css
h1 {
  font-style: italic;
  color: gray !important;
}
.title {
  color: black;
  background: silver;
}
* {
  background: black !important;
}
```

```html
<h1 class="title">NightWing</h1>
```

// 3-2

Important declarations and their handling are discussed in more detail in “The Cascade” on page 106.

## 3.2 Inheritance

As important as specificity may be to understanding how declarations are applied to a document, another key concept is inheritance. Inheritance is the mechanism by which some styles are applied not only to a specified element, but also to its descendants. If a color is applied to an h1 element, for example, then that color is applied to all text inside the h1, even the text enclosed within child elements of that h1:

```css
h1 {
  color: gray;
}
```

```html
<h1>Meerkat <em>Central</em></h1>
```

Both the ordinary h1 text and the em text are colored gray because the em element inherits the value of color from the h1. If property values could not be inherited by descendant elements, the em text would be black, not gray, and we’d have to color the elements separately.

Consider an unordered list. Let’s say we apply a style of color: gray; for ul elements:

```css
ul {
  color: gray;
}
```

We expect that style applied to a ul will also be applied to its list items, and also to any content of those list items. Thanks to inheritance, that’s exactly what happens, as Figure 3-3 demonstrates.

// 3-3

It’s easier to see how inheritance works by turning to a tree diagram of a document. Figure 3-4 shows the tree diagram for a very simple document containing two lists: one unordered and the other ordered.

// 3-4

When the declaration color: gray; is applied to the ul element, that element takes on that declaration. The value is then propagated down the tree to the descendant elements and continues on until there are no more descendants to inherit the value. Values are never propagated upward; that is, an element never passes values up to its ancestors.

There is an exception to the upward propagation rule in HTML: background styles applied to the body element can be passed to the html element, which is the document’s root element and therefore defines its canvas. This only happens if the body element has a defined background and the html element does not.

Inheritance is one of those things about CSS that is so basic that you almost never think about it unless you have to. However, you should still keep a couple of things in mind.

First, note that many properties are not inherited—generally in order to avoid undesirable outcomes. For example, the property border (which is used to set borders on elements) does not inherit. A quick glance at Figure 3-5 reveals why this is the case. If borders were inherited, documents would become much more cluttered—unless the author took the extra effort to turn off the inherited borders.

// 3-5

As it happens, most of the box-model properties—including margins, padding, backgrounds, and borders—are not inherited for the same reason. After all, you likely wouldn’t want all of the links in a paragraph to inherit a 30-pixel left margin from their parent element!

Second, inherited values have no specificity at all, not even zero specificity. This seems like an academic distinction until you work through the consequences of the lack of inherited specificity. Consider the following rules and markup fragment and compare them to the result shown in Figure 3-6:

```css
* {
  color: gray;
}
h1#page-title {
  color: black;
}
```

```html
<h1 id="page-title">Meerkat <em>Central</em></h1>
<p>
  Welcome to the best place on the web for meerkat information!
</p>
```

// 3-6

Since the universal selector applies to all elements and has zero specificity, its color declaration’s value of gray wins out over the inherited value of black, which has no specificity at all. Therefore, the em element is rendered gray instead of black.

This example vividly illustrates one of the potential problems of using the universal selector indiscriminately. Because it can match any element, the universal selector often has the effect of short-circuiting inheritance. This can be worked around, but it’s usually more sensible to avoid the problem in the first place by not using the universal selector indiscriminately.

The complete lack of specificity for inherited values is not a trivial point. For example, assume that a style sheet has been written such that all text in a “toolbar” is to be white on black:

```css
#toolbar {
  color: white;
  background: black;
}
```

This will work so long as the element with an id of toolbar contains nothing but plain text. If, however, the text within this element is all hyperlinks (a elements), then the user agent’s styles for hyperlinks will take over. In a web browser, this means they’ll likely be colored blue, since the browser’s internal style sheet probably contains an entry like this:

```css
a:link {
  color: blue;
}
```

To overcome this problem, you must declare something like this:

```css
#toolbar {
  color: white;
  background: black;
}
#toolbar a:link {
  color: white;
}
```

By targeting a rule directly at the a elements within the toolbar, you’ll get the result shown in Figure 3-7.

// 3-7

Another way to get the same result is to use the value inherit, covered in the previous chapter. We can alter the previous example like so:

```css
#toolbar {
  color: white;
  background: black;
}
#toolbar a:link {
  color: inherit;
}
```

This also leads to the result shown in Figure 3-7, because the value of color is explicitly inherited thanks to an assigned rule whose selector has specificity

## 3.3 The Cascade

Throughout this chapter, we’ve skirted one rather important issue: what happens when two rules of equal specificity apply to the same element? How does the browser resolve the conflict? For example, consider the following rules:

```css
h1 {
  color: red;
}
h1 {
  color: blue;
}
```

Which one wins? Both have a specificity of 0,0,0,1, so they have equal weight and should both apply. That can’t be the case because the element can’t be both red and blue. So which will it be?

At last, the name “Cascading Style Sheets” makes sense: CSS is based on a method of causing styles to cascade together, which is made possible by combining inheritance and specificity with a few rules. The cascade rules for CSS are:

1. Find all rules that contain a selector that matches a given element.
2. Sort all declarations applying to the given element by explicit weight. Those rules marked !important have a higher weight than those that are not.
3. Sort all declarations applying to the given element by origin. There are three basic origins: author, reader, and user agent. Under normal circumstances, the author’s styles win out over the reader’s styles. !important reader styles are stronger than any other styles, including !important author styles. Both author and reader styles override the user agent’s default styles.
4. Sort all declarations applying to the given element by specificity. Those elements with a higher specificity have more weight than those with lower specificity.
5. Sort all declarations applying to the given element by order. The later a declaration appears in the style sheet or document, the more weight it is given. Declarations that appear in an imported style sheet are considered to come before all declarations within the style sheet that imports them.

To be perfectly clear about how this all works, let’s consider some examples that illustrate the last four of the five cascade rules.

Some later CSS modules add more origins to the basic list of three; for example, the animation and transition origins. These are not covered here, but are addressed in the chapters on those topics.

### 3.3.1 Sorting by Weight and Origin

If two rules apply to an element, and one is marked !important, the important rule wins out:

```css
p {
  color: gray !important;
}
```

```html
<p style="color: black;">Well, <em>hello</em> there!</p>
```

Despite the fact that there is a color assigned in the style attribute of the paragraph, the !important rule wins out, and the paragraph is gray. This gray is inherited by the em element as well.

Note that if an !important is added to the inline style, then it will be the winner. Thus, given the following, the paragraph (and its descendant element) will be black:

```css
p {
  color: gray !important;
}
```

```html
<p style="color: black !important;">Well, <em>hello</em> there!</p>
```

In situations where the explicit weight is the same, the origin of a rule is considered. If an element is matched by normal-weight styles in both the author’s style sheet and the reader’s style sheet, then the author’s styles are used. For example, assume that the following styles come from the indicated origins:

```css
p em {
  color: black;
} /* author's style sheet */
p em {
  color: yellow;
} /* reader's style sheet */
```

In this case, emphasized text within paragraphs is colored black, not yellow, because normal-weight author styles win out over normal-weight reader styles. However, if both rules are marked !important, the situation changes:

```css
p em {
  color: black !important;
} /* author's style sheet */
p em {
  color: yellow !important;
} /* reader's style sheet */
```

Now the emphasized text in paragraphs will be yellow, not black.

As it happens, the user agent’s default styles—which are often influenced by the user preferences—are figured into this step. The default style declarations are the least influential of all. Therefore, if an author-defined rule applies to anchors (e.g., declaring them to be white), then this rule overrides the user agent’s defaults.

To sum up, there are five basic levels to consider in terms of declaration weight. In order of most to least weight, these are:

1. Reader important declarations
2. Author important declarations
3. Author normal declarations
4. Reader normal declarations
5. User agent declarations

Authors typically need to worry about only the first four weight levels, since anything declared by an author will win out over the user agent’s styles.

### 3.3.2 Sorting by Specificity

If conflicting declarations apply to an element and they all have the same explicit weight and origin, they should be sorted by specificity, with the most specific declaration winning out, like this:

```css
p#bright {
  color: silver;
}
p {
  color: black;
}
```

```html
<p id="bright">Well, hello there!</p>
```

Given the rules shown, the text of the paragraph will be silver, as illustrated in Figure 3-8. Why? Because the specificity of p#bright (0,1,0,1) overrode the specificity of p (0,0,0,1), even though the latter rule comes later in the style sheet.

// 3-8

### 3.3.3 Sorting by Order

Finally, if two rules have exactly the same explicit weight, origin, and specificity, then the one that occurs later in the style sheet wins out. Let’s return to our earlier example, where we find the following two rules in the document’s style sheet:

```css
h1 {
  color: red;
}
h1 {
  color: blue;
}
```

In this case, the value of color for all h1 elements in the document will be blue, not red. This is because the two rules are tied with each other in terms of explicit weight and origin, and the selectors have equal specificity, so the last one declared is the winner.

So what happens if rules from completely separate style sheets conflict? For example, suppose the following:

```css
@import url(basic.css);
h1 {
  color: blue;
}
```

What if h1 {color: red;} appears in basic.css? The entire contents of basic.css are treated as if they were pasted into the style sheet at the point where the @import occurs. Thus, any rule contained in the document’s style sheet occurs later than those from the @import. If they tie in terms of explicit weight and specificity, the document’s style sheet contains the winner. Consider the following:

```css
p em {
  color: purple;
} /* from imported style sheet */
p em {
  color: gray;
} /* rule contained within the document */
```

In this case, the second rule shown wins out over the imported rule because it was the last one specified.

Order sorting is the reason behind the often-recommended ordering of link styles. The recommendation is that you array your link styles in the order link-visited-focushover-active, or LVFHA, like this:

```css
a:link {
  color: blue;
}
a:visited {
  color: purple;
}
a:focus {
  color: green;
}
a:hover {
  color: red;
}
a:active {
  color: orange;
}
```

Thanks to the information in this chapter, you now know that the specificity of all of these selectors is the same: 0,0,1,0. Because they all have the same explicit weight, origin, and specificity, the last one that matches an element will win out. An unvisited link that is being “clicked” or otherwise activated, such as via the keyboard, is matched by four of the rules—:link, Lfocus, :hover, and :active—so the last one of those four will win out. Given the LVFHA ordering, :active will win, which is likely what the author intended.

Assume for a moment that you decide to ignore the common ordering and alphabetize your link styles instead. This would yield:

```css
a:active {
  color: orange;
}
a:focus {
  color: green;
}
a:hover {
  color: red;
}
a:link {
  color: blue;
}
a:visited {
  color: purple;
}
```

Given this ordering, no link would ever show :hover, :focus, or :active styles because the :link and :visited rules come after the other three. Every link must be either visited or unvisited, so those styles will always override the others.

Let’s consider a variation on the LVFHA order that an author might want to use. In this ordering, only unvisited links will get a hover style; visited links do not. Both visited and unvisited links will get an active style:

```css
a:link {
  color: blue;
}
a:hover {
  color: red;
}
a:visited {
  color: purple;
}
a:focus {
  color: green;
}
a:active {
  color: orange;
}
```

Such conflicts arise only when all the states attempt to set the same property. If each state’s styles address a different property, then the order does not matter. In the following case, the link styles could be given in any order and would still function as intended:

```css
a:link {
  font-weight: bold;
}
a:visited {
  font-style: italic;
}
a:focus {
  color: green;
}
a:hover {
  color: red;
}
a:active {
  background: yellow;
}
```

You may also have realized that the order of the :link and :visited styles doesn’t matter. You could order the styles LVFHA or VLFHA with no ill effect.

The ability to chain pseudo-classes together eliminates all these worries. The following could be listed in any order without any overrides:

```css
a:link {
  color: blue;
}
a:visited {
  color: purple;
}
a:link:hover {
  color: red;
}
a:visited:hover {
  color: gray;
}
```

Because each rule applies to a unique set of link states, they do not conflict. Therefore, changing their order will not change the styling of the document. The last two rules do have the same specificity, but that doesn’t matter. A hovered unvisited link will not be matched by the rule regarding hovered visited links, and vice versa. If we were to add active-state styles, then order would start to matter again. Consider:

```css
a:link {
  color: blue;
}
a:visited {
  color: purple;
}
a:link:hover {
  color: red;
}
a:visited:hover {
  color: gray;
}
a:link:active {
  color: orange;
}
a:visited:active {
  color: silver;
}
```

If the active styles were moved before the hover styles, they would be ignored. Again, this would happen due to specificity conflicts. The conflicts could be avoided by adding more pseudo-classes to the chains, like this:

```css
a:link:hover:active {
  color: orange;
}
a:visited:hover:active {
  color: silver;
}
```

This does have the effect of raising the specificity of the selectors—both have a specificity value of 0,0,3,1—but they don’t conflict because the actual selection states are mutually exclusive. A link can’t be an unvisited hovered active link and an unvisited hovered active link: only one of the two rules will match, and the styles applied accordingly.

### 3.3.4 Non-CSS Presentational Hints

It is possible that a document will contain presentational hints that are not CSS—for example, the font element. Such presentational hints are treated as if they have a specificity of 0 and appear at the beginning of the author’s stylesheet. Such presentation hints will be overridden by any author or reader styles, but not by the user agent’s styles. In CSS3, presentational hints from outside CSS are treated as if they belong to the user agent’s stylesheet, presumably at the end (although as of this writing, the specification doesn’t say).

## 3.4 Summary

Perhaps the most fundamental aspect of Cascading Style Sheets is the cascade itself—the process by which conflicting declarations are sorted out and from which the final document presentation is determined. Integral to this process is the specificity of selectors and their associated declarations, and the mechanism of inheritance.
