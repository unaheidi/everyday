---
published: true
---
## 前言
近来为新一代发布系统写使用文档，涉及公司网络模型演变的历史，认真读了同事的技术 blog 。打心底里认为这些 blog 不仅内容好，排版也很好。而且很佩服这位同事，养成了及时记录的习惯。  

于是翻看起自己的 blog，决定借着 2021 春节假期，对展示先做个改进。界面好看了，然后鼓励自己多做笔记。

## 问题
* blog 上图片无法展示。看起来整个页面立马 low 了不少。
* 阅读数之前是能正常显示并自动计数的，但现在显示为空。
* markdown 的 code 片段，原本只需一层背景说明它是代码，目前外部又多了一个背景，看起来特别丑。

## 解决方法
* 图片问题通过修改 ／etc/hosts 文件搞定了，查资料是域名被劫持引起的。 [参考](https://www.jianshu.com/p/65e99b0f82ac)
* 阅读数通过激活 leancloud 的应用搞定。
* code展示冗余背景的问题，通过修改 _sass/_highlights.scss 文件搞定。[参考](https://github.com/barryclark/jekyll-now/issues/1025)

## 额外收获
在找解决方法的过程中，翻看了 https://github.com/barryclark/jekyll-now README，
发现 Prose 这个在线编辑服务很不错，有了它，写 blog 会高效不少。  
![prose](https://raw.githubusercontent.com/unaheidi/unaheidi.github.io/master/_posts/images/prose.jpg)
