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
## 优化

1. 减少 HTTP 请求
2. 使用 HTTP2
解析速度快
多路复用
首部压缩
优先级
流量控制
服务器推送
3. 使用服务端渲染
客户端渲染过程
服务端渲染过程
4. 静态资源使用 CDN
CDN 原理
5. 将 CSS 放在文件头部，JavaScript 文件放在底部
6. 使用字体图标 iconfont 代替图片图标
压缩字体文件
7. 善用缓存，不重复加载相同的资源
8. 压缩文件
9. 图片优化
(1). 图片延迟加载
(2). 响应式图片
(3). 调整图片大小
(4). 降低图片质量
(5). 尽可能利用 CSS3 效果代替图片
(6). 使用 webp 格式的图片
10. 通过 webpack 按需加载代码，提取第三库代码，减少 ES6 转为 ES5 的冗余代码
根据文件内容生成文件名，结合 import 动态引入组件实现按需加载
提取第三方库
减少 ES6 转为 ES5 的冗余代码
11. 减少重绘重排
12. 使用事件委托
13. 注意程序的局部性
性能测试
14. if-else 对比 switch
15. 查找表
16. 避免页面卡顿
17. 使用 requestAnimationFrame 来实现视觉变化
18. 使用 Web Workers
19. 使用位操作
取模
取整
位掩码
20. 不要覆盖原生方法
21. 降低 CSS 选择器的复杂性
(1). 浏览器读取选择器，遵循的原则是从选择器的右边到左边读取。
(2). CSS 选择器优先级
22. 使用 flexbox 而不是较早的布局模型
23. 使用 transform 和 opacity 属性更改来实现动画
24. 合理使用规则，避免过度优化
检查加载性能
检查运行性能
25. 使用 sessionStorage 实时存储
sessionStorage 是个全局对象，它维护着在页面会话(page session)期间有效的存储空间。只要浏览器开着，页面会话周期就会一直持续。当页面重新载入(reload)或者被恢复(restores)时，页面会话也是一直存在的。每在新标签或者新窗口中打开一个新页面，都会初始化一个新的会话。

## lighthouse
DiagnosticsMore information about the performance of your application.  These numbers don't directly affect the Performance score.

有关应用程序性能的更多信息。这些数字不会直接影响性能得分。


Serve static assets with an efficient cache policy 2 resources found

使用找到的高效缓存策略2资源为静态资产提供服务


A long cache lifetime can speed up repeat visits to your page.  Learn more. 
URL 
Cache TTL 
Transfer Size 
/js/chunk-vendors.js(192.168.0.107) 
None 
865 KiB 
/js/app.js(192.168.0.107) 
None 
20 KiB

长缓存生存期可以加速对页面的重复访问。学习更多的知识。

https://web.dev/uses-long-cache-ttl/?utm_source=lighthouse&utm_medium=devtools

Keep request counts low and transfer sizes small 3 requests • 885 KiB 
To set budgets for the quantity and size of page resources, add a budget. json file.  Learn more.

保持请求计数低，传输大小小——3 requests • 885 KiB

要为页面资源的数量和大小设置预算，请添加 budget.json 文件。学习更多的知识。

https://web.dev/use-lighthouse-for-performance-budgets/?utm_source=lighthouse&utm_medium=devtools



Largest Contentful Paint element 

最大内容绘制

https://web.dev/lighthouse-largest-contentful-paint/?utm_source=lighthouse&utm_medium=devtools


Avoid long main-thread tasks 

避免长主线程任务

Lists the longest tasks on the main thread, useful for identifying worst contributors to input delay. Learn moreTBT

列出主线程上最长的任务，有助于识别造成输入延迟的最糟糕因素。学习moreTBT

https://web.dev/long-tasks-devtools/?utm_source=lighthouse&utm_medium=devtools


### Passed audits (35)通过了审核


Eliminate render-blocking resources
Properly size images
Defer offscreen images
Minify CSS
Minify JavaScript Potential savings of 5 KiB
Reduce unused CSS
Reduce unused JavaScript
Efficiently encode images
Serve images in next-gen formats
Enable text compression
Preconnect to required origins
Initial server response time was short Root document took 0 ms
Avoid multiple page redirects
Preload key requests
Use HTTP/2
Use video formats for animated content
Remove duplicate modules in JavaScript bundles
Avoid serving legacy JavaScript to modern browsers Potential savings of 0 KiB
Preload Largest Contentful Paint image
Avoids enormous network payloads Total size was 887 KiB
Avoids an excessive DOM size 15 elements
Avoid chaining critical requests
User Timing marks and measures
JavaScript execution time 0.3 s
Minimizes main-thread work 0.5 s
All text remains visible during webfont loads
Minimize third-party usage
Lazy load third-party resources with facades
Largest Contentful Paint image was not lazily loaded
Avoid large layout shifts
Uses passive listeners to improve scrolling performance
Avoids document.write()
Avoid non-composited animations
Image elements have explicit width and height
Has a <meta name="viewport"> tag with width or initial-scale

消除render-blocking资源
适当大小的图片
推迟私生活方面的图片
贬低CSS
潜在节省5kib
减少未使用的CSS
减少未使用JavaScript
有效的编码图像
提供下一代格式的图像
使文本压缩
预连接到所需的原点
初始服务器响应时间短，根文档花费0毫秒
避免多个页面重定向
预加载密钥请求
使用HTTP / 2
动画内容使用视频格式
删除JavaScript包中的重复模块
避免向现代浏览器提供传统的JavaScript服务可能节省0kib
预加载最大的内容油漆图像
避免了巨大的网络负载，总规模为887 KiB
避免过多的DOM大小为15个元素
避免链接关键请求
User计时标记和度量
JavaScript执行时间0.3秒
最大限度减少主线工作0.5秒
所有文本在网页字体加载期间保持可见
减少第三方使用
延迟加载带有facade的第三方资源
最大的Contentful Paint图像没有被惰性加载
避免大的布局变动
使用被动侦听器来提高滚动性能
避免document . write ()
避免non-composited动画
图像元素有明确的宽度和高度
有<meta name="viewport">标签宽度或初始缩放


### accessibility 辅助功能


These checks highlight opportunities to improve the accessibility of your web app. Only a subset of accessibility issues can be automatically detected so manual testing is also encouraged.


这些检查突出了提升网页应用可访问性的机会。只有一小部分可访问性问题可以被自动检测到，因此也鼓励手动测试。

Internationalization and localizationThese are opportunities to improve the interpretation of your content by users in different locales.

国际化和本地化这些都是提高不同地区用户对内容的理解的机会。



<html> element does not have a [lang] attribute
If a page doesn't specify a lang attribute, a screen reader assumes that the page is in the default language that the user chose when setting up the screen reader. If the page isn't actually in the default language, then the screen reader might not announce the page's text correctly. Learn more.

<html>元素没有[lang]属性
如果页面没有指定lang属性，屏幕读取器会假定该页面使用用户在设置屏幕读取器时选择的默认语言。如果页面实际上不是使用默认语言，那么屏幕阅读器可能无法正确宣布页面的文本。学习更多的知识。

Names and labelsThese are opportunities to improve the semantics of the controls in your application. This may enhance the experience for users of assistive technology, like a screen reader.

名称和标签这些是改进应用程序中控件语义的机会。这可能会增强用户使用辅助技术(如屏幕阅读器)的体验。



Form elements do not have associated labels

表单元素没有相关联的标签

Labels ensure that form controls are announced properly by assistive technologies, like screen readers. Learn more.

标签确保表单控件能够通过辅助技术(如屏幕阅读器)正确地显示出来。学习更多的知识。

Additional items to manually check (10) These items address areas which an automated testing tool cannot cover.  Learn more in our guide on conducting an accessibility review.

手动检查的附加项目(10)这些项目处理了自动化测试工具不能覆盖的区域。在我们的指南中了解更多关于进行易访问性审查的内容。



The page has a logical tab order
Interactive controls are keyboard focusable
Interactive elements indicate their purpose and state
The user's focus is directed to new content added to the page
User focus is not accidentally trapped in a region
Custom controls have associated labels
Custom controls have ARIA roles
Visual order on the page follows DOM order
Offscreen content is hidden from assistive technology
HTML5 landmark elements are used to improve navigation

页面有一个逻辑的选项卡顺序
交互式控制是键盘可调焦的
交互元素表明它们的目的和状态
用户的焦点被定向到添加到页面的新内容
用户的焦点不会意外地被困在某个地区
自定义控件具有关联的标签
自定义控件具有ARIA角色
页面上的视觉顺序遵循DOM顺序
屏幕外的内容对辅助技术来说是隐藏的
HTML5地标元素用于改善导航

### best pracitices最佳实践
Trust and Safety
Does not use HTTPS 4 insecure requests found
Ensure CSP is effective against XSS attacks
General
Missing source maps for large first-party JavaScript
Passed audits (15)
Not applicable (1)

信任和安全
不使用HTTPS 4不安全的请求发现

所有的站点都应该使用HTTPS来保护，即使是那些不处理敏感数据的站点。这包括避免混合内容，即一些资源通过HTTP加载，尽管最初的请求是通过HTTPS服务的。HTTPS防止入侵者篡改或被动地监听你的应用程序和用户之间的通信，它是HTTP/2和许多新的web平台api的先决条件

确保CSP对XSS攻击有效
一般

缺少大型第一方JavaScript的源映射

源映射将简化后的代码转换为原始源代码。这有助于开发人员在生产环境中进行调试。此外，灯塔还能提供更深入的见解。考虑部署源映射来利用这些优势。


通过审计(15)
不适用(1)



Links to cross-origin destinations are safe
Avoids requesting the geolocation permission on page load
Avoids requesting the notification permission on page load
Avoids front-end JavaScript libraries with known security vulnerabilities
Allows users to paste into password fields
Displays images with correct aspect ratio
Serves images with appropriate resolution
Page has the HTML doctype
Properly defines charset
Avoids unload event listeners
Avoids Application Cache
Detected JavaScript libraries
Avoids deprecated APIs
No browser errors logged to the console
No issues in the Issues panel in Chrome Devtools

到跨来源目的地的链接是安全的
避免在页面加载时请求地理位置权限
避免在页面加载时请求通知权限
避免具有已知安全漏洞的前端JavaScript库
允许用户粘贴到密码字段
显示图像与正确的长宽比
提供适当分辨率的图像
Page具有HTML文档类型
正确定义字符集
避免卸载事件监听器
避免应用程序缓存
检测到JavaScript库
避免弃用api
控制台没有记录浏览器错误
在Chrome Devtools的问题面板中没有问题

Not applicable (1)
Fonts with font-display: optional are preloaded
Preload `optional` fonts so first-time visitors may use them. Learn more  

不适用(1)
字体显示:可选的字体是预加载的
预加载“可选”字体，这样第一次访问的用户就可以使用它们。了解更多

### SEO
These checks ensure that your page is following basic search engine optimization advice. There are many additional factors Lighthouse does not score here that may affect your search ranking, including performance on Core Web Vitals. Learn more.


这些检查确保您的页面遵循基本的搜索引擎优化建议。还有许多其他因素Lighthouse没有得分，可能会影响您的搜索排名，包括核心Web Vitals的性能。学习更多的知识。

Content Best PracticesFormat your HTML in a way that enables crawlers to better understand your app’s content.

内容最佳实践格式化你的HTML，使爬虫更好地理解你的应用程序的内容。


Document does not have a meta description

文档没有元描述

Meta descriptions may be included in search results to concisely summarize page content. Learn more.

元描述可以包含在搜索结果中，以简洁地总结页面内容。学习更多的知识。

Additional items to manually check (1) Run these additional validators on your site to check additional SEO best practices.

手动检查的附加项(1)在你的站点上运行这些附加的验证器来检查额外的SEO最佳实践。


### Progressive Web App
These checks validate the aspects of a Progressive Web App. Learn more.
先进的Web应用程序
这些检查可以验证渐进式Web应用程序的各个方面。

Installable
Web app manifest or service worker do not meet the installability requirements 1 reason

可安装的
Web app manifest或service worker不满足可安装性要求1的原因

PWA Optimized
Does not register a service worker that controls page and start_url
Does not redirect HTTP traffic to HTTPS
Is not configured for a custom splash screenFailures: No manifest was fetched.
Does not set a theme color for the address bar.Failures: No manifest was fetched, No `<meta name="theme-color">` tag found.
Content is sized correctly for the viewport
Has a <meta name="viewport"> tag with width or initial-scale
Does not provide a valid apple-touch-icon
Manifest doesn't have a maskable iconNo manifest was fetched

PWA优化
不注册一个控制页面和start_url的service worker
不重定向HTTP流量到HTTPS
没有为自定义启动画面配置错误:没有获取清单。
没有为地址栏设置主题颜色。失败:没有获取清单，没有找到' <meta name="theme-color"> '标签。
视口的内容大小正确
有<meta name="viewport">标签宽度或初始缩放
没有提供一个有效的苹果触摸图标
Manifest没有一个可屏蔽的iconNo


Additional items to manually check (3) These checks are required by the baseline PWA Checklist but are not automatically checked by Lighthouse. They do not affect your score but it's important that you verify them manually.

手动检查的附加项目(3)这些检查是基线PWA检查表所要求的，但灯塔不自动检查。它们不会影响你的分数，但是手工验证是很重要的。