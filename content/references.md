# 引用

- 对所有的引用使用 `const` ；不要使用 `var`。 eslint: [`prefer-const`](http://eslint.cn/docs/rules/prefer-const), [`no-const-assign`](http://eslint.cn/docs/rules/no-const-assign)

> 为什么？这能确保你无法对引用重新赋值，也不会导致 bug 和难以理解的代码。

```javascript
// bad
var a = 1;
var b = 2;

// good
const a = 1;
const b = 2;
```

- 如果你需要对引用重新赋值，使用 `let` 代替 `var`。

> 为什么？因为 `let` 是块级作用域，而 `var` 是函数作用域。

```javascript
// bad
var count = 1;
if (true) {
    count += 1;
}

// good
let count = 1;
if (true) {
    count += 1;
}
```

- `let` 和 `const` 都是块级作用域。

```javascript
// const 和 let 只存在于它们被定义的区块内。
{
    let a = 1;
    const b = 1;
}
console.log(a); // ReferenceError
console.log(b); // ReferenceError
```
