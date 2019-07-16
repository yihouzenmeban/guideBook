# 配置文件

在根目录下创建 `.eslintrc.js`

```javascript
module.exports = {
    extends: 'airbnb-base',
    plugins: [
        'import'
    ],
    rules: {
        'no-console': 0,
        'no-alert': 0,
        'no-plusplus': 0,
        'no-unused-expressions': 0,
        'func-names': 0,
        'eqeqeq': 0,
        'no-underscore-dangle': 0,
        'no-param-reassign': 0,
        'no-new': 0,
        'import/no-unresolved': 0,
        'import/no-extraneous-dependencies': 0,
        'linebreak-style': 0,

        // error
        'indent': [2, 4, {
            SwitchCase: 1,
            VariableDeclarator: 1,
            outerIIFEBody: 1,
            FunctionDeclaration: {
                parameters: 1,
                body: 1
            },
            FunctionExpression: {
                parameters: 1,
                body: 1
            }
        }],
        'space-before-function-paren': [2, 'never'],
        'wrap-iife': [2, 'inside', { functionPrototypeMethods: true }],
        'comma-dangle': [2, 'never'],
        'max-len': [2, 120, 4, {
            ignoreUrls: true,
            ignoreComments: false,
            ignoreRegExpLiterals: true,
            ignoreStrings: true,
            ignoreTemplateLiterals: true
        }]
    }
};
```
