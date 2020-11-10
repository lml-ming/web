---
typora-copy-images-to: mdImg
---

# 学习目标

> - [x] 能够使用bootstrap的栅格系统
>
>   ```html
>   .col-取值1-取值2
>   
>   取值1：
>   	1、lg：大屏及以上屏幕生效
>   	2、md：中屏及以上屏幕生效
>   	3、sm：小屏及以上屏幕生效
>   	4、xs：超小屏及以上屏幕生效
>   
>   取值2：份数
>   ```
>
>   
>
> - [x] 能够使用bootstrap的基本样式
>
>   ```html
>   响应式容器：.container
>   
>   按钮：
>   	1、基本类：.btn
>   	2、颜色：.btn-danger .btn-warning .btn-success
>   ```
>
>   
>
> - [x] 能够使用bootstrap的响应式工具
>
>   ```html
>   响应式工具：隐藏相关
>   1、hidden：所有屏幕都隐藏
>   2、hidden-lg：只在大屏中隐藏
>   3、hidden-md：只在中屏中隐藏
>   4、hidden-sm：只在小屏中隐藏
>   5、hidden-xs：只在超小屏中隐藏
>   ```
>
>   
>
> - [ ] 能够完成微金所的头部
>
> - [ ] 能够完成微金所轮播图
>
> 。。。。。。



**理解上课的知识点......**



# bootstrap框架

> 在之前使用媒体查询的方式能手动写出响应式的简单效果，但是非常的麻烦，代码非常的多。在实际开发过程中，一般咱们会借助框架来完成响应式的开发，提高效率。
>
> 框架：顾名思义就是一套架构，它有一套比较完整的网页功能解决方案，而且控制权在框架本身，有预设的样式库、组件、插件等等。使用者要按照框架所规定的方式进行开发。
>
> Bootstrap，来自 Twitter，是目前很受欢迎的前端框架。Bootstrap 是基于 HTML、CSS、JAVASCRIPT 的，它简洁灵活，使得 Web 开发更加快捷。[前端流行框架排名](https://www.awesomes.cn/rank) 



## bootstrap的初体验

>  bootstrap框架现阶段可以简单的当做别人写好的代码。想要用，先去下载下来
>
>  [bootstrap中文网](http://www.bootcss.com/) 

**版本：**

- 2.x.x 停止维护

  > 做了很多兼容性处理，但是代码不够简洁，功能不够完善

- 3.x.x **目前使用较多**

  > 偏向于响应式开发布局，稳定。但是放弃了IE67的兼容，对IE8支持但是界面效果不友好

- 4.x.x 阶段 最新版，目前还不是很流行

**注意点：** Bootstrap中的  **js功能效果依赖于 jQuery** （ 第三方库, 后面有专门的课程讲解）



### 简单使用

> 说白了，bootstrap框架就是别人写好的代码，类似于：需要使用别人写好的css文件，只需要直接引入即可

- **引入文件**：`<link rel="stylesheet" href="bootstrap/css/bootstrap.css"> `

- bootstrap样式文件中有一些简单的**样式初始化**，所以引入之后不用再引入 `base.css` 文件

  > 但是bootstrap并没有将所有样式都重置，所有之后还需要自己手动写代码重置

- **学习bootstrap框架说白了就是学习类（学习每一个类的含义）**

  > 比如：fl——》左浮动、fr——》右浮动、clearfix——》清除浮动

  **以部分按钮为例：**

  |     类名     |             含义             |
  | :----------: | :--------------------------: |
  |     .btn     | 按钮的基础类（按钮必加的类） |
  | .btn-success |           绿色按钮           |
  | .btn-danger  |           红色按钮           |
  | .btn-primary |           深蓝按钮           |
  | .btn-default |           白色按钮           |



## bootstrap的布局容器

>之前给一个盒子设置响应式布局（不同屏幕下版心不同，移动端宽度100%），代码写了很多很麻烦
>
>但是使用bootstrap框架之后就非常方便，框架中响应式的框架已经写好的，使用的之后直接给标签加类即可

### 响应式布局容器（.container）

> **比较常用**

![container容器](mdImg/container容器.gif)

- 设置了该类的盒子，在不同屏幕下有不同的版心，到了移动端宽度为100%（之前写的效果一样）

  > 底层原理：就是之前写的媒体查询

- 设置了该类的盒子，左右有默认15px的padding

  > 写框架的作者觉得内容直接贴两边不好看，就设置了左右15px的padding

### 流式布局容器（.container-fluid）（了解）

> **了解即可**

![container-fluid容器](mdImg/container-fluid容器.gif)

- 设置了该类的盒子，宽度永远是100%
- 设置了该类的盒子，左右也有默认15px的padding

### 抵消父元素padding的类（.row）（了解）

> bootstrap中的布局容器默认都设置了左右15px的padding。
>
> 如果不需要这个效果，除了**可以通过选择器padding:0;直接覆盖**，还**可以通过.row类去掉**

- 设置了该类的子盒子，会抵消父元素左右15px的padding

  > 底层原理：通过margin为负值实现



##### ------------------------



## 栅格系统（重点）

> 在bootstrap中会把一行分成12列，通过对应的类名实现每个盒子宽度的动态变化
>
> 其实其中的原理大家一秒能懂

### 栅格系统的模拟

**需求：** 响应式容器中有两个盒子，只在大屏设备中宽度各占一半一行中显示，其他屏幕占满一行

- 使用之前的方法：浮动 + 宽度百分比 + 媒体查询 可以实现

---

- 其实在bootstrap中，也可以通过类完成以上效果（如：给两个盒子设置`.col-lg-6`）

  > 底层原理也是通过：浮动 + 宽度百分比 + 媒体查询 做到的。



### 栅格系统的介绍

> bootstrap中将一行分成了12份（12份更容易分配盒子的空间）

**底层原理：** **浮动（一行中显示） + 百分比（宽度均分） + 媒体查询（不同屏幕时才生效）**

**比如： **` .col-lg-6` 表示在大屏及以上屏幕生效，盒子宽度为一行的6/12——》50%；浮动在一行中显示

**语法：**

##### `.col-取值1-取值2`

| 取值1 |                 效果                 |
| :---: | :----------------------------------: |
|  lg   |         大屏及以上屏幕时生效         |
|  md   |         中屏及以上屏幕时生效         |
|  sm   |         小屏及以上屏幕时生效         |
|  xs   | 超小屏及以上屏幕生效（所有屏幕生效） |

**取值2：** 份数（0~12）

> 表示在一行中的宽度占几份

### 栅格系统的练习

```html
<!-- 
    需求:  响应式布局容器中一共有 12 个div
      如果是大屏幕设备, 每行放 6 个 div,  共两行
      如果是中屏设备,   每行放 4 个 div,  共三行
      如果是小屏设备,   每行放 3 个 div,  共四行
      如果是超小屏设备, 每行放 2 个 div,  共六行

    .col-取值1-取值2
      lg：大屏及以上生效
      md：中屏及以上生效
      sm：小屏及以上生效
      xs：所有屏幕都生效
  -->
```

##### ヾ(๑╹◡╹)ﾉ" 写微金所新手体验模块的响应式效果



## bootstrap全局样式阅读（了解）

> [bootstrap全局样式](https://v3.bootcss.com/css/)

**排版：对齐**

> 底层原理：就是一个text-align：left/center/right

|     类名     |     效果     |
| :----------: | :----------: |
|  .text-left  |  文本左对齐  |
| .text-center | 文本居中对齐 |
| .text-right  |  文本右对齐  |

**表格：基本（了解）**

|      类名      |                  效果                  |
| :------------: | :------------------------------------: |
|     .table     | 表格的基本样式（配合thead和tbody使用） |
| .table-striped |                隔行变色                |

**按钮：颜色**

> 按钮需要加上基本类 `.btn`

|         类名         |   效果   |
| :------------------: | :------: |
|     .btn-danger      | 红色按钮 |
|     .btn-success     | 绿色按钮 |
|     .btn-primary     | 深蓝按钮 |
|     .btn-default     | 白色按钮 |
|  .btn-info（了解）   | 浅蓝按钮 |
| .btn-warning（了解） | 黄色按钮 |
|  .btn-link（了解）   | 链接按钮 |

**按钮：尺寸**

> 按钮默认是中按钮

|  类名   |   效果   |
| :-----: | :------: |
| .btn-lg |  大按钮  |
| .btn-sm |  小按钮  |
| .btn-xs | 超小按钮 |

## 响应式工具介绍

> 在响应式布局中，有时候会设置不同屏幕下元素的显示或者隐藏

**需求：** 一个盒子大屏、中屏显示，小屏、超小屏隐藏

- 自己通过媒体查询实现

---

- 使用bootstrap中预定的.hidden相关类实现

**代码：**

> bootstrap中预定了一些类，可以控制盒子的显示或者隐藏

|    类名    |      效果      |
| :--------: | :------------: |
|  .hidden   | 所有屏幕都隐藏 |
| .hidden-xs | 只在超小屏隐藏 |
| .hidden-sm |  只在小屏隐藏  |
| .hidden-md |  只在中屏隐藏  |
| .hidden-lg |  只在大屏隐藏  |

##### ------------------------

## 组件介绍（了解）

> 组件比全局样式会多出一些功能出来，但是注意这些功能需要配合js文件一起使用

**组件：字体图标**

> 在bootstrap内部，内置了字体图标，只需要直接复制粘贴类名即可

**比如：**

```html
<span class="glyphicon glyphicon-heart"></span>
```

**组件：导航条**

> bootstrap中已经写好导航条的代码，使用的时候直接复制粘贴即可

```html
<nav class="navbar navbar-default">
  <div class="container-fluid">
    <!-- Brand and toggle get grouped for better mobile display -->
    <div class="navbar-header">
      <button type="button" class="navbar-toggle collapsed" data-toggle="collapse" data-target="#bs-example-navbar-collapse-1" aria-expanded="false">
        <span class="sr-only">Toggle navigation</span>
        <span class="icon-bar"></span>
        <span class="icon-bar"></span>
        <span class="icon-bar"></span>
      </button>
      <a class="navbar-brand" href="#">Brand</a>
    </div>

    <!-- Collect the nav links, forms, and other content for toggling -->
    <div class="collapse navbar-collapse" id="bs-example-navbar-collapse-1">
      <ul class="nav navbar-nav">
        <li class="active"><a href="#">Link <span class="sr-only">(current)</span></a></li>
        <li><a href="#">Link</a></li>
        <li class="dropdown">
          <a href="#" class="dropdown-toggle" data-toggle="dropdown" role="button" aria-haspopup="true" aria-expanded="false">Dropdown <span class="caret"></span></a>
          <ul class="dropdown-menu">
            <li><a href="#">Action</a></li>
            <li><a href="#">Another action</a></li>
            <li><a href="#">Something else here</a></li>
            <li role="separator" class="divider"></li>
            <li><a href="#">Separated link</a></li>
            <li role="separator" class="divider"></li>
            <li><a href="#">One more separated link</a></li>
          </ul>
        </li>
      </ul>
      <form class="navbar-form navbar-left">
        <div class="form-group">
          <input type="text" class="form-control" placeholder="Search">
        </div>
        <button type="submit" class="btn btn-default">Submit</button>
      </form>
      <ul class="nav navbar-nav navbar-right">
        <li><a href="#">Link</a></li>
        <li class="dropdown">
          <a href="#" class="dropdown-toggle" data-toggle="dropdown" role="button" aria-haspopup="true" aria-expanded="false">Dropdown <span class="caret"></span></a>
          <ul class="dropdown-menu">
            <li><a href="#">Action</a></li>
            <li><a href="#">Another action</a></li>
            <li><a href="#">Something else here</a></li>
            <li role="separator" class="divider"></li>
            <li><a href="#">Separated link</a></li>
          </ul>
        </li>
      </ul>
    </div><!-- /.navbar-collapse -->
  </div><!-- /.container-fluid -->
</nav>
```

**注意点：**

- 如果需要实现组件中如导航条的功能，需要引入bootstrap中的js文件才行
- bootstrap中的js需要依赖与jquery这个js文件的，所以需要一起引入jquery这个js文件才能生效！
- js文件通过script的src属性引入

```html
<script src="./jquery/jquery-1.12.4.js"></script>
<script src="./bootstrap/js/bootstrap.js"></script>
```



# 微金所项目

## 微金所项目搭建

- 新建项目文件夹

  - images文件夹：放项目需要的图片

  - css文件夹：放自己写的css文件

  - fonts文件夹：放自己项目的字体图标文件

    > 虽然bootstrap框架中内置了字体图标，但是实际开发中设计师会针对每个网页单独设计字体图标，使用方法和基础班一样

  - **lib文件夹**：放项目中框架相关的代码

    > lib文件夹中一般放框架（别人写好的代码）相关的代码

- 放入.ico图标

- 在 `index.html` 文件中引入相关文件

  - 引入.ico图标

  - 引入字体图标文件

  - 引入框架的css文件和js文件和jquery文件（因为bootstrap框架中的js依赖jquery）

    > 知道引入js之后能生效即可，js之后会详细去说

  - 引入自己写的css文件

## 微金所模块划分

![](mdImg/微金所模块划分.png)



## 响应式项目的思路

1. 先看有没有响应式版心（版心会不会跟随屏幕大小变化而变化）

   > 如果有响应式版心，设置 `.container` 即可

2. 在响应式版心中分配每一个盒子的空间

   > 利用栅格系统进行空间的分配

3. 设置整体大模块是否有显示与隐藏，直接给大模块设置hidden相关属性即可



## bootstrap导航条的改写（不做要求）

> 在bootstrap文档的组件中，有写好的导航条的代码，使用的时候直接复制改写即可。
>
> 因为现在还没学js等相关内容，所以对于以下改写的内容同学们可以直接复制改好的代码，现在学习的重点在于之后样式的覆盖（如果能理解是一种进阶）

**改写前先把不需要的属性和标签删除：**

> 以下属性和标签，在改写过程中可以直接删除，因为是给盲人设备使用的，删除之后便于理解结构（不删也可以）

- `aria-` 开头的属性，该属性可以直接删除
- `role` 属性，该属性可以直接删除
- 有 `sr-only` 类的标签，该标签可以直接删除 

```html
<nav class="navbar navbar-default">
    <!-- 有版心的布局容器 -->
    <div class="container">
        <!-- 小屏设备显示的左边大标题和右边切换按钮的组合 -->
        <div class="navbar-header">
            <!-- 小屏下右边的按钮 -->
            <button type="button" class="navbar-toggle collapsed" data-toggle="collapse"
                    data-target="#bs-example-navbar-collapse-1">
                <span class="icon-bar"></span>
                <span class="icon-bar"></span>
                <span class="icon-bar"></span>
            </button>
            <!-- 左边的大标题 -->
            <a class="navbar-brand" href="#">左边的大标题</a>
        </div>
<!--------------------------------------------------------------------------------------->
        <!-- 用于切换显示内容的结构 -->
        <div class="collapse navbar-collapse" id="bs-example-navbar-collapse-1">
            <!-- 左侧的导航 -->
            <ul class="nav navbar-nav">
                <li class="active"><a href="#">我要投资</a></li>
                <li><a href="#">我要借贷</a></li>
                <li><a href="#">平台介绍</a></li>
                <li><a href="#">新手专区</a></li>
                <li><a href="#">最新动态</a></li>
                <li><a href="#">微平台</a></li>
            </ul>
            <!-- 右侧的导航 -->
            <ul class="nav navbar-nav navbar-right">
                <li><a href="#">个人中心</a></li>
            </ul>
        </div>
    </div>
</nav>
```

## bootstrap标签页（tab栏）的改写

> 在bootstrap文本的JavaScript插件中，有写好的标签页（tab栏）的代码，使用的时候直接复制改写即可。

**改写前先把不需要的属性和标签删除：**

- `aria-` 开头的属性，该属性可以直接删除
- `role` 属性，该属性可以直接删除
- 有 `sr-only` 类的标签，该标签可以直接删除 

```html
<!-- 
    1、先去除没用的标签和属性
        1、aria-开头的属性，属性都删除
        2、role属性，该属性删除
        3、有sr-only类的标签，该标签直接删除

    2、bootstrap中，data-开头的属性，是用于添加js功能的，不要删除

    3、通过id属性将导航的按钮和面板绑定起来，所以id属性需要一一对应才行

    原理：点击某一个导航按钮时，让对应的导航面板显示，其他面板都隐藏即可！！！
-->
<div>
    <!-- 用于点击切换的按钮 -->
    <ul class="nav nav-tabs" role="tablist">
        <li class="active"><a href="#product01" data-toggle="tab">特别推荐</a></li>
        <li><a href="#product02" data-toggle="tab">微平台1</a></li>
        <li><a href="#product03" data-toggle="tab">微平台2</a></li>
        <li><a href="#product04" data-toggle="tab">微平台3</a></li>
        <li><a href="#product05" data-toggle="tab">微平台4</a></li>
        <li><a href="#product06" data-toggle="tab">微平台5</a></li>
        <li><a href="#product07" data-toggle="tab">微平台6</a></li>
    </ul>

    <!-- 用于点击切换的面板 -->
    <div class="tab-content">
        <div class="tab-pane active" id="product01">111</div>
        <div class="tab-pane" id="product02">222</div>
        <div class="tab-pane" id="product03">333</div>
        <div class="tab-pane" id="product04">444</div>
        <div class="tab-pane" id="product05">555</div>
        <div class="tab-pane" id="product06">666</div>
        <div class="tab-pane" id="product07">777</div>
    </div>
</div>
```

