# 模块

- 总是使用 (`import`/`export`) 而不是其他非标准模块系统。你可以编译为你喜欢的模块系统。

> 为什么？模块就是未来，让我们开始迈向未来吧。

```javascript
// bad
const AirbnbStyleGuide = require('./AirbnbStyleGuide');
module.exports = AirbnbStyleGuide.es6;

// ok
import AirbnbStyleGuide from './AirbnbStyleGuide';
export default AirbnbStyleGuide.es6;

// best
import { es6 } from './AirbnbStyleGuide';
export default es6;
```

- 不要使用通配符 import。

> 为什么？这样能确保你只有一个默认 `export`。

```javascript
// bad
import * as AirbnbStyleGuide from './AirbnbStyleGuide';

// good
import AirbnbStyleGuide from './AirbnbStyleGuide';
```

- 不要从 `import` 中直接 export。

> 为什么？虽然一行代码简洁明了，但让 import 和 export 各司其职让事情能保持一致。

```javascript
// bad
// filename es6.js
export { es6 as default } from './airbnbStyleGuide';

// good
// filename es6.js
import { es6 } from './AirbnbStyleGuide';
export default es6;
```

- 相同路径只使用一次 `import`。eslint: [`no-duplicate-imports`](http://eslint.cn/docs/rules/no-duplicate-imports)

> 为什么？同一个路径使用多个 `import` 会使代码变的难以维护。

```javascript
// bad
import foo from 'foo';
// … some other imports … //
import { named1, named2 } from 'foo';

// good
import foo, { named1, named2 } from 'foo';

// good
import foo, {
    named1,
    named2,
} from 'foo';
```

- 不要 `export` 可变的绑定。eslint: [`import/no-mutable-exports`](https://github.com/benmosher/eslint-plugin-import/blob/master/docs/rules/no-mutable-exports.md)

```javascript
// bad
let foo = 3;
export { foo };

// good
const foo = 3;
export { foo };
```

- 在一个只有一个 export 的模块中，最好用默认 export 覆盖名字 export。eslint: [`import/prefer-default-export`](https://github.com/benmosher/eslint-plugin-import/blob/master/docs/rules/prefer-default-export.md)

```javascript
// bad
export function foo() {}

// good
export default function foo() {}
```

- 把所有的 `import` 放在 no-import 声明之前。eslint: [`import/first`](https://github.com/benmosher/eslint-plugin-import/blob/master/docs/rules/first.md)

> 为什么？因为 `import` 作用域提升，把它们放在最前面防止意外.

```javascript
// bad
import foo from 'foo';
foo.init();

import bar from 'bar';

// good
import foo from 'foo';
import bar from 'bar';

foo.init();
```

- 多行的 imports 应该和多行数组以及字面值对象一样的缩进规则。

```javascript
// bad
import {longNameA, longNameB, longNameC, longNameD, longNameE} from 'path';

// good
import {
    longNameA,
    longNameB,
    longNameC,
    longNameD,
    longNameE,
} from 'path';
```

- 禁止 Webpack 的加载语法出现在模块 import 语句中。eslint: [`import/no-webpack-loader-syntax`](https://github.com/benmosher/eslint-plugin-import/blob/master/docs/rules/no-webpack-loader-syntax.md)

> 为什么？在 imports 中使用 Webpack 语法会导致最后打包的代码重复，最好在 `webpack.config.js` 中使用加载语法。

```javascript
// bad
import fooSass from 'css!sass!foo.scss';
import barCss from 'style!css!bar.css';

// good
import fooSass from 'foo.scss';
import barCss from 'bar.css';
```
