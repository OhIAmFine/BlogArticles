title: 详述css中百分比值
date: 2016-3-5
tags: [CSS, 转载]
---

转载地址：http://acgtofe.com/posts/2014/06/percentage-in-css  

## 前言
很多css属性的取值都可以是百分比值。虽然形式上来说，百分比值都是数字后跟%的形式（注意数字和%之间不可以有空格），但在不同的使用场合下，其意义会有很多不同。因此，百分比值可以说包含了相当丰富的内容。

## 百分比值是相对值
要理解诸如100%这样的百分比值，其关键点是要明白，百分比是一定有其对应的参照值的。也就是说，百分比值是一种相对值，任何时候要分析它的效果，都需要正确找到它的参照。  

一个css属性值从定义到最终实际使用，是存在一个过程的。这其中涉及到Specified Values（指定值）、Computed Values（计算值）、 Used Values（使用值）、Actual Values（实际值）等概念，可以想见到，百分比值实际会在这个过程中，根据它的参照计算转化为一个绝对值（比如100px），然后再被应用。这就是百分比值的意义。  

更多关于css属性值的处理过程的信息，可以查看[Value Processing](http://dev.w3.org/csswg/css-cascade/#value-stages)。  

## 百分比值的作用？
简单地说，就是可变性。这可以衍生出自适应、响应式等看起来很有用的东西。  

比如说，一个固定宽高的盒子，然后希望盒子内有一个绝对定位的，宽高和盒子一样的盖板（就这样称呼吧...），下面这样的写法会很合适：  

```css
.box{position:relative;width:100px;height:100px;}
.box_cover{position:absolute;width:100%;height:100%;left:0;top:0;}
```

这里使用百分比值的好处的是，如果需要修改盒子的尺寸，只需要修改盒子的宽高，而盖板会自动保持和盒子的尺寸一致。  

再一个例子是Bootstrap的栅格系统：  

![Bootstrap的栅格系统](https://github.com/Tommy-feng/images/blob/master/da640f30de7d9523712f6e5f26cb9671_articlex.png?raw=true)  

可以看到，栅格系统里会用到百分比值来实现确切的对空间的划分。百分比值是相对的，自适应的，因此栅格系统可以很好地用于响应式设计。  

## 可用百分比值的常见css属性  

**width & height**

宽和高在使用百分比值时，其参照都是元素的包含块（Containing Block，详情）。width参照包含块的宽度，height参照包含块的高度。在大部分情况下，包含块就是父元素的内容区（盒模型里的content）。  

我以前写过width:100%; height:100%;这样的代码来实现尺寸和父元素一致。但我发现有时候宽度是符合意思（100%）的，但高度却没有效果。请看下面这个示例：  

![图片](https://github.com/Tommy-feng/images/blob/master/53d60d04e5913997a9af08891abaf402_articlex.png?raw=true)  

关于这一点的详细解释是，当一个元素的高度使用百分比值，如果其包含块没有明确的高度定义（也就是说，取决于内容高度），且这个元素不是绝对定位，则该百分比值等同于auto。auto是初始默认值，所以看起来就像是“失效”了。  

如果元素是根元素（<html>），它的包含块是视口（viewport）提供的初始包含块（initial containing block），初始包含块任何时候都被认为是有高度定义的，且等于视口高度。所以，<html>标签的高度定义百分比总是有效的，而如果你希望在<body>里也用高度百分比，就一定要先为<html>定义明确的高度。这就是为什么在固定页脚一文中，有html, body{height:100%;}这样的写法。  

**margin & padding**  

这2个属性属于混合属性，也通过一个例子说明：  

![图片](https://github.com/Tommy-feng/images/blob/master/37245cb569e9f1035608f1bd970cc167_articlex.png?raw=true)  

可以分析得到，对于margin和padding，其任意方向的百分比值，参照都是包含块的宽度。  

为什么会多个方向都取包含块的宽度作为参照呢？在我看来，包含块的宽度在块布局的排版中是最有用的（想象一下word里输入文字，到宽度边缘后换行的场景），对应的，水平方向的内外边距一定要参照包含块的宽度。再考虑垂直方向的内外边距，它们如果不和水平方向取相同的参照物，就会因为不一致而很难使用。所以，总体来说，统一以包含块的宽度作为参考，会具有相对最好的可用性。  

严格地说，参照是包含块的宽度，是在样式属性writing-mode为默认值时的情况。不过这个属性极少被用到，所以在此不做考虑。  

**border-radius**  

你也许见过有人用下面的代码来让一个矩形变成刚好的圆形（请体会这个“刚好”）：  
```css
.circle{border-radius:50%;}
```  

对此的解释是，为一个元素的border-radius定义的百分比值，参照物是这个元素自身的尺寸。也就是说，假如这个元素宽是60px，高是50px（border-box的尺寸），那么border-radius:50%的结果等同于border-radius:30px/20px;。  

如果你还疑惑这里带/的圆角写法，请查看[MDN对border-radius的说明](https://developer.mozilla.org/en-US/docs/Web/CSS/border-radius)。  

**background-position**  

background-position的初始值就是百分比值0% 0%。下面是一个使用示例：  

![图片](https://github.com/Tommy-feng/images/blob/master/09fbbe7fd03a961360f6c9c8801e4e2f_articlex.png?raw=true)  

background-position的百分比值，取的参照是一个减法计算值，由放置背景图的区域尺寸，减去背景图的尺寸得到，可以为负值。对照上面的示例，思考一下，应该可以感受到，以这个减法计算值为参照的话，正好可以符合我们感官上对背景图位置的理解。  

这个属性包括水平位置和垂直位置，它们分别参照的是宽度减法计算值和高度减法计算值。  

你可能注意到了上面示例的最后一个竟然写了4个值（一般都只用2个值）。关于它的意义，请查看[W3C的background-position](https://www.w3.org/TR/css3-background/#background-position)。  

**font-size**  

参照是直接父元素的font-size。例如，一个元素的直接父元素的font-size是14px，无论这个是直接定义的，还是继承得到的，当该元素定义font-size:100%;，获得的效果就是font-size:14px;。  

**line-height**  

参照是元素自身的font-size。例如，一个元素的font-size是12px，那么line-height:150%;的效果是line-height:18px;。  

**vertical-align**
参照是元素自身的line-height（和前面很有关联吧，所以我排在了这里）。例如，一个元素的line-height是30px，则vertical-align:10%;的效果是vertical-align:3px;。  

对这个属性我还想说，尽管vertical-align可以使用数字，百分比值，但浏览器兼容性差异较大，在跨浏览器实现时可能需要较多hack。因此，我个人倾向于使用middle等相对来说兼容性差异较小的关键字类型的值。  

**定位用的bottom、left、right、top**  

参照是元素的包含块。left和right是参照包含块的宽度，bottom和top是参照包含块的高度。  

**transform: translate**  

平移变换，在水平方向和垂直方向上也可以使用百分比，其参照是变换的边界框的尺寸（等于这个元素自己的border-box尺寸）。例如，一个宽度为150px，高度为100px的元素，定义transform:translate(50%, 50%)的效果是transform:translate(75px, 50px);。  

还可以补充一点，translate3d对应是还有第三个维度的，但是，经过测试，最后的第3个值不可以使用百分比（否则样式定义无效）。至于为什么不可以参照呢，大概是因为那是神秘的第三维度吧...  

**其他**  

如果你想要知道更多的百分比值在css属性中的可用情况及参照值，请参考[MDN的CSS percentage values](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_percentage_values)。  

**百分比值的继承**  

请注意，当百分比值用于可继承属性时，只有结合参照值计算后的绝对值会被继承，而不是百分比值本身。例如，一个元素的font-size是14px，并定义了line-height:150%;，那么该元素的下一级子元素继承到的line-height就是21px，而不会再和子元素自己的font-size有关。  

**结语**  

好不容易终于看完了这么多百分比值的用法，有兴趣要使用一些吗？(・-・*)  

我自己的看法是，百分比值是css所提供的一种建立元素与元素之间，或者元素的不同属性之间的关联性的有效方法。只要是想建立一种关联性，都可以适当考虑使用百分比值。而且，不需自己做任何动态的事件处理和更新，任何时候，你都可以信赖这个百分比。  
