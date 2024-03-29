# 类型转换

- 在语句开始时执行类型转换。

- 字符串：

```javascript
// => this.reviewScore = 9;

// bad
const totalScore = this.reviewScore + ''; // 调用 this.reviewScore.valueOf()

// bad
const totalScore = this.reviewScore.toString(); // 不能保证返回一个字符串

// good
const totalScore = String(this.reviewScore);
```

- 对数字使用 `Number` 和 `parseInt` 转换，`parseInt` 要带上类型转换的基数。eslint: [`radix`](http://eslint.cn/docs/rules/radix)

```javascript
const inputValue = '4';

// bad
const val = new Number(inputValue);

// bad
const val = +inputValue;

// bad
const val = inputValue >> 0;

// bad
const val = parseInt(inputValue);

// good
const val = Number(inputValue);

// good
const val = parseInt(inputValue, 10);
```

- 如果因为某些原因 parseInt 成为你所做的事的瓶颈而需要使用位操作解决[性能问题](http://jsperf.com/coercion-vs-casting/3)时，留个注释说清楚原因和你的目的。

```javascript
// good
/**
    * 使用 parseInt 导致我的程序变慢，
    * 改成使用位操作转换数字快多了。
    */
const val = inputValue >> 0;
```

- **注:** 使用位操作运算符要小心。数字会被当成 [64 位值](http://es5.github.io/#x4.3.19)，但是位操作运算符总是返回 32 位的整数（[参考](http://es5.github.io/#x11.7)）。位操作处理大于 32 位的整数值时还会导致意料之外的行为。[关于这个问题的讨论](https://github.com/airbnb/javascript/issues/109)。最大的 32 位整数是 2,147,483,647：

```javascript
2147483647 >> 0 //=> 2147483647
2147483648 >> 0 //=> -2147483648
2147483649 >> 0 //=> -2147483647
```

- 布尔:

```javascript
const age = 0;

// bad
const hasAge = new Boolean(age);

// good
const hasAge = Boolean(age);

// good
const hasAge = !!age;
```
