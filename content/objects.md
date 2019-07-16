# 对象

- 使用字面值创建对象。eslint: [`no-new-object`](http://eslint.cn/docs/rules/no-new-object)

```javascript
// bad
const item = new Object();

// good
const item = {};
```

- 创建有动态属性名的对象时，使用可被计算的属性名称。

> 为什么？因为这样可以让你一次定义所有的对象属性。

```javascript
function getKey(k) {
    return `a key named ${k}`;
}

// bad
const obj = {
    id: 5,
    name: 'San Francisco',
};
obj[getKey('enabled')] = true;

// good
const obj = {
    id: 5,
    name: 'San Francisco',
    [getKey('enabled')]: true,
};
```

- 使用对象方法的简写。eslint: [`object-shorthand`](http://eslint.cn/docs/rules/object-shorthand)

```javascript
// bad
const atom = {
    value: 1,

    addValue: function (value) {
        return atom.value + value;
    },
};

// good
const atom = {
    value: 1,

    addValue(value) {
        return atom.value + value;
    },
};
```

- 使用对象属性值的简写。eslint: [`object-shorthand`](http://eslint.cn/docs/rules/object-shorthand)

> 为什么？因为这样更简短而且更形象。

```javascript
const lukeSkywalker = 'Luke Skywalker';

// bad
const obj = {
    lukeSkywalker: lukeSkywalker,
};

// good
const obj = {
    lukeSkywalker,
};
```

- 声明对象属性之前对简写的属性分组。

> 为什么？因为这样能清楚地看出哪些属性使用了简写。

```javascript
const anakinSkywalker = 'Anakin Skywalker';
const lukeSkywalker = 'Luke Skywalker';

// bad
const obj = {
    episodeOne: 1,
    twoJedisWalkIntoACantina: 2,
    lukeSkywalker,
    episodeThree: 3,
    mayTheFourth: 4,
    anakinSkywalker,
};

// good
const obj = {
    lukeSkywalker,
    anakinSkywalker,
    episodeOne: 1,
    twoJedisWalkIntoACantina: 2,
    episodeThree: 3,
    mayTheFourth: 4,
};
```

- 对无效的标识符使用引号。eslint: [`quote-props`](http://eslint.cn/docs/rules/quote-props)

> 为什么? 一般我们主观上认为这样可读性更好，这样可以改善语法高亮，而且更容易被 JS 引擎优化。

```javascript
// bad
const bad = {
    'foo': 3,
    'bar': 4,
    'data-blah': 5,
};

// good
const good = {
    foo: 3,
    bar: 4,
    'data-blah': 5,
};
```

- 最好使用[`扩展运算符`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_operator)代替 [`Object.assign`](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_Objects/Object/assign) 去浅拷贝对象，重新定义一个对象去得到一个去除确定属性的的新对象。

```javascript
// very bad
const original = { a: 1, b: 2 };
const copy = Object.assign(original, { c: 3 }); // this mutates `original` ಠ_ಠ
delete copy.a; // so does this

// bad
const original = { a: 1, b: 2 };
const copy = Object.assign({}, original, { c: 3 }); // copy => { a: 1, b: 2, c: 3 }

// good
const original = { a: 1, b: 2 };
const copy = { ...original, c: 3 }; // copy => { a: 1, b: 2, c: 3 }

const { a, ...noA } = copy; // noA => { b: 2, c: 3 }
```
