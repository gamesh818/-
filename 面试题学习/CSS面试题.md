### 1.介绍一下CSS的盒子模型

- 标准盒子模型

![](E:\github仓库\Study-the-warehouse\面试题学习\img\标准盒子模型.jpg)

- IE盒子模型

![](E:\github仓库\Study-the-warehouse\面试题学习\img\IE盒子模型.jpg)

```js
CSS的盒子模型有哪些： 标准盒子模型、IE盒子模型

CSS的盒子模型的区别：
	标准盒子模型：margin、border、padding、content
	IE盒子模型：margin、content（包含boder+padding+content）

如何通过CSS转换盒子模型：
	box-sizing：content-box  // 默认标准版盒子模型
	box-sizing: border-box  // IE盒子模型
```



### 2. line-height 和 height的区别

```
height是一个死值，就是这个盒子的高度。
line-height是每一行文字的高度值，文字换行盒子高度会增加（行数*行高）

```



### 3. Css选择符有哪些？哪些属性可以继承？

```css
CSS选择符：
通配符（*）
id选择器（#）
类选择器（.）
标签选择器（div、p、li、...）
相邻选择器（+）
后代选择器（ul li） [ul和li之间是空格]
子元素选择器(>)
属性选择器（a[xxx]）   [xxx]中的是标签内的属性 类似vue的 v-date-xxx


哪些属性可以继承：
	文字系列：font-size、color、line-height、text-align...
哪些不能继承：border、margin、padding...
```



### 4.CSS优先级算法如何计算？

```css
- 优先级比较：
!important>内联样式(标签里写style)>id选择器(#id)>类选择器(.class)>标签选择器(div、h1)>统配符选择器(*)>子选择器(ul<li)>后代选择器(ul空格li)>伪类选择器(a:hover,li:nth-child)>继承得来的属性

- css权重算法：
1.内联样式(style)	权重：1000
2.id选择器			权重：100
3.类选择器			权重：10
4.标签&伪类元素选择器 权重：1
5.统配(*)、>、+		权重：0

例子:
1  1    10  = 12
ul li .list1{
	background:blue;    
}
  10   = 10
.list1{
	background:red;    
}

12 > 10 权重值高就会覆盖

```



### 5.用CSS画一个三角形

```css
使用边框(border)画

div{
    width:0;
    height:0;
    /*哪个方向需要为三角形的底 就在哪个方向给颜色*/
    border-top:100px solid #ccc;
    border-bottom:100px solid tansparent;
    border-left:100px solid tansparent;
    border-right:100px solid tansparent;
        
}


宽高设为0，把左上右边框颜色都设置为透明，然后bottom给一个尺寸
```



### 6.一个盒子不给宽高如何水平居中

```css

<div class='container'>
	<div class='main'> main </div>
</div>
 

/*方法一：flex方式 */
关键代码： display:flex;  justify-content:center(主轴方向); align-items:center(侧轴方向);
        .container{
            width: 500px;
            height: 500px;
            border: 1px solid #ccc;

            display:flex;
            justify-content:center;
            align-items:center;
        }
        .main{
            background:red
        }

/*方拾二：定位方式配合transform:translate*/
        .container{
            width: 500px;
            height: 500px;
            border: 1px solid #ccc;

            position: relative;
        }
        .main{
            background:red;
            position: absolute;
            top: 50%;
            left: 50%;
            transform:translate(-50%,-50%)
        }

```





### 7.display有哪些值？说明他们的作用

```
1.none; 		隐藏元素
2.block; 		把某元素转化为块元素
3.inline; 		把某元素转化为行内元素
4.inline-block; 把某元素转化为行内块元素
```





### 8.对BFC的理解（块级格式化上下文）

```html
BFC就是页面上一个隔离的独立容器，容器里面的子元素不会影响到外面的元素。

1.了解BFC： 块级格式化上下文
2.BFC原则： 如果一个元素具有BFC，那么内部元素再怎么弄也不会影响外面的元素。
3.如何触发BFC：
	- float(浮动)的值非none
	- overflow的值非visible
	- display的值为： inline-block、table-cell...
```



### 9.清除浮动有哪些方式？

```css
1.触发BFC (overflow:hindden)
2.多创建一个盒子，添加clear:both；
3.*重要* 加一个after伪类元素 
ul:after{
    content:'';
    display:block.;
    clear:both;
}
```



### 10.在网页中应该使用奇数还是偶数的字体？为什么？

```
- UI设计图，一般设计时候使用偶数，布局方便，转化px也方便
- 偶数 让文字在浏览器上表现更好看
```



### 11.position（定位）有哪些值？分别是根据什么定位的？

```
static [默认值]	 没有定位
fixed  [固定定位]	相对于浏览器窗口进行定位
relative [相对定位]	相对于自身定位
absolute [绝对定位] 相对于第一个有relative的父元素，脱离文档流

relative和absolute的区别
1.relative不脱离文档流，absolute脱离文档流
2.relative相对于自身，absolute相对于第一个有relative的父元素
3.relative如果有 left、right、top、bottom  只能存在left、top  （有left不能有right，有top不能有bottom）
  absolute都能存在

```



### 12.响应式

```css
一个url响应多端

语法：@emdia only screen and (条件 max-width) {代码块}
only:可以排除不支持媒体查询的浏览器
screen:设备类型
max-width | max-height | min-width | min-height

当屏幕小于1000的时候 隐藏最后一个元素
@emdia only screen and (条件 max-width:1000px){
	ul li:last-child{
		display:none;
	}
}

```

































