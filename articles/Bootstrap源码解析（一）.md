# 前言  
很早就有读一读Bootstrap的源码的冲动，由于各方面的原因，一直没有全面的了解；刚好最近因为项目的需求要用sass，也趁这个机会读一读Bootstrap的sass源码，文本只是基于本人的理解与看法，若有偏差，还望大家指正。

# Bootstrap源码解析（一）
在Bootstrap的github上可以下载对于的sass源码，然后我们主要关注的是`assets/javascripts`和`assets/stylesheets`这两个目录。我们首先解析的是css部分，然后第一个需要关注的源文件是`_bootstrap.scss`，里面记录了bootstrap在sass源码解析的顺序。

## 全局变量定义、混合申明
### 全局变量定义（`_variables.scss`）  

全局变量里定义了包括颜色、字体；没有很难的内容，不用刻意去看代码，在后面看到用到了哪些变量，回过去再查找即可。  

不过这里我简单的介绍几个sass的语法，便于理解：  
  - `!default`：在sass中表示设置默认变量，如果需要覆盖这个默认变量，只需要在默认变量之前重新声明即可  
  - `lighten()/darken()/ceil()/floor()`：这是sass自带的[函数](http://sass-lang.com/documentation/Sass/Script/Functions.html)  

### 混合声明
sass中的混合声明可以比喻为公共代码块，作用是复用。
里面用的sass
