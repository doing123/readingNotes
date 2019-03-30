# CSS世界

无宽度，无图片，无浮动

首选最小宽度：实现凹凸效果

    background-clip/background-origin: content-box/padding-box/border-box

替换元素宽度自适应问题: display:block;//无法自适应宽度100%

    resize: none; // 去除textarea右下角的图标

绝对定位元素的百分比计算和非绝对定位元素的百分比计算是有区别的，区别 在于绝对定位的宽高百分比计算是相对于 padding box 的，也就是说会把 padding 大小值计算 在内，但是，非绝对定位元素则是相对于 content box 计算的

    min-height/min-width:超越!important，超越最大

幽灵空白节点：内联盒模型。

## 第四章：盒尺寸四大家族

注意，这里的<img>直接没有 src 属性，再强调一遍，是直接没有，不是 src=""，src=""在很多浏览器下依然会有请求，而且请求的是当前页面数据。当图片的 src 属性缺省的时候， 图片不会有任何请求，是最高效的实现方式。

CSS 重置的时候加上下面这行:

    img { display: inline-block; }

“我们是无法改变这个替换元素内容的固有尺寸的”
替换元素和非替换元素就是src或content，使用content属性，h1变成了替换元素

    text-align:justify;//两端对齐
    :before ：伪元素用于辅助实现底对齐

    content: attr(alt);
    content: attr(data-title);
      
padding 百分比值无论是水平方向还是垂直方向均是相对于宽度计算的!
对于内联元素，其 padding 是会断行的

元素尺寸：border-box; offsetHeight、offsetWidth
元素内部尺寸： padding-box; clientWidth、clientHeight
元素外部尺寸： margin-box; 无对应的原生DOM api
空块级元素的 margin 合并
margin 合并的计算规则总结为“正正取大值”“正负值相加”“负负最负值”

    writing-mode: vertical-lr; // 垂直居中
    margin: auto;

上下左右垂直居中：
father：position：relative；son：position: absolute;top:0;left:0;right:0;bottom:0;margin:auto;width和height固定

若想使 用 margin 属性改变自身的位置，必须是和当前元素定位方向一样的 margin 属性才可以，否 则，margin 只能影响后面的元素或者父元素

border-width: thin/medium/thick;
border-bottom: 0 none;
border-color的默认颜色就是color色值

## 第五章：内联元素与流

字母x与css中的x-height
行距=line-height - font-size；(行高 - em-box)(em-box就是其高度正好是1em)

图片为内联元素，会构成一个“行框盒子”，而在 HTML5 文档模式下，每一个“行框盒 子”的前面都有一个宽度为 0 的“幽灵空白节点”

    line-height: 80px; // 实现近似垂直居中
    display: inline-block; // 行框盒子--》幽灵空白节点，撑起高度

line-height 的各类属性值：150%、1.5em子元素继承的是计算值，而属性值1.5，子元素继承的是属性值1.5

内联元素line-height的“大值属性”

内联盒模型：只要有“内联盒子”在，就一定会有“行框盒子”，就是每一行内联元素外面包裹的一层看不见的盒子。在每个“行框盒子”前面有一个宽度为0的具有该元素的字体和行高属性的看不见的“幽灵空白节点”。

line-height: 起作用的地方vertical-align也一定起作用

margin/padding相对于宽度计算；line-height相对于font-size计算的；而vertical-align属性的百分比值则是相对于line-height的计算值计算的。
vertical-align作用的前提：只能应用于内联元素以及display值为table-cell的元素

inline-block 与 baseline 之间多变的关系:
一个 inline-block 元素，如果里面没有内联元素，或者 overflow 不是 visible，则该元素的基线就是其 margin 底边缘;否则其基线就是元素里面最后一行内联元素的基线

基于vertical-align属性的水平垂直居中弹框

## 第六章：流的破坏与保护

浮动的本质就是为了实现文字环绕效果，css2属性的设计都是为了图文展示服务的

float元素的“浮动参考”是“行框盒子”，也就是float元素在当前“行框盒子”内定位

浮动锚点、浮动参考

两列、三列布局，优先浮动一侧，使用margin-left控制另一侧的位置，宽度弹性

### 6.2 float的天然克星clear
clear：元素盒子的边不能和前面的浮动元素相邻

clear 属性只有块级元素才有效的。

    .clear:after{
        content: '';
        display: table;
        clear: both;
    }

clear: both; 的作用本质是让自己不和float元素在一行显示

## 6.3 CSS世界的结界--BFC：block formatting context，块级格式化上下文

触发BFC：
html根元素
float的值不为none
overflow的值为auto、scroll、hidden
display的值为table-cell、table-caption、inline-block
position的值不为relative、static

## 6.4 最佳结界overflow
overflow属性的原本的作用指定了块容器元素的内容溢出时是否需要裁剪，也就是“结界”只是其衍生出来的特性，“裁剪”才是其本职工作

overflow剪裁界线border box

如果 overflow-x 和 overflow-y 属性中的一个值设置为 visible 而另 外一个设置为 scroll、auto 或 hidden，则 visible 的样式表现会如同 auto

滚动栏所占据的宽度 17px

依赖overflow的样式表现

    text-overflow：ellipses；
    white-space：nowrap;
    overflow： hidden；

锚点定位行为的触发条件
URL地址中的锚链与锚点定位行为的发生
可focus的锚点元素处于focus状态

锚点定位行为的发生，本质上是通过改变容器滚动高度或者宽度来实现的。

元素设置了 overflow:hidden 声明，里面内容高度溢出的时候，滚 动依然存在，仅仅滚动条不存在!

### 6.5 float的兄弟position：absolute
absolute的包含块

添加 white-space: nowrap，让宽度表现从“包裹性”变成“最大可用宽度”

计算和定位是相对于祖先定位元素的 padding box
”无依赖绝对定位“: position: absolute; 不依赖父元素定位。不需要top\left等
浏览器不一致的行为表现应该属于“未定义行为”

### 6.6 absolute 与 overflow
如果overflow 不是定位元素，同时绝对定位元素和 overflow 容器之间也没有定位元素，则overflow 无法对 absolute 元素进行剪裁。

mix-blend-mode 描述了元素的内容应该与元素的直系父元素的内容和元素的背景如何混合,darken
利用 overflow 滚动 absolute 元素不滚动的特性

### 6.7 absolute 与 clip
clip 属性要想起作用，元素必须是绝对定位或者固定定位，也就是 position 属性值必须是absolute 或者 fixed。

clip 隐藏仅仅是决定了哪部分是可见的，非可见部分无法响应点击事件 等;然后，虽然视觉上隐藏，但是元素的尺寸依然是原本的尺寸
rect()和<top>和<bottom>指定偏移量是从元素盒子顶部边缘算起；<left>和<right>指定的偏移量是从元素盒子左边边缘算起著作权归作者所有。

### 6.8 absolute 的流体特性
设置了对立定位属性的绝对定位元素的表现神似普通的<div>元素，无论设置 padding 还是 margin，其占据的空间一直不变，变化的就是 content box的尺寸，这就是典型的流体表现特性。
absolute的margin：auto居中

### 6.9 relative才是大哥
relative 的定位有两大特性:一是相对自身;二是无侵入
relative的最小化影响原则

### 6.10 强悍的position：fixed固定定位
position：fixed不一样的“包含块”：根元素

    <div class="father">
      <div class="right">
        &nbsp;<div class="son"></div>
      </div>
    </div>
    .father {
      width: 300px; height: 200px;
      position: relative;
    }
    .right {
      height: 0;
      text-align: right;
      overflow: hidden;
    }
    .son {
      display: inline;
      width: 40px; height: 40px;
      position: fixed;
      margin-left: -40px;
    }

position：fixed与背景锁定

## 第七章：CSS世界的层叠规则

### 7.2 理解CSS世界的层叠上下文和层叠水平
层叠上下文：层叠结界

层叠水平：stacking level，决定了同一个层叠上下文中元素在Z轴上的显示顺序

z-index确实可以影响层叠水平，但是只限于定位元素以及flex盒子的孩子元素；而层叠水平所有的元素都存在

### 7.3 理解元素的层叠顺序
### 7.4 务必牢记的层叠准则
谁大谁上

后来居上

### 7.5 深入了解层叠上下文
层叠上下文的创建

天生派：页面根元素天生具有层叠上下文，称为根层叠上下文

正统派：z-index值为数值的定位元素的传统“层叠上下文”

扩招派：CSS3与新时代的层叠上下文
* (1)元素为 flex 布局元素(父元素 display:flex|inline-flex)，同时 z-index值不是 auto。
* (2)元素的 opacity 值不是 1。
* (3)元素的 transform 值不是 none。
* (4)元素 mix-blend-mode 值不是 normal。
* (5)元素的 filter 值不是 none。
* (6)元素的 isolation 值是 isolate。
* (7)元素的 will-change 属性值为上面 2~6 的任意一个(如 will-change:opacity、
will-chang:transform 等)。 
* (8)元素的-webkit-overflow-scrolling 设为 touch。

元素 一旦成为定位元素，其 z-index 就会自动生效，此时其 z-index 就是默认的 auto，也就是0 级别，根据上面的层叠顺序表，就会覆盖 inline 或 block 或 float 元素。而不支持 z-index的层叠上下文元素天然是 z-index:auto 级别，也就意味着，层叠上下文元素和定位元素是 一个层叠顺序的，于是当它们发生层叠的时候，遵循的是“后来居上”准则。

### 7.6 z-index负值深入理解
z-index 负值渲染的过程就是一个寻找第一个层叠上下文 元素的过程，然后层叠顺序止步于这个层叠上下文元素。

### 7.7 z-index“不犯二”准则

* 层叠上下文：background/border
* 负z-index
* block块状水平盒子
* float浮动盒子
* inline/inline-block水平盒子
* z-index：auto或看成z-index：0，不依赖z-index的层叠上下文
* 正z-index

## 第八章：强大的文本处理能力

### 8.1 line-height 的另一个朋友font-size
line-height 的部分类别属性值是相对于 font-size 计算的，vertical-align 百分比值属性值又是相对于line-height计算的
内联元素默认基线对齐，图片的基线可以看成是图片的下边缘，文字内容的基 线是字符 x 下边缘
理解font-size与ex、em和rem的关系
* ex：字符x的高度
* em相对于当前元素，rem相对于根元素，root em。

本质区别在于当前元素是多变的，根元素是固定的

理解font-size的关键字属性值
* 长度值、百分比值
* 相对尺寸关键字：larger、smaller
* 绝对尺寸关键字：xx-large、x-large、large、medium

font-size：0与文本的隐藏。html的font-size默认16px

### 8.2 字体属性家族的大家长font-family

了解衬线字体和无衬线字体：serif、sans-serif
等宽字体的实践价值

ch单位与等宽字体布局：ch相关的字符是0，1ch表示一个0字符的宽度。

### 8.3 字体家族其他成员
font-weight：normal、bold；lighter、bolder；100-900；400-normal；700-bold
font-style：文字造型是斜是正；italics（优先）、oblique
font-variant:small-caps;小体型大写字母

### 8.4 font属性
[ [ font-style || font-variant || font-weight ]? font-size [ / line-height ]?font-family ]

||表示或，?和正则表达式中的?的含义一致，表示 0 个或 1 个。
使用关键字值的font属性：font:caption | icon | menu | message-box | small-caption | status-bar

让网页的字体跟系统走

    html { font: menu; }
    body { font-size: 16px; }

### 8.5 真正了解@font face规则
@font face的本质是变量
“响应式图标”，指的是字号较大时图标字体细节更丰富，字号较小时图标字体更简 单的响应式处理。
unicode-range 的作用是可以让特定的字符或者特定范围的字符使用指定的字体
@font face 与字体图标技术

### 8.6 文本的控制

基于内联盒模型

    text-indent与内联元素缩进
    text-indent：3em ;
    padding-left: 3em; // 纯文本对齐
    letter-spacting与字符间距；-2em：字符反向排列 

    word-break：break-all和word-wrap：break-word的区别
    white-space与换行和空格的控制
    text-align与元素对齐
    text-align：justify；
    text-justify：inter-ideograph；
    font-size：.1px；
    font-size：-webkit-calc(0px + 0px);

解决text-decoration下划线和文本重叠的问题：border实现

一本万利的text-transform字符大小写：uppercase、lowercase

### 8.7 了解：first-letter/：first-line伪元素
:first-line 和:first-letter 伪元素一样，只能作用在块级元素上；仅支持部分CSS属性；color等继承属性的权重总是多了一层，毕竟称为“伪元素”，就好像里面还有个子元素

## 第九章 元素的装饰与美化

### 9.1 CSS世界的color很单调

### 9.2 CSS世界的background很单调
 
positionX = (容器的宽度 - 图片的宽度) * percentX; positionY = (容器的高度 - 图片的高度) * percentY;

background-repeat与渲染性能
外强中干的background-attachment：fixed

## 第十章 元素的显示与隐藏

### 10.1 display与元素的显隐

### 10.2 visibility与元素的显隐

father，visibility：hidden；child，visibility：visible；子元素显示
不仅仅是保留空间那么简单
CSS3 transition支持的CSS属性中有visibility，但是并没 有 display。

* (1)普通元素的 title 属性是不会被朗读的，除非辅以按钮等控件元
素，这里是因为设置了 role="button"所以才可以朗读。 
* (2)visibility:hidden 元素是不会被朗读的

## 第十一章 用户界面样式

### 11.1 盒border形似的outline属性
tabindex：可focus

:focus + label.btn

真正的不占据空间的outline及其应用

* 头像剪裁的矩形镂空效果
* 自动填满屏幕剩余空间的应用技巧
* 自定义光标

## 第十二章 流向的改变
direction改变水平流向：ltr/rtl

direciton的黄金搭档unicode-bidi:normal/embed/bidi-override

### 12.2 改变CSS世界纵横规则的writing-mode

writing-mode就是用来实现文字竖向呈现的
horizontal-tb、vertical-rl、vertical-lr

writing-mode不经意改变了哪些规则
* 水平方向也能margin合并
* 普通块元素可以使用margin：auto实现垂直居中
* 可以使用text-align：center实现图片垂直居中
* 可以使用text-indent实现文字下沉效果
* 可以实现全兼容的icon fonts 图标的旋转效果
* 充分利用高度的高度自适应布局

writing-mode 和 direction 的关系

     CSS 世界中三大可以改变文本布局 流向的属性
