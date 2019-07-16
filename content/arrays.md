# 数组

- 使用字面值创建数组。eslint: [`no-array-constructor`](http://eslint.cn/docs/rules/no-array-constructor)

```javascript
// bad
const items = new Array();

// good
const items = [];
```

- 向数组添加元素时使用 [`Array.push`](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_Objects/Array/push) 替代直接赋值。

```javascript
const someStack = [];


// bad
someStack[someStack.length] = 'abracadabra';

// good
someStack.push('abracadabra');
```

- 使用扩展运算符 `...` 复制数组

```javascript
// bad
const len = items.length;
const itemsCopy = [];
let i;

for (i = 0; i < len; i++) {
    itemsCopy[i] = items[i];
}

// good
const itemsCopy = [...items];
```

- 使用 [`Array.from`](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_Objects/Array/from) 把一个类数组对象转换成数组

```javascript
const foo = document.querySelectorAll('.foo');
const nodes = Array.from(foo);
```

- 在数组方法的回调函数中使用 return 语句。如果函数部分只有一个单行申明例如 [8.2](#8.2)，return 也可以省略掉。 eslint: [`array-callback-return`](http://eslint.cn/docs/rules/array-callback-return)

```javascript
// good
[1, 2, 3].map((x) => {
    const y = x + 1;
    return x * y;
});

// good
[1, 2, 3].map(x => x + 1);

// bad
const flat = {};
[[0, 1], [2, 3], [4, 5]].reduce((memo, item, index) => {
    const flatten = memo.concat(item);
    flat[index] = flatten;
});

// good
const flat = {};
[[0, 1], [2, 3], [4, 5]].reduce((memo, item, index) => {
    const flatten = memo.concat(item);
    flat[index] = flatten;
    return flatten;
});

// bad
inbox.filter((msg) => {
    const { subject, author } = msg;
    if (subject === 'Mockingbird') {
        return author === 'Harper Lee';
    } else {
        return false;
    }
});

// good
inbox.filter((msg) => {
    const { subject, author } = msg;
    if (subject === 'Mockingbird') {
        return author === 'Harper Lee';
    }

    return false;
});
```
