---
title: Modular CSS for Hugo
date: 2021-04-24T21:46:55+01:00
description: This is a blog post. There are tags, images and image ALT text in the Front Matter
tags: 
- modular
- css
- bem
images: 
- https://res.cloudinary.com/growdigital/image/upload/v1617310463/gorse-210401.jpg
imageAlt:
- Yellow flowers
draft: false
---

Godular is a [Hugo](https://gohugo.io/) starter site using Modular CSS.

## 1. Frontend build

* Modular CSS is a way of organising your CSS, and other assets, into discrete and re‑usable chunks.
* The individual chunks are concatenated, transformed and optimised.
* Godular uses [Hugo Pipes](https://gohugo.io/hugo-pipes/) with [PostCSS](https://gohugo.io/hugo-pipes/postcss/).

## 2. Code organisation

The code organisation is based on [Inverted Triangle CSS](https://github.com/itcss) by [Harry Roberts](https://twitter.com/csswizardry), from the most applicable styles (variables, base) to specific modules (objects and components) and to very specific trumping [utilities](https://github.com/suitcss/utils) and [shameful hacks](https://csswizardry.com/2013/04/shame-css/).

![Inverted code triangle showing organisation of modules](https://res.cloudinary.com/growdigital/image/upload/v1620509891/code-triangle.png)

1. **Variables**: global variables and site-wide settings eg `responsive.css`
2. **Base**: unclassed HTML elements eg `a {}`
3. **Objects**: cosmetic-free objects, abstractions, and design patterns eg `o-media.css`
4. **Components**: discrete, complete chunks of UI eg `button.css`
5. **Utilities**: high-specificity, very explicit selectors that trump everything else. Overrides and helper classes eg .`u-hiddenvisually {}`
6. **Shame**: temporarily disorganised CSS lives in `shame.css`

**All files relating to a particular module go in that module folder**: eg JavaScript, PNGs, JPEGs, SVGs, CSS, template snippet for styleguide etc.

## 3. CSS Syntax

<p><code style="font-size:big; color: red;">.block__element--modifier {}</code></p>

Modified BEM syntax
```
.block {}
.block__element {}
.block--modifier {}
```
The `block` is the module (object or component), the `block__element` is a descendant of that module and the `block--modifier` is a variation on that module.

For example:
```
.search {}
.search__field {}
.search--full {}
```

### BEM ground rules

* Hyphen to separate words in long names & two underscores to separate the name of the block from the name of the element:    
  `block-name__element-name`
* CSS class for a block coincides with its block name
* A modifier is a property of a block or an element that alters its look or behavior.
* A modifier has a name and a value. Several modifiers can be used at once.
* Double dash to separate name of block/element from name of modifier:  
  `menu menu--big`

### Namespacing

To add clarity to the `block__element--modifier` convention, use “namespacing” (prefixing a module with an identifying character)
```
.o-object {}
.component {}
.u-utility {}
.js-javascript {}
._-hack {}
.is-state {}, has-state {}
```
For example, `.button {}`, `.o-media {}`, `.u-cf`, `_-messy-hack`. The odd one is out component – no `c-` prefix here, because components are the most common type of module, and if it doesn’t have a prefix it’ll be a component.

## 4. Principles of Modular Code

### Why modular code

* Version control is much easier.
* Finding specific modules is simple.
* Building a style guide requires minimal setup.

### Key principles
1. Build what you need. Start simple. Stay simple.
2. **ID-based CSS selectors must not be used**. IDs have a much higher specificity leading to specifity wars.
3. **HTML elements must not be used in CSS selectors**. This means classes can be applied to any element eg `<input class="button" type="submit">` and `<button class="button">pushme</button>`.
4. **Only use module for one function** ([Single Responsibility Principle](https://en.wikipedia.org/wiki/Single_responsibility_principle)).
5. **Class names should be functional & independent of content**, makes module re-usable in different contexts.
6. Modules must have **unique names**.
