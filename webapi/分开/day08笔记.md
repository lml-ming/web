---
typora-copy-images-to: mdImg
---

# 学习目标

> - [ ] 能够使用swiper插件完成移动端轮播图的制作
> - [ ] 能够写出页面滚动事件
> - [ ] 能够写出页面被卷去头部的代码
> - [ ] 能够获取浏览器可视区的宽度和高度
> - [ ] 能够完成仿腾讯固定导航案例
> - [ ] 能够说出移动端touch三个事件
> - [ ] 能够利用classList操作类名
> 
>。。。。。。



**理解上课的知识点......**



# 通过swiper插件完成轮播图

> 实际开发的时候可以选择使用轮播图插件完成轮播图。会更加方便和快捷，并且功能也很强大，还兼容移动端。

[swiper官网](https://www.swiper.com.cn/)

**使用流程：**

- 在官网下载

- 按照官网的教程使用

  - 引入：css、js

  - 设置基本html结构

    ```html
    <div class="swiper-container">
      <div class="swiper-wrapper">
        <div class="swiper-slide">
          <a href="#">
            <img src="./images/1.jpg" alt="">
          </a>
        </div>
        <div class="swiper-slide">
          <a href="#">
            <img src="./images/2.jpg" alt="">
          </a>
        </div>
        <div class="swiper-slide">
          <a href="#">
            <img src="./images/3.jpg" alt="">
          </a>
        </div>
      </div>
      <!-- 如果需要分页器 -->
      <div class="swiper-pagination"></div>
    
      <!-- 如果需要导航按钮 -->
      <div class="swiper-button-prev"></div>
      <div class="swiper-button-next"></div>
    
    </div>
    ```

  - 设置js初始化

    ```js
    var mySwiper = new Swiper ('.swiper-container', {
      loop: true, // 循环模式选项
    
      // 如果需要分页器
      pagination: {
        el: '.swiper-pagination',
      },
    
      // 如果需要前进后退按钮
      navigation: {
        nextEl: '.swiper-button-next',
        prevEl: '.swiper-button-prev',
      },
    
    })  
    ```

- 按照API文档介绍常用属性

  ```js
  var mySwiper = new Swiper ('.swiper-container', {
  
    // direction：设置滑动的方向 可设置为水平方向切换(horizontal)或垂直方向切换(vertical)。
    // direction : 'horizontal',
  
    // 滑动的速度
    // speed: 2000,
  
    // 循环模式选项 false表示无缝轮播，true表示无缝轮播
    loop: true, 
  
    // 自动轮播
    // autoplay:true,//等同于以下设置
    // autoplay: {
    //   delay: 1000,
    //   // 切换到最后一张是否会停下：true表示会停下（如果loop为true无效），false表示不停下
    //   stopOnLastSlide: true,
    //   // 用户操作后是否禁用自动轮播：true表示会禁用自动轮播，false表示不会禁用自动轮播
    //   disableOnInteraction: false,
    // },
  
    // effect：切换的效果  默认为"slide"（位移切换），可设置为'slide'（普通切换、默认）,"fade"（淡入）"cube"（方块）"coverflow"（3d流）"flip"（3d翻转）。
    effect:'slide',
  
  
    // 如果需要分页器
    pagination: {
      el: '.swiper-pagination',
      // clickable：设置点击分页器是否可以切换
      clickable:true
    },
  
    // 如果需要前进后退按钮
    navigation: {
      nextEl: '.swiper-button-next',
      prevEl: '.swiper-button-prev',
    },
  
  }) 
  ```

  

# 三大家族

> 在DOM操作中有三大系列的属性比较常用，形象的称之为三大家族，三大系列
>
> 同学们需要记忆三大家族中常用的属性即可。

## offset系列

- **offsetWidth和offsetHeight：获取元素的实际大小**

  > content + padding + border

- offsetParent：获取元素最近的有定位的祖先元素

  - 如果祖先元素中有定位的元素——》找到最近的有定位的祖先元素
  - 如果祖先元素中没有定位的元素——》找到body

- **offsetLeft和offsetTop：获取元素距离offsetParent左边/上边的距离**



## scroll系列

> 通过scroll系列的相关属性可以用于获取内容区域的宽高、滚去的距离

- scrollWidth和scrollHeight：获取元素内容区域的宽高

  > 包含元素的填充（padding），不包含边框（border）

  **注意点：**如果盒子内容超出了，此时内容区域大小比盒子实际大小更大！！

- scrollLeft和**scrollTop**：获取元素内容在水平和垂直滚去的距离

<img src="mdImg/image-20201009195631543.png" alt="image-20201009195631543" style="zoom:80%;" />



**如果需要在滚动的时候实时拿到滚去的距离，通过onscroll事件即可：**

```js
var box = doucment.getElementById(“box”);
box.onscroll = function(){
	//事件处理程序
}
```

##### ------------------------

**需求：如何实时获取到页面滚去的距离？**

> 实际开发的时候不会单独获取一个盒子滚去的距离，一般获取的都是整个页面的scrollTop

- 一般推荐给window注册滚动事件

  >  老版本ie不支持document注册滚动事件，但是新老版本都支持给window注册

- 获取页面滚去的距离比较特殊，统一使用window.pageYOffset和window.pageXOffset获取

  > - window的scrollTop不支持
  >
  > - document的scrollTop不支持
  >
  > - 早期：获取html的scrollTop是支持的
  >
  > - 现在：统一使用window.pageYOffset和window.pageXOffset是支持的

```javascript
window.onscroll = function () {
    console.log( window.pageYOffset );
    console.log( window.pageXOffset );
}
```



##### ヾ(๑╹◡╹)ﾉ" 仿腾讯固定导航案例

> 当页面滚动到一定距离之后设置固定定位

- 给window注册onscroll事件
- 滚动的时候监测滚去的距离
- 当滚去的距离比header的高度更大，此时让nav固定定位
- 当滚去的距离比header的高度更小，此时让nav取消固定定位
- 当nav有固定定位的瞬间，脱标了，下面的main会跳上去，此时需要给main设置margin-top解决
- 同理，当高度没超过header的高度，则去掉多余的margin-top



## client系列

> 通过client系列的相关属性可以用于获取元素可视区域的宽高大小

- **clientWidth和clientHeight：获取元素可视区域的大小**

  > 包含元素的填充（padding），不包含边框（border）

  **注意点：** 和scroll系列不同，scroll系列是包含内容的超出部分，但是client只是当前可视区域

- clientLeft和clientTop：（没用）获取元素左边框和上边框的宽度

 ![client1](mdImg/client1-1602230074062.png)

> 三大家族对比

 ![client](mdImg/client-1602230074062.png)





**一般获取整个网页的可视窗口更常见，如果需要检测浏览器窗口变化，可以使用onresize事件**

> 获取浏览器窗口的大小，推荐使用window.innerWidth和window.innerHeight

```javascript
window.onresize = function () {
    console.log( '哈哈哈' );
    //  获取窗口的宽高
    // console.log( document.documentElement.clientWidth );
    // console.log( document.documentElement.clientHeight );

    // 现在的做法：
    console.log( window.innerWidth );
    console.log( window.innerHeight );
}
```



##### ヾ(๑╹◡╹)ﾉ" 使用client系列完成rem布局的适配：当在750的设计图中量取div的宽高为400*400，此时要求使用rem适配 `375`、`640`、`750`  的屏幕

> 之前是通过媒体查询设置不同屏幕宽度下的html标签的font-size，此时可以直接通过js设置即可

- 把标签的单位转换成rem

  > 一般750屏幕下html标签的font-size给50

- 设置不同屏幕下的html标签的font-size，需要保证等比例缩放

  > 比例===屏幕宽度/font-size ===750/50===15，
  >
  > 只需要拿：适配屏幕的宽度/比例——》html标签的font-size

- 在页面加载前，写js代码，计算并且设置当前屏幕宽度下，html的font-size应该为多少

  > 比之前媒体查询好的地方在于：媒体查询只适配一段的效果，而js可以每个屏幕都能适配

- 设置js适配的范围，设置屏幕计算的最大和最小值

- 此时会发现，只有窗口改变了才会触发，需要窗口没触发之前，先执行一遍适配的代码

##### ------------------------

# 移动端

## 完成京东移动端的动态效果

### 使用swiper完成轮播图

**banner部分的轮播图：**

- 引入swiper的css和js

- 设置swiper初始化代码

  > 为了页面中的轮播图初始化设置不会重复，因此选中初始化轮播图时，最好通过特定的类选中。

- 需要按照swiper使用说明，套用结构改标签

  > 标签可改，但是类名务必保证一致

**info部分的轮播图：**

- 引入swiper的css和js

- 设置swiper初始化代码

  > 为了页面中的轮播图初始化设置不会重复，因此选中初始化轮播图时，最好通过特定的类选中。

- 需要按照swiper使用说明，套用结构改标签

  > 标签可改，但是类名务必保证一致
  
- 如果需要禁止info部分滑动

  > 只需要在最外层的容器上增加class="swiper-no-swiping"



### 通过js动态设置秒杀产品部分的宽度

> 实际开发中可能会添加多个商品，此时固定宽度就不合适了——》需要通过js动态设置

- 找对象
- 给ul设置 `li的宽度*li的个数的宽度` 



**问题：之前是通过css设置的内容区域滚动在移动端中存在滚动条很丑，实际移动端项目中是没有滚动条**

- 不要滚动条，此时不能通过css的 `overflow:auto` 完成滚动效果
- 类似于拖拽案例，当手指在屏幕滑动的时候，内容区域跟着移动跑就行。但是之前拖拽案例是在pc端通过鼠标事件完成的，移动端没有鼠标怎么办？？
  - 之前
    - 鼠标按下，元素开始跟着跑
    - 鼠标移动，实时改变元素的位置
    - 鼠标弹起，不再改变元素的位置
  - 移动端：没关系，移动端有专门的touch事件完成类似的效果。
    - 开始触摸，元素开始跟着跑
    - 正在摸，实时改变元素的位置
    - 结束触摸，不再改变元素的位置



## 移动端touch事件

> 通过移动端的touch事件，可以在移动端中完成触摸区域滚动等效果

**移动端中有4个专属的触摸相关的事件：**

- touchstart：开始触摸事件
- touchmove：移动触摸事件（移动时多次触发）
- touchend：结束触摸事件
- touchcancel：取消触摸事件（系统取消的情况：比如来电话了）



**完全区域滚动的原理很简单，只需要知道手指滑动的距离，设置给盒子即可。那么如何知道手指的位置？？？——》事件对象**

> 每个触摸事件被触发后，会生成一个事件对象event对象，event对象中`changedTouches`会记录手指滑动的信息。

**事件对象中有这几个对象表示手指：**

- e.touches：当前屏幕上的总手指
- e.targetTouches：当前元素上的总手指
- e.changedTouches：状态改变的总手指（比如：从屏幕上离开）

**注意点：单指触摸在touchstart、touchmove中以上三个对象一样，但是在touchend离开屏幕后，只能通过changedTouches获取到变化的手指（手指从在屏幕上到不在屏幕上产生的变化，浏览器储存起来了）。**



**拿到每一个touch对象中每一个手指对象既可以获取到相关的位置都有包含以下位置信息：**

- screenX和screenY：触摸点相当于屏幕的位置

- clientX和clientY：触摸点相对于浏览器窗口的位置

- pageX和pageY：触摸点相对于页面的位置

  > 包含滚动条的部分

##### ------------------------



##### ヾ(๑╹◡╹)ﾉ" 实现区域滚动效果

**结构：在父元素中有一个宽度超出的子元素，让子元素在移动端中触摸实现区域滚动效果**

```html
<style>
  * {
    margin: 0;
    padding: 0;
  }

  .father {
    width: 100px;
    height: 100px;
    border: 10px solid #000;
    margin: 100px auto;
    position: relative;
  }

  .son {
    width: 400px;
    height: 100px;
    background-color: pink;
    user-select: none;
    display: flex;
    position: absolute;
  }

  .son .item {
    flex: 1;
    border-right: 1px solid orange;
    line-height: 100px;
    text-align: center;
    font-size: 16px;
  }

</style>

<div class="father">
  <div class="son">
    <div class="item">图片1</div>
    <div class="item">图片2</div>
    <div class="item">图片3</div>
    <div class="item">图片4</div>
  </div>
</div>
```



**思路：在触摸移动过程中，手指在屏幕移动了多少，让子元素在开始基础上继续跟着移动多少即可。**

- 手指移动了多少？？
  - 开始触摸的位置 - 手指移动中的位置
- 子元素的位置：开始的位置 + 需要变化的位置



## 通过iscroll实现区域滚动

> 区域滚动很常见，所以有一个插件iscroll可以使用

**使用流程：**

- 引入iscroll.js

- 按照[文档配置](http://caibaojian.com/iscroll-5/)即可

  ```js
  // iscroll必须满足的结构：两个盒子，子盒子超出父盒子
  new IScroll('父容器的选择器',{
      // 水平方向是否可以滚动
      scrollX:true,
      // 垂直方向是否可以滚动
      scrollY: false
  }) 
  ```

##### ヾ(๑╹◡╹)ﾉ" 使用iscroll完成京东实现区域滚动效果



### 设置倒计时功能（作业）

- 计算倒计时中的时分秒
- 找到需要设置的span对象，设置时分秒
- 通过定时器设置时间
- 需要考虑到如果剩余时间为负数，此时需要结束定时器，不用继续设置时间了



# 类名操作

> 之前：通过className设置类名
>
> 缺点：如果元素本身有类名，需要拼接，麻烦
>
> 推荐：classList是一个集合，会存储某个元素上所有的类名，使用classList来替代className操作class类

**每一个元素都增加了一个属性：classList，并且classList上还有4个方法：**

- classList.add()：往元素上**添加类名**，不会覆盖原有类名
- classList.remove()：往元素上**移除类名**，不会影响其他
- classList.contains()：判断元素的类名中是否**包含此类名**
- classList.toggle()：**切换类名**，原本无就添加，原本无就删除



##### ヾ(๑╹◡╹)ﾉ" 将之前的登录框按照修改成可以拖拽的效果（作业）

- 点击之后通过js让登录框在页面中是居中的

  - 设置登录框的left值为：`（浏览器可视区宽度 - 登录框的宽度）/ 2`
  - 设置登录框的top值为：`（浏览器可视区高度 - 登录框的高度）/ 2`

- 拖拽效果基本实现

  - 给title注册鼠标按下事件，按下后注册鼠标移动事件

  - 给整个网页注册鼠标弹起事件，弹起后清除鼠标的移动事件

    > 如果给title注册弹起事件，很可能移动过程中鼠标超出了title，此时没法移出

    - 在鼠标移动过程中，将鼠标的坐标设置给login的left和top

- 解决按下的时候盒子瞬间移动的问题

  - 先求出按下的时候，鼠标在盒子中的x和y

    > 鼠标相对于页面的距离 - 盒子相对于页面的距离

    - 注意点：直接拿title的left和top的offsetLeft/offsetTop是0，因为拿最近的有定位的父元素距离
    - 解决方案：可以直接拿login的offsetLeft/offsetTop，距离左边和上边的距离是一样的。

  - 在具体设置login的left和top时，将去上面算出的x和y

- 解决login部分拖拽的范围问题，需要把拖拽的范围限定在可视区范围内

  - 设置login水平的移动范围：0 ~ 可视区宽度 - login宽度
  - 设置login垂直的移动范围：0 ~ 可视区高度 - login高度
  - 防止关闭按钮被遮住
    - 水平方向最大值少21px
    - 垂直方向最小值大21px