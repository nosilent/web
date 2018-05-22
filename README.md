[TOC]

## grid

```
.grid {
  display: grid;
  width: 750px;
  grid-template-columns: 150px 1fr 2fr;
}
```

![1526954755083](C:\Users\ADMINI~1\AppData\Local\Temp\1526954755083.png)



```
.grid {
  display: grid;
  grid-template-columns: min-content max-content auto;
}
```

![1526954820135](C:\Users\ADMINI~1\AppData\Local\Temp\1526954820135.png)

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
