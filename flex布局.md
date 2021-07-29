### 1、block, inline, inline-block, flex



```css
// 默认样式block(块级元素)
display: inline-block;//一般display属性,我们设置为flex,flex布局

// flex 弹性盒子布局, 容器设置为flex并不会取消容器块级元素的特性
// inline-flex：将对象作为内联块级弹性伸缩盒显示
display: flex;//一旦设置为flex,它里面的子元素就不再是块级元素,子元素设置display是无效的,默认容器里的元素横向排列.
```

### 2、flex-direction 排列方式



```css
// row colum row-reverse colum-reverse
flex-direction: column //竖直排列
flex-direction: row-reverse; //横向倒序排列,对齐方式发生改变,靠右对齐

// 如果容器不设置宽高, 宽度默认占满屏幕100%, 高度默认自适应(根据容器里子元素的高度)
```

### 3、justify-content 主轴对齐方式, align-items 交叉轴对齐方式



```css
// flex-start flex-end center 
// justify-content独有属性:space-between、space-around(等距分布, 子元素两侧距离相等)
// align-items独有属性: base1line(让相邻元素里面的文字基线对齐)、stretch(让容器里子元素呈现一个拉伸的效果)
```

### 4、flex-wrap换行



```css
// 小程序处理: 如果总元素的宽度大于屏幕宽度,然后没有设置让它换行,它会让容器里面的元素重新分配宽度,相当于 总宽度/n个元素 这样一个宽度.
// nowrap(默认,不换行)、 wrap(换行, 换行后的元素平均间距居中显示,消除间距的方法:容器高度等于子元素换行后高度) 
```

