# 逗号

- 行首逗号：**不需要**。eslint: [`comma-style`](http://eslint.cn/docs/rules/comma-style)

```javascript
// bad
const story = [
        once
    , upon
    , aTime
];

// good
const story = [
    once,
    upon,
    aTime,
];

// bad
const hero = {
        firstName: 'Ada'
    , lastName: 'Lovelace'
    , birthYear: 1815
    , superPower: 'computers'
};

// good
const hero = {
    firstName: 'Ada',
    lastName: 'Lovelace',
    birthYear: 1815,
    superPower: 'computers',
};
```

- ~~增加结尾的逗号: **需要**。eslint: [`comma-dangle`](http://eslint.cn/docs/rules/comma-dangle)~~ `已删除`

> ~~为什么? 这会让 git diffs 更干净。另外，像 babel 这样的转译器会移除结尾多余的逗号，也就是说你不必担心老旧浏览器的[尾逗号问题](es5/README.md#commas)。~~
> 禁止添加结尾的逗号。

```diff
// bad - git diff without trailing comma
const hero = {
        firstName: 'Florence',
-    lastName: 'Nightingale'
+    lastName: 'Nightingale',
+    inventorOf: ['coxcomb chart', 'modern nursing']
};

// good - git diff with trailing comma
const hero = {
        firstName: 'Florence',
        lastName: 'Nightingale',
+    inventorOf: ['coxcomb chart', 'modern nursing'],
};
```

```javascript
// bad
const hero = {
    firstName: 'Dana',
    lastName: 'Scully'
};

const heroes = [
    'Batman',
    'Superman'
];

// good
const hero = {
    firstName: 'Dana',
    lastName: 'Scully',
};

const heroes = [
    'Batman',
    'Superman',
];

// bad
function createHero(
    firstName,
    lastName,
    inventorOf
) {
    // does nothing
}

// good
function createHero(
    firstName,
    lastName,
    inventorOf,
) {
    // does nothing
}

// good (note that a comma must not appear after a "rest" element)
function createHero(
    firstName,
    lastName,
    inventorOf,
    ...heroArgs
) {
    // does nothing
}

// bad
createHero(
    firstName,
    lastName,
    inventorOf
);

// good
createHero(
    firstName,
    lastName,
    inventorOf,
);

// good (note that a comma must not appear after a "rest" element)
createHero(
    firstName,
    lastName,
    inventorOf,
    ...heroArgs
);
```
