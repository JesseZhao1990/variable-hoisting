#变量提升

变量提升也叫声明提升。是描述了这样一种现象：js在解析的时候总是会将var, function这类关键词的声明语句提升至该作用域的最顶部(注意：这里只会提升声明部分)

**注意：“变量提升” 名词是随大流叫法，“变量提升” 改为 “标识符提升” 更准确**

## 1.变量未声明直接使用会怎样？ ##

[演示地址](http://codepen.io/zhaojianxin/pen/VKbVOx?editors=1111)

```
function testFn(){
	console.log(a);
}

testFn();

```

很明显会报错：a 未定义
Uncaught ReferenceError: a is not defined

## 2.变量声明在末尾会怎么样？##

[演示地址](http://codepen.io/zhaojianxin/pen/yabGBO?editors=1111)

```
function testFn(){
	console.log(a);
}

testFn();

var a;

```

没有报错，在控制台输出了undefined。

## 3.变量声明在末尾并且赋值会怎么样？##

[演示地址](http://codepen.io/zhaojianxin/pen/LRyrEd?editors=1111)

```
function testFn(){
	console.log(a);
}

testFn();

var a="i am here";

```

没有报错，在控制台同样输出了undefined。但是为什么没输出"i am here"呢？ 所以。2和3都用到了变量提升。在函数运行之前，先在作用域的顶端声明后边出现的变量。以上代码等于这样书写。

```
var a;
function testFn(){
	console.log(a);
}

testFn();

a="i am here";

```

## 4.函数函数表达式同样存在变量提升（标识符提升） ##

[演示地址](http://codepen.io/zhaojianxin/pen/YGVdWJ?editors=1111)

```
function testFn() {
    console.log(func); // undefined
    var func = function() {};
    console.log(func);  //function() {};
}
testFn();

```

但是此时。你想在开头使用后来声明的函数表达式是不行的。
[演示地址](http://codepen.io/zhaojianxin/pen/pEPqPN?editors=1111)

```
function testFn() {
    func(); // 这里会报错。说func不是一个函数
    var func = function() {};
}
testFn();

```

## 5.函数声明的名也会提升到当前作用域顶部，不会存在4的函数未定义的情况 ##

[演示地址](http://codepen.io/zhaojianxin/pen/QKvzrN?editors=1111)

```
function testFn() {
    func(); // 这里不会报错。正常使用
    function func() {};
}
testFn();

```

变量提升（Hoisting），属于js语言当初设计的时候考虑把js做成灵活性的一种语言的考虑。但是现代的js程序越来越大，越来越复杂。这必然要求语言越来越规范化。so ES6 的 let/const 到来结束了，ES里除全局变量外，其它都使用 let/const，var 替换成 let 后变量提升就不复存在了。绝大部分的浏览器还没有实现ES6. 即使实现了也需要向下兼容。也需要掌握变量提升的技巧。因此，变量提升几乎在每家公司的面试题中都会涉及到。以下列出一些题目。以供练习。

题1：

```
// 写出以下代码的运行结果
 var tt = 'aa';   
 function test(){

       alert(tt);
       var tt = 'dd';
       alert(tt);    

       }   
  test();

```

题2：

```
var tt = 'aa';

 function test(){
  alert(tt);
        }
   test();

```


题3：
```
// 写出以下代码的运行结果
var a = 1;
function fn() {
    if (!a) {
        var a = 2;
    }
    alert(a); // ?
}
fn();

```

题4：
```
// 写出以下代码的运行结果
var a = 1;
function fn() {
    a = 2;
    return;
    function a() {}
}
fn();
alert(a); // ?

```

