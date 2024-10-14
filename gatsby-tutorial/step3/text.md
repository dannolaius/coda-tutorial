# Setting up linting with ESLint 

Linting is useful to find both style and programming errors.  We'll use the *eslint-config-react-app* package

### Install ESLint 

Let's install the ESLint package

```plain
npm install --save-dev eslint-config-react-app
```{{exec}}

### Configure ESLint

```plain
vim .eslintrc.js
```{{exec}}

Add this to the file:

```js
module.exports = {
  globals: {
    __PATH_PREFIX__: true,
  },
  extends: `react-app`,
  rules: {
    'prefer-const': 'error',
  },
};
```

### Add lint script in package.json

To run the linter from the commandline add a script to *package.json*

Open the *package.json* file:

```plain
vim package.json
```{{exec}}

Find the *"scripts"* section and add the following line:

```json
"lint": "eslint src/**/*.{js,jsx,ts,tsx}",
```{{exec}}

You might've to add a comma to the line above as well

Now ESLint can be run with the command

```plain
npm run lint
```{{exec}}