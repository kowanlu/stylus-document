## 选择器(Selectors) ##

### 缩进 ###

Stylus类似于Python，通过缩进对齐表达代码逻辑，如下所示：

``` css
body
  color white
```

编译CSS为：

``` css
body {
  color: #fff;
}
```

如果愿意，你也可以使用冒号分隔符：

``` css
body
  color: white
```

### 规则集 ###

Stylus就像CSS一样，允许你使用逗号同时给多个选择器定义属性。

``` css
textarea, input
  border 1px solid #eee
```

同样可以用换行达到一样效果：

``` css
textarea
input
  border 1px solid #eee
```

编译CSS为：

``` css
textarea,
input {
  border: 1px solid #eee;
}
```

该规则唯一例外就是属性选择器。例如，下面的`foo bar baz`可能一个属性或一个选择器：

``` css
foo bar baz
> input
  border 1px solid
```

所以出于这个原因（或者首选解决方法），我们使用逗号分隔：

``` css
foo bar baz,
form input,
> a
  border 1px solid
```

### 父级引用 ###

字符`&`表示父级选择器。下面的示例中,我们两个选择器 （textarea和input）通过:hover伪选择器都改变了color色值。

``` css
textarea
input
  color #A7A7A7
  &:hover
    color #000
```

编译CSS为：

``` css
textarea,
input {
  color: #a7a7a7;
}
textarea:hover,
input:hover {
  color: #000;
}
```

下面这个例子，在IE浏览器利用了父级引用以及混合来实现宽度为`2px`的边框。

``` css
  box-shadow()
    -webkit-box-shadow arguments
    -moz-box-shadow arguments
    box-shadow arguments
    html.ie8 &,
    html.ie7 &,
    html.ie6 &
      border 2px solid arguments[length(arguments) - 1]

  body
    #login
      box-shadow 1px 1px 3px #eee
```

编译CSS为：

``` css
  body #login {
    -webkit-box-shadow: 1px 1px 3px #eee;
    -moz-box-shadow: 1px 1px 3px #eee;
    box-shadow: 1px 1px 3px #eee;
  }
  html.ie8 body #login,
  html.ie7 body #login,
  html.ie6 body #login {
    border: 2px solid #eee;
  }
```

### 消除歧义 ###

像`padding - n`这样的表达式，既可以被解释成减法运算，也可以被解释成一元减号。为了避免这种歧义，用括号包裹表达式：

``` css
pad(n)
  padding (- n)

body
  pad(5px)
```

编译CSS为：

``` css
body {
  padding: -5px;
}
```

然而，只有在函数中才会存在这问题（因为函数返回值同时扮演了混合或回调）。

下面这个例子就没有问题（产生与上面相同的结果）：

``` css
body
  padding -5px
```

是否有Stylus无法处理的属性值？unquote()可以帮助你：

``` css
filter unquote('progid:DXImageTransform.Microsoft.BasicImage(rotation=1)')
```

编译CSS为：

``` css
filter progid:DXImageTransform.Microsoft.BasicImage(rotation=1)
```