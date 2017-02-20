---
title: Taking advantage of CSS Custom Properties
authorId: ande
date: 2017-02-16 20:03:00
tags:
  - zonkytech
  - css
  - javascript
---

The draft for [Custom CSS Properties](https://drafts.csswg.org/css-variables/) has existed for quite some time and since implementation for it started in [Microsoft Edge](https://developer.microsoft.com/en-us/microsoft-edge/platform/status/csscustompropertiesakacssvariables/), all of the major browsers will soon [support](http://caniuse.com/#feat=css-variables) it. If you haven't looked at it yet, now might be a good time to prepare for it.

<!-- more -->


## What are CSS Custom Properties?
Custom properties makes it possible to define variables that can be used in your CSS code. The following example adds a custom color variable that can be reused.

```css
/* Define variable*/
:root {   
  --big-margin: 100px;
}
#my-container {   
  margin: var(--big-margin);
}
```

Variables are defined by prefixing our variable name with two dashes and can be accessed using the `var()` function. It is also possible to extend the properties when different styling is used in other contexts.

```css
span {
  color:var(--span-color, red);
}
.my-div {   
  --span-color: blue;
}
```
This of course works similar to regular CSS extensions, one could simply write `.my-div span { color:blue } ` to achieve the same effect. But the benefit of using variables becomes obvious when we want to change the style of multiple components within a certain context. Shown below are two examples of CSS code that does the same thing, the first one using basic CSS and the second one using custom properties.

```css
.reply-button {
  background-color: #ccc;
}

.cancel-button {
  background-color: #ddd;
}

.content {
  font-size: 12px;
  padding: 0 10px;
}

.comment-section {
  margin: 10px;
}

.comment-section .content {
  font-size: 10px;
}

.comment-section .reply-button {
  background-color: #fff;
}

.comment-section .cancel-button {
  background-color: #eee;
}
```

The above code could instead be written as:

```css
.reply-button {
  background-color: var(--reply-bg-color, #ccc);
}

.cancel-button {
  background-color: var(--cancel-bg-color, #ddd);
}

.content {
  font-size: var(--content-font-size, 12px);
  padding: var(--content-padding: 0 10px);
}

.comment-section {
  margin: 10px;
  --content-font-size: 10px;
  --reply-bg-color: #fff;
  --cancel-bg-color: #eee;
}
```

While similar functionality has existed in preprocessors such as [SASS](http://sass-lang.com/) and [LESS](http://lesscss.org/) for a while (with arguably better looking syntax as well), the main difference is that the variables can be used at runtime. This gives us the possibility to write CSS in a way that was not possible before, and possibly write cleaner code at the same time. A typical example of when one would benefit from this, is when using `@media` rules.


## Using `@media` rules
Since the variables can be changed at runtime, they work very well for when we want different styling depending on certain screen width values. Instead of writing new rules for each width, we can simply update the variable.

```css
:root {
  --item-margin: 40px;
}

@media (min-width: 1000px) {
  :root {
    --item-margin: 30px;
  }
}
@media (min-width: 800px) {
  :root {
    --item-margin: 20px;
  }
}

.item {
  margin: var(--item-margin);
}
```

## Using Javascript
Variables can also be updated through JavaScript using getPropertyValue and setProperty.

```JavaScript
// Set margin value
document.body.style.setProperty('--item-margin', '50px');

// Get margin value
document.body.style.getPropertyValue('--item-margin');

```


Custom Properties are a much needed improvement to the CSS standard, but there are still advantages to preprocessors, such as nested syntax, that will probably keep the majority of developers from ditching their favorite tools completely. But the CSS standard is slowly catching up to the preprocessors in terms of functionality. Tools such as the [PostCSS](https://github.com/postcss/postcss) plugin [cssnext](http://cssnext.io/) translates CSS written using the newest syntax from the W3C drafts into browser compatible code, with the goal of being future proof so that the tool one day can be seamlessly removed. Who knows, one day we might not need any CSS preprocessors at all.

## Recommended Reading
[Let's Talk about CSS Variables](http://www.xanthir.com/blog/b4KT0) - Tab Atkins Jr
[CSS Custom Properties - CSSWG Editors Draft](https://drafts.csswg.org/css-variables/)
[CSS Variables: Why should you care? ](https://developers.google.com/web/updates/2016/02/css-variables-why-should-you-care) - Rob Dodson
