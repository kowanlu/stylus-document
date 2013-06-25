## 变量 ##

我们可以声明变量，并在整个样式表中使用：

``` css
 font-size = 14px

 body
   font font-size Arial, sans-serif
```

编译CSS为：

``` css
 body {
   font: 14px Arial, sans-serif;
 }
```

变量甚至可以包含在表达式中：

``` css
font-size = 14px
font = font-size "Lucida Grande", Arial

body
  font font sans-serif
```

编译CSS为：

``` css
body {
  font: 14px "Lucida Grande", Arial sans-serif;
}
```

标识符 （变量名、 函数等） 也可以是`$`开始。例如：

``` css
$font-size = 14px
body {
  font: $font-size sans-serif;
}
```

## 属性查找 ##

Stylus另一个很酷的、特有功能就是可以不用定义变量而引用属性。
另一个很酷的功能独有的手写笔是而不将它们的值分配给变量定义的引用属性的能力。下面是个很好的例子，让元素水平垂直居中对齐（典型的方法是使用百分比和margin负值）：

``` css
 #logo
   position: absolute
   top: 50%
   left: 50%
   width: w = 150px
   height: h = 80px
   margin-left: -(w / 2)
   margin-top: -(h / 2)
```

我们可以不使用变量`w`和`h`，而是简单地通过`@`字符获取属性对应的值：

``` css
 #logo
   position: absolute
   top: 50%
   left: 50%
   width: 150px
   height: 80px
   margin-left: -(@width / 2)
   margin-top: -(@height / 2)
```

另外一种使用情况就是在混合中根据其他属性来定义属性值。在下面这个例子中，我们定义在z-index未被指定情况下默认值为1。

``` css
  position()
    position: arguments
    z-index: 1 unless @z-index

  #logo
    z-index: 20
    position: absolute

  #logo2
    position: absolute
```

属性查找通过"冒泡"方式直到找到相应的值，或该属性不存在则返回null。在以下示例中， @color被解析为blue:

``` css
  body
    color: red
    ul
      li
        color: blue
        a
          background-color: @color
```