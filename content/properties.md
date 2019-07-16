# 属性

- 使用 `.` 来访问对象的属性。eslint: [`dot-notation`](http://eslint.cn/docs/rules/dot-notation)

```javascript
const luke = {
    jedi: true,
    age: 28,
};

// bad
const isJedi = luke['jedi'];

// good
const isJedi = luke.jedi;
```

- 当通过变量访问属性时使用 `[]`。

```javascript
const luke = {
    jedi: true,
    age: 28,
};

function getProp(prop) {
    return luke[prop];
}

const isJedi = getProp('jedi');
```
