### boxShadow

boxShadow属性把一个或多个下拉阴影添加到框上。该属性是一个用逗号分隔阴影的列表，每个阴影由 2-4 个长度值、一个可选的颜色值和一个可选的 inset 关键字来规定。省略长度的值是 0

`box-shadow: h-shadow v-shadow [blur spread color inset]`

- `h-shadow` 水平阴影的位置。允许负值
- `v-shadow` 垂直阴影的位置。允许负值
- `blur` 模糊距离
- `spread` 阴影大小
- `color` 阴影颜色
- `inset` 从外层的阴影（开始时）改变阴影内侧阴影

### transform 实现2D/3D转换

- translate()方法，根据左(X轴)和顶部(Y轴)位置给定的参数，从当前元素位置移动。

  `transform: translate(50px,100px)`

  2D转换可以单独指定translateX、translateY属性；定义3D转换时可以额外单独指定translateZ属性；

- rotate()方法，在一个给定度数顺时针旋转的元素。负值是允许的，这样是元素逆时针旋转。

  `transform: rotate(30deg)`

  只有定义3D转换时可以单独指定rotateX、rotateY、rotateZ属性；

- scale()方法，该元素增加或减少的大小，取决于宽度（X轴）和高度（Y轴）的参数。

  `transform: scale(2,3)`

  scale（2,3）转变宽度为原来的大小的2倍，和其原始大小3倍的高度

  2D转换可以单独指定scaleX、scaleY属性；定义3D转换时可以额外单独指定scaleZ属性；

- skew()方法，包含两个参数值，分别表示X轴和Y轴倾斜的角度，如果第二个参数为空，则默认为0，参数为负表示向相反方向倾斜。

  `transform: skew(30deg,20deg)`

  2D转换可以单独指定skewX、skewY属性，不能进行3D转换

### transition 实现过渡

需要指定要添加效果的CSS属性和效果的持续时间； 如果未指定的期限，transition将没有任何效果，因为默认值是0；要添加多个样式的变换效果，添加的属性由逗号分隔。

`transition: width 2s, height 2s, transform 2s;`

### CSS3弹性盒子

弹性盒子由弹性容器(Flex container)和弹性子元素(Flex item)组成，弹性容器通过设置 display 属性的值为 flex 或 inline-flex将其定义为弹性容器，弹性容器内包含了一个或多个弹性子元素。弹性容器外及弹性子元素内是正常渲染的。弹性盒子只定义了弹性子元素如何在弹性容器内布局。

- `flex-direction` 属性指定了弹性子元素在父容器中的位置。
  - `row`(从左到右) 默认
  - `row-reverse`(从右到左) 
  - `column`(从上到下) 
  - `column-reverse`(从下到上)
- `justify-content`属性应用在弹性容器上，把弹性项沿着弹性容器的主轴线（main axis）对齐
  - `flex-start`：弹性项目向行头紧挨着填充。（默认值）
  - `flex-end`：弹性项目向行尾紧挨着填充
  - `center`：弹性项目居中紧挨着填充。（如果剩余的自由空间是负的，则弹性项目将在两个方向上同时溢出）
  - `space-between`：弹性项目平均分布在该行上。如果剩余空间为负或者只有一个弹性项，则该值等同于flex-start。否则，第1个弹性项的外边距和行的main-start边线对齐，而最后1个弹性项的外边距和行的main-end边线对齐，然后剩余的弹性项分布在该行上，相邻项目的间隔相等。
  - `space-around`：弹性项目平均分布在该行上，两边留有一半的间隔空间。如果剩余空间为负或者只有一个弹性项，则该值等同于center。否则，弹性项目沿该行分布，且彼此间隔相等（比如是20px），同时首尾两边和弹性容器之间留有一半的间隔（1/2*20px=10px）。
- `align-items` 设置或检索弹性盒子元素在侧轴（纵轴）方向上的对齐方式
  - `flex-start`：弹性盒子元素的侧轴（纵轴）起始位置的边界紧靠住该行的侧轴起始边界
  - `flex-end`：弹性盒子元素的侧轴（纵轴）起始位置的边界紧靠住该行的侧轴结束边界
  - `center`：弹性盒子元素在该行的侧轴（纵轴）上居中放置。（如果该行的尺寸小于弹性盒子元素的尺寸，则会向两个方向溢出相同的长度）。
  - `baseline`：如弹性盒子元素的行内轴与侧轴为同一条，则该值与'flex-start'等效。其它情况下，该值将参与基线对齐。
  - `stretch`：如果指定侧轴大小的属性值为'auto'，则其值会使项目的边距盒的尺寸尽可能接近所在行的尺寸，但同时会遵照'min/max-width/height'属性的限制。(默认)
- `flex-wrap`  属性用于指定弹性盒子的子元素换行方式.
  - `nowrap ` 弹性容器为单行(默认)
  - `wrap ` 弹性容器为多行。该情况下弹性子项溢出的部分会被放置到新行，子项内部会发生断行
  - `wrap-reverse` 反转 wrap 排列
- `align-content` 属性用于修改 `flex-wrap` 属性的行为。类似于 `align-items`, 但它不是设置弹性子元素的对齐，而是设置各个行的对齐
  - `stretch` 默认。各行将会伸展以占用剩余的空间。
  - `flex-start` 各行向弹性盒容器的起始位置堆叠。
  - `flex-end` 各行向弹性盒容器的结束位置堆叠。
  - `center` 各行向弹性盒容器的中间位置堆叠。
  - `space-between` 各行在弹性盒容器中平均分布。
  - `space-around` 各行在弹性盒容器中平均分布，两端保留子元素与子元素之间间距大小的一半。
- 子元素属性
  - `order：int`  排序：用整数值来定义排列顺序，数值小的排在前面。可以为负值。
  - 设置"margin"值为"auto"值，自动获取弹性容器中剩余的空间。所以设置垂直方向margin值为"auto"，可以使弹性子元素在弹性容器的两上轴方向都完全居中。
  - 设置 `margin: auto;` 可以使得弹性子元素在两上轴方向上完全居中
  - `align-self` 属性用于设置弹性元素自身在侧轴（纵轴）方向上的对齐方式。
    - `auto`：如果'align-self'的值为'auto'，则其计算值为元素的父元素的'align-items'值，如果其没有父元素，则计算值为'stretch'。
    - `flex-start`：弹性盒子元素的侧轴（纵轴）起始位置的边界紧靠住该行的侧轴起始边界。flex-end：弹性盒子元素的侧轴（纵轴）起始位置的边界紧靠住该行的侧轴结束边界。
    - `center`：弹性盒子元素在该行的侧轴（纵轴）上居中放置。（如果该行的尺寸小于弹性盒子元素的尺寸，则会向两个方向溢出相同的长度）。
    - `baseline`：如弹性盒子元素的行内轴与侧轴为同一条，则该值与'flex-start'等效。其它情况下，该值将参与基线对齐。
    - `stretch`：如果指定侧轴大小的属性值为'auto'，则其值会使项目的边距盒的尺寸尽可能接近所在行的尺寸，但同时会遵照'min/max-width/height'属性的限制。
  - `flex` 属性用于指定弹性子元素如何分配空间。（一般用数值）

### CSS3媒体查询
`@media not|only|all mediatype and (expressions) { CSS 代码...;}`

`mediatype`：all 所有设备、print打印机、screen屏幕设备如手机平板电脑等、speech屏幕阅读器

`expressions`：min-width最小宽度 max-width最大宽度