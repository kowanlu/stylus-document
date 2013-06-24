## CSS 需要英雄 ##

``` css
body {
  font: 12px Helvetica, Arial, sans-serif;
}
a.button {
  -webkit-border-radius: 5px;
  -moz-border-radius: 5px;
  border-radius: 5px;
}
```

## 如果我们省略大括号？ ##

``` css
body
  font: 12px Helvetica, Arial, sans-serif;
  
a.button
  -webkit-border-radius: 5px;
  -moz-border-radius: 5px;
  border-radius: 5px;
```

## 那分号了？ ##

``` css
body
  font: 12px Helvetica, Arial, sans-serif
  
a.button
  -webkit-border-radius: 5px
  -moz-border-radius: 5px
  border-radius: 5px
```

## 到此为止？除去冒号 ##

``` css
body
  font 12px Helvetica, Arial, sans-serif
  
a.button
  -webkit-border-radius 5px
  -moz-border-radius 5px
  border-radius 5px
```

## 让事情更简洁 ##

``` css
border-radius()
  -webkit-border-radius arguments
  -moz-border-radius arguments
  border-radius arguments
  
body
  font 12px Helvetica, Arial, sans-serif
  
a.button
  border-radius(5px)
```

## 混合书写又如何？ ##

``` css
border-radius()
  -webkit-border-radius arguments
  -moz-border-radius arguments
  border-radius arguments
  
body
  font 12px Helvetica, Arial, sans-serif
  
a.button
  border-radius 5px
```

## 创建与分享 ##

``` css
@import 'vendor'

body
  font 12px Helvetica, Arial, sans-serif
  
a.button
  border-radius 5px
```

## 甚至使用函数! ##

``` css
sum(nums...)
  sum = 0
  sum += n for n in nums
  
sum(1 2 3 4)
// => 10
> 
```

## 如果所有都是可选的又将怎样？ ##

``` css
fonts = helvetica, arial, sans-serif

body {
  padding: 50px;
  font: 14px/1.4 fonts;
}
```

## 获取、安装Stylus ##

``` js
$ npm install stylus
```

如果你已经迫不及待想尝试这些功能，赶紧去[GitHub](http://github.com/learnboost/stylus)查看。

### 功能 ###

- 冒号可选
- 分号可选
- 逗号可选
- 括号可选
- 变量
- 插值
- 混合
- 算术
- 强制类型转换
- 动态导入
- 条件语句
- 迭代
- 嵌套选择
- 父级引用
- 变量函数调用
- 词法作用域
- 内置函数 （> 25）
- 内部语言函数
- 压缩可选
- 图像内联可选
- 可执行Stylus
- 健壮的错误报告
- 单行和多行注释
- CSS 字面量
- 转义字符
- TextMate 捆绑
- ...