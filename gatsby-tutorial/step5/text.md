# Linting for Jest 

We'll install a plugin allowing us to Lint our jest tests with specific rules for Jest functions and avoiding testing mistakes

### Integrate Jest with ESLint

First install the *eslint-plugin-jest*

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

You should also add the following as a rule, in the same file, to avoid the nuisance of needing assertions for every test.

```js
'jest/prefer-expect-assertions': 'off',
```

