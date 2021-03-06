---
title: Tree shaking goodness
description: Tree shaking is a simple concept to reduce the size of production build to have faster TTFB (Time To First Byte or page load time)...
date: 2020-09-11
img: tree-shaking.jpeg
---

![Trees, Berat Çıldır, unsplash](tree-shaking.jpeg)

> Tree shaking is a term commonly used in the JavaScript context for dead-code elimination. It relies on the static structure of ES2015 module syntax, i.e. import and export. The name and concept have been popularized by the ES2015 module bundler rollup. [Webpack](https://webpack.js.org/guides/tree-shaking/)

We're not going to deep dive in **tree shaking**, just talk about its benefits and examples. If you're an npm package developer, You should check out [Webpack tree shaking](https://webpack.js.org/guides/tree-shaking/) or [Rollup tree shaking](https://rollupjs.org/guide/en/#tree-shaking) to give the users and developers a better experience.

Tree shaking is a simple concept to reduce the size of production build to have faster TTFB (Time To First Byte or page load time).

## Why? 🤔
It allows the bundler to modify some parts of the production code to remove the unused parts. 

Imagine we have a file **meet.js**: 
```js
// meet.js
function hi() {
    ...
}
function bye() {
    ...
}

export { bye, hi }
```
Now import it in another file: 
```js
import { hi } from './meet.js'

hi();
```
Here is the point, maybe you thought we just imported the **hi**, but not, We imported all of the **meet.js**, that means we have **bye** in the production, too. So the production build has unused code, so we don't want that.

In some packages, we do this too, we import the needed parts, but in production, we have unused code when using object destructuring, but there is a way to get rid of the unused code! 

## How? 😬

Here we can use tree shaking, but if the package that we're using implemented the tree shaking feature.
```js
import { chunk } from 'lodash-es/array/chunk'
```
Almost every package has its way to implement its tree shaking, and it's not wildly different!

For bigger packages, see What happens when we don't use tree shaking. 
```js 
import { chunk } from 'lodash-es' // No tree shaking
// 30Kb just for one function, what! 👎

import { chunk } from 'lodash-es/array/chunk' // With tree shaking
// 1Kb for one function, That's awesome 👍

// https://github.com/webpack/webpack/issues/1750
```

## Note
I think you should use or implement this feature because reducing the build size is so important and the users love the speed. In the previous [article](/post/Next-Dynamic-imports), I said to use the dynamic import feature when you have TTFB issues, and if you use it always, It will affect the TTFB and slows it down sometimes, But tree shaking is a great feature, So use it always when you can.

I hope you enjoyed this small article and You know we don't have likes or comments here, but you can share it. If you wanted to tell me something, tell me in twitter or mention me anywhere else, You can create an issue in GitHub too. 🐞