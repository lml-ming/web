---
typora-copy-images-to: mdImg
---

# 学习目标

>
>- [x] 能够写出链接伪类选择器a语法
>
>  ```html
>  a:link 链接未访问过的状态
>  a:visited  链接访问过之后的状态
>  a:hover  鼠标移入的状态
>  a:active  鼠标按下的状态
>  ```
>
>  
>
>- [x] 能够说出盒子模型四大组成部分
>
>  - 内容：content
>  - 内边距：padding
>  - 边框：border
>  - 外边距：margin
>
>- [x] 能够写出1像素实线红色边框的代码
>
>  ```css
>  border: 1px solid red;
>  ```
>
>  
>
>- [x] 能说出padding:10px 20px; 代表的意思
>
>- 盒子上下是10px的padding，左右是20px的padding
>
>
>
>
>- [x] 能够计算盒子实际大小
>  - 盒子的实际大小组成的部分
>    - border+padding+content 
>  - 实际计算的时候：宽度
>    - 左border + 左padding + content的宽度 + 右padding + 右border
>
>
>。。。。。。



**理解上课的知识点**......



##### ヾ(๑╹◡╹)ﾉ" 五彩导航



## :focus 伪类选择器

> 针对于input系列标签还存在一个获取焦点的状态，同样也可以通过focus这种伪类选择器选中

**定义：**:focus 伪类选择器用于选取获得焦点的表单元素。

焦点就是光标，一般情况如 `<input>`  表单类元素才能获取



# 行高的补充

### 行高能让哪些元素垂直居中

> 行高除了可以让单行文本垂直居中之外，还可以让其他元素垂直居中

- 单行文本

- span、a标签（行内元素）

- input、img标签（行内块元素）

  > 特殊情况：要让 `img标签`  通过 `line-height垂直居中` ，需要单独给 `img标签` 设置 ` vertical-align: middle;` 属性

如果想让以上元素垂直居中，需要配合以上元素的所在标签（父元素）设置 `line-height:标签的高度` 



### 行高与font的连写

> 字体连写里面还有行高属性

**完整版的font连写形式：**

`font: style weight size/line-height family`

**注意点：**

- line-height 如果写在 font 连写前面，会被层叠掉

  ```css
  /*line-height书写位置：*/
  /*1. 写在font里 OK */
  font: italic bold 20px/200px '楷体';
  
  /*2. 写在font后面 OK*/
  font: italic bold 20px '楷体';
  line-height: 200px;
  
  /* 3. 写在font前面 会覆盖  */
  line-height: 200px;
  font: italic bold 20px '楷体';
  /* 因为font的连写中有行高属性，连写中省略相当于设置了默认值 */
  ```

- 如果用到了line-height和font的连写

  - 要么把 `line-height` 写在 `font连写`的下面
  - 要么把 `line-height` 写进 `font连写` 的里面 



##### ヾ(๑╹◡╹)ﾉ" PS的基本使用

> 开发中需要根据设计图量取对应的数据进行设置。因此需要学会一些基本的操作



##### ------------------------

# 盒子模型

> 万物皆盒子

![t1](mdImg/t1.png)

## 盒子模型的组成

> 盒子模型的四个组成部分

**生活中普通的盒子：**

![](mdImg/20171105195348.jpg)

**盒子模型的眼光：**

![box](mdImg/box.jpg)

---

**回到代码的总结：**

- 内容：`content` 即**盒子里面的文字或者标签**
- 内边距：`padding` 即**盒子边框到内容之间的距离**
- 边框：`border` 即**盒子的边框**
- 外边距：`margin` 即**盒子与盒子之间的距离**

## 边框：border

### 属性

#### 单个属性

- **border-width**：边框的宽度
- **border-style**：边框的样式
  - **solid**：实线
  - **dashed**：虚线
  - **dotted**：点线
- **border-color**：边框的颜色



#### 连写形式

**代码：** `border:1px solid #000;`

**书写顺序** ：`border: 边框宽度  边框样式 边框颜色;`



#### 单方向设置

> 单独设置盒子的一条边框

**代码：** 

```css
/* border-方位名词：边框粗细  边框样式  边框颜色； */
/* border-left:1px solid #000; */

border-left 左边框
border-right 右边框
border-top 上边框
border-bottom 下边框
```



### 边框合并：border-collapse

> 之前使用表格属性完成的效果存在一个问题：边框比较粗，此时我们可以完全通过css完成

##### ヾ(๑╹◡╹)ﾉ"使用css改写之前的表格案例

**代码：** `border-collapse:collapse；`

**效果：**

> 让表格的边框变成真正的一条边框

<img src="mdImg/细线表格.png" width="500px">

### 盒子大小的初级计算公式

> 学完border之后，可以学习盒子大小的初级计算公式

**需求：**

```html
<!-- 需求 : 
	盒子尺寸 400*400 , 背景绿色, 边框: 10px 实线 黑色 
-->
```

- 设置的width和height其实是内容的宽高
- 设置border会撑大盒子

**使用开发者工具查看盒子模型**

> 谷歌浏览器会帮构建出一个盒子模型
>
> 并且鼠标移入某部分的时候，页面中的对应的盒子的部分会高亮

![box1](mdImg/box1.png)

**盒子大小的初级计算公式：**

`盒子的宽度 = 左边框 + 内容的宽度 + 右边框`

高度同理

**问题：**现在设置完border之后盒子会撑大，怎么样才能满足需求呢？

**解决：** 手动内减

> 手动计算多余的值，然后在内容中减去即可

结果就是：

- 盒子内容：380*380。即width和height都是380px



##### ヾ(๑╹◡╹)ﾉ"写一个小盒子（由内容和边框组成）

![边框练习](mdImg/边框练习.png)

##### ヾ(๑╹◡╹)ﾉ"不low导航~

![效果](mdImg/效果-1537767437391.png)

##### -----------------------------

## 内边距：padding

> 盒子边框与内容之间的距离——》可以控制内容与边框之间的距离

### 取值

- **一个值：** `padding：10px;`
  - **上右下左**都设置为10px
- **两个值：** `padding：10px 20px;`
  - **上下**设置为10px
  - **左右**设置为20px
- **三个值：** `padding：10px 20px 30px;` 
  - **上**设置为10px
  - **左右**设置为20px
  - **下**设置为30px
- **四个值：** `padding：10px 20px 30px 40px;`
  - **上**设置为10px
  - **右**设置为20px
  - **下**设置为30px
  - **左**设置为40px

**记忆规则：** 从上开始顺时针赋值，如果没有赋值的，看对面的

#### 单方向设置padding

> 单独设置盒子的一边padding

**代码：** 

```css
/* padding-方位名词：边框粗细  边框样式  边框颜色； */
/* padding-left:10px; */

padding-top 上内边距
padding-right 右内边距
padding-bottom 下内边距
padding-left 左内边距
```

### 盒子大小的终极计算公式

> 学完padding之后，可以学习盒子大小的终极计算公式了

**需求：** 

```html
<!-- 需求 : 
	盒子尺寸 300*300 , 背景粉色, 上下左右20px的padding , 边框: 10px 实线 黑色 
-->
```

- width和height设置的是内容的宽高
- border会撑大盒子
- padding也会撑大盒子

**盒子大小的终极计算公式：**

`盒子的宽度 = 左border+ 左padding + 内容的宽度 + 右padding + 右border`

高度同理

**问题：** 现在设置完border和padding之后盒子会撑大，怎样才能满足需求呢？

> 同样也是手动计算多余的值，然后在内容中减去即可

结果就是：

- 盒子内容：240*240。即width和height都是380px

---

### 不会撑大盒子的特殊情况

两个互相嵌套的块级元素，如果子盒子没有设置宽度，此时子盒子的宽度默认就是父盒子的宽度。当给子盒子设置以下属性时，子盒子的宽度不会被撑大。
- padding-left
- padding-right
- border-left
- border-right


##### ヾ(๑╹◡╹)ﾉ" 新浪导航（不low导航升级版）~

> 用之前的方法，当a标签的文字数量不确定时，页面会有问题。
>
> 普遍的方法应该使用padding

![导航](mdImg/导航-1537767908758.png)

### CSS3盒模型（自动内减→box-sizing）

> 在实际项目中会大量的用到盒子模型，如果每个盒子都去手动内减，就和不方便，此时我们可以让浏览器帮咱们自动内减
>
> CSS3的新属性：box-sizing可以完成自动内减的效果

**需求：**

```html
<!-- 需求 : 
	盒子尺寸 400*400 , 背景绿色, 边框: 10px 实线 黑色  padding:20px
-->
```

- 手动内减

  > 项目中计算量太大，很麻烦

- 自动内减

  > 给盒子设置 `box-sizing:border-box` 属性。此时设置的`width`和`height`就是盒子的实际宽度

##### ------------------------------

##### ヾ(๑╹◡╹)ﾉ"新闻列表案例

> 熟悉border和padding的使用

![04-练习-新闻列表](mdImg/04-练习-新闻列表.png)









## 外边距：margin

> 盒子与盒子之间的距离——》可以控制盒子的位置

### 取值

- **一个值：** `margin：10px;`
  - **上右下左**都设置为10px
- **两个值：** `margin：10px 20px;`
  - **上下**设置为10px
  - **左右**设置为20px
- **三个值：** `margin：10px 20px 30px;` 
  - **上**设置为10px
  - **左右**设置为20px
  - **下**设置为30px
- **四个值：** `margin：10px 20px 30px 40px;`
  - **上**设置为10px
  - **右**设置为20px
  - **下**设置为30px
  - **左**设置为40px

**记忆规则：** 从上开始顺时针赋值，如果没有赋值的，看对面的

#### 单方向设置margin

> 单独设置盒子的一边margin

**代码：**

```css
/* margin-方位名词：边框粗细  边框样式  边框颜色； */
/* margin-left:10px; */

margin-top 上外边距
margin-right 右外边距
margin-bottom 下外边距
margin-left 左外边距
```

---

### marign单方向的应用

- 上下应用
  - margin-top：能让盒子下移
  - margin-bottom：能让下面的盒子往下移

- 左右应用（先转换成行内块）
  - margin-left：能让盒子右移
  - margin-right：能让右边的盒子往右移动

---

### 清除默认内外边距

> 浏览器会默认给一些标签设置margin和padding，在项目开始之前需要清除这些标签默认的margin和padding，留给自己设置。

比如：

```
body 标签: 自带 margin: 8px; 的属性
p 标签: 默认带有 margin: font-size 的值
ul标签: ul 标签默认带有上下的 margin, 和 padding-left
...
```

因为要清除所有标签默认的内外边距，此时可以使用通配符完成

```
* { 
	padding: 0;
	margin: 0;
}
```

##### ------------------------------

##### ヾ(๑╹◡╹)ﾉ"爱宠知识案例（作业）~

![05-练习-爱宠知识](mdImg/05-练习-爱宠知识.png)
