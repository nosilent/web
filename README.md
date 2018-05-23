

# css



## grid



### track-repeat

```
grid-template-columns: repeat(4, 30px 100px);
```

​	等同于：

```
grid-template-columns: 30px 100px 30px 100px 30px 100px 30px 100px;
```



### grid-template

​	`grid-template`是`grid-template-columns`和`grid-template-rows`和`grid-template-areas`的简写方式。

```
grid-template: none | [ <‘grid-template-rows’> / <‘grid-template-columns’> ] | [ <line-names>? <string> <track-size>? <line-names>? ]+ [ / <explicit-track-list> ]?	
```

​	`none`：设置3个属性的初始值为none。

#### grid-template-areas

​	`grid-template-areas`为对应的栅格命名。

```
grid-template-areas: "logo stats"
                       "score stats"
                       "board board"
                       "... controls";
```

通过`grid-area`就对应栅格分配给具体元素：

```
.logo { grid-area: logo; }
```



### grid-grap

​	是grid-template-grap和 grid-row-gap简写方式。指定栅格间的间隙，栅格边缘不适用。属性值可为任意css长度值或百分比。

```
grid-gap: <‘grid-row-gap’> <‘grid-column-gap’>
```

​	当只有一个值时，表示间隙相同。

### grid-items

- row-start line

- row-end line

- row span

- column-start line

- column-end line

- column span

  

  `grid-column-star`值大于`grid-column-end`时，交换两个值；当两个值相同时，会忽略`end line`的值。

```
.grid__item { grid-column-start: 5; grid-column-end: 2; }
等同于：
.grid__item { grid-column-start: 2; grid-column-end: 5; }
```



​	`start line`和`end line`指定了`span`时，`end line`会被忽略。

```
.grid__item { grid-column-start: span 3; grid-column-end: span 2; }
等同于：
.grid__item { grid-column-start: span 3; }
```



​	`span`指定了一个栅格名，则会当成`span 1`

```
.grid__item { grid-column-start: span [foo]; }
.grid__item { grid-column-start: span 1; }
```



### grid-row和grid-column

​	`grid-row`是`grid-row-start`和 `grid-row-end`的简写方式；

​	`grid-column`是`grid-column-start`和 `grid-column-end`的简写方式；

```
grid-row: <grid-line> [ / <grid-line> ]? 
grid-column: <grid-line> [ / <grid-line> ]?
```



### grid-area

```
grid-area: <grid-line> [ / <grid-line> ]{0,3}
```

​	定义4个边界的栅格线，顺序分别表示 `row start / column-start / row-end / column-end` ，后3个值是可选的。



### grid Alignment

#### justify-content

```
justify-content: center | start | end | space-between | space-around | space-evenly
```

​	用于设置各栅格域相对于栅格容器水平方向对齐属性，栅格容器属性。



#### align-content

```
align-content: center | start | end | space-between | space-around | space-evenly
```

​	用于设置各栅格域相对于栅格容器边界垂直方向对齐属性，栅格容器属性。



#### justify-items

```
justify-items: center | start | end | stretch
```

​	用于设置各栅格域相对于自身边界水平方向对齐属性，栅格容器属性。



#### align-items

```
align-items: center | start | end | stretch
```

​	用于设置各栅格域相对于自身边界垂直方向对齐属性，栅格容器属性。



#### justify-self

```
justify-self: center | start | end | stretch
```

​	用于设置栅格域相对于自身边界水平方向对齐属性，栅格域属性。



#### align-self

```
align-self: center | start | end | stretch
```

​	用于设置栅格域相对于自身边界垂直方向对齐属性，栅格域属性。



## media query 

```
@media [not | only] <media-type> [and] (<media-condition>);
```



### Media types

- all  :所有设备
- print  :打印设备
- screen  :显示设备
- speech  :阅读设备



## Function



### attr() 

​	`attribute `的缩写，返回元素指定属性的值，没有对应的属性将返回空字符串。

```
a[href]::after {
    content: attr(href);
```



### calc() 

​	可实现四则运算，将计算结果作为对应属性的值。不同类型的属性值不能计算，同一类型不同单位的属性值可以计算。

```
margin: calc(1rem - 2px) calc(1rem - 1px);
background-image: linear-gradient(to right, silver,white 50px,white calc(100% - 50px),silver);
width: calc(100% / 6 * 5);
width: calc(100% - 20px)
```



### hsl() hsla()

​	设置颜色的函数。

``` 
hsl(200, 10%, 50%) 
hsla(200, 100%, 50%, .1)
```

- 第一个值表示颜色，用度数表示；red = 0° = 360° ，green = 120°, blue = 240°，可以为负值或超过360°。
- 第二个值表示饱和度，用百分比表示。1或100%表示满饱和度，0%表示灰色。
- 第三个值表示亮度，用百分比表示。100%表示白色，0%表示黑色，50%表示正常。
- 第四个值表示透明度，用0~1表示。0表示全透明，1表示不透明。



### inset() 

```  
inset() = inset( [offset]{1,4} [round <border-radius>]? )
offset = <length> | <percentage>
```

​	在内部定义一个矩形，与margin等同。设置1到4个值。

``` 
inset(10% 20% round 5px);
```

​	round后值表示矩形圆角，与border-radius等同。



### linear-gradient() 

​	线性渐变，从一个颜色值到另一个颜色值。渐变方向可以是水平、垂直、对角、任一角度。

``` 
linear-gradient(angle/direction, color stop, color stop, ...);
```

- angle：表示渐变起点。`0deg` 表示下到上 ，相当于`to top`;`90deg`表示左到右,相当于`to right` ;`180deg`表示从上到下，相当于`to bottom`;`270deg`表示从右到左，相当于`to left`。
- direction：`to top left`, `to top right`, `to bottom right`,  `to bottom left`. 

```
//从左到右，0%处为yellow，50%处为#009966,100%处为purple
linear-gradient(to right, yellow, #009966,purple);
//从左到右，0%处为yellow，20%~80%为#009966,100%处为purple
linear-gradient(to right, yellow, #009966 20%, #009966 80%, purple);
//从左到右，0%~20%为yellow，20%~80%为#009966,80%~100%为purple
linear-gradient(to right, yellow, yellow 20%, #009966 20%, #009966 80%, purple 80%, purple);
```

- 颜色起止点位置可以是绝对长度px、em等或百分比，必须在颜色值后面指定，在颜色前面指定无效。必须按大小顺序指定。
- 若第一个和最后一个颜色没有指定起止点位置，则默认分别为0%和100%。

```
linear-gradient(red, white 20%, blue);
linear-gradient(red 0%, white 20%, blue 100%);
```

- 若一个颜色指定位置小于前一个颜色指定位置，则为前一个指定位置.没有指定位置的为前后两端的中点值。

``` 
linear-gradient(red 80px, white 0px, black, blue 100px);
linear-gradient(red 80px, white 80px, black 90px, blue 100px);
```

#### Repeating Gradients 

​	可以使用 repeating-linear-gradient()创建重复渐变，也可以用background-size和background-repeat创建。



### radial-gradient() 

```
radial-gradient(circle at 0% 50%, yellow, #009966, purple);
```

- center：定义径向渐变的开始位置。默认位置为中心。
- ending shape：定义渐变的形状。圆`circle` 或椭圆 `ellipse` 。
- color stops ：颜色起止位置。



#### size

```
radial-gradient(100px circle at 0% 50%, yellow, #009966, purple);
```

​	大小在位置前指定。百分比只能用来指定椭圆。

```
radial-gradient(200px 100px ellipse at 25% 50%, yellow, #009966, purple);
```

​	第一个值表示椭圆的水平半径，第二个值表示椭圆的垂直半径。

- **closest-side:**  渐变中心到渐变容器最近的边。
- **farthest-side:** 渐变中心到渐变容器最远的边。
- **closest-corner:** 渐变中心到渐变容器最近的角。
- **farthest-corner:** 渐变中心到渐变容器最远的角，默认值。