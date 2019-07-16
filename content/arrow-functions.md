# 箭头函数

- 当你必须使用函数表达式（或传递一个匿名函数）时，使用箭头函数符号。eslint: [`prefer-arrow-callback`](http://eslint.cn/docs/rules/prefer-arrow-callback), [`arrow-spacing`](http://eslint.cn/docs/rules/arrow-spacing)

> 为什么?因为箭头函数创造了新的一个 `this` 执行环境（译注：参考 [Arrow functions - JavaScript | MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Arrow_functions) 和 [ES6 arrow functions, syntax and lexical scoping](http://toddmotto.com/es6-arrow-functions-syntaxes-and-lexical-scoping/)），通常情况下都能满足你的需求，而且这样的写法更为简洁。
> 为什么不？如果你有一个相当复杂的函数，你或许可以把逻辑部分转移到一个函数声明上。

```javascript
// bad
[1, 2, 3].map(function (x) {
    const y = x + 1;
    return x * y;
});

// good
[1, 2, 3].map((x) => {
    const y = x + 1;
    return x * y;
});
```

- 如果一个函数适合用一行写出并且只有一个参数，那就把花括号、圆括号和 `return` 都省略掉。如果不是，那就不要省略。eslint: [`arrow-parens`](http://eslint.cn/docs/rules/arrow-parens), [`arrow-body-style`](http://eslint.cn/docs/rules/arrow-body-style)

> 为什么？语法糖。在链式调用中可读性很高。

```javascript
// bad
[1, 2, 3].map(number => {
    const nextNumber = number + 1;
    `A string containing the ${nextNumber}.`;
});

// good
[1, 2, 3].map(number => `A string containing the ${number}.`);

//bad
[1, 2, 3].map(number => {
    const nextNumber = number + 1;
    return `A string containing the ${nextNumber}.`;
});

// good
[1, 2, 3].map((number) => {
    const nextNumber = number + 1;
    return `A string containing the ${nextNumber}.`;
});

// good
[1, 2, 3].map((number, index) => ({
    [index]: number,
}));
```

- 当表达式占用了多行的时候，为了更好的可读性，用括号包裹起来。

> 为什么? 函数内容看起来会很清晰。

```javascript
// bad
['get', 'post', 'put'].map(httpMethod => Object.prototype.hasOwnProperty.call(
        httpMagicObjectWithAVeryLongName,
        httpMethod,
    )
);

// good
['get', 'post', 'put'].map(httpMethod => (
    Object.prototype.hasOwnProperty.call(
        httpMagicObjectWithAVeryLongName,
        httpMethod,
    )
));
```

- 避免箭头函数语法 (`=>`) 和一些比较操作 (`<=`, `>=`) 对人造成困惑。eslint: [`no-confusing-arrow`](http://eslint.cn/docs/rules/no-confusing-arrow)

```javascript
// bad
const itemHeight = item => item.height > 256 ? item.largeSize : item.smallSize;

// bad
const itemHeight = (item) => item.height > 256 ? item.largeSize : item.smallSize;

// good
const itemHeight = item => (item.height > 256 ? item.largeSize : item.smallSize);

// good
const itemHeight = (item) => {
    const { height, largeSize, smallSize } = item;
    return height > 256 ? largeSize : smallSize;
};
```
