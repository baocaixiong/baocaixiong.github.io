---
title: Golang一道关于值传递和defer的题目
date: 2019-01-23 14:19:00
tags: 
- golang
- defer
categories:
- golang
---

今天在`Go语言专栏读者`群里，郝林问了一道题，请看下面的代码：

```go
package main

import (
	"fmt"
)

type TestStruct struct {
	a int
	b string
}

func (T *TestStruct) setA(i int) {
	T.a = i
}

func NewStructV(value int, s string) TestStruct {
	T := TestStruct{a: value, b: s}
	p := &T
	fmt.Println(p, "__4__")
	fmt.Println(T, "__5__")
	p.setA(2)
	fmt.Println(p, "__6__")
	fmt.Println(T, "__7__")
	T.setA(3)
	fmt.Println(p, "__8__")
	fmt.Println(T, "__9__")
	defer fmt.Println(T, "__10__")
	defer fmt.Println(*p, "__11__")
	defer fmt.Println(p, "__12__")
	defer fmt.Println(&T, "__13__")
	defer p.setA(4)
	fmt.Printf("%p__14__\n", p)
	return T
}

func main() {
	q := NewStructV(1, "hello")
	k := &q
	fmt.Printf("%p__1__\n", k)
	fmt.Println(q, "__2__")
	fmt.Println(k, "__3__")
}
```

执行后输出：

```go
&{1 hello} __4__
{1 hello} __5__
&{2 hello} __6__
{2 hello} __7__
&{3 hello} __8__
{3 hello} __9__
0xc000044420__14__
&{4 hello} __13__
&{4 hello} __12__
{3 hello} __11__
{3 hello} __10__
0xc000044400__1__
{3 hello} __2__
&{3 hello} __3__
```

疑问一：为什么输出后缀为12、13的语句和输出后缀为10、11的语句的输出结果不一样？

疑问二：输出后缀为2和3的内容中，为什么字段a的值依然是3？



---



<details>
    <summary>第一个问题解答</summary>
    因为 fmt.Println 在这里实为 defer 函数，defer 函数的参数在 defer 语句执行时会先被求值。注意 defer 语句执行的时机并不是函数即将结束的时候，而是 Go 编译器读到这条语句的时候。然而，defer 函数会在函数即将结束时执行。这时，当初对 T 和 *p 的求值结果（实际上都是 T）已经被复制并另行保存在专用的栈里了。所以你后边再通过 p 改变其中的字段值已经不会对它们产生任何影响了（它们与 T 已经完全是两个值了）。
</details>

<details>
    <summary>第二个问题解答</summary>
    这也是值拷贝的问题，return语句被执行的时候，结果值会被复制和另存。如果函数返回的是普通的值的话，后边执行的defer函数再对原值进行改动就不关结果值的事了。它们已经是两个值了。
</details>

