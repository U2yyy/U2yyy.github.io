---
title: 了解CSS
date: 2022-08-23 11:59:41
categories:
- 青训笔记
---
CSS的了解
<!-- more -->
> **这是我参与「第四届青训营 」笔记创作活动的的第2天**

- 其实刚把今天的课程看了四十多分钟，但已经迫不及待地想要写一篇有关CSS的小笔记了

## 了解CSS

- **CSS是什么？**
  - CSS是层叠样式表的缩写，英文全称为Cascading Style Sheets，是一种用来表现HTML的计算机语言，拥有对王爷对象和模式样式编辑的能力
  - 可以这样说，HTML是页面主体内容的体现，但仅靠HTML是远远不足以呈现好看美观的页面的，想要让页面变得美观、现代化，掌握CSS是必须的

  ![屏幕截图 2022-07-25 101738.png](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/d60eb08d170d4fe19795891220e9e466~tplv-k3u1fbpfcp-watermark.image?)


---



- **怎么在页面中使用CSS？**

  - 外链——最为常用的方法

    > 将HTML文件与外部的CSS文件用`<link>`标签连接起来，从而实现分文件处理

  - 嵌入

    > 即在HTML文件内部用`<style>`标签直接指定各元素的样式，适用于不太复杂的情况

  - 内联

    >直接在各元素内部使用`style`标签指定样式

  ![屏幕截图 2022-07-25 102136.png](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/5a1203b04d604d68bcc913a42f8e0321~tplv-k3u1fbpfcp-watermark.image?)


---

- **选择器**

  > 选择器是CSS里面的一大重点，它的作用是找出页面中的元素，以便设置样式
  >
  > 选择器的选择方法有很多种

  - 按照标签名选择，即直接根据标签名如`<p>`等进行选择

  - 按照类名选择，给元素指定类名，在CSS文件中直接用`.class`选择
  - 按照id选择，给元素指定名称id，在CSS文件中直接用`#id`选择
  - 按照属性选择，如`[attribute]`即为选择所有带有attribute的元素

    除此以外，还有`*选择器`——选择所有元素的选择器等

  ![屏幕截图 2022-07-25 102453.png](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/6b111241808a49b2b52b17f0e6688a8c~tplv-k3u1fbpfcp-watermark.image?)
  > 说到选择器，绕不开的一个东西便是组合方式
  >
  > 使用组合方式，我们可以很好地运用逻辑关系选择自己想要的元素


  

  ![屏幕截图 2022-07-25 103855.png](https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/b8688878a47f441baa61187c967697ef~tplv-k3u1fbpfcp-watermark.image?)


> 使用选择器组则能选择多种元素，一并添加样式

   ![屏幕截图 2022-07-25 104043.png](https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/7e342ed9b288446c94ac077cef0090e4~tplv-k3u1fbpfcp-watermark.image?)

- **颜色和字体**

  > 颜色和字体一定永远是最直观的东西，直接影响了页面的美观
  >
  > 一个审美良好的前端开发者，页面的颜色和字体一定是拿捏的相当到位的，让人赏心悦目

- 颜色的选择是用RGB选择的，前端开发者一定会有自己牢记于心的RGB值，比如这次的掘金编辑器的purple主题，这个紫色我就非常喜欢

  ![屏幕截图 2022-07-25 104421.png](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/b2c21fc9c033498aa4b1f458bd565f27~tplv-k3u1fbpfcp-watermark.image?)
- 字体则直接影响读者的阅读体验，易读美观的字体同样是网页设计里面重要的一环
- 讲师今天提到的一个小技巧，就是当需要应用英文和中文两种相冲突的字体主题时，当主体语言是中文时，可以采用把英文主题放在中文主题前的做法，这样可以使得浏览器在遇到英文字体时应用英文主题，而遇到中文字体时由于英文字体不匹配从而向后推，继而采用中文主题，这样就实现了两个主题的同时运用
![屏幕截图 2022-07-25 104445.png](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/cb7889e6b88d4d9187d872ea47f91e1e~tplv-k3u1fbpfcp-watermark.image?)

  ![屏幕截图 2022-07-25 104643.png](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/620325f2112a480cabac7d7be6c90830~tplv-k3u1fbpfcp-watermark.image?)
  
 > CSS进阶的内容我会在下午去学习，希望能掌握更多有关CSS的好技术
  
