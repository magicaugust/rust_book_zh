if
===

Rust 里的 if 并不复杂，更接近动态类型语言的用法。

	let x = 5;
	if x == 5 {
		println!("x is five!");
	}

如果把 x 改成 5 以外的值，打印语句就不会执行。也就是说 if 后面的表达式结果为 true 就会被执行；如果是 false 则不会。

如果你想在 false 的时候做一些操作，那么就要用到 else：

	let x = 5;
	if x == 5 {
		println!("x is five!");
	} else {
		println!("x is not five");
	}

这是标准的写法，当然你也可以这么写：

	let x = 5;
	let y = if x == 5 {
	    10
	} else {
	    15
	}; // y: i32

甚至这么写：

	let x = 5;
	let y = if x == 5 { 10 } else { 15 }; // y: i32

#表达式和声明

Rust 是一门基于表达式的语言，除了两种的声明以外全都是表达式。

表达式和声明的区别在于表达式返回一个值而声明不会。在大多数语言里 if 只是个声明，因此像 `let x = if ...` 是没有意义的。但在 Rust 里 if 就是个表达式，他会返回一个值，我们也就可以用返回值来初始化绑定。

绑定是 rust 两种声明里的一种。

在一些语言里值绑定不仅可以写成声明还可以写成表达式，比如 Ruby ：

	x = y = 5

而在 rust 里如果用 let 创建绑定那么这就不是一个表达式。这面的写法会导致编译错误：

	let x = (let y = 5); // expected identifier, found keyword `let`

编译器说这是个表达式而 let 只能用在声明里。

给绑定过的值赋值也是一个表达式。和 C 赋值之后得到一个新的值不一样的是在 Rust 里赋值操作的返回值是 单元类型 `()`， 这我们后面会说到。

第二种声明就是表达式声明。作用是把任意的表达式转化成声明。Rust 的语法是希望声明和声明连在一起，表达式之间要用 `;` 隔开。几乎每一句结尾都要跟个分号。

为什么说是“几乎”呢？比如：

	let x = 5;
	let y: i32 = if x == 5 { 10 } else { 15 };

注意这里我们给 y 指定了类型 i32.

如果你写成这样：

	let x = 5;
	let y: i32 = if x == 5 { 10; } else { 15; };

是不会编译通过的，报错：

	error: mismatched types: expected `i32`, found `()` (expected i32, found ())

这里我们需要的是一个 i32 ，结果返回的是 ()，我们称这个类型为单元，是 rust 的一个特殊类型。i32 类型的值是不能为 () 的。只有 () 类型的值才能是 () 。分号会忽略所有表达式的值然后返回 () 从而把表达式转化成声明。

还有一个地方你不需要分号，下一章《函数》里我们在介绍。