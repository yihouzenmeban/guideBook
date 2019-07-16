# 命名规则

- 避免单字母命名。命名应具备描述性。eslint: [`id-length`](http://eslint.org/docs/rules/id-length)

```javascript
// bad
function q() {
    // ...stuff...
}

// good
function query() {
    // ..stuff..
}
```

- 使用驼峰式命名对象、函数和实例。eslint: [`camelcase`](http://eslint.cn/docs/rules/camelcase)

```javascript
// bad
const OBJEcttsssss = {};
const this_is_my_object = {};
function c() {}

// good
const thisIsMyObject = {};
function thisIsMyFunction() {}
```

- 使用帕斯卡式命名（首字母大写）构造函数或类。eslint: [`new-cap`](http://eslint.cn/docs/rules/new-cap)

```javascript
// bad
function user(options) {
    this.name = options.name;
}

const bad = new user({
    name: 'nope',
});

// good
class User {
    constructor(options) {
        this.name = options.name;
    }
}

const good = new User({
    name: 'yup',
});
```

- ~~不要使用下划线 `_` 开头或者结尾进行命名。eslint: [`no-underscore-dangle`](http://eslint.cn/docs/rules/no-underscore-dangle)~~ `已删除`

```javascript
// bad
this.__firstName__ = 'Panda';
this.firstName_ = 'Panda';
this._firstName = 'Panda';

// good
this.firstName = 'Panda';
```

- ~~别保存 `this` 的引用。使用箭头函数或 [Function#bind](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/bind)。~~ `已删除`

```javascript
// bad
function foo() {
    const self = this;
    return function() {
        console.log(self);
    };
}

// bad
function foo() {
    const that = this;
    return function() {
        console.log(that);
    };
}

// good
function foo() {
    return () => {
        console.log(this);
    };
}
```

- 如果你的文件只输出一个类，那你的文件名必须和类名完全保持一致。

```javascript
// file 1 contents
class CheckBox {
    // ...
}
export default CheckBox;

// file 2 contents
export default function fortyTwo() { return 42; }

// file 3 contents
export default function insideDirectory() {}

// in some other file
// bad
import CheckBox from './checkBox'; // PascalCase import/export, camelCase filename
import FortyTwo from './FortyTwo'; // PascalCase import/filename, camelCase export
import InsideDirectory from './InsideDirectory'; // PascalCase import/filename, camelCase export

// bad
import CheckBox from './check_box'; // PascalCase import/export, snake_case filename
import forty_two from './forty_two'; // snake_case import/filename, camelCase export
import inside_directory from './inside_directory'; // snake_case import, camelCase export
import index from './inside_directory/index'; // requiring the index file explicitly
import insideDirectory from './insideDirectory/index'; // requiring the index file explicitly

// good
import CheckBox from './CheckBox'; // PascalCase export/import/filename
import fortyTwo from './fortyTwo'; // camelCase export/import/filename
import insideDirectory from './insideDirectory'; // camelCase export/import/directory name/implicit "index"
// ^ supports both insideDirectory.js and insideDirectory/index.js
```

- 当你导出默认的函数时使用驼峰式命名。你的文件名必须和函数名完全保持一致。

```javascript
function makeStyleGuide() {
}

export default makeStyleGuide;
```

- 当你导出单例、函数库、空对象时使用帕斯卡式命名。

```javascript
const AirbnbStyleGuide = {
    es6: {
    }
};

export default AirbnbStyleGuide;
```

- 缩略词或者缩写的单词应该全部大写或者小写。

> 为什么？为了更好的可读性。

```javascript
// bad
import SmsContainer from './containers/SmsContainer';

// bad
const HttpRequests = [
    // ...
];

// good
import SMSContainer from './containers/SMSContainer';

// good
const HTTPRequests = [
    // ...
];

// best
import TextMessageContainer from './containers/TextMessageContainer';

// best
const Requests = [
    // ...
];
```
