---
typora-copy-images-to: mdImg
---

# 学习目标

> - [x] 能够说出BOM是什么
>
>   - BOM：浏览器对象模型——》一套操作浏览器的方法
>
> - [x] 能够写出页面加载事件
>
>   - window.onload = function(){ 会等到页面中的所有的资源（如：标签、图片....）加载完毕之后，才会执行的代码 }
>
> - [x] 能够写出2种定时器的使用语法
>
>   ```js
>   延时器
>   setTimeout(function (){}，延时的时间)
>   
>   定时器
>   setInterval(function(){},间隔的时间)
>   ```
>
>   
>
> - [x] 能够开启和清除延时器与定时器
>
>   ```js
>   // 延时器
>   var timeId = setTimeout(fn,延时的时间)
>   clearTimeout(timeId)
>   
>   // 定时器
>   var timeId = setInterval(fn,间隔的时间)
>   clearInterval(timeId);
>   ```
>
>   
>
> - [x] 能够写出5秒钟之后跳转页面的案例
>
>   ```js
>   // 找对象
>   var link = document.querySelector('a');
>   
>   // 用变量表示剩余的时间
>   var time = 3;
>   
>   setInterval(function () {
>     time--;
>   
>     link.innerText = '注册成功，' + time + '秒后自动跳转';
>   
>     // 当剩余时间为0秒，自动跳转
>     if ( time === 0 ) {
>       location.href = link.href;
>     }
>   
>   },1000)
>   ```
>
>   
>
> - [x] 能够说出location对象以及常用属性和方法
>
>   - location.href：可以获取、可以设置（跳转）
>   - location.reload()：重新加载，刷新
>
> - [x] 能够使用history对象实现网页的前进和后退
>
>   - 前进
>     - history.forward()
>     - history.go(1)
>   - 后退
>     - history.back()
>     - history.go(-1)
>
> - [x] 能够封装简单的动画函数
>
>   ```js
>   function animate(element,target) {
>   
>     var timeId = setInterval(function () {
>       var current = element.offsetLeft;
>       current += 10;
>       element.style.left = current + 'px';
>   
>       if ( current === target ) {
>         clearInterval(timeId);
>       }
>     },16)
>   
>     }
>   ```
>
>   
>
> - [ ] 能够说出缓动动画的实现原理
>
> - [ ] 能够封装缓动动画函数
>
> 。。。。。。



**理解上课的知识点......**

# BOM

> BOM（Browser Object Model）：浏览器对象模型，提供了一套操作浏览器功能的工具。

 ![1](mdImg/1.png)

BOM包含的内容很多，但是很多东西都不太常用，但在BOM中是有一个需要大家掌握的东西，那就是***定时器*** 

## window对象

**window对象是浏览器的顶级对象，也是一个全局对象（可以直接使用）**

> 普天之下莫非王土

- document、alert()、confirm()、prompt()、console.log()...... 所有东西都是window对象上的

- 我们定义在全局作用域中的变量、函数，其实也是window上的属性和方法
- window非常常用，如果每次都要加很麻烦，所以使用的时候可以省略

---



### window.onload（掌握）

> window.onload事件会在网页加载完成后执行，通常我们称之为**入口函数**

**需求：把script标签写在head中，获取页面中的元素**

> 浏览器会从上往下依次执行代码：
>
> - 如果script中的代码放在body标签的最后，此时浏览器已经加载完毕元素，可以通过js获取到元素
> - 如果script中的代码放在body标签的前面，此时浏览器还没有加载完元素，直接通过js获取不到
>
> 所以虽然js基础的时候说过，虽然script可以写在任意位置。一般script标签写在body标签内容的最后

**如果需要script不管写在哪里，都要在元素加载完毕后再执行，可以通过window.onload事件完成。**

**语法：**

```javascript
window.onload = function(){
	// 会在网页加载完成（包括文档、图片、文件的加载完成）后才会执行
}
```

---



**需求：通过js直接拿图片的宽高**

> 注意点：浏览器对页面加载有优化，当加载图片时，图片的加载会延迟

- 在直接获取图片宽高时，一般代码需要写在window.onload里面，否则会出现图片没有加载完成，获取到的宽度和高度不对的情况。



## 延时器与定时器（重要）

### 延时器：setTimeout

> setTimeout延时器可以让代码延时执行一次

**需求1：让一段代码2秒后再执行**

> 如果需要让代码延时执行，可以使用延时器实现

**设置延时器：**

```javascript
// 语法：setTimeOut(func, time);
// 	参数1：需要延时执行的代码函数
// 	参数2：延时多少时间（单位：毫秒）
// 	返回值：当前延时器的id（用于等会清除）

var timeId = setTimeOut(function(){
	// 1秒后将执行的代码。
}, 1000);
```

**需求2：给两个按钮注册点击事件，一个点击装炸弹、一个点击拆炸弹**

**清除延时器**

```javascript
// 语法：clearTimeOut(timeId)
//  参数：需要清除的延时器id

//示例：
clearTimeOut(timeId);//清除上面定义的定时器
```

---



### 定时器：setInterval

> setInterval定时器可以让代码隔一段时间就执行一次，除非被清除，否则一直执行下去

**需求1：让一段代码隔1s就执行一遍**

**设置定时器：**

```javascript
// 语法：setInterval(func, time);
//  参数1：需要重复执行的代码函数
//  参数2：每次间隔的毫秒数
//  返回值：当前定时器的id（用于清除）

var timeId = setInterval(function(){
	//重复执行的代码。
}, 1000);
```

**需求2：给两个按钮注册点击事件，一个点击装连环炸弹、一个点击拆炸弹**

**清除定时器：**

```javascript
// 语法：clearInterval(timeId)
//  参数：需要清除的定时器id

clearInterval(timeId);//清除上面定义的定时器
```

---

##### ------------------------

##### ヾ(๑╹◡╹)ﾉ" 电子表：在box盒子中设置当前的时间

> 先获取当前的时间，然后设置到box的内容中去

![电子表案例](mdImg/电子表案例.gif)

```html
<style>
  #box {
    width: 600px;
    height: 200px;
    position: absolute;
    left: 50%;
    top: 50%;
    transform: translate(-50%,-50%);
    box-shadow: 12px 12px 18px 3px #ccc;
    text-shadow: 0px 3px 0px #b2a98f, 0px 14px 10px rgba(0,0,0,0.15), 0px 24px 2px rgba(0,0,0,0.1), 0px 34px 30px rgba(0,0,0,0.1);
    line-height: 200px;
    font-size: 40px;
    text-align: center;
  }
</style>

<div id="box"></div>
```



- 获取当前日期对象
- 把日期对象转换成本地格式字符串
- 把日期字符串设置到box中
- 需要隔1s执行一次——》定时器
- 因为定时器中的函数不会立马执行，如果需要让页面一刷新立马有时间——》在定时器前先执行一遍代码

---

##### ヾ(๑╹◡╹)ﾉ" 短信验证码案例

> 按钮点击发送之后，需要到时间之后才能继续点击发送（防止用户一直点击，短信轰炸）

![短信验证码案例](mdImg/短信验证码案例.gif)

- 使用一个变量计数，表示还剩余的时间

- 给按钮注册点击事件，点击后禁用按钮，同时定时器计数，修改内容

- 点击之后开启定时器计数，每秒改变button内容

  > 注意点：在定时器中的this指向的是window

- 当计数到达指定时间后，清除定时器，启用按钮，恢复button内容

---



## location对象

> location对象也是window对象上的一个属性，其实对应的就是浏览器中的地址栏。
>
> 通过location对象上的相关属性，可以实现如：跳转、刷新等效果

**location.href——》地址栏的地址：**

```javascript
// 获取地址
console.log( location.href );// 拿到地址栏的地址

// 设置跳转
location.href = "http://www.baidu.com";// 让页面跳转到百度
```

**location.reload()——》重新加载（刷新）**

```javascript
location.reload();// 重新加载，刷新页面
```

---

##### ヾ(๑╹◡╹)ﾉ" a标签自动跳转功能

> 用户可以直接点a标签跳转，也可以自动3秒倒计时后跳转

<img src="mdImg/自动跳转案例.gif" alt="自动跳转案例" style="zoom:80%;" />

- 设置变量计数，表示还剩多少时间
- 设置定时器，每一秒改变a标签的内容
- 当时间结束时，通过js跳转到目标网页



## history对象（了解）

> history对象表示页面的历史，可以通过history对象的属性完成：前进、后退等效果。

**功能：**

```javascript
// 页面前进
history.forward();
// 页面后退
history.back();

// ------------------------------------------
history.go(1);// 前进一页，相当于：history.forward();
history.go(0);// 刷新当前页，相当于：location.onload();
history.go(-1);// 后退一页，相当于：history.back();
```



## navigator对象（了解）

> window.navigator的一些属性可以获取客户端的一些信息

```javascript
//navigator.userAgent：浏览器版本
```

##### ------------------------



# js中的动画

> 之前通过css的过渡以及动画可以完成动画效果，其实js也可以完成、

## js动画初体验

> 动画的原理：让元素在原有基础上移动一点，连贯着运动就是动画效果
>
> 具体实现原理：通过定时器（setInterval）不断移动盒子的位置

**需求1：点击一下button，就让div往右移动一步10px**

> 按一下走一步

```html
<style>
  * {
    margin: 0;  
    padding: 0;
  }

  div {
    width: 100px;
    height: 100px;
    background-color: pink;
    /* 设置定位 */
    position: absolute;
  }
</style>

<button>奔跑吧</button>
<div>小犊子</div>
```

- 找对象
- 给button注册点击事件
- 点击后让div在原来位置上往右多移动10px

---



**需求2：（优化）点击一下button，让div自动一步一步的往右移动400px就停止**

> 按一下自动走多步，到指定位置

- 找对象
- 给button注册点击事件
- 点击之后通过定时器设置盒子自动移动距离
- 最后如果发现当前盒子位置current的值等于400时，立刻清除定时器停止



## js动画函数封装

> 如果页面中多个元素有动画，一个一个设置动画代码太过麻烦。
>
> 针对于重复的需求代码，可以封装成一个函数，做到不同元素（element）移动到不同位置（target）。（函数一次声明、多次调用）

**需求1：点击button1，让div往右移动到400px，点击button2，让div往右移动到800px（封装函数的函数完成）**

> 多处需要用到动画的代码，此时封装成一个函数——》可以让任意元素移动任意距离

---



**需求2：（优化）如果快速点击button按钮，发现盒子移动的越来越快？？**

> 因为每次点击button都会开启新定时器，多个定时器同时作用导致越走越快

- 每次设置定时器前，需要保证把之前的定时器清除

- 需要保证timeId是全局变量，让每次使用animate函数时都能清除之前的定时器

- 但是如果timeId是全局变量，每次使用的调用的时候需要保证全局有一个timeId变量，这样animate函数对于timeId的依赖太高，不够独立

- 其实全局变量就是在window对象上添加一个属性，类比来说：可以把timeId添加到当前对象的属性上

  > 好比是：自己的东西不要存到外面公共的储物箱里，这样其他人用的时候可能会出问题。可以自己揣自己兜里即可。









## js缓动动画封装

> 之前写的动画函数确实能让盒子移动，但是每一步都是相同距离，其实此时是匀速动画

**对比：**

- 匀速动画：移动每一步都是相同距离——》匀速

  - 如果用户从第一页切换到第二页，是匀速动画但是距离较短，需要时间是翻开1页的时间

  - 如果用户从第一页直接切换到最后一页，是匀速动画但是距离较远，需要的时间是翻1页的5倍时间

    > 效果不好，实际页面中需要保证用户无论是切换几页，花费的时间需要差不多

- 缓动动画：每一步是剩下距离的百分比，不是固定的值——》变速

  - 不论距离近还是远，每一步都是剩下距离的百分比计算，运动的状态都是最终慢慢慢下来（缓动）


**实现公式：先快再慢，慢慢停下来的变速动画 **

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

