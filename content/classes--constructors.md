# 类 & 构造器

- 总是使用 `class`。避免直接操作 `prototype` 。

> 为什么? 因为 `class` 语法更为简洁更易读。

```javascript
// bad
function Queue(contents = []) {
    this._queue = [...contents];
}
Queue.prototype.pop = function() {
    const value = this._queue[0];
    this._queue.splice(0, 1);
    return value;
}


// good
class Queue {
    constructor(contents = []) {
        this._queue = [...contents];
    }
    pop() {
        const value = this._queue[0];
        this._queue.splice(0, 1);
        return value;
    }
}
```

- 使用 `extends` 继承。

> 为什么？因为 `extends` 是一个内建的原型继承方法并且不会破坏 `instanceof`。

```javascript
// bad
const inherits = require('inherits');
function PeekableQueue(contents) {
    Queue.apply(this, contents);
}
inherits(PeekableQueue, Queue);
PeekableQueue.prototype.peek = function() {
    return this._queue[0];
}

// good
class PeekableQueue extends Queue {
    peek() {
        return this._queue[0];
    }
}
```

- 方法可以返回 `this` 来帮助链式调用。

```javascript
// bad
Jedi.prototype.jump = function() {
    this.jumping = true;
    return true;
};

Jedi.prototype.setHeight = function(height) {
    this.height = height;
};

const luke = new Jedi();
luke.jump(); // => true
luke.setHeight(20); // => undefined

// good
class Jedi {
    jump() {
        this.jumping = true;
        return this;
    }

    setHeight(height) {
        this.height = height;
        return this;
    }
}

const luke = new Jedi();

luke.jump()
    .setHeight(20);
```

- 可以写一个自定义的 `toString()` 方法，但要确保它能正常运行并且不会引起副作用。

```javascript
class Jedi {
    constructor(options = {}) {
        this.name = options.name || 'no name';
    }

    getName() {
        return this.name;
    }

    toString() {
        return `Jedi - ${this.getName()}`;
    }
}
```

- 没有指定构造函数的类都有一个默认的构造函数，没有必要提供一个空的构造函数或只是简单的调用父类这样的构造函数。 eslint: [`no-useless-constructor`](http://eslint.cn/docs/rules/no-useless-constructor)

```javascript
// bad
class Jedi {
    constructor() {}

    getName() {
        return this.name;
    }
}

// bad
class Rey extends Jedi {
    constructor(...args) {
        super(...args);
    }
}

// good
class Rey extends Jedi {
    constructor(...args) {
        super(...args);
        this.name = 'Rey';
    }
}
```

- 不允许类成员中有重复的名称。 eslint: [`no-dupe-class-members`](http://eslint.cn/docs/rules/no-dupe-class-members)

> 为什么？重复的声明类成员都会被最后一个覆盖。

```javascript
// bad
class Foo {
    bar() { return 1; }
    bar() { return 2; }
}

// good
class Foo {
    bar() { return 1; }
}

// good
class Foo {
    bar() { return 2; }
}
```
