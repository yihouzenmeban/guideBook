# Strings

- 字符串使用单引号 `''` 。eslint: [`quotes`](http://eslint.cn/docs/rules/quotes)

```javascript
// bad
const name = "Capt. Janeway";

// good
const name = 'Capt. Janeway';
```

- 字符串超过 120 个字节不要使用字符串连接符写成多行。

> 为什么? 拆成多行的字符串很难维护而且不易于搜索。

```javascript
// bad
const errorMessage = 'This is a super long error that was thrown because \
of Batman. When you stop to think about how Batman had anything to do \
with this, you would get nowhere \
fast.';

// bad
const errorMessage = 'This is a super long error that was thrown because ' +
    'of Batman. When you stop to think about how Batman had anything to do ' +
    'with this, you would get nowhere fast.';

// good
const errorMessage = 'This is a super long error that was thrown because of Batman. When you stop to think about how Batman had anything to do with this, you would get nowhere fast.';
```

- 程序化生成字符串时，使用模板字符串代替字符串连接。

> 为什么？模板字符串更为简洁，更具可读性。

```javascript
// bad
function sayHi(name) {
    return 'How are you, ' + name + '?';
}

// bad
function sayHi(name) {
    return ['How are you, ', name, '?'].join();
}

// bad
function sayHi(name) {
    return `How are you, ${ name }?`;
}

// good
function sayHi(name) {
    return `How are you, ${name}?`;
}
```

- 永远不要对字符串使用 `eval()`，这个函数会引起很多问题。

- 不要在字符串中使用无意义的转义 eslint: [`no-useless-escape`](http://eslint.cn/docs/rules/no-useless-escape)

> 为什么? 反斜杠使可读性变差，因此只在必要的时候使用。

```javascript
// bad
const foo = '\'this\' \i\s \"quoted\"';

// good
const foo = '\'this\' is "quoted"';
const foo = `my name is '${name}'`;
```
