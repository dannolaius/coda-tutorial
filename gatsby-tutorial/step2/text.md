# Set up a git and your GitHub repo


(Before starting ensure that you're inside your gatsby directory)
Go to [GitHub](https://github.com) and create a new repository:
   - Navigate to your GitHub dashboard.
   - Click the **New** button next to **Repositories**.
   - Choose a **repository name**.
   - Set the repository to **public** ()
   - Click **Create repository**.

#### Generating a Personal Access Token (PAT)

Because we wouldn't want you to enter unscoped credentials into KillerCoda, which you should **NOT** do, we'll need to create a temporary and fine-grained Personal Access Token (PAT) to authenticate your git commands when pushing to GitHub. Follow these steps:

1. Visit [GitHub PAT settings](https://github.com/settings/tokens) to create a new token.
2. Click **Generate new token**.
3. Choose **Fine-grained token** for better security control.
4. Enter a **token name** and choose an **expiration date** (this limits how long the token can access the repository).
5. Under **Repository access**:
   - Select **Only select repositories**.
   - Choose **<repository-name>** (this is the new repository you just created for this tutorial).
6. Under **Repository permissions**, allow:
   - **Read** and **write** permissions for **all repository permissions**. (you need to do it one permission at a time, sorry)
   - **No access** for all **account permissions** (since this PAT will only be used for this repository).
7. Click **Generate token** and copy the generated token. **(Make sure to save it somewhere safe, as you won’t be able to view it again later!)**

####  Configure Git  and make it use your PAT

Start by initializing git in your repository.

 ```plain
git init
```{{exec}}

And adding a remote origin using the link to the repo you just created

```plain
git remote add origin https://github.com/<your-user-name>/<your-repository-name>.git
```{{terminal}}

Now we'll add commit and push the changes

1. Add all files to the staging area:

    ```plain
    git add .
    ```{{exec}}

2. Commit your changes:

    ```plain
    git commit -m "Initial commit"
    ```{{exec}}

3. Push your changes to GitHub:

    ```plain
    git push --set-upstream origin main
    ```{{exec}}

(set-upstream origin main flag is only necessary during the first push)

You'll be asked to provide your github username and password **DO NOT** use your actual password instead use the generated fine-grained PAT token you just created

To avoid entering the token every time you push a new change, you can set up the remote URL to include your GitHub username and the token. This is a temporary workaround for the purpose of this tutorial—do **not** use this method in real projects as it exposes your token. Instead, use **SSH keys** in production environments.

```plain
git remote set-url origin https://<your-username>:<your-token>@github.com/<your-username>/<repository-name>.git
```{{terminal}}


If you followed the steps correctly, your code will now be pushed to the GitHub repository. Congratulations!