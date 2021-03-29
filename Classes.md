---
title: JS - Classes
description: 
published: true
date: 2020-12-02T13:55:20.992Z
tags: javascript, classes
editor: markdown
dateCreated: 2020-08-13T05:13:30.162Z
---

# Javascript classes

I see classes as defining how an object should look like and give some 'predefined' parameters. Like in the example below; a rectangle has a `Height` and a `Width`.


> Classes in JS are built on prototypes but also have some syntax and semantics that are not shared with ES5 classalike semantics.
> [MDN Source](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Classes)
{.is-info}

---

# Example

```js
class Rectangle {
  constructor(height, width) {
    this.height = height;
    this.width = width;
  }
}
```