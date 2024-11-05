# Add the CI/CD Workflow

Firstly we need to navigate to 

```plain
https://github.com/<user-name>/<repository-name>/settings/actions
```


and change the workflow permissions to read and write. This is to allow our workflow to create a branch for deployment.

Then we have to create *.github/workflows* directory and then add a yaml file that describes our CI/CD workflow

```plain
mkdir -p .github/workflows
vim .github/workflows/deploy.yml
```{{exec}}

Add the following code:

```yml
name: Gatsby CI/CD

on:
  push:
    branches:
      - main

jobs:
  lint:
    name: Lint Code
    runs-on: ubuntu-latest
    steps:
      - name: Checkout Code
        uses: actions/checkout@v3

      - name: Set up Node.js
        uses: actions/setup-node@v3
        with:
          node-version: '20' 

      - name: Install Dependencies
        run: npm install --legacy-peer-deps

      - name: Run Lint
        run: npm run lint
       

  test:
    name: Run Tests
    runs-on: ubuntu-latest
    needs: lint 
    steps:
      - name: Checkout Code
        uses: actions/checkout@v3

      - name: Set up Node.js
        uses: actions/setup-node@v3
        with:
          node-version: '20'

      - name: Install Dependencies
        run: npm install --legacy-peer-deps

      - name: Run Tests
        run: npm test
        

  deploy:
    name: Deploy to GitHub Pages
    runs-on: ubuntu-latest
    needs: test 
    steps:
      - name: Checkout Code
        uses: actions/checkout@v3

      - name: Set up Node.js
        uses: actions/setup-node@v3
        with:
          node-version: '20'

      - name: Install Dependencies
        run: npm install --legacy-peer-deps

      - name: Build Gatsby
        run: npm run build -- --prefix-paths

      - name: Deploy to GitHub Pages
        uses: peaceiris/actions-gh-pages@v3
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          publish_dir: ./public 
        

```{{exec}}

The workflow runs the linting, and tests and prevents deployment if there are any big errors.

If there are no big errors we'll run the gatsby building process, taking all the react code and templates to create the static HTML, CSS and javascript files it can send to the end user, and store them in the  in the public directory. In deployment we then upload the contents of this public directory.


![CI/CD Workflow](./workflow.png)

Add the line to the *gatsby-config-.js* file inside *module.exports*.


```js
pathPrefix: '/<your-repo-name>'
```

This ensures the site still works even if it will be hosted not on the root of the website which it won't be by default when we deploy using github pages. 


 
### Locally running tests from the workflow

Let's locally run the and fix issues before pushing

```plain
npm run lint 
```{{exec}}

As you can see there are a few errors. Fix them by running 

```plain
npm run lint --fix
```{{exec}}

One error isn't fixed by running this command. We'll manually disable that check with a comment in **src/__test__/Counter.test.js** like below

```js
describe('counter', () => {
  // eslint-disable-next-line jest/no-hooks
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
```

There is still a warning, but that won't stop us from deploying

We'll also do 

```plain
npm run test
```{{exec}}

and 

```plain 
npm run build
```{{exec}}

Since they all work we'll try running them using Github actions by pushing into our repository

```plain
git add -A
git commit -m "Add CI/CD Workflow"
git push
```{{exec}}

In Github you'll now be able to see that your workflow is running in the action tab.

Congratulations! You have now set up a projects with a CI/CD workflow. In the next page we'll show you how to deploy the website using gh-pages if you'd like that.