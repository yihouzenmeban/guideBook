# 存取器

- 属性的存取函数不是必须的。

- 不要使用 JavaScript `getters/setters`，因为它们会引起副作用，而且会导致代码很难测试，维护和阅读。如果创建获取函数，使用 getVal() 和 setVal('hello')。

```javascript
// bad
class Dragon {
    get age() {
        // ...
    }

    set age(value) {
        // ...
    }
}

// good
class Dragon {
    getAge() {
        // ...
    }

    setAge(value) {
        // ...
    }
}
```

- 如果属性是布尔值，使用 `isVal()` 或 `hasVal()`。

```javascript
// bad
if (!dragon.age()) {
    return false;
}

// good
if (!dragon.hasAge()) {
    return false;
}
```

- 创建 `get()` 和 `set()` 函数是可以的，但要保持一致。

```javascript
class Jedi {
    constructor(options = {}) {
        const lightsaber = options.lightsaber || 'blue';
        this.set('lightsaber', lightsaber);
    }

    set(key, val) {
        this[key] = val;
    }

    get(key) {
        return this[key];
    }
}
```
