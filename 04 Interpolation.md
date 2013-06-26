## 插值 ##

Stylus通过使用`{}`包裹表达式来进行插值。例如，-webkit-{'border' + '-radius'}等同于-webkit-border-radius。

比较典型的例子就是各浏览器私有属性前缀：

``` css
  vendor(prop, args)
    -webkit-{prop} args
    -moz-{prop} args
    {prop} args

  border-radius()
    vendor('border-radius', arguments)

  box-shadow()
    vendor('box-shadow', arguments)

  button
    border-radius 1px 2px / 3px 4px
```

编译CSS为：

``` css
  button {
    -webkit-border-radius: 1px 2px / 3px 4px;
    -moz-border-radius: 1px 2px / 3px 4px;
    border-radius: 1px 2px / 3px 4px;
  }
```

## 选择器插值 ##

选择器也可以使用插值。在下面示例中，我们可以遍历设置表格前5行的`height`属性：

``` css
table
  for row in 1 2 3 4 5
    tr:nth-child({row})
      height: 10px * row
```

编译CSS为：

``` css
table tr:nth-child(1) {
  height: 10px;
}
table tr:nth-child(2) {
  height: 20px;
}
table tr:nth-child(3) {
  height: 30px;
}
table tr:nth-child(4) {
  height: 40px;
}
table tr:nth-child(5) {
  height: 50px;
}
```
