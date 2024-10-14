# Integrating ESLint with Jest

### Integrate Jest with ESLint

First install Jest plugin for ESlint

```plain
npm i eslint-plugin-jest --save-dev --legacy-peer-deps
```{{exec}}

This now requires uss to update our ESLint configuration file *.eslintrc.js*

```plain
vim .eslintrc.js
```{{exec}}

We'll replace:

```js
extends: 'react-app',
```
with: 

```js
extends: [`react-app`, 'plugin:jest/all'],
```

Avoid needing to use assertions by adding this rule to *.eslintrc.js* because not all tests need assertions, and it can be quite a nuisance to enforce this lint rule

```plain
vim .eslintrc.js
```{{exec}}

```js
'jest/prefer-expect-assertions': 'off',
```

