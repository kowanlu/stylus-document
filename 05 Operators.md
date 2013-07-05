## 运算符优先级 ##

下面是运算符优先级表中，最高到最低：

``` css
 []
 ! ~ + -
 is defined
 ** * / %
 + -
 ... ..
 <= >= < >
 in
 == is != is not isnt
 is a
 && and || or
 ?:
 = := ?= += -= *= /= %=
 not
 if unless
```

## 一元运算符 ##

以下的一元运算符是可用的，!not， -， +，和~.

!0
// => true

!!0
// => false

!1
// => false

!!5px
// => true

-5px
// => -5px

--5px
// => 5px

not true
// => false

not not true
// => true
> 
逻辑not运算符具有低优先级，因此下面的示例可以替换为

a = 0
b = 1

!a and !b
// => false
// pased as: (!a) and (!b)
与：

not a or b
// => false
// parsed as: not (a or b)

二元运算符

下标运算符使我们能够抓住内通过索引的表达式的值。带括号的表达式可以作为元组 （例如(15px 5px)、 (1 2 3)).

下面是使用元组为错误的示例，处理 （和展示此构造的多功能性）：

 add(a, b)
   if a is a 'unit' and b is a 'unit'
     a + b
   else
     (error 'a and b must be units!')

 body
   padding add(1,'5')
   // => padding: error "a and b must be units";

   padding add(1,'5')[0]
   // => padding: error;

   padding add(1,'5')[0] == error
   // => padding: true;

   padding add(1,'5')[1]
   // => padding: "a and b must be units";
> 
这里是一个更复杂的例子。现在我们要调用返回错误消息，在内置error()函数每当 ident （第一个值） 等于error.

 if (val = add(1,'5'))[0] == error
   error(val[1])

范围...…

包容性 (..) 和专属 (......) 范围，提供的运算符，扩大到的表达式：

 1..5
 // => 1 2 3 4 5

 1...5
 // => 1 2 3 4

添加剂： +-

乘法和添加剂的二进制运算符按预期方式工作。类型转换内单位类型的类，或者默认值应用于文本值。例如5s - 2px结果在3s.

15px - 5px
// => 10px

5 - 2
// => 3

5in - 50mm
// => 3.031in

5s - 1000ms
// => 4s

20mm + 4in
// => 121.6mm

"foo " + "bar"
// => "foo bar"

"num " + 15
// => "num 15"
乘法： / * %

2000ms + (1s * 2)
// => 4ms

5s / 2
// => 2.5s

4 % 2
// => 0

当在属性值内使用/ ，你必须换用 parens。否则/是采取逐字地 （支持 CSSline-height):

font: 14px/1.5;

但以下计算为14px ÷ 1.5:

font: (14px/1.5);

这是只有所需的/运算符。

指数： * *

指数运算符：

2 ** 8
// => 256

平等与关系： = =! = > = <>< =

可以使用相等运算符将等同于单位、 颜色、 字符串和甚至标识符。这是一个强大的概念，作为甚至任意标识符 （如作为wahoo） 可以用作原子。函数可以返回yes或no而不是true或false （虽然不建议）。

5 == 5
// => true

10 > 5
// => true

#fff == #fff
// => true

true == false
// => false

wahoo == yay
// => false

wahoo == wahoo
// => true

"test" == "test"
// => true

true is true
// => true

'hey' is not 'bye'
// => true

'hey' isnt 'bye'
// => true

(foo bar) == (foo bar)
// => true

(1 2 3) == (1 2 3)
// => true

(1 2 3) == (1 1 3)
// => false

只有精确值匹配。例如， 0 == false和null == false是这两个false.

别名：

==    is
!=    is not
!=    isnt

真实性

几乎一切内触笔将解析为true的包括单位的后缀。甚至0%、 0px等将解析为true （因为它是共同的在手写笔 mixins 或函数接受单位作为有效）。

然而， 0本身是false的算术。

表达式 （或"列表"），其长度大于 1 被认为是 truthy。

true的例子：

  0% 
  0px
  1px 
  -1
  -1px
  hey
  'hey'
  (0 0 0)
  ('' '')

false的例子：

 0 
 null
 false
 ''

逻辑运算符： & & | |和或

逻辑运算符&&和||是别名and/or适用相同的优先级。

5 && 3
// => 3

0 || 5
// => 5

0 && 5
// => 0

#fff is a 'rgba' and 15 is a 'unit'
// => true

存在运算符： 在

检查是否存在的左侧操作数内的右侧的表达式。

简单的例子：

  nums = 1 2 3
  1 in nums
  // => true

  5 in nums
  // => false

一些未定义的标识符：

  words = foo bar baz
  bar in words
  // => true

  HEY in words
  // => false

太与元组的工作：

  vals = (error 'one') (error 'two')
  error in vals
  // => false

  (error 'one') in vals
  // => true

  (error 'two') in vals
  // => true

  (error 'something') in vals
  // => false

在混合料搅拌设备用法的示例：

  pad(types = padding, n = 5px)
    if padding in types
      padding n
    if margin in types
      margin n

  body
    pad()

  body
    pad(margin)

  body
    pad(padding margin, 10px)

收益率：

  body {
    padding: 5px;
  }
  body {
    margin: 5px;
  }
  body {
    padding: 10px;
    margin: 10px;
  }

有条件的转让：? =: =

条件赋值运算符?= (别名为:=） 让我们定义的变量没有篡改的旧值 （如果存在）。此运算符将扩展到内三元is defined二元运算。

例如，以下是等效的：

color := white
color ?= white
color = color is defined ? color : white

当使用纯=时，我们只是重新分配：

color = white
color = black

color
// => black

但在使用时?=，我们第二次尝试失败 （因为已定义该变量）：

color = white
color ?= black

color
// => white

实例检查： 是

触笔提供名为二进制运算符is a用来类型检查。

15 is a 'unit'
// => true

#fff is a 'rgba'
// => true

15 is a 'rgba'
// => false

或者，我们可以使用type()国际仁爱基金会：

type(#fff) == 'rgba'
// => true       
                                                                     
注：color是唯一的特殊情况，评估为true时将左边的操作数是一个RGBA或HSLA的节点。

被定义的变量的定义：

此伪二元运算符不接受右边的运算符，并不会不评价左。这使我们能够检查是否变量的值分配给它。

foo is defined
// => false

foo = 15px
foo is defined
// => true

#fff is defined
// => 'invalid "is defined" check on non-variable #fff'

或者，一个可以使用lookup(name)内置函数来执行此操作 — — 或执行动态查找：

name = 'blue'
lookup('light-' + name)
// => null

light-blue = #80e2e9
lookup('light-' + name)
// => #80e2e9

此运算符是必不可少的因为未定义的标识符仍然是一个 truthy 的值。例如：

body
  if ohnoes
    padding 5px

将产生以下 CSS 时未定义的：

body {
  padding: 5px;
}

但是这将是安全的：

body
  if ohnoes is defined
    padding 5px

三元

三元运算符工作正如我们期望在大多数语言中。它是唯一具有三个操作数 （条件表达式、 表达式的真值和假表达式） 运算符。

num = 15
num ? unit(num, 'px') : 20px
// => 15px

铸造

作为unit()内置函数简洁的替代方法，语法(expr) unit可用于强制后缀。

body
  n = 5
  foo: (n)em
  foo: (n)%
  foo: (n + 5)%
  foo: (n * 5)px
  foo: unit(n + 5, '%')
  foo: unit(5 + 180 / 2, deg)

颜色操作

在颜色上的业务提供简洁、 富有表现力的方式来改变组件。例如，我们可以在每个 RGB 上操作：

#0e0 + #0e0
// => #0f0

另一个例子是通过添加或减去一个百分比调整的明度值。要减轻一种颜色，请添加 ；变暗，减去。

#888 + 50%
// => #c3c3c3

#888 - 50%
// => #444

调整色调也可能是通过添加或减去同度。例如，将50deg添加到黄色这红色值结果：

 #f00 + 50deg
 // => #ffd500

值适当地夹紧。例如，我们可以"自旋"色相 180 度，并且如果当前值是320deg，它会解析到140deg.

我们也可能会调整一次 （包括 alpha） 的几个值通过使用rgb()、 rgba()、 hsl()或hsla():

  #f00 - rgba(100,0,0,0.5)
  // => rgba(155,0,0,0.5)

Sprintf

字符串 sprintf 样运算符%可以用于生成一个文本值，内部传递参数通过s()内置：

   'X::Microsoft::Crap(%s)' % #fc0
   // => X::Microsoft::Crap(#fc0)

多个值应带圆括号：

  '-webkit-gradient(%s, %s, %s)' % (linear (0 0) (0 100%))
  // => -webkit-gradient(linear, 0 0, 0 100%)