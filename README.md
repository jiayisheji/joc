# joc
这是一个个人标准css书写命名规范
1、结构与样式的分离
每个元素都有不同的视觉展现，但是在同一项目中按钮、导航、下拉菜单等等是可以高度复用的，也许在页面A你使用的按钮，在页面B使用的时候只是调整了一下大小和颜色，所以如果结构和样式分离，控制大小的分别是.btn-sm和.btn-lg类，控制颜色的是.btn-info和.btn-error类，那么你基本就完成了结构与样式的分离。
2、容器与内容的分离
基于OOCSS建立的类模块，书写的样式不依赖于任何不必要的父级元素。这意味着它们可以在文档的任何地方被复用，无论结构如何，深度定制的设计样式模型应该单独去书写；简而言之，你的共用样式不要依赖于设计逻辑，不要为了实现一个效果给一个class写非常多的属性，如果一个class里超过10行属性，这时候你可能就要考虑是不是有些东西可以抽离出来，做到这点需要有很好的大局观，可能对于新手来说确有难度，但是请细心领悟这一点。
3、使用类名扩展基础类
一个对象总是由一个基础类，和多个扩展类拼装而成，请记住这一点。
4、坚持语义化定义
刚刚的那个例子中颜色为什么不定义.btn-bule和.btn-red类，这就要讨论面向对象的css的本质是对象，info和error显然更具化，专业的说叫语义化，这就大大降低了复用的成本，因为你知道错误的颜色就是.btn-error。

## 分类方法

### CSS文件的分类和引用顺序

通常，一个项目我们只引用一个CSS，但是对于较大的项目，我们需要把CSS文件进行分类。

我们按照CSS的性质和用途，将CSS文件分成“全局公共型样式”、“全局特殊型样式”、“全局皮肤型样式”、“当前页面样式”，并以此顺序引用（按需求决定是否添加版本号）。

公共型样式：包括了以下几个部分：“标签的重置和设置默认值”、“统一调用背景图和清除浮动”、“网站通用布局和常用盒子模型样式”、“通用模块和其扩展”、“通用组件和其扩展”、“元件和其扩展”、“功能类样式”、“皮肤类样式”。
特殊型样式：当某个栏目或页面的样式与网站整体差异较大或者维护率较高时，可以独立引用一个样式：“特殊的布局、模块、组件和元件及扩展”、“特殊的功能、颜色和背景”，也可以是某个大型控件或模块的独立样式。
皮肤型样式：如果产品需要换肤功能，那么我们需要将颜色、背景等抽离出来放在这里。
当前页面样式：如果不是做SPA单页应用，我们需要在不同页面写不同的样式，除开上面的一些公共样式以外。


```
<link href="assets/css/global.css" rel="stylesheet" type="text/css"/>
<link href="assets/css/public.css" rel="stylesheet" type="text/css"/>
<link href="assets/css/skin.css" rel="stylesheet" type="text/css"/>
<link href="assets/css/index.css" rel="stylesheet" type="text/css"/>
```

### CSS内部的前缀

1. 重置（reset）和默认（base）（tags）：消除默认样式和浏览器差异，并设置部分标签的初始样式，以减少后面的重复劳动！你可以根据你的网站需求设置！
2. 布局（grid）（.g-）：将盒子模型宽度，高度，边框，外边距，内填充统一声明，按需使用，通常被重复用。
3. 盒子模型 （Box Model） （.b-）：将盒子模型宽度，高度，边框，外边距，内填充统一声明，按需使用，通常被重复用。
4. 功能（function）（.f-）：为方便一些常用样式的使用，我们将这些使用率较高的样式剥离出来，按需使用，通常这些选择器具有固定样式表现，比如清除浮动等！不可滥用。
5. 皮肤 （skin）（.s-）：如果你需要把皮肤型的样式抽离出来，通常为文字色、背景色（图）、边框色等。
6. 图标 （iconfont）（.i-）：图标分为图标字体和图片图标，这些图标网站整体统一可以共用，图片可以同雪碧图。
7. 模块 （module）（.m-）：通常是一个语义化的可以重复使用的较大的整体！比如导航、登录、注册、各种列表、评论、搜索等。
8. 组件 （widget）（.w-）：通常是一个语义化的可以重复使用的独立的较大的整体！比如模态，灯箱，轮播图，选项卡，提示等。
9. 元件  （unit）（.u-）：通常是一个不可再分的较为小巧的个体，通常被重复用于各种模块和组件中！比如按钮、输入框、loading等。
10. 状态  （condition）（.c-）: 为状态类样式加入前缀，统一标识，方便识别
11. js使用 （JavaScript）（.j-）：特殊前缀.j-将被专用于JS获取节点，请勿使用.j-定义样式。

## 命名规则

### 由来
一开始写css就是参照一些网站给的命名，直接是一些英文单词，就会出现很多重名，和覆盖问题。为了解决这些痛点，尝试过很多命名方式，下划线，中划线，驼峰等。直到我学习js时候，发现有一个命名方式匈牙利命名法。

> 匈牙利命名法是一种编程时的命名规范。基本原则是:变量名=属性+类型+对象描述，其中每一对象的名称都要求有明确含义，可以取对象名字全称或名字的一部分。命名要基于容易记忆容易理解的原则。保证名字的连贯性是非常重要的。

我想到了，那么css是不是也可以这样的，命名前缀+语义描述。通过大量实践总结了这9种前缀命名规范。

有一天发现了一个网站既然和我想法一样。
> [网易NEC](http://nec.netease.com/)

我现在文档格式就是参照它的来写的。我的前缀比他更细化一些。

### 使用类选择器，放弃ID选择器
ID在一个页面中的唯一性导致了如果以ID为选择器来写CSS，就无法重用。

> id和class区别
使用css时候，id选择器不能结合使用，只能使用一次，而class可以多次使用。当使用js时候需要用到id。
从数据加载来说：先找到id在找到结构，然后渲染，而class先渲染在找结构，最后找到内容。

### JOC特殊字符："-"连字符
"-"在本规范中并不表示连字符的含义。
只表示两种含义：分类前缀分隔符、扩展分隔符。

```
.u-btn{}
.u-btn-default{}
```




