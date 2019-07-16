# Iterators and Generators

- 不要使用 iterators。使用高阶函数替代 `for-in` 和 `for-of`。eslint: [`no-iterator`](http://eslint.cn/docs/rules/no-iterator) [`no-restricted-syntax`](http://eslint.cn/docs/rules/no-restricted-syntax)

> 为什么？这加强了我们不变的规则。处理纯函数的回调值更易读，这比它带来的副作用更重要。
> 使用 `map()` / `every()` / `filter()` / `find()` / `findIndex()` / `reduce()` / `some()` / ... iterate 数组，`Object.keys()` / `Object.values()` / `Object.entries()` 产生数组然后 iterate 对象。

```javascript
const numbers = [1, 2, 3, 4, 5];

// bad
let sum = 0;
for (let num of numbers) {
    sum += num;
}

sum === 15;

// good
let sum = 0;
numbers.forEach((num) => sum += num);
sum === 15;

// best (use the functional force)
const sum = numbers.reduce((total, num) => total + num, 0);
sum === 15;

// bad
const increasedByOne = [];
for (let i = 0; i < numbers.length; i++) {
    increasedByOne.push(numbers[i] + 1);
}

// good
const increasedByOne = [];
numbers.forEach(num => increasedByOne.push(num + 1));

// best (keeping it functional)
const increasedByOne = numbers.map(num => num + 1);
```

- 现在还不要使用 generators。

> 为什么？因为它们现在还没法很好地编译到 ES5。 (译者注：目前(2016/03) Chrome 和 Node.js 的稳定版本都已支持 generators)

- 如果你一定要使用 generators，不想搭理 [11.2](#generators--nope)，请强制 generator 函数中 * 周围使用正确的空格。eslint: [`generator-star-spacing`](http://eslint.cn/docs/rules/generator-star-spacing)

> 为什么？`function` 和 `*` 同一个概念的关键字中的一部分，`*` 不是修饰 `function` 的，`function*` 和 `function` 不是一个东西。

```javascript
// bad
function * foo() {
    // ...
}

// bad
const bar = function * () {
    // ...
};

// bad
const baz = function *() {
    // ...
};

// bad
const quux = function*() {
    // ...
};

// bad
function*foo() {
    // ...
}

// bad
function *foo() {
    // ...
}

// very bad
function
*
foo() {
    // ...
}

// very bad
const wat = function
*
() {
    // ...
};

// good
function* foo() {
    // ...
}

// good
const foo = function* () {
    // ...
};
```
