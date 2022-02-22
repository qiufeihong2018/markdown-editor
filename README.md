# markdown-editor

## Question
实现简单的markdown editor。解析markdown的部份可用remarkable这个库。

效果如：https://maxiang.io/，在左边打字，右边显示结果


期间我调研了各种解析 markdown 的方法，也尝试了好几种方式，比如使用过 marked.js（用于解析 Markdown 的低级 markdown 编译器，无需长时间缓存或阻塞）。

源码包中我使用了 remarkable（remarkable 是一个纯 JavaScript 的 markdown 解析器，解析速度快而且易于扩展。100% 支持 Commonmark）解析markdown

使用方法：
```js
var Remarkable = require('remarkable');

// This values are default
var md = new Remarkable({
  html:         false,        // Enable html tags in source
  xhtmlOut:     false,        // Use '/' to close single tags (<br />)
  breaks:       false,        // Convert '\n' in paragraphs into <br>
  langPrefix:   'language-',  // CSS language prefix for fenced blocks
  linkify:      false,        // Autoconvert url-like texts to links
  typographer:  false,        // Enable smartypants and other sweet transforms

  // Highlighter function. Should return escaped html,
  // or '' if input not changed
  highlight: function (/*str, , lang*/) { return ''; }
});

console.log(md.render('# Remarkable rulezz!'));
// => <h1>Remarkable rulezz!</h1>
```
最后将 remarkable 解析生成的 html 内容用 v-html 生成 dom 元素并展示。

## Project setup
```
npm install
```

### Compiles and hot-reloads for development
```
npm run serve
```

### Compiles and minifies for production
```
npm run build
```

### Run your tests
```
npm run test
```

### Lints and fixes files
```
npm run lint
```

### Customize configuration
See [Configuration Reference](https://cli.vuejs.org/config/).
