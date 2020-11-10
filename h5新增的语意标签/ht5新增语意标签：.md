1. ### ht5新增语意标签：

1. 说明：这些布局标签都是块级元素，用法和div一样，只不过比div多了一些语意。

   | header  | 网页的头部   |
   | :-----: | ------------ |
   |   nav   | 网页的导航栏 |
   | footer  | 网页的底部   |
   |  aside  | 网页的侧边栏 |
   | section | 网页的区块   |
   | article | 网页的文章   |

1. html中新增的表单，更多的针对移动端。

   | url    | 限制用户输入的必须为url格式（如：网址）      |
   | ------ | -------------------------------------------- |
   | email  | 限制用户啊输入必须为email格式                |
   | date   | 限制用户输入必须为日期格式（显示日期选择框） |
   | time   | 限制用户必须为时间类型（显示时间选择框）     |
   | month  | 限制用户必须为月类型（显示月选择框）         |
   | week   | 限制用户必须为周类型（显示日选择框）         |
   | color  | 显示颜色选择器                               |
   | tel    | 手机号输入（移动端生效）                     |
   | search | 搜索框                                       |
   | number | 输入数字格式                                 |

2. 表单属性：

   1. placeholder：占位符
   2. autofocus：自动获取焦点
   3. autocomplete：on（打开）off（关闭）
   4. Required：该选项是必填的，不填无法提交

3. 多媒体标签：在网页中播放音乐。

   1. 音频标签：audio <audio src="" controls></audio>
      1. 属性：
         1. src：路径
         2. controls：播放的控制按钮
         3. autoplay:自动播放
         4. loop：循环播放
      2. 注意；只支持：mp3 wav ogg
   2. 视频标签：video
      1. 属性：
         1. src：路径
         2. controls：播放的控制按钮
         3. autoplay:自动播放
         4. loop：循环播放
         5. muted：静音播放

1. ### css3

   1. 找到页面中有class属性的div标签：div[ class ]{ }

      1. 找到页面中有class属性并且class属性为verypurple的div标签:div[ class="verypuple"]

      1. 找到页面中有class属性并且class属性中以very开头的div
         ：div[ class^="very"]. 以#结尾div[ class$="#"] 中间有# div[ class*="#"]

      1. 属性选择器用于选择input标签更多。input[type="text"]

   2. 文字阴影：text-shadow

      1. 取值：水平偏移量 垂直偏移量 模糊度 阴影颜色

   3. 盒子阴影：box-shadow

      1. 属性值：水平偏移量 垂直偏移量 模糊度（外延值） 阴影的颜色（内阴影 inset）

   4. 背景图片的大小：background-size

      1. 取值：
         1. 数字+px
         2. 百分比
         3. 关键字
            1. contain：将背景图等比例缩放，直到不会超出盒子的最大
               1. 优点：图片不会变形
               2. 缺点：盒子可能会留白
            2. cover：将图片等比例缩放，直到填满整个盒子没有空白。
               1. 优点：等比例缩放，图片不会变形
               2. 缺点：图片可能会超出。
      2. 缺点：图片可能变形
      3. 注意点：background-size

   5. 背景渐变

      1. 线性渐变：沿着一个方向颜色进行线性渐变
         1. 属性名：background-image
         2. 属性值：linear-gradient（ 方向，颜色  范围，颜色  范围）
            1. 方向：默认是从上往下渐变的
               1. 取值：to+方位名词
               2. 度（deg），0deg从下往上，值越大，顺时针转
            2. 范围：%

   6. 径向渐变：由中心向四周渐变

      1. 属性名：background-image
      2. 属性值：radial-gradient（半径 at 圆心的位置，颜色 范围，颜色 范围）
         1. 圆心的位置：和background-position一样
            1. 关键字：
            2. 数字+px

   7. 滤镜：filter

      1. blur（）模糊度  <html>filter:blur(0px)</html>
      2. Filter:grayscale(%);灰度

