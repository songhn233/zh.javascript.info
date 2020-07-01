# 运算符

我们从学校里了解到过很多运算符，比如说加号 `+`、乘号 `*`、减号 `-` 等。

在这个章节，我们将关注一些在学校数学课程中没有涵盖的运算符。

## 术语：“一元运算符”，“二元运算符”，“运算元”

在正式开始前，我们先简单浏览一下常用术语。

- **运算元** —— 运算符应用的对象。比如说乘法运算 `5 * 2`，有两个运算元：左运算元 `5` 和右运算元 `2`。有时候人们也称其为“参数”而不是“运算元”。
- 如果一个运算符对应的只有一个运算元，那么它是 **一元运算符**。比如说一元负号运算符（unary negation）`-`，它的作用是对数字进行正负转换：

    ```js run
    let x = 1;

    *!*
    x = -x;
    */!*
    alert( x ); // -1，一元负号运算符生效
    ```
- 如果一个运算符拥有两个运算元，那么它是 **二元运算符**。减号还存在二元运算符形式：

    ```js run no-beautify
    let x = 1, y = 3;
    alert( y - x ); // 2，二元运算符减号做减运算
    ```

    严格地说，在上面的示例中，我们使用一个相同的符号表征了两个不同的运算符：负号运算符，即反转符号的一元运算符，减法运算符，是从另一个数减去一个数的二进制运算符。

## 字符串连接，二元运算符 +

下面，让我们看一下在学校数学课程范围外的 JavaScript 运算符特性。

通常，加号 `+` 用于求和。

但是如果加号 `+` 被应用于字符串，它将合并（连接）各个字符串：

```js
let s = "my" + "string";
alert(s); // mystring
```

注意：只要其中一个运算元是字符串，那么另一个运算元也将被转化为字符串。

举个例子：

```js run
alert( '1' + 2 ); // "12"
alert( 2 + '1' ); // "21"
```

可以看出，字符串在前和在后并不影响这个规则。简单来说：如果任一运算元是字符串，那么其它运算元也将被转化为字符串。

但是，请注意：运算符的运算方向是由左至右。如果是两个数字，后面再跟一个字符串，那么两个数字会先相加，再转化为字符串：


```js run
alert(2 + 2 + '1' ); // "41" 而不是 "221"
```

字符串连接和转化是二元运算符加号 `+` 的一个特性。其它的数学运算符都只对数字有效。通常，他们会把运算元转化为数字。

举个例子，减法和除法：

```js run
alert( 2 - '1' ); // 1
alert( '6' / '2' ); // 3
```

## 数字转化，一元运算符 +

加号 `+` 有两种形式。一种是上面我们刚刚讨论的二元运算符，还有一种是一元运算符。

一元运算符加号，或者说，加号 `+` 应用于单个值，对数字没有任何作用。但是如果运算元不是数字，加号 `+` 则会将其转化为数字。

例如：

```js run
// 对数字无效
let x = 1;
alert( +x ); // 1

let y = -2;
alert( +y ); // -2

*!*
// 转化非数字
alert( +true ); // 1
alert( +"" );   // 0
*/!*
```

它的效果和 `Number(...)` 相同，但是更加简短。

我们经常会有将字符串转化为数字的需求。比如，如果我们正在从 HTML 表单中取值，通常得到的都是字符串。如果我们想对他们求和，该怎么办？

二元运算符加号会把他们合并成字符串：

```js run
let apples = "2";
let oranges = "3";

alert( apples + oranges ); // "23"，二元运算符加号合并字符串
```

如果我们想把它们当做数字对待，我们需要转化它们，然后再求和：

```js run
let apples = "2";
let oranges = "3";

*!*
// 在二元运算符加号起作用之前，所有的值都被转化为了数字
alert( +apples + +oranges ); // 5
*/!*

// 更长的写法
// alert( Number(apples) + Number(oranges) ); // 5
```

从一个数学家的视角来看，大量的加号可能很奇怪。但是从一个程序员的视角，没什么好奇怪的：一元运算符加号首先起作用，他们将字符串转为数字，然后二元运算符加号对它们进行求和。

为什么一元运算符先于二元运算符作用于运算元？接下去我们将讨论到，这是由于它们拥有 **更高的优先级**。

## 运算符优先级

如果一个表达式拥有超过一个运算符，执行的顺序则由 **优先级** 决定。换句话说，所有的运算符中都隐含着优先级顺序。

从小学开始，我们就知道在表达式 `1 + 2 * 2` 中，乘法先于加法计算。这就是一个优先级问题。乘法比加法拥有 **更高的优先级**。

圆括号拥有最高优先级，所以如果我们对现有的运算顺序不满意，我们可以使用圆括号来修改运算顺序，就像这样：`(1 + 2) * 2`。

在 JavaScript 中有众多运算符。每个运算符都有对应的优先级数字。数字越大，越先执行。如果优先级相同，则按照由左至右的顺序执行。

这是一个摘抄自 Mozilla 的 [优先级表](https://developer.mozilla.org/en/JavaScript/Reference/operators/operator_precedence)（你没有必要把这全记住，但要记住一元运算符优先级高于二元运算符）：

| 优先级 | 名称 | 符号 |
|------------|------|------|
| ... | ... | ... |
| 17 | 一元加号 | `+` |
| 17 | 一元负号 | `-` |
| 15 | 乘号 | `*` |
| 15 | 除号 | `/` |
| 13 | 加号 | `+` |
| 13 | 减号 | `-` |
| ... | ... | ... |
| 3 | 赋值符 | `=` |
| ... | ... | ... |

我们可以看到，“一元加号运算符”的优先级是 `17`，高于“二元加号运算符”的优先级 `13`。这也是为什么表达式 `"+apples + +oranges"` 中的一元加号先生效，然后才是二元加法。

## 赋值运算符

我们知道赋值符号 `=` 也是一个运算符。从优先级表中可以看到它的优先级非常低，只有 `3`。

这也是为什么，当我们赋值时，比如 `x = 2 * 2 + 1`，所有的计算先执行，然后 `=` 才执行，将计算结果存储到 `x`。

```js
let x = 2 * 2 + 1;

alert( x ); // 5
```

链式赋值也是可以的：

```js run
let a, b, c;

*!*
a = b = c = 2 + 2;
*/!*

alert( a ); // 4
alert( b ); // 4
alert( c ); // 4
```

链式赋值由右向左执行。首先执行最右侧表达式 `2 + 2`，然后将结果赋值给左侧：`c`、`b`、`a`。最后，所有的变量都共享一个值。

````smart header="赋值运算符 `\"=\"` 会返回一个值"
每个运算符都有一个返回值。对于以加号 `+` 或者乘号 `*` 为例的大部分运算符而言，这一点很显然。对于赋值运算符而言，这一点同样适用。

语句 `x = value` 把 `value` 的值写入 `x` **然后返回 x**。

下面是一个在复杂语句中使用赋值的例子：

```js run
let a = 1;
let b = 2;

*!*
let c = 3 - (a = b + 1);
*/!*

alert( a ); // 3
alert( c ); // 0
```

上面这个例子，`(a = b + 1)` 的结果是赋给 `a` 的值（也就是 `3`）。然后该值被用于进一步的运算。

这段代码是不是很好玩儿？我们应该理解它的原理，因为我们有时会在第三方库中见到这样的写法，但我们自己不应该这样写。这样的小技巧让代码变得整洁度和可读性都很差。
````

## 求余运算符 %

求余运算符 `%` 尽管看上去是个百分号，但它和百分数没有什么关系。

`a % b` 的结果是 `a` 除以 `b` 的余数。

举个例子：

```js run
alert( 5 % 2 ); // 1 是 5 / 2 的余数
alert( 8 % 3 ); // 2 是 8 / 3 的余数
alert( 6 % 3 ); // 0 是 6 / 3 的余数
```

## 幂运算符 **

幂运算符 `**` 是最近被加入到 JavaScript 中的。

对于自然数 `b`，`a ** b` 的结果是 `a` 与自己相乘 `b` 次。

举个例子：

```js run
alert( 2 ** 2 ); // 4  (2 * 2)
alert( 2 ** 3 ); // 8  (2 * 2 * 2)
alert( 2 ** 4 ); // 16 (2 * 2 * 2 * 2)
```

这个运算符对于 `a` 和 `b` 是非整数的情况依然适用。

例如：

```js run
alert( 4 ** (1/2) ); // 2 (1/2 幂相当于开方，这是数学常识)
alert( 8 ** (1/3) ); // 2 (1/3 幂相当于开三次方)
```

## 自增/自减

<!-- 在标题中我不能把 -- 写出来，因为内置的插件会把它转为 - -->

对一个数进行加一、减一是最常见的数学运算符之一。

所以，对此有一些专门的运算符：

- **自增** `++` 将变量与 1 相加：

    ```js run no-beautify
    let counter = 2;
    counter++;      // 和 counter = counter + 1 效果一样，但是更简洁
    alert( counter ); // 3
    ```
- **自减** `--` 将变量与 1 相减：

    ```js run no-beautify
    let counter = 2;
    counter--;      // 和 counter = counter - 1 效果一样，但是更简洁
    alert( counter ); // 1
    ```

```warn
自增/自减只能应用于变量。试一下，将其应用于数值（比如 `5++`）则会报错。
```

运算符 `++` 和 `--` 可以置于变量前，也可以置于变量后。

- 当运算符置于变量后，被称为“后置形式”：`counter++`。
- 当运算符置于变量前，被称为“前置形式”：`++counter`。

两者都做同一件事：将变量 `counter` 与 `1` 相加。

那么他们有区别吗？有，但只有当我们使用 `++/--` 的返回值时才能看到区别。

详细点说。我们知道，所有的运算符都有返回值。自增/自减也不例外。前置形式返回一个新的值，但后置返回原来的值（做加法/减法之前的值）。

为了直观看到区别，看下面的例子：

```js run
let counter = 1;
let a = ++counter; // (*)

alert(a); // *!*2*/!*
```

`(*)` 所在的行是前置形式 `++counter`，对 `counter` 做自增运算，返回的是新的值 `2`。因此 `alert` 显示的是 `2`。

下面让我们看看后置形式：

```js run
let counter = 1;
let a = counter++; // (*) 将 ++counter 改为 counter++

alert(a); // *!*1*/!*
```

`(*)` 所在的行是后置形式 `counter++`，它同样对 `counter` 做加法，但是返回的是 **旧值**（做加法之前的值）。因此 `alert` 显示的是 `1`。

总结：

- 如果自增/自减的值不会被使用，那么两者形式没有区别：

    ```js run
    let counter = 0;
    counter++;
    ++counter;
    alert( counter ); // 2，以上两行作用相同
    ```
- 如果我们想要对变量进行自增操作，**并且** 需要立刻使用自增后的值，那么我们需要使用前置形式：

    ```js run
    let counter = 0;
    alert( ++counter ); // 1
    ```
- 如果我们想要将一个数加一，但是我们想使用其自增之前的值，那么我们需要使用后置形式：

    ```js run
    let counter = 0;
    alert( counter++ ); // 0
    ```

````smart header="自增/自减和其它运算符的对比"
`++/--` 运算符同样可以在表达式内部使用。它们的优先级比绝大部分的算数运算符要高。

举个例子：

```js run
let counter = 1;
alert( 2 * ++counter ); // 4
```

与下方例子对比：

```js run
let counter = 1;
alert( 2 * counter++ ); // 2，因为 counter++ 返回的是“旧值”
```

尽管从技术层面上来说可行，但是这样的写法会降低代码的可阅读性。在一行上做多个操作 —— 这样并不好。

当阅读代码时，快速的视觉“纵向”扫描会很容易漏掉 `counter++`，这样的自增操作并不明显。

我们建议用“一行一个行为”的模式：

```js run
let counter = 1;
alert( 2 * counter );
counter++;
```
````

## 位运算符

位运算符把运算元当做 32 位整数，并在它们的二进制表现形式上操作。

这些运算符不是 JavaScript 特有的。大部分的编程语言都支持这些运算符。

下面是位运算符：

- 按位与 ( `&` )
- 按位或 ( `|` )
- 按位异或 ( `^` )
- 按位非 ( `~` )
- 左移 ( `<<` )
- 右移 ( `>>` )
- 无符号右移 ( `>>>` )

这些操作使用得非常少。为了理解它们，我们需要探讨底层的数字表达形式，现在不是做这个的最好时机。尤其是我们现在不会立刻使用它。如果你感兴趣，可以阅读 MDN 中的 [位运算符](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Operators/Bitwise_Operators) 相关文章。当有相关实际需求的时候再去阅读是更明智的选择。

## 修改并替换

我们经常需要对一个变量进行操作，并把计算得到的新结果存储在这个变量中。

举个例子：

```js
let n = 2;
n = n + 5;
n = n * 2;
```

这个操作可以通过使用运算符 `+=` 和 `*=` 进行简化：

```js run
let n = 2;
n += 5; // now n = 7 (同 n = n + 5)
n *= 2; // now n = 14 (同n = n * 2)

alert( n ); // 14
```

简短的“修改并替换”运算符对所有的运算符包括位运算符都有效：`/=`、`-=`等等。

这些运算符和正常的赋值运算符拥有相同的优先级，因此它们会在其它大部分运算完成之后运行：

```js run
let n = 2;

n *= 3 + 5;

alert( n ); // 16（右侧计算首先进行，和 n *= 8 相同）
```

## 逗号运算符

逗号运算符 `,` 是最少见最不常使用的运算符之一。有时候它会被用来写更简短的代码，因此为了能够理解代码，我们需要了解它。

逗号运算符能让我们处理多个语句，使用 `,` 将它们分开。每个语句都运行了，但是只有最后的语句的结果会被返回。

举个例子：

```js run
*!*
let a = (1 + 2, 3 + 4);
*/!*

alert( a ); // 7（3 + 4 的结果）
```

这里，第一个语句 `1 + 2` 运行了，但是它的结果被丢弃了。随后计算 `3 + 4`，并且该计算结果被返回。

```smart header="逗号运算符的优先级非常低"
请注意逗号运算符的优先级非常低，比 `=` 还要低，因此上面你的例子中圆括号非常重要。

如果没有圆括号：`a = 1 + 2, 3 + 4` 会先执行 `+`，将数值相加得到 `a = 3, 7`，然后赋值运算符 `=` 执行, 'a = 3'，然后逗号之后的数值 `7` 不会再执行，它被忽略掉了。相当于 `(a = 1 + 2), 3 + 4`。
```

为什么我们需要这样一个运算符，它只返回最后一个值呢？

有时候，人们会使用它把几个行为放在一行上来进行复杂的运算。

举个例子：

```js
// 一行上有三个运算符
for (*!*a = 1, b = 3, c = a * b*/!*; a < 10; a++) {
 ...
}
```

这样的技巧在许多 JavaScript 框架中都有使用，这也是为什么我们提到它。但是通常它并不能提升代码的可读性，使用它之前，我们要想清楚。