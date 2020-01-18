# css 层叠样式表

# 引入 css 的三种方式
```html
<!-- 首先是内联样式，不推荐使用，因为如果有 1000 个标签就需要写 1000 次，如果涉及到要修改就会更加烦躁。 -->
<p style="color: red; font-size: 20px;"></p>

<!-- 第二种方式将样式写到 head 中的 style 标签中,
他的问题在于它只能对一个页面生效 -->
<head>
  <style>
    p {
      color: red;
    }
  </style>
</head>

<!-- 第三种方式 外部文件引入，开发中用这个就对了
外部引入的可以用到 css 的缓存机制 从而加快网页的加载速度，提高用户体验-->
<link rel="stylesheet" href="css文件">
```

## CSS 语法
css 注释 
```css
/* css 中的注释 */
```

css 的基本语法
```css
/* 首先是选择器，用于指定样式生效位置 */
p {
  /* 设置属性和属性的值 */
  color: red;
}
```

### CSS 常用选择器
- 元素选择器
- id 选择器
- class 选择器
- * 通配符选择器

选中 div 并且 class 是 red 的元素
div.red

多选
```css
h1,
h2,
h3 {
  color: red;
}
```

关系选择器
父元素
子元素    父元素 > 子元素
祖先元素
后代元素  父元素 子元素
兄弟元素  哥哥 + 弟弟
弟弟们    哥哥 ~ 弟弟


属性选择器
选择器[属性]    选中属性名匹配的元素
选择器[属性="值"]    选中属性名和属性值都匹配的元素
选择器[属性^="值"]    选中指定属性值开头的元素
选择器[属性$="值"]    选中指定属性值结尾的元素
选择器[属性*="值"]    选中含有指定属性值的元素


伪类选择器
伪类就是特殊的类，一个不存在的类，用来描述一个元素的特殊状态，比如第一个元素，被点击的元素，鼠标移入的元素等等
伪类一般都是以冒号开头
- :first-child  第一个子元素
- :last-child  最后一个子元素
- :nth-child(n)  选中第 n 个子元素

- :first-of-type
- :last-of-type
- :nth-of-type(n)

- :not()

a 元素的伪类
:link  没访问过的伪类
:visited  用来表示访问过的链接
:hover 用来表示鼠标移入
:active 按下的时候

伪元素选择器
伪元素表示页面中并不真实存在的元素
::first-letter  表示第一个字母
::first-line  表示第一行
::selection  表示选中的内容

下面两个伪元素必须结合 content 属性来使用
::before  表示元素起始位置
::after  表示元素结束位置


### 继承
我们为一个元素设置样式同时也会应用到它的后代中
继承是发生在祖先元素和后代中的
利用继承可以极大的方便开发，我们可以将一些通用的样式设置到共同的祖先元素上，这样只需设置一次即可让所有的元素都具有该样式
注意：并不是所有的东西都会被继承，布局、背景之类的就不会被继承


### 选择器的权重
- 无敌权重    !important
- 内联样式    1000
- id         0100
- 类伪类      0010
- 元素选择器   0001
- 通配符选择器  0000
- 继承的权重没有优先级

注意这些是256进制


### 长度单位
像素
  200px
  需要注意同样的像素在不同设备上大小是不一样的

百分比
  100%
  取的是它父元素属性的百分比

em
  em 是相对于元素的字体大小来计算的
  1em 等于 1个字体大小
  em 会根据字体大小发生变化

rem
  rem 是相对于根元素字体大小来计算的


# CSS 颜色
颜色名
  red
RGB
  rgb(255, 0, 0)
RGBA
  rgba(255, 0, 0, .2)
十六进制 RGB
  #FF0000
HSL
  hsl(0, 100%, 50%)
HSLA


# 文档流
元素在文档流中的特点
  块元素
    块元素会在页面中独占一行
    默认宽度是父元素的全部
    默认高度是被子元素撑开

  行内元素
    行内元素不会独占一行，只占自身大小
    行内元素在页面中从左向右水平排列
    行内元素的默认宽高都是被内容撑开


# 盒子模型
盒模型的组成
  content
  padding
    内边距
  border
    width 默认一般 3px    可以分别设置四个方向的宽度  上右下左
      border-top-width
    color
      如果不指定颜色，默认使用文字颜色
    style
      默认是 none
      solid
      dotted
      dashed
      double
    简写形式 1px solid #ccc
  margin
    外边距
    默认情况下设置 margin-right 不会产生任何效果
    margin 可以是负值


### 盒子的水平布局
一个元素在其父元素中，水平布局必须要满足以下的等式
  左右margin + 左右border + 左右padding + content == 它父元素 content 宽度  (必须满足)
  上面的名称叫过度约束
  如果某个值为 auto，则会自动调整 auto 使等式成立

### 垂直方向的布局
默认情况下父元素的高度被内容撑开
但是，如果父元素设置了高度，那么子元素如果比父元素高，就会发生溢出
overflow 可以设置如何处理溢出 overflow-x overflow-y
  visible 默认值  子元素会从父元素中溢出，在父元素外部的位置显示
  hidden  溢出的内容将会被裁剪不会显示
  scroll  出现两个滚动条
  auto    根据需要生成滚动条

### 外边距合并
两个垂直相邻的元素会发生外边距合并问题
父子嵌套 父子外边距相邻 如果给子添加 mt 那么父元素也会被牵连
解决方式：
  添加边框
  给父添加 padding


# 行内元素的盒模型
行内元素不支持设置宽度和高度
行内元素可以设置 padding border margin，但是垂直方向不会影响页面的布局

display 用来设置元素显示的类型
  inline
  block
  inline-block
    既可以设置高度，又不会独占一行
  table
    将元素设置为一个表格
  none

visibility 用来设置元素的显示状态
  visible 默认值，元素在页面中正常显示
  hidden 元素在页面中隐藏，但是位置保留


### 浏览器中的默认样式
list-style: none;

统一浏览器默认样式
normalize.css
重置浏览器默认样式
reset.css

### 盒子大小
outline 用来设置轮廓线，用法和 border 一模一样，但是他不会把下面的元素即开

### 盒子阴影
box-shadow: 左右 上下 模糊半径 颜色

### 圆角
border-radius: 圆角半径


# 浮动
float
元素设置浮动以后，等式就可以不满足了
元素设置浮动以后，会从文档流中脱离，不再占用文档流中的位置，文档流中的其他元素会顶上去
浮动的主要作用就是让页面中的元素可以水平排列

浮动元素不会盖住文字，通过设置浮动可以产生文字环绕效果
元素设置浮动以后，将会从文档流中脱离，从文档流中脱离以后，元素的一些特点也会发生变化
块元素浮动以后的特点
    不再独占一行
    宽度和高度被内容撑开

行内元素浮动以后的特点
    行内元素脱离文档流以后会变成块儿元素，特点和块儿元素一样

脱离文档流以后，就不需要区分行内元素和块儿元素了


box-sizing: border-box;

### 高度塌陷问题
在浮动布局中，父元素的高度默认是被子元素撑开的，当子元素浮动以后，将无法撑起父元素的高度，还会导致下面的元素顶上去

解决方案：
    高度写死
    BFC 块级格式化环境：一个元素开启 BFC 之后会变成一个独立布局区域
    元素开启 BFC 之后的特点
        开启 BFC 的元素不会被浮动元素覆盖
        开启 BFC 的元素子元素和父元素不会重叠
        开启 BFC 的元素可以包含浮动的子元素

        BFC 的开启方式
            设置元素浮动
            将元素设置为行内块元素
            overflow: 非 visible 常用 hidden
  
开启 BFC 之后，父元素就可以包含浮动的子元素


### clear 清除浮动
给一个元素设置清除浮动以后，它就不会因为别的元素浮动而产生变化

## 练习：通过 after 伪类解决高度塌陷



```css
/* 同时解决高度塌陷和外边距重叠问题 */
.clearfix::before,
.clearfix::after {
  content: '';
  display: table;
  clear: both;
}
```


# 定位
绝对定位

相对定位

固定定位

粘滞定位
   sticky


# 字体
字体颜色
    color
字体大小
    font-size
字体单位
    px
    em
    rem
字体格式
    font-family
        serif   衬线字体
        san-serif   非衬线字体
        monospace   等宽字体
        cursive   艺术字体
        fantasy   虚幻字体

```css
@font-face {
  /* 使用 font-face 需要注意 加载速度问题/版权问题/体格格式 ！ */
  font-family: 'myfont';
  src: url() format("truetype");
}
```


## 字体图标
把字体作为图标使用
    iconfont  icomoon fontawesome

## 字体的简写属性
字体的行间距 = 行高 - 字体大小

```css
div {
  font: 字重 font-style 字体大小/行高 '字体';
}
```

## 文本样式
水平居中
  text-align: center
    justify 两端对齐
设置元素垂直的对其方式
  vertical-align
    baseline
    top
    bottom
    middle
    还可以指定 px
文本修饰
  text-decoration
    line-through  删除线
    underlien  下划线
    none  什么都没有
    overline  上划线

  white-space 设置网页如何处理空白
    nowarp  不换行
    pre 保留空白
    
  text-overflow: ellipsis;


## 背景
```css
div {
  background-color
  background-image: url('路径');
  background-repeat: repeat; x; y; no-repeat;
  background-position: top left right bottom center;
  background-origin: content-box;
  background-clip: content-box;
  background-size: cover contain;
  background-attachment: scroll; fiexd;

  background: 颜色 图片 位置/大小 是否重复 是否固定
}

```
渐变
background-image: linear-gradient(to right, red, yellow);
                                  deg
                                  turn

                  repeating-linear-gradient(red 50px, yellow 100px);

radial-gradient()  径向渐变
