# Set up linting with ESLint 

In this step we'll set up linting. Linting is a type of static code analysis that can be useful for identifying programming errors or stylistic errors. 

### Install ESLint 

Let's install the ESLint package

```plain
npm install --save-dev --legacy-peer-deps eslint-config-react-app eslint@8.57.1
```{{exec}}

### Configure ESLint

Create the *.eslintrc.js* file:

```plain
vim .eslintrc.js
```{{exec}}

Add this to the file:

```js
module.exports = {
  globals: {
    __PATH_PREFIX__: true,
  },
  extends: 'react-app',
  rules: {
    'prefer-const': 'error',
  },
};
```{{exec}}

### Add lint script in *package.json*

To run the linter from the commandline add a script to *package.json*

Open the *package.json* file:

```plain
vim package.json
```{{exec}}

Find the *"scripts"* section and add the following line:

```js
"lint": "eslint src/**/*.{js,jsx,ts,tsx}"
```{{exec}}

Ensure that all scripts, except the last one, end with a comma!

Now ESLint can be run with the command

```plain
npm run lint
```{{exec}}

You've now added lint to your project congratulations!