---
typora-copy-images-to: mdImg
---

# 学习目标

> - [x] 能够说出缓动动画的实现原理
>
>   - 效果：先快后慢——》通过改变每一步的距离
>     - 先每一步比较大，后每一步比较小
>   - 公式
>     - step = 剩余的距离 / 10
>     - step = ( target - current ) / 10
>
> - [x] 能够封装缓动动画函数
>
>   ```js
>   // js动画函数的封装
>   // 希望最终得到的函数——》可以让不同的元素可以动画到不同的位置
>   //                         element           target
>   function animate(element,target) {
>   
>     // 在开启新的定时器之前，需要上一个定时器清除
>     clearInterval(element.timeId);
>     console.log( element.timeId );
>   
>     // 通过定时器，让div可以一直不停的往前走
>     element.timeId = setInterval(function () {
>   
>       // offsetLeft获取到的位置是四舍五入
>       var current = element.offsetLeft;
>   
>       // 把每一步距离变成变量表示
>       var step = ( target - current ) / 10;
>   
>       // 如果是0.4的情况，需要让step向上取整，最终走1px
>       // 如果是-0.9的情况，需要让step向下取整，最终走-1px
>       // step = Math.ceil(step);
>       step = step > 0 ? Math.ceil(step) : Math.floor(step);
>   
>       console.log( current,step );
>   
>       current += step;
>       element.style.left = current + 'px';
>   
>   
>       // 需要判断当前的位置是不是已经到了400——》如果已经到了目标位置，此时就不需要往前跑，清除定时器
>       if ( current === target ) {
>         clearInterval(element.timeId);
>       }
>     },16)
>   
>   }
>   ```
>
>   
>
> - [x] 能够说出制作网页轮播图的思路过程
>
>   - 整体有box，box的大小和一张图片的大小保持一致，设置溢出隐藏
>   - box的里面有ul，ul要足够长让li可以一行放的下
>   - 让轮播图动起来，让ul改变left的值
>   - 通过animate()函数进行移动
>
> - [x] 能够实现轮播图效果（小圆点）
>
> - [x] 能够实现轮播图效果（左右箭头）
>
> - [x] 能够实现轮播图效果（无缝滚动）
>
> - [x] 能够实现轮播图效果（完整版）
>
> - [ ] 
>
> - [ ] 能够使用swiper插件完成移动端轮播图的制作
>
> - [ ] 能够写出页面滚动事件
>
> - [ ] 能够写出页面被卷去头部的代码
>
> 。。。。。。



**理解上课的知识点......**



# js缓动动画封装

> 之前写的动画函数确实能让盒子移动，但是每一步都是相同距离，其实此时是匀速动画
>
> 缓动动画的效果：让元素的运动慢慢的停下来——》开始走的距离大，后面走的距离越来越小

**实现公式：先快再慢，慢慢停下来的变速动画——》每次移动的距离减小即可 **

- **每一步的距离 === 剩下距离 / 10**
- **每一步的距离 === （ 目标距离 - 当前距离 ） / 10**
- **每一步的距离 === （ target - current） / 10**



**需求：将刚刚的匀速动画按照上面的公式，改写成缓动动画的效果**

- 每一步移动的距离不是固定的，需要先把每一步移动的距离抽离成变量step表示
- 将step设置为 （ target - current ） / 10



**优化1：发现此时移动的距离并没有到达准确的400，而是误差零点几，需要到达准确的400怎么解决？？？**

> 因为offsetLeft获取到的当前元素的距离是默认四舍五入到整数的，因此根本拿不到除不尽的小数部分，最终无法移动到准确的值

- 发现因为始终没有到达目标位置，结束条件定时器一直在执行，此时需要将step的值算到零点几的时候直接向上取整（ Math.ceil() ）到整数px，此时就解决小数时卡住的问题。

**优化2：优化1过后，到400或者到800没问题，但是从800——》400有问题，同样无法准确到达，如何解决？？？**

> 因为从800——》400此时距离为负数，负数在向上取整的时候取大的那一个，导致每次都无法往左减去小数部分

- **分情况而定：**
  - 判断：如果step为正数，此时step向上取整（ Math.ceil() ）设置
  - 判断：如果step为负数，此时step向下取整（ Math.floor() ）设置



##### ヾ(๑╹◡╹)ﾉ" 使用刚刚封装好的缓动动画函数，完成筋斗云案例

> 封装好的动画函数为了方便后续多次使用，可以抽取出一个单独的.js文件方便复用

![筋斗云案例](mdImg/筋斗云案例.gif)

- 给所有的li注册鼠标移入事件，移入之后让cloud通过动画移动到当前li同位置
- 给所有的li注册鼠标移出事件，移出之后，让cloud通过动画移动固定位置
- 给所有的li注册点击事件，点击之后，让cloud的固定位置设置为当前li的位置



# 轮播图



## 简单小圆点轮播图

### 1、完成静态结构

- 整体box
  - ul宽度为li宽度之和
    - li里面放a
      - a里面放img
  - ol表示点击的小圆点列表
    - li表示每一个小圆点

---



### 2、小圆点点击变红

> 同一时间只需要一个li变红，其他的不变红——》排他

- 找到所有的小圆点，注册点击事件
- 点击之后让自己添加active类
- 同时只需要一个变红——》排他：自己加类前先让所有的小圆点都去除类

---



### 3、点击小圆点，让ul移动

- 点击小圆点时，让ul往左移动：`下标*图片宽度` 的距离

  > 此时可以把小圆点的下标提前储存在对象本身去，并且保证ul是有定位的

- 让li移动有动画效果，引入之前写的动画函数

---



##### ------------------------

## 左右按钮轮播图

### 1、完成左右按钮静态结构

---



### 2、给左右箭头添加点击移动功能

- 给左右箭头注册点击事件

- 将当前显示li的下标用全局变量储存起来

  > 点击之后需要知道应该切换到哪一张？——》把当前的下标用全局变量储存起来
  >
  > 全局变量的原因是需要左右箭头点击后都能操作到这个变量

- 点击按钮之后要修改变量储存的下标

  - 点左箭头让变量储存的下标--
  - 点右箭头往变量储存的下标++

- 点击后改变变量储存下标的同时，需要让ul进行移动

- 不能让变量储存的下标无限变化，需要限定下标的范围，超出范围则结束立即结束时间处理函数不移动



##### ------------------------

## 无缝滚动轮播图

> 实际网页中的轮播图应该可以无限滚动的

- 去掉范围，右击到最后一张时，再右击需要瞬间切换到第一张

  > 要瞬间切换过来，不能使用动画

- 但是此时会直接从0——》1，0这一项一闪而过，需要让用户看到0这一张怎么办？

  - 此时可以在最后**添加假图片0到最后去**，这样用户可以看到0，并且有无限滚动的效果

- 同理，给左击到第一张的时候，再左击需要瞬间切换到最后一张（假图片）



## 轮播图完整版

### 1、同步小圆点的高亮

> 通过count的变化设置小圆点高亮即可

- 在左右按钮的点击事件最后（count处理完之后），再根据count让小圆点高亮

- 排他

  > 先都不亮，再设置当前变亮

- 右箭头点击时，当count到了假图片的时候会出问题，报错

  > 因为count的个数其实比小圆点个数差一，最后一张的时候不能依据count设置谁高亮了

  - 用户是把最后一张当做第一张的，所以当展示的是最后一张，直接让第一个小圆点亮即可



### 2、轮播图自动轮播功能

> 当用户没有点击时，可以自动滚动

- 设置定时器，隔一段时间，调用right的onclick事件即可

- 当用户鼠标移入box时，需要清除定时器不用——》方便用户购买产品

- 当用户鼠标移出box时，需要继续添加定时器——》继续轮播图

  > 注意点：timeId需要保证是全局变量，在移入的时候才能清除



### 3、一些bug的解决

- 用户通过点击小圆点到指定位置后，此时点右箭头去下一张，此时会滚动多张
  > 因为点击小圆点时没有同步count，此时点击右箭头去下一张还是按照原来的情况滚动

  - 只要在每个小原点点击的同时，同步count值即可

- 淘宝也存在的问题：当到假图片右击右箭头展示到第一张时，用户以为是真图片，此时点击第一个小圆点会露馅

  > 右箭头已经处理过，但是小圆点点击的时候没有处理假图片的过去

  - 如果发现小圆点点击时，当前count为假图片时，此时在执行动画之前，直接让ul的位置瞬间切换到第一张的位置即可



##### ヾ(๑╹◡╹)ﾉ" 把轮播图完整版整体梳理一遍

---

##### ------------------------

# 通过swiper插件完成轮播图

> 实际开发的时候可以选择使用轮播图插件完成轮播图。会更加方便和快捷，并且功能也很强大，还兼容移动端。

[swiper官网](https://www.swiper.com.cn/)

**使用流程：**

- 在官网下载

- 按照官网的教程使用

  - 引入：css、js

  - 基本配置

    ```js
    var mySwiper = new Swiper ('.swiper-container', {
      // direction: 'vertical', // 垂直切换选项
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
    
      // 如果需要滚动条
      // scrollbar: {
      //   el: '.swiper-scrollbar',
      // },
    })  
    ```

- 按照API文档介绍常用属性

  



# 三大家族

## offset系列

> offset系列用于用于获取元素**自身的大小**和**位置**，在网页特效中有广泛应用
>
> offset系列主要有：offsetHeight、offsetWidth、offsetParent、offsetLeft、offsetTop

### offsetWidth与offsetHeight

**作用：**通过offsetWidth和offsetHeight可以直接获取元素的**实际大小宽高**

**注意点：**

- 获取的是盒子的实际大小

  > content+ padding + border三部分组成

- 获取到的结果是数字类型，可以直接计算

- offsetWidth和offsetHeight是只读属性，不能修改设置

  > 只能看，不能动

---



### offsetParent

> 找到当前元素的最近的有定位的祖先元素

**区别：**

- parentNode：找到的是最近的父元素

- offsetParent：找到的是最近的有定位的父元素

  > 如果父元素中都没有定位，此时就找到body



### offsetLeft与offsetTop

> 用于获取元素的真实位置

- offsetLeft：获取元素距离offsetParent左边的距离
- offsetTop：获取元素距离offsetParent上边的距离

**注意点：**

- 获取的都是距离offsetParent的真实距离
- 获取到的是数值类型，可以直接计算
- offsetLeft和offsetTop同样都是只读类型，不能修改设置

 ![1](mdImg/1.png)

---



## scroll系列

> scroll家族用来获取盒子**内容的大小**和**位置**
>
> scroll家族有：scrollWidth、scrollHeight、scrollLeft、scrollTop

### scrollWidth与scrollHeight

**作用：**通过scrollWidth和scrollHeight可以直接获取**元素内容的真实宽高**，和盒子的大小无关，只与内容有关

> 比如：文字超出盒子，此时scroll系列拿到的就是文字内容实际的的宽高，而非盒子的宽高

---

### scrollLeft与scrollTop

> 用于获取元素内容滚动的距离，如果没有滚动条，则是0

- scrollLeft：获取元素内容水平方向滚动的距离
- scrollTop：获取元素内容垂直方向滚动的距离

 ![scroll](mdImg/scroll.png)

**需求：需要在滚动的时候实时拿到内容滚去的距离，怎么做到呢？？**

- 可以注册onscroll事件

  > 对于有滚动条的盒子注册onscroll事件，当元素滚动时就会触发

  ```js
  var box = doucment.getElementById(“box”);
  box.onscroll = function(){
  	//事件处理程序
  }
  ```

---

**通常来说，scroll家族用的最多的地方就是用来获取页面被卷去的宽度和高度，非常的常用**

> 实际开发的时候不会单独获取一个盒子的scrollTop，一般获取的都是整个页面的scrollTop

```javascript
window.onscroll = function () {
    // 如何拿到页面顶部滚去的距离呢？？？
    // 早期：一般通过html的scrollTop获取滚去的距离
    console.log( document.documentElement.scrollTop );
  
   	// 现在：统一使用window.pageYOffset和window.pageXOffset获取垂直和水平滚去的距离
    console.log( window.pageYOffset );
    console.log( window.pageXOffset );
}
```

##### ヾ(๑╹◡╹)ﾉ" 仿腾讯固定导航案例

> 当页面滚动到一定距离之后设置固定定位

- 找对象
- 给window注册onscroll事件
- 获取垂直滚动条的距离
- 将滚动的距离和header的高度进行对比，如果大于header的高度，让nav固定定位，苟泽取消nav的固定定位
- 当nav有固定定位的瞬间，脱标了，下面的main会跳上去，此时需要给main设置margin-top解决
- 同理，当高度没超过header的高度，则去掉多余的margin-top



## client系列

> client家族用于获取盒子可视区的大小
>
> client家族有clientWidth、clientHeight、clientLeft、clientTop

### clientWidth与clientHeight

**作用：**通过clientWidth和clientHeight获取的是可视区大小，盒子大小**不包括边框**

> 获取的是盒子的padding + content的大小

---

### clientLeft与clientTop（没用）

- clientLeft：获取元素左边框的宽度
- clientTop：获取元素上边框的宽度

 ![client1](mdImg/client1.png)

> 三大家族对比

 ![client](mdImg/client.png)



**如果需要检测浏览器窗口变化，可以使用onresize事件**

> 通过onresize事件，可以通过js完成响应式布局的效果

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

##### ヾ(๑╹◡╹)ﾉ" 使用client系列完成rem布局的适配：比如750屏幕下 盒子200*200

> 之前是通过媒体查询设置不同屏幕宽度下的html标签的font-size，此时可以直接通过js设置即可

- 把标签的单位转换成rem

- 在页面加载前，写js代码，计算并且设置当前屏幕宽度下，html的font-size应该为多少

  > 比之前媒体查询好的地方在于：媒体查询只适配一段的效果，而js可以每个屏幕都能适配

- 设置js适配的范围，设置屏幕计算的最大和最小值

- 此时会发现，只有窗口改变了才会触发，需要窗口没触发之前，先执行一遍适配的代码
