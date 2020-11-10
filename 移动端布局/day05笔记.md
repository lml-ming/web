---
typora-copy-images-to: mdImg
---

# 学习目标

> - [x] 能够完成骰子案例
>
> - [x] 独立完成携程移动端首页案例
>
> - [x] 掌握媒体查询的基本语法
>
>   ```css
>   @media screen and (条件) {
>     选择器
>   }
>   
>   条件：
>   1、min-width：样式生效的最小宽
>   2、max-width：样式生效的最大宽
>   3、width：样式生效的宽度
>   ```
>
>   
>
> - [x] 了解less的作用
>
>   - **写样式**——》写完less——》编译成css——》浏览器用的css文件
>
> - [x] 能够了解less的基本语法
>
>   ```less
>   // 注释
>   
>   变量： @变量名:值;
>   
>   嵌套：标签的关系可以通过嵌套表示
>   
>   函数： .函数名() { 重复的样式 }
>   
>   引入：@import 'less路径'
>   ```
>
>   
>
> - [x] 能够理解rem和em的区别
>
>   - em：1em = 当前标签的font-size
>   - rem：1rem = html标签的font-size
>
> - [ ] 
>
> - [ ] 掌握媒体查询+rem适配
>
> - [ ] 能够完成苏宁rem布局首页
>
> 。。。。。。



**理解上课的知识点......**



# LESS的学习

>  在写css的时候，可以直接写一个.css文件，但是实际开发中也会使用less的方法写css。
>
>  less的写法比css的写法功能更加强大。

## 维护css的弊端

> css是一门非编程式语言，没有变量、函数、作用域等概念

- css需要书写大量没有逻辑的代码，冗余度较高

  ```css
    div {
      background-color: skyblue;
    }
  
    p {
      background-color: skyblue;
    }
  
    span {
      background-color: skyblue;
    }
  ```

- 不方便修改维护和拓展，不利于复用

- css没有很好的计算能力



> 使用less就能解决以上css中的弊端

## Less的介绍

> [Less](http://lesscss.cn/) 是一门 CSS 预处理语言，也叫做css的预处理器。它扩展了 CSS 的写法，增加了变量、函数等特性。

```less
less作为css的拓展，并没有减少css的功能，而是在现有的css语法中，加入了程序式语言的特性
less在css的语法基础上，引入了变量、运算以及函数等功能，大大简化了css的编写，并且减低了css的维护成本，正如其名字一样：less可以让我们用更少（less）的代码做更多的事情
当然，常见的css预处理器有：Less、Sass、Stylus
```

**注意点：**

- 在less中，完全兼容css的语法，所以可以直接在less文件中写css没问题

- **浏览器不认识less文件**，需要需要使用less中的样式，需要先把less文件编译成.css文件，再使用！！

  > index.less——》index.css——》再在html页面中引入css使用



## less的编译插件及配置

> less写完之后需要编译.css文件才能使用，此时可以使用VScode中的插件完成。

**插件的安装步骤：**

1. 选择左侧第五个拓展按钮，下载插件 **`easy less`** ，点击安装，再点击重新加载

   > 安装好之后，重新加载或者关闭vscode重新打开

   ![easyless安装](mdImg/easyless安装.gif)

2. 实际开发中需要对插件进行配置

   > 让编译好的css文件在css文件夹中

   在设置代码中添加一下配置即可

   > 使用的时候直接复制粘贴，**注意在上一行的最后加一个逗号**
   >
   > 设置完之后需要**重新打开vscode**即可

   ```json
   "less.compile": {
       "out": "../css/"
   }
   ```

   ![easyless配置](mdImg/easyless配置.gif)



**注意点：**

- 以后项目中如果有less文件之后，样式都**写在less文件**中写即可，不用去修改css文件

  > 因为css文件都是less编译之后的结果，只需要关注less的修改即可

- 但是页面中**引入的是编译之后的css文件**



## Less语法

### less的注释

> 在less文件中可以写两种注释

- 一种是css的注释：`/* 注释的内容 */` ，最后会编译展示在css文件中
- 一种是less的注释：`// 注释的内容` ，只在less中使用，不会编译展示在css文件中

> 一般在less文件中，推荐使用less的注释方法

### less的变量

> 一般在网站中会有主题色（当前网页中用的较多的颜色），如果此时需要改换网页的主题色，一个个去改非常麻烦，此时可以使用less中的变量完成效果

**语法：**

```css
变量：可以变化的量
语法：@变量名:变量值;
作用：编译的时候会把less中所有的变量名替换成变量值，这样可以统一修改某一个值（如主题色）
```

**例子：**

```less
@mainColor:#e92322;

.box1 {
  width: 200px;
  height: 200px;
  background-color: @mainColor;
}
.box2 {
  width: 200px;
  height: 200px;
  background-color: @mainColor;
}
.box3 {
  width: 200px;
  height: 200px;
  background-color: @mainColor;
}
```

### less的嵌套

> 在less中，选择器的关系可以通过嵌套来表示

```less
// less中的嵌套：less中选择器可以嵌套
// 1、后代选择器，选择器嵌套即可
// 2、子代选择器，前面使用>
// 3、并集选择器，前面直接写,
// 4、交集选择器，前面使用&（&表示上一级选择器）
// 5、伪元素，前面使用&（&表示上一级选择器）

.father {
  width: 600px;
  height: 600px;
  background-color: pink;
    
   // 后代的关系，直接嵌套即可
  .son {
    width: 400px;
    height: 400px;
    background-color: blue;
	
    // 子代选择器，前面加一个>
    >.sun {
      width: 200px;
      height: 200px;
      background-color: yellow;
    }
  }
    
  // 并集选择器
  .box1,
  .box2 {
    width: 100px;
    height: 100px;
    background-color: orange;
  }

  // 交集选择器
  &.active {
    background-color: red;
  }
    
  // 伪元素
  &::after {
    content: '';
  }

}
```

### less的运算

> 在less代码中可以直接写加减乘除进行计算

```less
.box {
  width: 200px;
  height: 200px;
  background-color: pink;

  // 伪类的写法
  &:hover {
    // less中可以直接计算加减乘除计算的，编译之后会把计算的结果直接显示在css文件中。之后学习的rem布局中需要使用到less运算的功能
    width: 200px / 3;
    width: 200px * 2;
    width: 200px + 100;
    width: 200px - 100;
  }
}
```

### less的函数（了解）

> 针对于css中重复的样式，除了可以使用定义公共类的方式，还可以使用less中的函数来处理（函数在之后的js会详细说到，先简单了解下）

**需求：**

> 每一个选择器中的width和height代码都重复了，节省代码的方式

```css
.red {
  width: 300px;
  height: 300px;
  background-color: red;
}
.blue {
  width: 300px;
  height: 300px;
  background-color: blue;
}
.green {
  width: 300px;
  height: 300px;
  background-color: green;
}
```

- 可以提取出一个公共类出来，然后给对应的标签上加公共类
- 也可以使用less中的函数，给选择器上使用函数也可以
- 语法：**`.函数名(){重复的样式}`** 

```less
// 在less中也一种处理重复样式的方法：函数。直接在选择器里面使用
// 函数的写法和定义公共类很像，后面需要加上括号

// 定义函数
.common() {
  width: 300px;
  height: 300px;
}

.red {
  // 使用函数
  .common();
  background-color: red;
}

.blue {
  .common();
  background-color: blue;
}

.green {
  .common();
  background-color: green;
}

```

**拓展（了解）：**

函数里面可以传参，让函数中样式的取值变化（变化的量→变量）

> 比如让红盒子`100*100`， 蓝盒子`200*200` ，绿盒子`300*300`

```less
.common(@value) {
  width: @value;
  height: @value;
}

.red {
  // 使用函数
  .common(100px);
  background-color: red;
}

.blue {
  .common(200px);
  background-color: blue;
}

.green {
  .common(300px);
  background-color: green;
}
```



##### ヾ(๑╹◡╹)ﾉ" 使用less实现京东头部

> 让同学们熟悉通过less写项目的操作

- 视口：

  ```html
  <meta name="viewport" content="width=device-width, user-scalable=no, initial-scale=1.0, maximum-scale=1.0, minimum-scale=1.0">
  ```

- 全局容器



### less的引入（了解）

> 之前写css，一个html网页中需要引入很多css文件，需要写很多个link标签分别引入
>
> 使用less之后，可以直接把很多的less文件引入在一个less文件中（把多个less文件变成一个less文件），最后网页这边只需要引入一个css文件即可。

**语法：**

```less
@import '需要引入的less文件的路径'
 
注意点：一般引入的文件写在最前面，保证自己的样式写在后，优先
```

**对比：**

- 原来的分开引入：

  ![image-20200906150053061](mdImg/image-20200906150053061.png)

- 现在的@import合并引入：

  ![image-20200906150139510](mdImg/image-20200906150139510.png)





# rem布局

> 现阶段很常见的布局

## 为什么要用rem布局？

**之前学习的：**

- 流式布局/flex布局：都是针对于盒子宽度的适配变化，但是盒子的高度和文字的大小等是无法适配变化的

  > 在较大屏幕下看，盒子高度和文字大小不会变化，用户观感：盒子拉长了、盒子太扁，文字太小，效果不好

**现在学习的：**

- rem布局：针对于页面中所有盒子的宽高、文字大小等，所有元素都能做到跟随屏幕**等比例缩放**。

  > 不管在大屏还是小屏看，以为是等比例缩放，不会有盒子拉长、文字太小的问题，用户观感较好。

- 而rem布局就能做到让页面中所有的元素大小跟随屏幕宽度进行变化（包括盒子的宽高、文字大小......）



**总而言之：如果需要让页面中所有元素大小一起等比例缩放，目前会使用rem布局**



## rem单位的学习

> 想实现rem布局，主要用到的rem其实是一个单位。



### em和rem的区别

> 在布局中，除了px之外，还有两个常见的单位，em和rem

**em：** 相对于当前元素的字体大小→ `1em = 当前标签的font-size`

**rem：** 相对于根元素（html）的字体大小→ `1rem = html标签的font-size`

> 浏览器默认的font-size的大小为16px



### rem布局的基本原理

> 页面中的元素单位如果是rem，此时只需要控制html标签的font-size大小，即可统一控制页面中所有元素的大小变化了——》完成等比例缩放的效果

**rem布局的效果：**

- 屏幕越大，标签就越大
- 屏幕越小，标签就越小

**rem布局的基本原理：**

- 当屏幕越大，让html标签的font-size变大即可
- 当屏幕越小，让html标签的font-size变小即可

**之后rem布局的两个必要操作：**

- 元素的单位使用rem单位
- **动态根据当前屏幕宽度，自动改变html标签的font-size大小**



**问题：**怎么动态根据当前屏幕宽度，自动改变html标签的font-size大小呢？？

- js代码可以完成——》后面会学习
- css3中的新语法：媒体查询可以完成这件事——》现在学习



# 媒体查询

> 刚刚说了rem布局原理是：***动态根据当前屏幕宽度，自动改变html标签的font-size大小***
>
> 所以需要根据不同屏幕的宽度，改变样式。
>
> 可以通过css3中新增的媒体查询完成效果。
>

**媒体查询（Media Query）：**是CSS3新增的方法，媒体查询可以动态查询屏幕的宽度，根据不同的屏幕宽度设置样式是否生效！！



**需求：** 要求在不同屏幕下，盒子的大小和背景颜色进行变化？？？（如果要求：600~800屏幕宽度之间生效呢？）



**语法：** 

```css
@media screen and (条件) {
    选择器......
}
```



**作用：** 根据当前屏幕宽度是否满足条件——》控制其中的选择器是否生效

- 如果条件满足，选择器生效
- 如果条件不满足，选择器失效



**条件：**

|   条件    |       含义       |                     解释                     |
| :-------: | :--------------: | :------------------------------------------: |
| min-width | 样式生效的最小宽 | 当屏幕宽度大于等于该宽度时，选择器样式才生效 |
| max-width | 样式生效的最大宽 | 当屏幕宽度小于等于该宽度时，选择器样式才生效 |
|   width   |  样式生效的宽度  | 当屏幕宽度正好等于该宽度时，选择器样式才生效 |



**注意点：** 媒体查询仅仅只是控制选择器是否生效，不会提升选择器的优先级！！

- 媒体查询只能控制选择器是否生效，不能提升选择器优先级！！

  > 还是要判断选择器自己的优先级

- 媒体查询中可以同时设置多个条件，条件之间以and连接

- 媒体查询语法格式中空间不要省略



##### ヾ(๑╹◡╹)ﾉ" 通过媒体查询给盒子设置以下不同屏幕下的样式

```css
/* 1、屏幕宽度：200~400     盒子大小：100*100px  背景：红色 */
/* 2、屏幕宽度：400~600     盒子大小：200*200px  背景：绿色 */
/* 3、屏幕宽度：600~800     盒子大小：300*300px  背景：蓝色 */
/* 4、屏幕宽度：800~1000    盒子大小：400*400px  背景：黄色 */
/* 5、屏幕宽度：1000~正无穷  盒子大小：500*500px  背景：紫色 */
```



##### ------------------------



# rem布局的适配方案

> 知道rem布局的原理是：使用rem单位之后，动态根据当前屏幕宽度，自动改变html标签的font-size大小。
>
> 那具体如何改变html标签的font-size大小呢？？？



## 技术方案

> 两种方法都可以实现

**方案一：**

- less
- 媒体查询
- rem

**方案二：**

- js（后面会讲如何通过js源码实现，目前可以用现成的如：flexible.js）
- rem



## 具体适配操作（以方案一为例）



### 设计稿常见尺寸

|     设备     | 设计稿宽度 |
| :----------: | :--------: |
|  iPhone 4/5  |    640     |
| iPhone 6/7/8 |    750     |

**一般情况下，我们尽量适配大部分用户的情况，放弃放弃极端情况，牺牲部分效果，目前一般较多的是以750px为准**



### rem布局适配具体步骤

> rem布局适配的原理说白了，就是根据屏幕的大小，动态的改变html标签的font-size的大小，此时就可以配合媒体查询做到不同屏幕的适配。
>
> 注意点：rem布局进行的是元素**等比例缩放**



**需求：**当在750的设计图中量取div的宽高为400*400，此时要求使用rem适配 `375`、`640`、`750`  的屏幕



#### 适配的步骤

1. **根据设计图尺寸，先把px的单位转换成rem单位（根据设计图屏幕下html的font-size转换）**

   > `标签的px值 = rem单位*html标签的font-size`

   - **rem单位 == 标签的px值 / html标签的font-size**
   - 为了计算方便，一般我们会**针对于设计图的大小**自定义一个html标签的font-size的大小（比如：750设计图自定义50px）

2. **配合媒体查询，当屏幕越小的时候，需要让html标签的font-size的变小（等比例缩放）**

   - 保持比例相同：**比例 == 屏幕宽度 / 当前html标签的font-size**

     > 其实在上一步根据设计图自定义font-size的时候，比例已经确定了，后面直接计算即可

   - 推导：**当前html标签的font-size ==屏幕宽度/比例** 

   

因为要求页面是**等比例缩放**的，所以：

`屏幕1宽度/屏幕1html标签font-size` = `屏幕2宽度/屏幕2html标签font-size`

> 保证屏幕宽度与html标签font-size的比例相同，就可以轻松适配多个屏幕

![rem适配比例关系](mdImg/rem适配比例关系.png)

```css
/* 1、把px单位通过计算转换成rem单位（除以设计图尺寸屏幕中自定义的font-size：比如50px） */
div {
    width: 8rem;
    height: 8rem;
    background-color: pink;
}

/* ---------------------------------------------------------------------------- */
/* 2、保持比例相同，进行不同屏幕的适配 */
/* 
此时需要适配640px的屏幕的font-size
比例：15
font-size = 屏幕宽度/比例 = 375 / 15 = 25
*/
@media screen and (min-width: 375px) {
    html {
        font-size: 25px;
    }
}

/* 此时需要适配640px的屏幕的font-size
比例：15
屏幕的宽度/font-size =  15
font-size = 屏幕宽度 / 比例 = 640 / 15 = 42.66
*/
@media screen and (min-width:640px) {
    html {
        font-size: 42.66px;
    }
}

/* 此时这是适配750px的屏幕的font-size的设置
比例：屏幕的宽度 / font-size = 750 / 50 = 15
*/
@media screen and (min-width:750px) {
    html {
        font-size: 50px;
    }
}
```

**注意点：为了保证大屏的媒体查询不被覆盖，媒体查询一般从小屏往大了写。**



# 苏宁易购

> [苏宁](https://m.suning.com/)

## 项目搭建

- images文件夹

- less文件夹（之后使用less写项目）

  - 有index.less
  - 有base.less

- 新建html页面

  - 引入css文件

  - 移动端项目设置视口

    ```html
    <meta name="viewport" content="width=device-width, user-scalable=no, initial-scale=1.0, maximum-scale=1.0, minimum-scale=1.0">
    ```

  - 设置全局容器

## rem布局首先进行适配工作

**适配的步骤：**

1. 先适配设计图的屏幕大小（比如：750px），并且根据设计图屏幕大小定义一个html标签的font-size的大小（比如：50px），此时屏幕大小与font-size的比例为15
2. 因为是等比例缩放的，所以每一个适配的屏幕大小与font-size的比例都是相同的，所以各个屏幕大小除以比例就能得出font-size的大小

```less
// 苏宁官网中适配了：750 720 540 480 424 414 400 384 375 360 320
.adapter(@width) {
  @media screen and (min-width:@width) {
    html {
      // round(数值)：让这个数值四舍五入
      // round(数值，保留几位小数)
      font-size: round(@width/15,2);
    }
  }
}

.adapter(320px);
.adapter(360px);
.adapter(375px);
.adapter(384px);
.adapter(400px);
.adapter(414px);
.adapter(424px);
.adapter(480px);
.adapter(540px);
.adapter(720px);
.adapter(750px);

// 适配750的屏幕
// 定义设计图屏幕大小html的font-size值为50px，
// 比例为15
// @media screen and (min-width:750px) {
//   html {
//     font-size: 50px;
//   }
// }
```

## px2rem插件的使用

> 在写项目中，每一次都需要手动写式子把px转换成rem比较麻烦，此时可以使用vscode的插件，完成对应的效果

1. 安装插件 **px2rem** 

   ![px2rem的安装](mdImg/px2rem的安装.gif)

2. 每次写数字px之后，会有提示转换成rem，按下键回车即可

3. 插件中默认html的font-size的大小为16px，所以默认是除以16的如果需要更改，需要进行配置（如：设计如是750，html标签的font-size的大小为50px，此时应该除以50）

   > 在设置中搜索px2rem，然后直接修改设置即可，**注意设置完了之后需要重启才能生效！！**

   ![px2rem的设置](mdImg/px2rem的设置.gif)

