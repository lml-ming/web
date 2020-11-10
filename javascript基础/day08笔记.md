---
typora-copy-images-to: mdImg
---

# 学习目标

> - [x] 能够说出数组对象的增删操作
>
>   - push:在数组的最后添加一项或者多项——》返回新数组的长度
>   - pop:在数组的最后删除一项——》返回删除的这一项
>   - unshift：在数组的最前添加一项或者多项——》返回新数组的长度
>   - shift：在数组的最前删除一项——》返回删除的这一项
>
> - [x] 能够使用数组的排序和翻转操作
>
>   - 数组的翻转：arr.reverse()
>
>   - 数组的排序：arr.sort()
>
>     ```js
>     arr.sort(function (a,b) {
>     // a表示前一项
>     // b表示后一项
>     // 如果返回值大于0，此时会交换位置
>     ```
>
>   // 从小到大
>   return a - b;
>
>   // 从大到小
>   return b - a;
>     })
>     ```
>   
>     
>     ```
>
> - [x] 能够说出什么是基本包装类型
>
>   - 如果简单数据类型需要用到属性和方法——》自身没有
>   - 先把简单类型包装成复杂数据类型——》此时身上已经有属性和方法，此时可以得到结果
>   - 把包装之后的复杂数据类型恢复成原来的简单类型
>
> - [x] 能够说出字符串对象的3-4个方法
>
>   - indexOf
>
>   - lastIndexOf
>
>   - **去除首尾的空格：trim()**
>
>   - **转大写：toUpperCase（）**
>
>   - **转小写：toLowerCase（）**
>
>   - 拼接：arr1.concat(arr2)
>
>   - 截取：
>
>     - **slice（begin，end）**
>     - substring（begin，end）
>     - substr（begin，length）
>
>   - **分割成数组：split(‘分隔符’)**
>
>   - **替换：replace（‘aa’,'bb'） 表示把第一个aa替换成bb**
>
>     ```js
>     str.replace(/aa/g,'bb');// 表示把str中的所有的aa替换成bb
>     ```
>
>     
>
>
>   。。。。。。



**理解上课的知识点......**



# 内置对象

> JS内置对象就是指Javascript自带的一些对象，供开发者使用，这些对象提供了一些常用的的功能。
>
> 常见的内置对象有Math、String、Array、Date等

## Math对象

> Math对象中封装很多与数学相关的属性和方法。

- **圆周率**

  `Math.PI`

- **最大值/最小值**

  ```
  Math.max(1,2,3,4,5,6);
  Math.min(1,2,3,4,5,6);
  ```

- **取整**

  ```javascript
  Math.ceil();//天花板，向上取整，取大的那个
  Math.floor();//地板，向下取整，取小的那个
  Math.round();//四舍五入，如果是.5，则取更大的那个数
  
  console.log( Math.ceil(1.1) );
  console.log( Math.ceil(1.9) );
  console.log( Math.ceil(-1.1) );
  console.log( Math.ceil(-1.9) );
  ```

![image-20200922104218694](mdImg/image-20200922104218694.png)

- **随机数**

  ```javascript
  Math.random();//返回一个[0,1)之间的数，能取到0，取不到1
  ```

  - **小案例：**随机获取0、1、2这三个数
  
    ```js
  // --------------获取0~2.9999的随机数
    Math.random()*3
  //---------------只需要把小数点之后的去掉即可
    parseInt(Math.random()*3)
    ```
  
    > 求0~n的整数随机数
    >
    > `parseInt(Math.random()*(n+1))`

  - **小案例：** 随机生成一个rbg颜色

    ```js
    var colorA = parseInt( Math.random() * 256 );
    var colorB = parseInt( Math.random() * 256 );
    var colorC = parseInt( Math.random() * 256 );
    var str = 'rgb('+ colorA + "," + colorB + ',' + colorC +')';
    console.log(str);
    //----------------------设置body的颜色（web api内容）
    document.body.style.backgroundColor = str;
    ```

- **绝对值**

  ```javascript
  Math.abs();//求绝对值
  //-----------------------------
  console.log(Math.abs(1));  // 1
  console.log(Math.abs(-1));  // 1
  ```

- **次幂（次方）**

  ```javascript
  Math.pow(num, power);//求num的power次方
  //-----------------------------
  console.log(Math.pow(3, 2));  // 3的平方  9
  console.log(Math.pow(10, 3)); // 10的三次方 1000
  console.log(Math.pow(100, 0.5));  // 100的开方  10
  ```

- **开平方**

  ```js
  Math.sqrt(num);//对num开平方
  //-----------------------------
  console.log(Math.sqrt(9));  // 3
  ```



## Date对象

> js提供了一个**Date构造函数**，通过Date构造函数可以创建不同的日期对象
>
> ——》因为日期都是不同的！！！
>
> Date对象用来处理日期和时间

- **创建一个日期对象**

  ```javascript
  var now = new Date();//不传参，默认是一个当前时间的对象
  var date = new Date("2019-05-20 12:00:00");//(格式固定)指定具体的时间对象，后面的时分秒可以省略
  console.log(now);
  console.log(date);
  //-----------------------------不常用的方式
  var date = new Date(2019,4,20,12,0,0);// 可以把每一个项分别传入，但是注意月份从0开始的，0~11
  var date = new Date(1558324800000);// 直接传入时间戳也行
  ```

- **日期格式化方法（了解，不用）**

  > Date对象中有默认的方法可以进行日期格式化，但是不好看，一般不用。

  ```javascript
  var now = new Date()；
  console.log(now);// 默认直接打印now对象，会默认调用toString方法，打印结果是一个字符串
  console.log(now.toString());// 转成标准的字符串日期数据输出（默认）
  console.log(now.toLocaleString()); // 输出本地格式日期
  console.log(now.toLocaleDateString());  // 本地格式日期，只输出日期部分
  console.log(now.toLocaleTimeString());  // 本地格式日期，只输出时间部分
  ```

- **获取日期的指定部分**

  > 之前默认的日期格式化格式很丑，一般不用——》通过获取日期的指定部分，可以自定义格式化日期

  ```javascript
  var now = new Date(); // 当前时间
  
  // 获取年份
  var year = now.getFullYear();
  
  // 获取月份——》月份从0开始，范围是0~11，一般会+1
  var month = now.getMonth() + 1;
  
  // 获取日——》一个月的几号——》getDay表示获取星期几（从0开始，0表示周日，1表示周一）
  var day = now.getDate();
  
  // 获取时
  var hours = now.getHours();
  
  // 获取分
  var minutes = now.getMinutes();
  
  // 获取秒
  var seconds = now.getSeconds();
  
  var str = year + '年' + month + '月' + day + '日, ' + hours + '时' + minutes + '分' + seconds + '秒';
  document.write(str);
  ```

---

- **时间戳**

  > 一般日期打印出来，是字符串的形式
  >
  > **时间戳则是日期的数字形式**，可以运算

  **时间戳：**表示距离1970年01月01日00时00分00秒起，过去的总毫秒数

  **作用：** 用来计算时间差

  **代码：** `var date = +new Date();`

  - 可以统计代码执行的时间

    ```js
    // ------------------------获取开始的时间
    var begin = +new Date(); 
    var sum = 0;
    for (var i = 1; i <= 100000000; i++) {
        sum += i;
    }
    console.log(sum);
    // -------------------------------获取结束的时间
    var end = +new Date();  
    console.log(end - begin);  // 计算时间差，可以得出代码的执行时间毫秒数
    ```

  - 倒计时（距离下课的时间）

    ```js
    // -----------------------------------当前时间
    var now = new Date();
    // ----------------------------------将来需要倒计时的时间
    var future = new Date('2019-5-20 12:00:00'); 
    
    // ------------------------------得到时间差——》转换成秒数（小数后忽略）
    var time = parseInt((future - now) / 1000);  
    
    // --------------------------------秒数中获取时——》1小时=3600秒
    var hours = parseInt(time / 3600);
    
    // --------秒数中获取分——》1分钟=60秒, 对所有的分钟数, 对60求余数即可(超过60的进位到小时中了）
    var minutes = parseInt(time / 60) % 60;
    
    // ---------获取秒数，对秒数求60的余数（超过60的部分进位到分钟去了)
    var seconds = time % 60;
    
    var str = "距离下课还有: " + hours + '小时' + minutes + '分钟' + seconds + '秒';
    document.write(str);
    ```



## Array对象

> js中内置了一个**Array构造函数**，可以用来创建数组对象（万物皆对象），每个对象中也有对应的方法

- **数组转换成字符串：arr.join(字符串分隔符)**

  > 作用：**将数组中的每一项拼接成字符串**

  ```javascript
  // 语法：arr.join(分隔符)
  var arr = ['张三','李四','王五','赵六'];
  var str = arr.join();  // 不传参数，默认每一项之间以 逗号 进行拼接
  var str = arr.join("-");//按 - 进行拼接
  var str = arr.join("");//分隔符为空串，中间就没有分隔符
  ```

---

- **数组的增删操作：push、pop、unshift、shift**

  ```javascript
  // --------------------在数组的最后，添加一个或多个项，返回添加后数组的length
  array.push();
  // -------------------在数组的最后，删除一项，返回删除的项
  array.pop();
  // --------------------在数组的
  最前面，添加一个或多个项，返回添加后数组的length
  array.unshift();
  // ---------------------在数组的最前面，删除一项，返回删除的项
  array.shift();
  ```

##### ------------------------

##### ヾ(๑╹◡╹)ﾉ" 数组的增删操作练习

  ```js
//练习1
var arr = ["刘备"];
//添加数据后变成：["赵云","马超","刘备","关羽","张飞"]

//接着删除数据后变成：["关羽","张飞"]

console.log(arr);

//练习2
var arr = ["赵云","马超","刘备","关羽","张飞"];
//把数组的最后一个元素变成数组的第一个元素

//把数组的第一个元素变成数组的最后一个元素

console.log(arr);
  ```

---

- **数组的翻转与排序：reverse、sort**

  ```javascript
  //------------------让当前数组反转
  arr.reverse();
  //-------------------让当前数组排序，默认按照首字符排序
  arr.sort();
  
  //--------------sort方法可以传递一个函数作为参数，设置是升序还是降序排序
  arr.sort(function(a, b){
    // a表示前一项，b表示后一项
    // 如果返回值 >0,则交换位置
    // --------------从小到大升序排列
    return a - b;
    //---------------从大到小降序排列
    return b - a;
  });
  ```

  ---

  ##### ヾ(๑╹◡╹)ﾉ" 数组的排序练习

  ```javascript
  //1、将[3, 6, 1, 5, 10, 2,11]从小到大排列
  
  //2、将字符串数组按照字符长度从小到大排列——》比较的a.length和b.age
  var arr = ['bb', 'a', 'dddd', 'ccc'];
  
  //3、将学生数组按照年龄从小到大排列——》比较的a.age和b.age
  var arr = [
      {name: 'zs', age: 18, score: 100},
      {name: 'ls', age: 38, score: 120},
      {name: 'ww', age: 28, score: 20},
      {name: 'zl', age: 16, score: 15},
  ];
  ```



- **数组的合并和截取：concat、slice**

  > 数组的合并

  ```javascript
  //-----------------合并数组，不会改变原数组，会返回一个新的拼接好的数组
  var newArr = arr.concat(arr2);
  ```

  > 数组的截取

  ```js
  var arr = ["赵云","马超","刘备","关羽","张飞"];
  //--------------------------数组的截取，从数组中截取一部分，不会改变原数组，返回截取的新数组
  var newArr = arr.slice();// 不传参——》从开始截取到最后，截取整个数组——》相当于复制一份
  var newArr = arr.slice(begin);// 从begin（下标）开始，截取到最后，包括begin！！
  var newArr = arr.slice(begin,end);// 从begin开始，截取到end，包括begin，不包括end！！！
  ```

---

- **数组的删除、添加、替换：splice**

  > splice可以在数组的任意位置，添加或者删除任意项，会改变原数组

  ```js
  //------------------splice 方法可以在数组的任意位置，添加或者删除任一项（会改变原数组）
  arr.splice(从哪开始删除，删除几个，添加的项1，添加的项2，......)
  arr.splice(begin,deleteCount,item1,item2,...)
  
  var arr = ["赵云","马超","刘备","关羽","张飞"];           
             
  //删除--------------------从下标为1开始删除，删除两项
  arr.splice(1,2);// 删除
  
  //添加--------------------把第一项、第二项添加到下标2的位置
  arr.splice(2,0,'第一项','第二项');// 添加
  
  //替换--------------------把下标2这一项替换成新项（先删除，再添加）
    arr.splice(2,1,'新项');// 替换
  ```

---

##### ------------------------

#####  ヾ(๑╹◡╹)ﾉ" 数组的截取与添加练习

  ```js
//练习：
var arr = ["赵云","马超","刘备","关羽","张飞"];
//1、截取["刘备","关羽"]
//2、在马超后面增加 马腾
//3、删除关羽
  ```

> **增删操作，都会改变原数组！！**



- **数组查找元素：indexOf、lastIndexOf**

  > 查找值在数组中某元素的下标

  ```javascript
  //------------indexOf()——》查找数组中元素第一次出现的下标——》如果找不到，返回-1
  var arr = [1,2,3,4,5,4,3,2,1];
  console.log(arr.indexOf(2));// 查找2在数组中第一次出现的下标
  console.log(arr.indexOf(100));// 数组中不存在的值，返回-1
  
  // 需求: 判断 arr 中是否有 赵六
  var arr = ['张三', '田七', '李四', '王五'];
  var index = arr.indexOf('赵六');
  if (index === -1) {
      console.log('没有');
  }
  else {
      console.log('有赵六, 下标是' + index);
  }
  
  //-------------lastIndexOf()——》查找数组中元素最后一次出现的下标——》如果找不到，返回-1
  var arr = [1,2,3,4,5,4,3,2,1];
  console.log(arr.lastIndexOf(2));// 查找2在数组中第一次出现的下标
  console.log(arr.lastIndexOf(100));// 数组中不存在的值，返回-1
  ```

- **清空数组**

  ```javascript
  var arr = [1,2,3,4,5];
  
  // 1、------------------将数组赋值为一个空数组，推荐
  arr = [];
  
  // 2、-----------------直接修改数组的长度为0
  arr.length = 0;
  
  // 3、-------------------删除数组中的所有元素
  arr.splice(0,arr.length);// 从下标0开始，删除arr.length个元素
  ```

---

##### ヾ(๑╹◡╹)ﾉ" 数组的综合练习

```javascript
var arr = ["c", "a", "z", "a", "x", "a", "a", "z", "c", "x", "a", "x"]
//1. 找到数组中第一个a出现的位置
//2. 找到数组中最后一个a出现的位置
//3. 找到数组中每一个a出现的位置(遍历——》打印下标)
//4. 数组去重，返回一个新数组
//   1、遍历原数组
//   2、看arr[i] 在 newArr中是否存在，存在就加入newArr，如果不存在，就不加。
```



## 基本包装类型

> **简单数据类型本身是没有任何属性和方法的**。
>
> 但是为了方便操作基本数据类型，js中还提供了三个特殊的复杂类型：String、Number、Boolean对象。可以使用其中的方法：
>
> `Number：    var num = new Number(123);`
>
> `String：    var str = new String('abc');`
>
> `Boolean：   var flag = new Boolean(true);`

**基本包装类型：**把基本类型包装成复杂类型

```javascript
//-------------------------简单数据类型没有任何的属性和方法
var str = “abc”;
//---但是却可以直接使用.length方法——》原因是底层浏览器默认把简单数据类型包装成复杂类型，就可以调用方法了
console.log(str.length);
```

**基本包装类型的步骤：**

1. 在js中为了操作方便，如果是简单数据类型要获取方法时——》默认转换成复杂数据类型
2. 变成复杂数据类型之后——》调用其方法，得出结果
3. 结束时，在还原成简单数据类型

### Number对象

> Number对象是数字的包装类型，数字可以直接使用这些方法

```javascript
var num = 11.111111;
//------------------保留几位小数
console.log(num.toFixed(2));
//--------------------转成字符串
console.log(num.toString(2));
```

### Boolean对象

> Boolean对象是布尔类型的包装类型。

```javascript
var flag = true;
//-------------------转成字符串
console.log(flag.toString();)//底层先转成基本包装类型——》使用方法得到字符串——》还原成简单数据类型
```

> undefined和null没有包装类型！！！所以没有方法！！

---

##### ------------------------

### String对象

> 字符串可以类似于看做是一个数组（不是真的数组——》伪数组）

- **字符串可以遍历——》字符串不是数组，不是真的数组**

  ```js
  var str = 'abcdefg';
  // 底层会默认转换成 String对象，var str = new String('abcdefg');
  //----------------------打印字符串中下标为0的字符
  console.log(str[0]);
  //-----------------------字符串的遍历（类似于数组）
  for (var i = 0; i < str.length; i++) {
      console.log(str[i]);
  }
  ```

- **查找指定字符的位置：indexOf、lastIndexOf**

  ```javascript
  //------------indexOf()——》查找字符第一次出现的下标——》如果找不到，返回-1
  var str = "abdedba";
  console.log(str.indexOf(a));// 查找a在str中第一次出现的下标
  
  //-------------lastIndexOf()——》查找字符最后一次出现的下标——》如果找不到，返回-1
  var str = "abdedba";
  console.log(str.lastIndexOf(a));// 查找a在str中最后一次出现的下标
  ```

- **去除字符串首尾的空格：trim**

  ```javascript
  var str = '      hello world      ';
  //----------------------------去除字符串首尾的空格，中间的不管
  str = str.trim();// 返回去除首尾空格之后的字符串，重新赋值给str
  console.log(str);
  ```

- **字母大小写转换：toUpperCase、toLowerCase**

  ```javascript
  var myName = 'ZhangSan';
  //-----------------------------------每个英文字母转换成大写
  console.log(myName.toUpperCase());
  //-----------------------------------每个英文字母转换成小写
  console.log(myName.toLowerCase());
  ```



- **字符串拼接与截取：concat、slice、substring、substr**

  > 拼接——》+用的最多

  ```js
  var str1 = 'abc';
  var str2 = 'def';
  //----------------------拼接+用的最多
  console.log(str1 + str2);
  //------------------------拼接字符串（不用）会返回一个新字符串
  var newStr = str1.concat(str2);
  console.log(newStr);
  ```

  > 字符串的截取

  ```javascript
  var str = 'abcdefg';
  //-----------------------slice(begin,end)——》从begin开始，截取到end（有始无终）
  console.log(str.slice(1, 3)); 
  //-------------------------subString(begin,end)——》从begin开始，截取到end（有始无终）
  console.log(str.substring(1, 3)); 
  //------------------------subStr(begin,length)——》从begin开始，截取length个，包括begin
  console.log(str.substr(1, 3));  // bcd
  ```

---

- **将字符串分割成一个数组：split**

  > 和arr.join（）正好相反

  ```javascript
  // join 将数组的值拼接成一个字符串
  // split('分割符') 将字符串分割成一个数组, 返回值, 就是分割后得到的数组
  
  var str = 'a|b|c|d';
  //-----------------split('分割符'): 将字符串通过分隔符分割成一个数组, 返回分割后得到的数组
  var arr = str.split('|');
  console.log(arr);  // ["a", "b", "c", "d"]
  ```

- **字符串替换：replace**

  > 可以把字符串中特定字符替换掉

  ```javascript
  var words = '大菜鸡, 真坑啊!!! 大菜鸡, 大菜鸡';
  //-----------------------str.replace('aa','bb'):将str中的第一个aa替换成bb——》返回替换后的结果
  words = words.replace('菜鸡', '***');
  console.log(words);
  
  //--------------------------------------（拓展）替换所有的需要使用后面讲的正则——》g：全局
  words = words.replace(/菜鸡/g, '***')
  console.log(words);
  ```

---

##### ヾ(๑╹◡╹)ﾉ"字符串小练习

```javascript
//1. 截取字符串"我爱中华人民共和国"，中的"中华"
//2. "abcoefoxyozzopp"查找字符串中所有o出现的位置
//3. 把字符串中所有的o替换成!
//4. 把一个字符串中所有的空格全部去掉
```

##### ヾ(๑╹◡╹)ﾉ"字符串大练习

  ```js
// var str = 'my_name_is_jim_green';
// 需求: 变成驼峰命名  myNameIsJimGreen
  ```



##### 小作业

```js
// 1、将数组['赵云']，添加数据之后变成['马超','刘备','赵云','张飞','关羽','诸葛亮']

// 2、将数组['马超','刘备','赵云','张飞','关羽','诸葛亮']，通过数组的操作将首尾数据调换成['诸葛亮','刘备','赵云','张飞','关羽','马超']

// 3、将数组['诸葛亮','刘备','赵云','张飞','关羽','马超']中，'刘备'的后面增加'孙尚香'，在'关羽'的前面添加'貂蝉'

// 4、将学生数组的成绩按照从大到小排布，alert出成绩最高的同学的名字以及成绩是多少？
var arr = [
  {name: 'zs', age: 18, score: 33},
  {name: 'ls', age: 13, score: 64},
  {name: 'ww', age: 15, score: 87},
  {name: 'zl', age: 12, score: 100},
  {name: 'tq', age: 10, score: 77},
  {name: 'wb', age: 16, score: 68},
];

// 5、数组去重，去除下列数组中重复的名字
var arr = ['赵六','李四','王五','赵六','赵六','田七','李四','王五','王五','张三','王五','李四','张三','王五','李四','张三','李四','张三','李四','田七','李四','田七','田七','王五','田七','李四','李四','李四'];

// 6、把字符串'my-name-is-cool-man',转换成'myNameIsCoolMan'

// 7、（拓展题） 统计出下列数组中每个名字出现的次数（可以储存到对象中去）
var arr = ['赵六','李四','王五','赵六','赵六','田七','李四','王五','王五','张三','王五','李四','张三','王五','李四','张三','李四','张三','李四','田七','李四','田七','田七','王五','田七','李四','李四','李四'];

















// 拓展题答案----------------------------------------------------
// 1、创建一个对象，用于统计——》其中属性名为对应的名字，属性为出现的次数，
var obj = {};

// 2、遍历数组，
//  1、如果名字在对象中有该属性，则让该属性的属性值（即：次数）+1。
//  2、如果名字在对象中没有该属性，则表示第一次遇到这个名字，创建该名字为属性名，属性值统计为1即可
for ( var i = 0 ; i < arr.length ; i++ ) {

  // 判断当前名字在对象中有没有储存过——》注意arr[i]是变量，作为属性名访问数据，需要通过中括号语法
  if ( obj[arr[i]] === undefined  ) {
    // 1、如果属性值是undefined，则表示第一次遇到该名字，之前并未出现，在对象中创建这一项并且计数为1
    obj[arr[i]] = 1;
  } else {
    // 2、如果属性值不是undefined，则表示不是第一次遇到该名字，只需要把其次数（即：属性值）+1
    obj[arr[i]] += 1;
  }

}

// 最后看对象就可以知道结果了
console.log( obj );
```

