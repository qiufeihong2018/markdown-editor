<template>
  <div class="main-container">
    <textarea :value="input" @input="update"></textarea>
    <div class="main-container__html" v-html="compiledMarkdown"></div>
  </div>
</template>

<script>
import { Remarkable } from "remarkable";
import _ from "lodash";
export default {
  data() {
    return {
      input: `# hello world
      
**马克飞象**是一款专为印象笔记（Evernote）打造的Markdown编辑器，通过精心的设计与技术实现，配合印象笔记强大的存储和同步功能，带来前所未有的书写体验。特点概述：
 
- **功能丰富** ：支持高亮代码块、*LaTeX* 公式、流程图，本地图片以及附件上传，甚至截图粘贴，工作学习好帮手；
- **得心应手** ：简洁高效的编辑器，提供[桌面客户端][1]以及[离线Chrome App][2]，支持移动端 Web；
- **深度整合** ：支持选择笔记本和添加标签，支持从印象笔记跳转编辑，轻松管理。
      `,
      compiledMarkdown: "",
      // Remarkable的详细配置
      options: {
        html: false, // Enable HTML tags in source
        xhtmlOut: false, // Use '/' to close single tags (<br />)
        breaks: false, // Convert '\n' in paragraphs into <br>
        langPrefix: "language-", // CSS language prefix for fenced blocks
        // Enable some language-neutral replacement + quotes beautification
        typographer: false,
        // Double + single quotes replacement pairs, when typographer enabled,
        // and smartquotes on. Set doubles to '«»' for Russian, '„“' for German.
        quotes: "“”‘’",
        // Highlighter function. Should return escaped HTML,
        // or '' if the source string is not changed
        highlight: function (/*str, lang*/) {
          return "";
        },
      },
    };
  },
  watch: {
    input: {
      handler(n) {
        // 缓存markdown原文
        sessionStorage.setItem("markdownContent", n);
        const md = new Remarkable(this.options);
        const result = md.render(n);
        // 缓存解析后的html内容
        sessionStorage.setItem("htmlContent", result);
        this.compiledMarkdown = result;
      },
    },
  },
  mounted() {
    // 读取默认值
    this.readDefault();
    // 读取缓存
    this.readStorage();
  },
  methods: {
    readStorage() {
      const markdownContent = sessionStorage.markdownContent;
      if (markdownContent) {
        this.input = markdownContent;
      }
      const htmlContent = sessionStorage.htmlContent;
      if (htmlContent) {
        this.compiledMarkdown = htmlContent;
      }
    },
    readDefault() {
      if (this.input) {
        const md = new Remarkable(this.options);
        const result = md.render(this.input);
        this.compiledMarkdown = result;
      }
    },
    update: _.debounce(function (e) {
      this.input = e.target.value;
    }, 500),
  },
};
</script>

<style>
html,
body,
.main-container {
  margin: 0;
  height: 100%;
  font-family: "Helvetica Neue", Arial, sans-serif;
  color: #2c3f51;
}

textarea,
.main-container__html {
  display: inline-block;
  width: 49%;
  height: 100%;
  vertical-align: top;
  box-sizing: border-box;
  padding: 0 30px;
}

textarea {
  border: none;
  border-right: 1px solid #ccc;
  resize: none;
  outline: none;
  background-color: #36312c;
  color: #ebd1b7;
  font-size: 14px;
  font-family: "Monaco", courier, monospace;
  padding: 20px;
}
::-webkit-scrollbar {
  height: 10px;
  width: 7px;
  background: transparent;
}
::-webkit-scrollbar-corner {
  background: #000;
}
::-webkit-scrollbar-thumb {
  background: rgba(0, 0, 0, 0.3);
  -webkit-border-radius: 6px;
}
</style>
