# 分号

- **使用分号** eslint: [`semi`](http://eslint.cn/docs/rules/semi)

```javascript
// bad
(function() {
    const name = 'Skywalker'
    return name
})()

// good
(() => {
    const name = 'Skywalker';
    return name;
})();

// good (防止函数在两个 IIFE 合并时被当成一个参数)
;(() => {
    const name = 'Skywalker';
    return name;
})();
```

[Read more](https://stackoverflow.com/questions/7365172/semicolon-before-self-invoking-function/7365214%237365214)
