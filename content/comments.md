# 注释

- 使用 `/** ... */` 作为多行注释。

```javascript
// bad
// make() returns a new element
// based on the passed in tag name
//
// @param {String} tag
// @return {Element} element
function make(tag) {

    // ...

    return element;
}

// good
/**
    * make() returns a new element
    * based on the passed-in tag name
    */
function make(tag) {

    // ...

    return element;
}
```

- 使用 `//` 作为单行注释。在评论对象上面另起一行使用单行注释。在注释前插入空行。

```javascript
// bad
const active = true;  // is current tab

// good
// is current tab
const active = true;

// bad
function getType() {
    console.log('fetching type...');
    // set the default type to 'no type'
    const type = this._type || 'no type';

    return type;
}

// good
function getType() {
    console.log('fetching type...');

    // set the default type to 'no type'
    const type = this._type || 'no type';

    return type;
}

// also good
function getType() {
    // set the default type to 'no type'
    const type = this.type || 'no type';

    return type;
}
```

- 在所有的注释内容开始之前添加一个空格使它更容易被阅读。eslint: [`spaced-comment`](http://eslint.cn/docs/rules/spaced-comment)

```javascript
// bad
//is current tab
const active = true;

// good
// is current tab
const active = true;

// bad
/**
    *make() returns a new element
    *based on the passed-in tag name
    */
function make(tag) {

    // ...

    return element;
}

// good
/**
    * make() returns a new element
    * based on the passed-in tag name
    */
function make(tag) {

    // ...

    return element;
}
```

- 给注释增加 `FIXME` 或 `TODO` 的前缀可以帮助其他开发者快速了解这是一个需要复查的问题，或是给需要实现的功能提供一个解决方式。这将有别于常见的注释，因为它们是可操作的。使用 `FIXME -- need to figure this out` 或者 `TODO -- need to implement`。

- 使用 `// FIXME`: 标注问题。

```javascript
class Calculator {
    constructor() {
        // FIXME: shouldn't use a global here
        total = 0;
    }
}
```

- 使用 `// TODO`: 标注问题的解决方式。

```javascript
class Calculator {
    constructor() {
        // TODO: total should be configurable by an options param
        this.total = 0;
    }
}
```
