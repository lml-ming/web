---
typora-copy-images-to: mdImg
---

# 学习目标

> - [x] 能够跟随课程写出品优购shortcut（快捷菜单）
>
> - [x] 能够说出实际开发logo我们需要做哪些优化
>
>   - logo盒子需要有一个h1
>   - h1标签里面一般放a标签
>   - a标签里面放文字
>   - 不需要用户看到字，需要隐藏文字
>     - font-size：0
>     - text-indent:-9999px; overflow:hidden
>
> - [x] 能够跟随课程写出品优购首页header部分
>
> - [x] 能够跟随课程写出品优购首页推荐模块
>
> - [x] 能够写出3中常见的鼠标样式（cursor）
>
>   - 默认的箭头：default
>   - 小手：pointer
>   - 选择文本的工字型：text
>   - 十字光标：move
>
> - [ ] 能够用CSS写出三角形
>
>   
>
>
> 。。。。。。



**理解上课的知识点......**



# 品优购的布局

## shortcut模块

![image-20200830084012707](mdImg/image-20200830084012707.png)

## header模块

![image-20200830090641431](mdImg/image-20200830090641431.png)



### logo部分的seo优化

> 一般网页的logo需要考虑到seo的优化，实际的做法是会使用h1标签包裹

- **logo** 部分中先需要一个 **h1**标签包裹，提升seo
- 一般logo部分点击能跳转，需要h1中包裹一个a标签，并且a标签的范围需要占满h1标签
- 给a标签设置背景图片
- 为了给seo提供文字类信息，还需要给a中添加文字，但是又不需要用户看到
  - 方法一：设置`text-indent`将文字移出盒子（`text-indent: -999px`），然后配合`overflow:hidden` 溢出隐藏
  - 方法二：直接设置`font-size:0` 

## nav模块

![image-20200830102303083](mdImg/image-20200830102303083.png)





## main模块

![image-20200830105031990](mdImg/image-20200830105031990.png)



## recommend模块

![image-20200830115516921](mdImg/image-20200830115516921.png)



# 三种鼠标（光标）常见的样式

> 通过cursor属性来设置鼠标移入盒子中的样式

取值：

- **default** ：光标为一个箭头（默认样式） 
- **pointer** ：光标为一只小手（a标签的默认样式）
- **text** ：此光标指示文本 
- **move**：显示十字光标（表示可移动的效果）



# 使用css写出一个三角形

> 有时候需要在页面中展示一个三角形，并且要求只使用css代码，不用图片或者字体图标，怎么实现？

**例如：**

![jd](mdImg/jd.png)

**可以通过边框来实现：**

- 设置一个盒子
- 设置四周不同颜色的边框
- 盒子的宽高设置为0

![](mdImg/css三角形.png)

- 此时每一个方向的边框就是一个三角形了，选择一个之后让其他边框的颜色为**全透明**即可

## 背景透明

> 设置透明的方法

- **rgba（0,0,0,0）**
- **transparent**：表示全透明的颜色



**代码：**

```css
/* ------------------------------------方法一------------------------------------ */
div {
    width: 0;
    height: 0;
    border-left: 100px solid purple;
    border-bottom: 100px solid transparent;
    border-right: 100px solid transparent;
    border-top: 100px solid transparent;
}
/* -----------------------------------方法二--------------------------------------- */
div {
    width: 0px;
    height: 0px;
    border-width: 100px;
    border-style: solid;
    border-color: transparent transparent transparent purple;
}
```



# 拓展

## 属性选择器的一些匹配规则（知道即可）

> 可以通过标签的属性选择标签

```html
<style>
    /* 让带有class属性的div变成绿色*/
    div[class] {
        color: green;
    }
    /*让class属性值为sellmeng的div变红*/
    div[class="sellmeng"] {
        color: red;
    }
    /*让class属性值以very开头的div变粉色*/
    div[class^="very"] {
        color: pink;
    }
    /*让class属性值以meng结尾的div变蓝*/
    div[class$="meng"] {
        color: blue
    }
    /*让class属性值中有meng的div变黄*/
    div[class*="meng"] {
        color: yellow;
    }
</style> 
-------------------------------------------------
<body>
  <div class="sellmeng">小可爱</div>
  <div class="mengmengda">大可爱</div>
  <div class="veryclever">燕燕</div>
  <div class="verymeng">怡口莲</div>
  <div>棠哥</div>
</body>
```

- **E[class]**

  选择带有class属性的E元素。 

  如：选中**带有class属性**的元素为绿色

- **E[class="attr"]**

  选择带有class属性，并且属性值是attr的E元素

  如：选中**class属性值为sellmeng**的元素为黄色

- **E[class^="attr"]**

  选择带有class属性，并且属性值是 **以attr开头** 的E元素

  如：选中**class属性值以very开头**的元素为粉色

- **E[class$="attr"]**

  选择带有class属性，并且属性值是 **以attr结尾** 的E元素

  如：选中**class属性值以meng结尾**的元素为蓝色

- **E[class*="attr"]**

  选择带有class属性，并且属性值是 **包含attr** 的E元素

  如：选中**class属性值里包含meng**的元素为紫色

**常见的情况：**

选取input标签的不同形态

> 单独选中文本框或者按钮

**注意点：**

元素与[]之间不能有空格！！！
