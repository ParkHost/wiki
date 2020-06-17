---
title: Deno
description: 
published: true
date: 2020-06-15T20:04:30.098Z
tags: 
editor: undefined
---


![DENO](https://devland.at/assets/images/deno-the-better-node/deno-logo.png =200x200){.align-right} 
is the 'new NodeJS', it is the server side javascript renderer.
It is made by the same creator as NodeJS [Ryan Dahl](https://en.wikipedia.org/wiki/Ryan_Dahl).

After 11 years of Node.js he sees all the flaws of Node and wanted to create a better version. He could only accomplished this by building it from the ground up.
It is made with Rust and now we can use WebAssembly within Deno.


# Installation
With [Chocolatey](/Chocolatey):
```ps
choco install deno
```

> Github Repo: https://github.com/denoland/deno

---

# Usage
Deno is fully [TypeScript](/TypeScript) and `JavaScript` based.


# Modules
it doesn't use a node_module system. You load modules from direct links to (mostly) TypeScript files, which will be cached at the first run.
### Example
```js
import { parseDate, parseDateTime } from 'https://deno.land/std/datetime/mod.ts'

parseDate("20-01-2019", "dd-mm-yyyy") // output : new Date(2019, 0, 20)
parseDate("2019-01-20", "yyyy-mm-dd") // output : new Date(2019, 0, 20)
```

> Deno's Standard Library: https://deno.land/std
{.is-info}


---

