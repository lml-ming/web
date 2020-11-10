---
  typora-copy-images-to: mdImg
---

# 学习目标

> - [x] 能够写出H5新增获取元素方式
>
>   ```js
>   // 通过css选择器获取元素
>   // 1、获取单个元素
>   var box = document.querySelector('选择器');
>   
>   // 2、获取多个元素
>   var boxs = document.querySelectorAll('选择器');
>   ```
>
>   
>
> - [x] 能够使用querySelector与querySelectorAll获取元素
>
>   ```js
>   // 通过css选择器获取元素
>   // 1、获取单个元素
>   var box = document.querySelector('选择器');
>   
>   // 2、获取多个元素
>   var boxs = document.querySelectorAll('选择器');
>   ```
>
>   
>
> - [x] 能够设置获取自定义属性
>
>   ```js
>   // 点语法针对于自定义属性不能获取和设置
>   // 需要用到attribute系列的方法——》可以操作自定义属性和固有属性
>   
>   // 获取属性
>   getAttribute('属性名');
>   
>   // 设置属性
>   setAttribute('属性名','属性值');
>   
>   // 移出属性
>   removeAttribute('属性名');
>   ```
>
>   
>
> - [x] 能够获取元素的子元素、父节点、兄弟元素
>
>   - 子元素：children
>   - 兄弟
>     - 上一个兄弟元素：previousElementSibling
>     - 下一个兄弟元素：nextElementSibling
>   - 父节点：parentNode
>
>   
>
> - [x] 能够使用appendChild和insertBefore添加节点
>
>   ```js
>   parent.appendChild(child)// 把child添加到parent内容的最后
>   parent.insertBefore(newChild,refChild)// 把newChild添加到parent内部refChild的前面
>   ```
>
>   
>
> - [x] 能够删除和复制节点
>
>   - 删除节点：parent.removeChild（child）
>   - 复制节点：node.cloneNode(true)
>
> 
>
> - [x] 能够完成许愿墙案例
>
> 。。。。。。



**理解上课的知识点......**



##### ヾ(๑╹◡╹)ﾉ" 复习tab栏案例



# 获取元素的方法

> 其实获取元素的方法有多种

## 通过id获取（通用）

**代码：**`document.getElementById("id属性值");`

**返回值：** 一个元素。如果不存在，会返回null

```javascript
// 参数：元素的id属性值
// 返回值： 一个元素。如果不存在，会返回null
document.getElementById("id");
```

## 通过标签名获取（通用）

**代码：**`document.getElementsByTagName("标签名");`

**返回值：** 伪数组。无论找到几个元素，返回值都是伪数组

```javascript
// 参数：标签名
// 返回值：伪数组。无论找到几个元素，返回值都是伪数组
document.getElementsByTagName("tagName");
```

> 以上两个是没有兼容性问题的，以下方法ie678不支持

---

## 通过类名获取（一般不用）

**代码：**`document.getElementsByClassName("类名");`

**返回值：** 伪数组。无论找到几个元素，返回值都是伪数组

```javascript
// 参数：类名
// 返回值：伪数组。无论找到几个元素，返回值都是伪数组
document.getElementsByClassName("类名")
```



## 通过name获取（一般不用）

> 只能用于表单元素，一般不用

**代码：**`document.getElementsByName("name属性值");`

**返回值：** 伪数组。无论找到几个元素，返回值都是伪数组

```javascript
// 参数：name属性值
// 返回值：伪数组。无论找到几个元素，返回值都是伪数组
document.getElementsByName("name属性值");
```



## 通过css选择器获取（常用）

> 比较好用的方法

### 获取单个元素

**代码：**`document.querySelector('css选择器');`

**返回值：** 一个元素。如果有多个，之后返回第一个，如果没有返回null

```js
// 参数：css选择器
// 返回值：一个元素。如果有多个，之后返回第一个，如果没有返回null
document.querySelector('css选择器')
```

### 获取多个元素

**代码：**`document.querySelectorAll('css选择器');`

**返回值：** 伪数组。无论找到几个元素，返回值都是伪数组

```java
// 参数：css选择器
// 返回值：伪数组。无论找到几个元素，返回值都是伪数组
document.querySelectorAll('css选择器');
```



# 标签的自定义属性

> 标签上属性可以大致分成两类：
>
> - 固有属性：标签上本来就有的属性：如：title、id、class......
> - 自定义属性：标签上本来没有的属性，自己随意添加的属性

**需求：通过js获取标签上的属性**

如果要获取**html标签上**的固有属性（本来就有的属性：title、id、class），可以直接通过dom对象点语法获取和设置

**比如：**

```html
<div title="one">我是一个标签</div>

<script>
  var box = document.querySelector('div');
  console.log(box.title);// one
</script>
```

---

但是如果要获取**html标签上**的自定义属性（本来没有的属性，自己随意添加的），使用点语法就不行了，需要通过特殊的方法获取和设置

**比如：**

```html
<div aa="one" >我是一个标签</div>

<script>
  var box = document.querySelector('div');
  console.log( box.aa );// undefined
</script>
```



---

**注意点：**标签的自定义属性在DOM对象中是不存在的，DOM对象中只会储存固有属性

> 如果需要通过DOM对象操作标签上的自定义属性，此时需要通过attribute相关的方法完成



## attribute方法

> attribute系列方法是通用的操作标签属性的方法，不管是固有属性还是自定义属性都可以操作

```js
// 获取标签的属性
box.getAttribute('属性名');
// 设置标签的属性
box.setAttribute('属性名', '属性值');
// 移除标签的属性
box.removeAttribute('属性名');
```

**注意点：attribute方法可以操作标签的自定义属性和固有属性**

##### ------------------------

# DOM树

> 文档页面中的很多节点之间，其实可以通过树状结构表示——》DOM树

html中所有的内容可以通过树状的结构表示，如：

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
  </head>
  <body>

    <div>
      <span>我是span1</span>
      <span>我是span2</span>
    </div>
    <!-- 我是一个注释 -->
    <p>我是一个p标签</p>
    
  </body>
</html>
```

用根据元素之间的关系可以通过树状图表示如下：

> 就类比如元素的族谱图

![dom树](mdImg/dom树.png)

> 之前查找元素是直接在文档中查找的，但是通过DOM树这样的结构，我们可以拓展找元素的方式，直接通过当前节点可以找到其兄弟节点、父子节点
>
> - 之前：直接在整个页面中查找元素——》好比是在全国范围去找某个人
> - 现在：可以通过节点之间的关系查找元素——》好比是可以通过家族关系，去找到父子、找兄弟等会之类的

---



# 节点查找

> 之后可以通过节点查找的方式找到对应的元素。

## 孩子节点

> 获取元素的用的较多

```html
<ul>
  <li>张三</li>
  <li>李四</li>
  <!-- 我是一个注释 -->
  <li>王五</li>
  <li>赵六</li>
</ul>
```



|                          作用                          |         属性          |
| :----------------------------------------------------: | :-------------------: |
|   获取所有子节点（包括元素节点、注释节点、文本节点）   |      childNodes       |
|           获取**所有子元素**（只有元素节点）           |     **children**      |
|  获取第一个子节点（包括元素节点、注释节点、文本节点）  |      firstChild       |
|          获取**第一个子元素**（只有元素节点）          | **firstElementChild** |
| 获取最后一个子节点（包括元素节点、注释节点、文本节点） |       lastChild       |
|         获取**最后一个子元素**（只有元素节点）         | **lastElementChild**  |

---



## 兄弟节点

> 获取元素的用的较多

```html
<ul>
  <li>张三</li>
  <li class="ls">李四</li>
  <!-- 我是一个注释 -->
  <li>王五</li>
  <li>赵六</li>
</ul>
```

|                          作用                          |            属性            |
| :----------------------------------------------------: | :------------------------: |
| 获取上一个兄弟节点（包括元素节点、注释节点、文本节点） |      previousSibling       |
|         获取**上一个兄弟元素**（只有元素节点）         | **previousElementSibling** |
| 获取下一个兄弟节点（包括元素节点、注释节点、文本节点） |        nextSibling         |
|         获取**下一个兄弟元素**（只有元素节点）         |   **nextElementSibling**   |

---



## 父节点

```html
<ul>
  <li>张三</li>
  <li class="ls">李四</li>
  <!-- 我是一个注释 -->
  <li>王五</li>
  <li>赵六</li>
</ul>
```

|    作用    |    属性    |
| :--------: | :--------: |
| 获取父节点 | parentNode |

> 一般html中都是标签包裹内容，所以一般获取父节点就是父元素

---



##### ヾ(๑╹◡╹)ﾉ"  节点查找的小结

> 重点在于查找元素的那几个

---



##### ヾ(๑╹◡╹)ﾉ" 隔行变色的效果

> 通过js：让一个div中的标签中的不同标签隔行变色

---



##### ヾ(๑╹◡╹)ﾉ" 表单校验效果

> 需要在用户**输入时**判断内容的长度是否满足2~6位之间

![表单校验效果](mdImg/表单校验效果.gif)

##### keydown与keyup事件

|   事件    |          功能          |                  注意点                   |
| :-------: | :--------------------: | :---------------------------------------: |
| onkeydown | 当键盘按下时触发的事件 |  获取文本框的值，此时value的值是上一次的  |
|  onkeyup  | 当键盘弹起时触发的事件 | 获取文本框的值，此时value的值是本次输入的 |

> 一般校验的时候，如果需要判断用户此时输入的数据，需要通过onkeyup事件。

---



##### ------------------------



# 节点操作

## 添加节点：appendChild(newChild)

**需求：**点击按钮之后，把一个div.red添加另一个div.father里面（移花接木）

> 此时需要使用添加节点的方法

```html
<style>
  .father {
    width: 400px;
    height: 400px;
    border: 1px solid #000;
  }

  .red {
    width: 100px;
    height: 100px;
    background-color: red;
  }
</style>

<button>移花接木</button>
<div class="father">
  这是.father的盒子
</div>

<div class="red">
  这是.red的盒子
</div>
```



**语法：** `parent.appendChild(newChild)` 

- parent：要添加内容的父节点
- newChild：需要添加进入的子节点

**作用：**表示把newChild添加到parent内容的**最后**

---



## 插入节点：insertBefore(newChild,refChild)

> 可以将页面中的节点插入到目标节点的前面

**需求：** 点击按钮，在把田七添加到王五前面

```html
<button>点击插队</button>
<ul>
  <li>张三</li>
  <li>李四</li>
  <li class="ww">王五：我预感等会田七会插到我前面</li>
  <li>赵六</li>
</ul>

<li class="tq">田七：我要插队！！</li>
```



**语法：** `parent.insertBefore(newChild,refChild)`

**参数：**

- parent：要插入元素的父元素
- newChild：添加的元素
- refChild：被插入前面的元素

**作用：** 把newChild添加到parent里面的refChild节点的前面

**注意点：** 

- 如果是在父元素内容的最前添加，可以使用 `parent.inserBefore(newChild,firstElementChild);`

- 如果是在父元素内容的最后添加，可以使用appendChild，也可以使用 `parent.insertBefore(newChild,null)`

  >  其实就是appendChild的效果

---



## 复制（克隆）节点：cloneNode()

**需求：**将上面的移花接木优化，点击按钮之后之后复制div.red添加到div.father里面去（真.移花接木）

> 如果复制的div中有内容呢？

```html
<style>
  .father {
    width: 400px;
    height: 400px;
    border: 1px solid #000;
  }

  .red {
    width: 100px;
    height: 100px;
    background-color: red;
  }
</style>

<button>移花接木</button>
<div class="father">
  这是.father的盒子
</div>

<div class="red">
  这是.red的盒子
</div>
```



**语法：** `node.cloneNode()`

**作用：** 在内存中复制克隆一份node节点

**参数：**

- false：浅克隆，只克隆当前节点，不包含其中内容节点
- true：深克隆，克隆当前节点以及其中所有内容节点



---

## 删除节点：removeChild(child)

**需求：** 点击哪一个li，就删除这个一个li

**语法：** `parent.removeChild(child)`

**参数：**

- parent：要删除元素的父元素
- child：需要删除的元素

**作用：** 通过父节点调用，删除其中的某个子节点



##### ヾ(๑╹◡╹)ﾉ" 许愿墙案例

- 在页面中克隆十份许愿纸

---

##### ------------------------

- 设置许愿纸在许愿墙的随机位置

---

- 给许愿纸设置点击事件，点击之后层级最高

##### ヾ(๑╹◡╹)ﾉ" 页面中三个盒子定位，点谁谁上来

> 需要通过变量储存层级，每次用完之后++

---

- 点击关闭x时，删除当前许愿纸

---

- 双击许愿纸头部，删除当前许愿纸

  > **双击事件：ondblclick**
  >
  > 当双击时触发事件

​	 
