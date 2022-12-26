# grid布局

### 1.介绍
- flex 布局是轴线布局，只能指定‘项目’ 针对轴线的位置，可以看作
是一维布局。grid布局则是将容器划分成行和列，产生单元格，然后指定
‘项目所在’的单元格，可以看作是二维布局，grid布局远比flex布局
强大

### 2.基本概念
1.容器——有容器属性（container）

2.项目——有项目属性（items）

### 3.属性值
#### 1. 容器属性
   ##### 1.1 grid-template
```css
  /*  
  grid-template-*
  你想要多少行或者列，就填写相应属性值的个数，不填写自动分配
    
  */
/*三行两列 每个项目的大小都是100*100*/
    grid-template-columns:100px 100px;
    grid-template-rows:100px 100px 100px;

/*简便写法*/
/*grid-template-cloumns:repeat(行数or列数/宽度值or高度值)*/
    gorid-template-cloumns:repeat(2,100px);

/*auto-fill 有时，单元格的大小是固定的，但是容器的大小不确定，这个属性就会自动填充*/
    grid-template-columns：repeat(auto-fill,100px)

/* fr 为了方便表示比例关系，网格布局提供了fr关键字 （fraction的缩写，意为片段）*/
    grid-template-columns:repeat(4,1fr) //分为四份 宽度平均分为四份
/* minmax() 函数产生一个长度范围，表示长度就在这个范围之中它接受两个参数，分别为最小值和最大值*/
	grid-template-columns:1fr minmax(150px,1fr)
/* auto,表示由浏览器自己决定长度 */
	grid-template-columns:100px auto 100px;
/* 网格线 可以用方括号定义网格线名称，方便以后定位引用*/
	gird-template-columns:[c1] 100px [c2] 100px [c3] 100px [c4]//此为三列 四条线
```
##### 1.2column-gap/row-gap
item之间相互的间距
```css
    column-gap:20px;
    row-gap:20px;
    /* 上面两条可以简写为下面一条 */
    gap:20px;

```
##### 1.3grid-template-areas
一个区域由单个或多个单元格组成，由你决定（具体使用，需要在项目属性里面设置）
```css
    grid-template-areas:'a b c' 'd e f' 'g h i'
 /*
 区域不利用可以使用.来表示
 区域的命名会影响到网格线每个区域的起始网格线 会自动命名为区域名-start 终止网格线自动命名为区域名-end
 */   
 grid-template-areas：'a . c' 'd . f' 'g . i'
```
##### 1.4grid-auto-flow
划分网格以后，容器的子元素会按照顺序，自动放置在每一个网格 默认的放置顺序是先行后列即先填满第一行再开始放第二行（就是子元素的排放顺序）
```css
grid-auto-flow:row
grid-autoflow:column

/* dance  将容器填充好*/
grid-auto-flow：row dance；
```
##### 1.5justify-item（水平方向）/align-items（垂直方向）
相对与间距来排列这些内容
```css
justify-item：start | end | center | strech（填充满）

/*当设置了两个方向的排列顺序时可以使用*/
palce-items：center strech
```
 ##### 1.6 justify-content/ailgn-content
相对与容器来排列这些内容
```css
	justify-content:start | end | cemter | strech | space-around | space-between | space-evenly
```

##### 1.7grid-auto-columns /grid-auto-rows
用来设置多出来的项目宽和高
```css
grid-auto-rows：50px
3*3的元素 但是实际有10个 整个属性就是用来设置多出来的项目
```

#### 2.元素属性
 ##### 2.1 grid-columns-start/grid-columns-end/grid-row-start/grid-row-end
用来指定item的具体位置 根据在那根网格线
```css
/*列方向 占用从第一根到第三根*/
gird-columns-start：1
gird-columns-end：3
gird-columns-strat：span 3 //span表示占几个位置 start 是从左往右 end 是从右往左
```
##### 2.2grid-column/grid-row
grid-column属性是grid-column-start和grid-column-end的合并简写
grid-row属性是grid-row-start和grid-row-end的合并简写
```css
grid-column：1/3  开始为1 结束为3
```
##### 2.3gird-area
指定项目放在哪一个区域
```css
	grid-template-areas:'a b c' 'd e f' 'g h i'

	grid-area: b

	可以将 
	grid-column-start：1;
	grid-column-end：3;
	grid-row-start：2;
	grid-row-end：4;
	简写为
	grid-area：2/1/4/3
```
##### 2.4justify-self/align-self/place-self
设置单元格内容的水平or垂直的位置

##### 2.5order
可以使用order重写它的顺序类似 z-index