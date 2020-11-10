1. ### css动画属性

   1. #### 过渡属性：transition

      1. 属性值：时间（秒）
      2. 作用：让元素的样式慢慢的变化
      3. 注意点：
         1. 过渡应该给需要过渡的元素本身设置
         2. 如果需要看到过渡的效果，需要保证两个状态的样式不同。
         3. 过渡给不同状态设置，效果是不同的 
         4. 移入和移出都有，要给默认状态设置，移入有效果，移出没有要给效果设置。

   2. #### 2D转换（transform）

      1. 说明：元素在平面上，进行实现缩放，旋转等

      2. 属性名：transform

      3. ##### 属性值：scale

         1. 取值：

            1. scaleX（倍数）：沿着水平方向进行缩放
            2. scaleY（倍数）：沿着垂直方向进行缩放
            3. scale（x，y）<!--transform:scale(2,2)-->
            4. 转换原点：属性名：transform-origin
               1. 属性名：和background-position一样的
                  1. 方位名词
                  2. 数字+px（坐标）
                  3. <html>transform-origin:center bottom </html>

         2. ##### 旋转：rotate

            1. 属性名：transform
            2. 属性值：rotate（旋转的角度：deg）
            3. <html>transform:rotate(360deg)</html>

         3. ##### 平移

            1. 属性名：transform
            2. 属性值：translate
               1. 取值：translateX（距离）：沿着X轴水平平移
                  1. translateY；沿着y轴垂直方向平移
            3. 注意点：
               1. 平移的取值可以是数字+px，也可以是百分比（相对于自己的宽和高）
               2. 平移之后的元素，不会影响其他元素的布局（类似相对定位）

         4. 注意：在合写的时候先写选择那样X轴会跟着选择。

   3. 3D转换（transform）

      1. perspective：视距：
         1. 作用：给子元素添加近大远下的视觉效果
         2. 取值：
            1. 如果取值越小，表示距离越近，近大远小的效果越明显
            2. 如果取值越大，表示距离越远，近大远小的效果不明显。
      2. transform：旋转
         1. 属性名：transform
         2. 属性值：当旋转沿着x轴和y轴旋转时，此时就是3D旋转.
      3. 