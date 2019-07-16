# 空白

- 使用 4 个空格作为缩进。eslint: [`indent`](http://eslint.cn/docs/rules/indent)

```javascript
// bad
function() {
∙∙const name;
}

// bad
function() {
∙const name;
}

// good
function() {
∙∙∙∙const name;
}
```

- 在花括号前放一个空格。

```javascript
// bad
function test(){
    console.log('test');
}

// good
function test() {
    console.log('test');
}

// bad
dog.set('attr',{
    age: '1 year',
    breed: 'Bernese Mountain Dog',
});

// good
dog.set('attr', {
    age: '1 year',
    breed: 'Bernese Mountain Dog',
});
```

- 在控制语句（`if`、`while` 等）的小括号前放一个空格。在函数调用及声明中，不在函数的参数列表前加空格。eslint: [`keyword-spacing`](http://eslint.cn/docs/rules/keyword-spacing)

```javascript
// bad
if(isJedi) {
    fight ();
}

// good
if (isJedi) {
    fight();
}

// bad
function fight () {
    console.log ('Swooosh!');
}

// good
function fight() {
    console.log('Swooosh!');
}
```

- 使用空格把运算符隔开。eslint: [`space-infix-ops`](http://eslint.cn/docs/rules/space-infix-ops)

```javascript
// bad
const x=y+5;

// good
const x = y + 5;
```

- 在文件末尾插入一个空行。eslint: [`eol-last`](https://github.com/eslint/eslint/blob/master/docs/rules/eol-last.md)

```javascript
// bad
import { es6 } from './AirbnbStyleGuide';
    // ...
export default es6;
```

```javascript
// bad
import { es6 } from './AirbnbStyleGuide';
    // ...
export default es6;↵
↵
```

```javascript
// good
import { es6 } from './AirbnbStyleGuide';
    // ...
export default es6;↵
```

- 在使用长方法链时进行缩进（超过两个方法时）。使用前面的点 `.` 强调这是方法调用而不是新语句。eslint: [`newline-per-chained-call`](http://eslint.cn/docs/rules/newline-per-chained-call) [`no-whitespace-before-property`](http://eslint.cn/docs/rules/no-whitespace-before-property)

```javascript
// bad
$('#items').find('.selected').highlight().end().find('.open').updateCount();

// bad
$('#items').
    find('.selected').
    highlight().
    end().
    find('.open').
    updateCount();

// good
$('#items')
    .find('.selected')
    .highlight()
    .end()
    .find('.open')
    .updateCount();

// bad
const leds = stage.selectAll('.led').data(data).enter().append('svg:svg').classed('led', true)
    .attr('width', (radius + margin) * 2).append('svg:g')
    .attr('transform', `translate(${radius + margin},${radius + margin})`)
    .call(tron.led);

// good
const leds = stage.selectAll('.led')
    .data(data)
    .enter().append('svg:svg')
    .classed('led', true)
    .attr('width', (radius + margin) * 2)
    .append('svg:g')
    .attr('transform', `translate(${radius + margin},${radius + margin})`)
    .call(tron.led);

// good
const leds = stage.selectAll('.led').data(data);
```

- 在块末和新语句前插入空行。

```javascript
// bad
if (foo) {
    return bar;
}
return baz;

// good
if (foo) {
    return bar;
}

return baz;

// bad
const obj = {
    foo() {
    },
    bar() {
    },
};
return obj;

// good
const obj = {
    foo() {
    },

    bar() {
    },
};

return obj;

// bad
const arr = [
    function foo() {
    },
    function bar() {
    },
];
return arr;

// good
const arr = [
    function foo() {
    },

    function bar() {
    },
];

return arr;
```

- 禁止块内填充空行。eslint: [`padded-blocks`](http://eslint.cn/docs/rules/padded-blocks)

```javascript
// bad
function bar() {

    console.log(foo);

}

// also bad
if (baz) {

    console.log(qux);
} else {
    console.log(foo);

}

// good
function bar() {
    console.log(foo);
}

// good
if (baz) {
    console.log(qux);
} else {
    console.log(foo);
}
```

- 不要在圆括号内加空格。eslint: [`space-in-parens`](http://eslint.cn/docs/rules/space-in-parens)

```javascript
// bad
function bar( foo ) {
    return foo;
}

// good
function bar(foo) {
    return foo;
}

// bad
if ( foo ) {
    console.log(foo);
}

// good
if (foo) {
    console.log(foo);
}
```

- 不要在方括号内加空格。eslint: [`array-bracket-spacing`](http://eslint.cn/docs/rules/array-bracket-spacing)

```javascript
// bad
const foo = [ 1, 2, 3 ];
console.log(foo[ 0 ]);

// good
const foo = [1, 2, 3];
console.log(foo[0]);
```

- 在花括号内加空格。eslint: [`object-curly-spacing`](http://eslint.cn/docs/rules/object-curly-spacing)

```javascript
// bad
const foo = {clark: 'kent'};

// good
const foo = { clark: 'kent' };
```

- 单行代码不要超过 120 个字符串（空格计算在内, 这个是大家投票出来确定的数值）。 注意：[above](#strings--line-length), 长字符串不遵循这条规则而且长字符串不应该被折行。eslint: [`max-len`](http://eslint.cn/docs/rules/max-len)

> 为什么？为了可读性和可维护性。

```javascript
// bad
const foo = jsonData && jsonData.foo && jsonData.foo.bar && jsonData.foo.bar.baz && jsonData.foo.bar.baz.quux && jsonData.foo.bar.baz.quux.xyzzy;

// bad
$.ajax({ method: 'POST', url: 'https://airbnb.com/', data: { name: 'John' } }).done(() => console.log('Congratulations!')).fail(() => console.log('You have failed this city.'));

// good
const foo = jsonData
    && jsonData.foo
    && jsonData.foo.bar
    && jsonData.foo.bar.baz
    && jsonData.foo.bar.baz.quux
    && jsonData.foo.bar.baz.quux.xyzzy;

// good
$.ajax({
    method: 'POST',
    url: 'https://airbnb.com/',
    data: { name: 'John' },
})
    .done(() => console.log('Congratulations!'))
    .fail(() => console.log('You have failed this city.'));
```
