# 比较运算符 & 等号

- ~~优先使用 `===` 和 `!==` 而不是 `==` 和 `!=`。eslint: [`eqeqeq`](http://eslint.cn/docs/rules/eqeqeq)~~ `已删除`

- 条件表达式例如 `if` 语句通过抽象方法 `ToBoolean` 强制计算它们的表达式并且总是遵守下面的规则：

    - **对象** 被计算为 **true**
    - **undefined** 被计算为 **false**
    - **null** 被计算为 **false**
    - **布尔值** 被计算为 **布尔的值**
    - **数字** 如果是 **+0、-0、或 NaN** 被计算为 **false**, 否则为 **true**
    - **字符串** 如果是空字符串 `''` 被计算为 **false**，否则为 **true**

```javascript
if ([0] && []) {
    // true
    // An array is an object, objects evaluate to true
}
```

- 使用简写，显示的字符串和数字对比除外。

```javascript
// bad
if (isValid === true) {
    // ...
}

// good
if (isValid) {
    // ...
}

// bad
if (name) {
    // ...
}

// good
if (name !== '') {
    // ...
}

// bad
if (collection.length) {
    // ...
}

// good
if (collection.length > 0) {
    // ...
}
```

- 想了解更多信息，参考 Angus Croll 的 [Truth Equality and JavaScript](http://javascriptweblog.wordpress.com/2011/02/07/truth-equality-and-javascript/#more-2108)。

- 使用花括号创建块作用域来包裹 `case` 和 `default`，如果子句包含词法声明(例如：`let`, `const`, `function`, `class`)。eslint: [`no-case-declarations`](http://eslint.cn/docs/rules/no-case-declarations).

> 为什么? 因为词法声明在整个 switch 作用域都有效，但是它只有在运行到它定义的 `case` 语句时，才会进行初始化操作。这回导致很多 `case` 的子句定义同一个东西。

```javascript
// bad
switch (foo) {
    case 1:
        let x = 1;
        break;
    case 2:
        const y = 2;
        break;
    case 3:
        function f() {
            // ...
        }
        break;
    default:
        class C {}
}

// good
switch (foo) {
    case 1: {
        let x = 1;
        break;
    }
    case 2: {
        const y = 2;
        break;
    }
    case 3: {
        function f() {
            // ...
        }
        break;
    }
    case 4:
        bar();
        break;
    default: {
        class C {}
    }
}
```

- 禁止使用嵌套的三元运算符。eslint rules: [`no-nested-ternary`](http://eslint.cn/docs/rules/no-nested-ternary)

```javascript
// bad
const foo = maybe1 > maybe2
    ? "bar"
    : value1 > value2 ? "baz" : null;

// better
const maybeNull = value1 > value2 ? 'baz' : null;

const foo = maybe1 > maybe2
    ? 'bar'
    : maybeNull;

// best
const maybeNull = value1 > value2 ? 'baz' : null;

const foo = maybe1 > maybe2 ? 'bar' : maybeNull;
```

- 不要使用无意义的三元运算符。eslint rules: [`no-unneeded-ternary`](http://eslint.cn/docs/rules/no-unneeded-ternary)

```javascript
// bad
const foo = a ? a : b;
const bar = c ? true : false;
const baz = c ? false : true;

// good
const foo = a || b;
const bar = !!c;
const baz = !c;
```
