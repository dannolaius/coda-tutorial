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
extends: ['react-app', 'plugin:jest/all'],
```

You should also add the following as a rule to avoid the nuisance of needing assertions for every test.

```js
'jest/prefer-expect-assertions': 'off',
```

