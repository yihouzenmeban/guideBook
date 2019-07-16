# 解构

- 使用解构存取和使用多属性对象。jscs: [`requireObjectDestructuring`](http://jscs.info/rule/requireObjectDestructuring)

> 为什么？因为解构能减少临时引用属性。

```javascript
// bad
function getFullName(user) {
    const firstName = user.firstName;
    const lastName = user.lastName;

    return `${firstName} ${lastName}`;
}

// good
function getFullName(obj) {
    const { firstName, lastName } = obj;
    return `${firstName} ${lastName}`;
}

// best
function getFullName({ firstName, lastName }) {
    return `${firstName} ${lastName}`;
}
```

- 对数组使用解构赋值。jscs: [`requireArrayDestructuring`](http://jscs.info/rule/requireArrayDestructuring)

```javascript
const arr = [1, 2, 3, 4];

// bad
const first = arr[0];
const second = arr[1];

// good
const [first, second] = arr;
```

- 需要回传多个值时，使用对象解构，而不是数组解构。jscs: [`disallowArrayDestructuringReturn`](http://jscs.info/rule/disallowArrayDestructuringReturn)

> 为什么？增加属性或者改变排序不会改变调用时的位置。

```javascript
// bad
function processInput(input) {
    // then a miracle occurs
    return [left, right, top, bottom];
}

// 调用时需要考虑回调数据的顺序。
const [left, __, top] = processInput(input);

// good
function processInput(input) {
    // then a miracle occurs
    return { left, right, top, bottom };
}

// 调用时只选择需要的数据
const { left, right } = processInput(input);
```
