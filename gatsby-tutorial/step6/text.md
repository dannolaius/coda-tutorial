# Create tests for the React Components

We'll want to create tests for react components. This requires installing more libraries.

```plain
npm install --save-dev --legacy-peer-deps @testing-library/react @testing-library/dom @testing-library/jest-dom jest-environment-jsdom @testing-library/user-event
```{{exec}}

This library requires a setup file that'll now create.

```plain
vim setup-test-env.js
```{{exec}}

Add this code to the file
```js
import '@testing-library/jest-dom';
```{{exec}}

### Integrate with Jest

We'll make Jest run the setup file by updating the Jest configuration file


```plain
vim jest.config.js
```{{exec}}

Add these lines:

```javascript
testEnvironment: 'jsdom',
setupFilesAfterEnv: ['<rootDir>/setup-test-env.js'],
```

### Create some react components:

Let's create a react component just to show the principles of how you create tests for certain components.

```plain 
mkdir src/components
```{{exec}}
```plain 
vim src/components/Counter.js
```{{exec}}

Add the following code

```js
import React from 'react';

const Counter = () => {
  const [count, setCount] = React.useState(0);

  const increment = () => {
    setCount(count + 1);
  };

  const decrement = () => {
    setCount(count - 1);
  };

  return (
    <div>
      <h1>Counter</h1>
      <p>Current count: {count}</p>
      <button onClick={increment}>Increment</button>
      <button onClick={decrement}>Decrement</button>
    </div>
  );
};

export default Counter;
```{{exec}}

The code describes a Counter with increment and decrement buttons. The details of this code doesn't really matter we're just adding any component that we can test.


Thereafter we'll add this component to *index.js* which will display it on your webites root.

```plain
vim src/pages/index.js 
```{{exec}}

Add following code (you can remove the code that was there previously):

```js
import * as React from 'react';
import Counter from '../components/Counter';

const IndexPage = () => {
  return (
    <div>
      <h1>Home Page</h1>
      <Counter />
    </div>
  );
};

export default IndexPage;

export const Head = () => <title>Home Page</title>;
```{{exec}}

### Create a test for the component

Create directory to store tests:

```plain
mkdir src/components/__tests__
```{{exec}}


```plain
vim src/components/__tests__/Counter.test.js
```{{exec}}

Add the following code for a test:

```js
import React from 'react';
import { render, screen, cleanup } from '@testing-library/react';
import userEvent from '@testing-library/user-event';
import Counter from '../Counter';

describe('counter', () => {
  afterEach(() => {
    cleanup();
  });

  it('counter increments the count', async () => {
    render(<Counter />);
    const user = userEvent.setup();
    const counter = screen.getByText(/Current count/i);
    expect(counter).toHaveTextContent('Current count: 0');
    await user.click(screen.getByText(/Increment/i));
    expect(counter).toHaveTextContent('Current count: 1');
  });
});
```{{exec}}

This code will test wether the component actually increments with a user click by rendering the Counter using the react testing-library functions and checking that it behaves correctly using jest functions.

Congratulations you've now added a component to your website and a test for that component.

