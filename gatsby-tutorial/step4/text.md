### Set Up Testing with Jest

In this step we're setting up the testing framework Jest 

### Install Jest

Use npm to install jest and other related packages

```plain
npm install --save-dev --legacy-peer-deps jest babel-jest babel-preset-gatsby identity-obj-proxy
```{{exec}}

### Create Jest config

Open *jest.config.js* file:

```plain
vim jest.config.js
```{{exec}}

And add the following content:

```js
module.exports = {
  transform: {
    '^.+\\.jsx?$': '<rootDir>/jest-preprocess.js',
  },
  moduleNameMapper: {
    '.+\\.(css|styl|less|sass|scss)$': 'identity-obj-proxy',
    '.+\\.(jpg|jpeg|png|gif|eot|otf|webp|svg|ttf|woff|woff2|mp4|webm|wav|mp3|m4a|aac|oga)$': '<rootDir>/_mocks/file-mock.js',
  },
  testPathIgnorePatterns: ['node_modules', '\\.cache', '<rootDir>.*/public'],
  transformIgnorePatterns: ['node_modules/(?!(gatsby|gatsby-script|gatsby-link)/)'],
  globals: {
    __PATH_PREFIX__: true,
  },
  testEnvironmentOptions: {
    url: 'http://localhost/',
  },
  setupFiles: ['<rootDir>/loadershim.js'],
};

```{{exec}}

Create a preprocessor file so that jest can handle Gatsby's syntax

```plain
vim jest-preprocess.js
```{{exec}}

Add the following content:

```js
const babelOptions = {
  presets: ['babel-preset-gatsby'],
};{{exec}}

module.exports = require('babel-jest').default.createTransformer(babelOptions);
```

Next, create the *loadershim.js* file to mock Gatsby’s loader object:

```plain
vim loadershim.js
```{{exec}}

Add the following code:

```js
global.loader = {
  enqueue: jest.fn(),
};
```{{exec}}

### Add script in *package.json*

Open *package.json*:

```plain
vim package.json
```{{exec}}

In the *"scripts"* section, add the following line:

```js
"test": "jest"
```

### Create example Test File

Now, let’s create a template of a test file First, create a `tests` directory inside the `src` folder:

```plain
mkdir src/tests
```{{exec}}

Then, create the `example.test.js` file inside `src/tests`:

```plain
vim src/tests/example.test.js
```{{exec}}

Add the following basic test:

```js
describe('example', () => {
  test('should pass', () => {
    expect(true).toBe(true);
  });
});
```{{exec}}
Now we can run tests using 

```plain
npm run test
```{{exec}}







