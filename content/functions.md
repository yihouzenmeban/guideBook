# 函数

- ~~使用函数表达式代替函数声明。~~ `已删除`

> 为什么？函数声明会把整个函数提升（hoisted），这意味着我们很容易在函数定义的位置之前去引用这个函数，会影响到代码的可维护性和可读性。

```javascript
// bad
function foo() {
}

// good
const foo = function () {
};
```

- 把需要立即执行的函数包裹起来（包裹 function 表达式）。eslint: [`wrap-iife`](http://eslint.cn/docs/rules/wrap-iife)

```javascript
// 立即调用的函数表达式 (IIFE)
(() => {
    console.log('Welcome to the Internet. Please follow me.');
})();
```

- 永远不要在一个非函数代码块（`if`、`while` 等）中声明一个函数。把那个函数赋给一个变量再使用。虽然浏览器允许你这么做，但它们的解析表现不一致。eslint: [`no-loop-func`](http://eslint.cn/docs/rules/no-loop-func)

- **注意:** ECMA-262 把 `block` 定义为一组语句。函数声明不是语句。[阅读 ECMA-262 关于这个问题的说明](http://www.ecma-international.org/publications/files/ECMA-ST/Ecma-262.pdf#page=97)。

```javascript
// bad
if (currentUser) {
    function test() {
        console.log('Nope.');
    }
}

// good
let test;
if (currentUser) {
    test = () => {
        console.log('Yup.');
    };
}
```

- 永远不要把参数命名为 `arguments`。这将覆盖原来函数作用域内的 `arguments` 对象。

```javascript
// bad
function nope(name, options, arguments) {
    // ...
}

// good
function yup(name, options, args) {
    // ...
}
```

- 不要使用 `arguments`。可以选择 rest 语法 `...` 替代。

> 为什么？使用 `...` 能明确你要传入的参数。另外 rest 参数是一个真正的数组，而 `arguments` 是一个类数组。

```javascript
// bad
function concatenateAll() {
    const args = Array.prototype.slice.call(arguments);
    return args.join('');
}

// good
function concatenateAll(...args) {
    return args.join('');
}
```

- 直接给函数的参数指定默认值，不要改变函数参数。

```javascript
// really bad
function handleThings(opts) {
    // 不！我们不应该改变函数参数。
    // 更加糟糕: 如果参数 opts 是 false 的话，它就会被设定为一个对象。
    // 但这样的写法会造成一些 Bugs。
    //（译注：例如当 opts 被赋值为空字符串，opts 仍然会被下一行代码设定为一个空对象。）
    opts = opts || {};
    // ...
}

// still bad
function handleThings(opts) {
    if (opts === void 0) {
        opts = {};
    }
    // ...
}

// good
function handleThings(opts = {}) {
    // ...
}
```

- 直接给函数参数赋值时需要避免副作用。

> 为什么？因为这样的写法让人感到很困惑。

```javascript
var b = 1;
// bad
function count(a = b++) {
    console.log(a);
}
count();  // 1
count();  // 2
count(3); // 3
count();  // 3
```

- 把有默认值的参数放在最后面。

```javascript
// bad
function handleThings(opts = {}, name) {
    // ...
}

// good
function handleThings(name, opts = {}) {
    // ...
}
```

- 永远不要使用 `Function` 去构造一个新的函数。eslint: [`no-new-func`](http://eslint.cn/docs/rules/no-new-func)

> 为什么？用这种方式去创建一个新的函数相当于对字符串使用 `eval()`，会引起很多问题。

```javascript
// bad
var add = new Function('a', 'b', 'return a + b');

// still bad
var subtract = Function('a', 'b', 'return a - b');

// good
var x = function (a, b) {
    return a + b;
};
```

- 在函数的圆括号前后添加空格。 eslint: [`space-before-function-paren`](http://eslint.cn/docs/rules/space-before-function-paren) [`space-before-blocks`](http://eslint.cn/docs/rules/space-before-blocks)

> 为什么? 一致性很重要，而且在添加或者删除函数名字的时候不需要添加或者删除空格了。

```javascript
// bad
const f = function(){};
const g = function (){};
const h = function() {};

// good
const x = function () {};
const y = function a() {};
```

- ~~永远不要操作参数。eslint: [`no-param-reassign`](http://eslint.cn/docs/rules/no-param-reassign)~~ `已删除`

> 为什么？对函数参数中的变量进行操作可能会误导读者，导致混乱，也会改变 `arguments` 对象。

```javascript
// bad
function f1(obj) {
    obj.key = 1;
}

// good
function f2(obj) {
    const key = Object.prototype.hasOwnProperty.call(obj, 'key') ? obj.key : 1;
}
```

- 永远不要对参数重新赋值。eslint: [`no-param-reassign`](http://eslint.cn/docs/rules/no-param-reassign)

> 为什么? 重新赋值参数会导致一些不可预料的情况发生，比如当访问 `arguments` 对象的时候。这也会影响一些性能优化问问题，特别是在 [`v8`](https://github.com/v8/v8) 引擎中。

```javascript
// bad
function f1(a) {
    a = 1;
    // ...
}

function f2(a) {
    if (!a) { a = 1; }
    // ...
}

// good
function f3(a) {
    const b = a || 1;
    // ...
}

function f4(a = 1) {
    // ...
}
```

- 最好使用扩展运算符 `...` 调用可变参数函数。eslint: [`prefer-spread`](http://eslint.cn/docs/rules/prefer-spread)

> Why? It's cleaner, you don't need to supply a context, and you can not easily compose `new` with `apply`.

```javascript
// bad
const x = [1, 2, 3, 4, 5];
console.log.apply(console, x);

// good
const x = [1, 2, 3, 4, 5];
console.log(...x);

// bad
new (Function.prototype.bind.apply(Date, [null, 2016, 8, 5]));

// good
new Date(...[2016, 8, 5]);
```

- 有多个参数的函数在调用或者定义的时候，如果要使用换行缩进，应该和其它多行列表使用一个标准：每一条语句占用一行，在最后加上一个逗号。

```javascript
// bad
function foo(bar,
                baz,
                quux) {
    // ...
}

// good
function foo(
    bar,
    baz,
    quux,
) {
    // ...
}

// bad
console.log(foo,
    bar,
    baz);

// good
console.log(
    foo,
    bar,
    baz,
);
```
