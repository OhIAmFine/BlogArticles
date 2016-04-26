title: CSS3基础--transform,transition,animation
date: 2016-3-16
tags: [CSS, CSS3, 原创]
categories: CSS

---

## 前言

在CSS3中增加制作动画的几个属性：变形（transform）、转换（transition）、动画（animation）。一般的CSS3参考只是列出了可设置的属性，对于很多同学来说比较抽象，我希望通过这篇文章大家能有进一步的认识。  

## 变形（transform）

变形，顾名思义，就是元素就是改变原来的位置、形状。CSS3中规定了几种变形：旋转（rotate）、倾斜（skew）、缩放（scale）和移动（translate）。

**基点**  
介绍transform前，先理解基点这个概念。基点，即变形参照的点。  
```css
  transform-origin(X,Y)
```
默认是元素的中心点。其中X和Y的值可以是百分值,em,px，其中X也可以是字符参数值left,center,right；Y可以为top,center,bottom。  

**语法**

```css
transform ： none | <transform-function> [ <transform-function> ]*
也就是：
transform: rotate | scale | skew | translate |matrix;
```

none:表示不变换；`<transform-function>`表示一个或多个变换函数，以空格分开。

**旋转** rotate(angle)：以元素中心为基点，angle为角度，为正表示顺时针，为负表示逆时针。  
**倾斜** skew(angle[,angle])：以元素中心为基点，第一个参数对应X轴，第二个参数对应Y轴；其中第二个参数是可选参数，如果没有设置第二个参数，那么Y轴为0deg。  
**缩放** scale(number[, number])：以元素中心为基点，第一个参数对应X轴水平方向的缩放，第二个参数对应Y轴垂直方向的缩放，而第二个参数为可选项，如果没有表示与第一个参数相同。  
**移动** translate(translation-value[, translation-value])：以元素中心为基点，第一个参数对应X轴水平方向的移动值，第二个参数对应Y轴垂直方向的移动值，而第二个参数为可选项，如果没有表示移动为0。  

## 转换（transition）

转化其实定义了元素在变化的过程是怎么样的。

**语法**

```css
 transition: transition-property || transition-duration || transition-timing-function || transition-delay [, transition-property || transition-duration || transition-timing-function || transition-delay]*
```
**transition-property: **: 转换属性，值为none/all；all为默认属性。  
**transition-duration: time[,time]***：持续时间，time单位为s或者ms。  
**transition-timing-function: single-transition-timing-function[,single-transition-timing-function]***：转换函数，值为ease、ease-in、ease-out、ease-in-out、linear。  
**transition-delay: time[,time]***：延迟时间，time单位为s或者ms。


## 动画（animation）

**关键帧（keyframes）**  
关键帧就是animation在设计动画时，中间每一步需要做什么。keyframes的语法由"@keyframes"开头，后面紧接着是这个“动画的名称”加上一对花括号“{}”，括号中就是一些不同时间段样式规则，有点像我们css的样式写法一样。对于一个"@keyframes"中的样式规则是由多个百分比构成的，如“0%”到"100%"之间，我们可以在这个规则中创建多个百分比，我们分别给每一个百分比中给需要有动画效果的元素加上不同的属性，从而让元素达到一种在不断变化的效果，比如说移动，改变元素颜色，位置，大小，形状等，不过有一点需要注意的是，我们可以使用“fromt”“to”来代表一个动画是从哪开始，到哪结束，也就是说这个 "from"就相当于"0%"而"to"相当于"100%",值得一说的是，其中"0%"不能像别的属性取值一样把百分比符号省略，我们在这里必须加上百分符号（“%”）如果没有加上的话，我们这个keyframes是无效的，不起任何作用。因为keyframes的单位只接受百分比值。

```css
@keyframes IDENT {
   from {
     Properties:Properties value;
   }
   Percentage {
     Properties:Properties value;
   }
   to {
     Properties:Properties value;
   }
 }
```

**语法**

```css
animation: animation-name> || animation-duration> || animation-timing-function || animation-delay || animation-iteration-count || animation-direction [, animation-name || animation-duration || animation-timing-function || animation-delay || animation-iteration-count || animation-direction]*

```

**animation-name: none | IDENT[,none | IDENT]***：none表示没有动画效果，IDENT表示动画的名称。  
**animation-duration: time[,time]***：持续时间，time表示时间。  
**animation-timing-function:ease | linear | ease-in | ease-out | ease-in-out**：动画的函数。  
**animation-delay: time[,time]***：元素动画开始时间。  
**animation-iteration-count:infinite | number [, infinite | number]***：可以为具体某个值，也可以为infinite，无限次循环。  
**animation-direction: normal | alternate [, normal | alternate]***：指定动画播放的方向，默认为normal；alternate动画播放在第偶数次向前播放，第奇数次向反方向播放。

## 结语
文中只是大概列出了每个属性的意义，没有具体demo示例，如果你想从代码级别了解，欢迎访问我的[CodePen](http://codepen.io/fengzheqi/)

## 参考资料
- [CSS3 Transition](http://www.w3cplus.com/content/css3-transition)  
- [CSS3 Animation](http://www.w3cplus.com/content/css3-animation)  
- [CSS3 Transform](http://www.w3cplus.com/content/css3-transform)  
- [CSS参考手册](http://www.css88.com/book/css/css3-quicksearch.htm)  
