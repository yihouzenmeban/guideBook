# 变量

- [13.1](#variables--const) 一直使用 `const` 来声明变量，如果不这样做就会产生全局变量。我们需要避免全局命名空间的污染。[地球队长](http://www.wikiwand.com/en/Captain_Planet)已经警告过我们了。（译注：全局，global 亦有全球的意思。地球队长的责任是保卫地球环境，所以他警告我们不要造成「全球」污染。）eslint: [`no-undef`](http://eslint.cn/docs/rules/no-undef) [`prefer-const`](http://eslint.cn/docs/rules/prefer-const)

```javascript
// bad
superPower = new SuperPower();

// good
const superPower = new SuperPower();
```

- 使用 `const` 声明每一个变量。eslint: [`one-var`](http://eslint.cn/docs/rules/one-var)

> 为什么？增加新变量将变的更加容易，而且你永远不用再担心调换错 `;` 跟 `,`。

```javascript
// bad
const items = getItems(),
    goSportsTeam = true,
    dragonball = 'z';

// bad
// (compare to above, and try to spot the mistake)
const items = getItems(),
    goSportsTeam = true;
    dragonball = 'z';

// good
const items = getItems();
const goSportsTeam = true;
const dragonball = 'z';
```

- 将所有的 `const` 和 `let` 分组

> 为什么？当你需要把已赋值变量赋值给未赋值变量时非常有用。

```javascript
// bad
let i, len, dragonball,
    items = getItems(),
    goSportsTeam = true;

// bad
let i;
const items = getItems();
let dragonball;
const goSportsTeam = true;
let len;

// good
const goSportsTeam = true;
const items = getItems();
let dragonball;
let i;
let length;
```

- 在你需要的地方给变量赋值，但请把它们放在一个合理的位置。

> 为什么？`let` 和 `const` 是块级作用域而不是函数作用域。

```javascript
// bad - 无意义的函数调用
function checkName(hasName) {
    const name = getName();

    if (hasName === 'test') {
        return false;
    }

    if (name === 'test') {
        this.setName('');
        return false;
    }

    return name;
}

// good
function checkName(hasName) {
    if (hasName === 'test') {
        return false;
    }

    const name = getName();

    if (name === 'test') {
        this.setName('');
        return false;
    }

    return name;
}
```

- 不要链式定义。

> 为什么? 链式定义会引起隐式的全局定义。

```javascript
// bad
(function example() {
    // JavaScript 解释为
    // let a = ( b = ( c = 1 ) );
    // let 只作用于 a，b 和 c 变成了全局定义。
    let a = b = c = 1;
}());

console.log(a); // undefined
console.log(b); // 1
console.log(c); // 1

// good
(function example() {
    let a = 1;
    let b = a;
    let c = a;
}());

console.log(a); // undefined
console.log(b); // undefined
console.log(c); // undefined

// `const` 也一样。
```

- ~~不要使用一元操作符 (++, --)。 eslint [`no-plusplus`](http://eslint.cn/docs/rules/no-plusplus)~~ `已删除`

> 为什么? 按照 eslint 的文档，一元操作符 `++` 和 `--` 会自动添加分号，不同的空白可能会改变源代码的语义。而且还会在项目中导致一些意外。

```javascript
// bad

const array = [1, 2, 3];
let num = 1;
num++;
--num;

let sum = 0;
let truthyCount = 0;
for (let i = 0; i < array.length; i++) {
    let value = array[i];
    sum += value;
    if (value) {
        truthyCount++;
    }
}

// good

const array = [1, 2, 3];
let num = 1;
num += 1;
num -= 1;

const sum = array.reduce((a, b) => a + b, 0);
const truthyCount = array.filter(Boolean).length;
```
