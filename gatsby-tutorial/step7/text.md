# Add the CI/CD Workflow

Firstly we need to navigate to 
```plain
https://github.com/<user-name>/<repository-name>/settings/actions
``` 
and change the workflow permissions to read and write

Then we have to create *.github/workflows* directory and then add a yaml file that describes our CI/CD workflow

```plain
mkdir -p .github/workflows
vim .github/workflows/deploy.yml
```{{exec}}

Add the following code:
```yml
name: Gatsby CI/CD

# Run the workflow on push to the main branch and pull requests
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
          node-version: '20' # Ensure you're using the correct version

      - name: Install Dependencies
        run: npm install --legacy-peer-deps

      - name: Run Lint
        run: npm run lint
        # Use your linter command (e.g., `npm run lint` or `eslint .`)

  test:
    name: Run Tests
    runs-on: ubuntu-latest
    needs: lint # Ensure linting passes before testing
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
        # Use your testing command (e.g., `npm test` or `jest`)

  deploy:
    name: Deploy to GitHub Pages
    runs-on: ubuntu-latest
    needs: test # Ensure tests pass before deploying
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
        run: npm run build

      - name: Deploy to GitHub Pages
        uses: peaceiris/actions-gh-pages@v3
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          publish_dir: ./public # The directory where the built files are located
```

Now we just push it to our repository

```plain
git add -A
git commit -m "Add CI/CD Workflow"
git push
```{{exec}}