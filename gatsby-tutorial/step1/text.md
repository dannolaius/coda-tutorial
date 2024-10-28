# An Introduction to Gatsby and basic initialization

In this section we'll explain what Gatsby is and how you initialize a Gatsby project. 

### What is Gatsby?

Gatsby is a **static site generator**. Meaning it takes source files containing content and files defining the template to create static HTML files that can be served during build. This makes loading faster than for websites that does this creating of HTML files upon user requests.

What makes Gatsby different than so many other 

### Prerequisites

Let's start by getting **Node.js** installed. 

1. Install NVM (Node Version Manager):

    ```plain
    curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.4/install.sh | bash
    ```{{exec}}

2. Load NVM into the current shell session:

    ```plain
    source ~/.bashrc
    ```{{exec}}

3. Install the latest LTS version of Node.js:

    ```plain
    nvm install --lts
    ```{{exec}}

4. Check that Node.js is installed correctly:

    ```plain
    node -v
    ```{{exec}}

Additionally, let's configure git that should already be installed on the machine:

1. Set your Git email:

    ```plain
    git config --global user.email "gatsby@tutorial.com"
    ```{{exec}}

2. Set your Git username:

    ```plain
    git config --global user.name "Gatsby Gat"
    ```{{exec}}

### Initializing a Gatsby Project

To create a new Gatsby project, follow these steps:

1. Run the following command to initialize a new Gatsby project:

    ```plain
    npm init gatsby
    ```{{exec}}

2. Follow the prompts:
   - Press Enter (or type y) to install the necessary package.
   - Press Enter for the default project name.
   - Press Enter for the default folder name.
   - Press Enter to choose Javascript over Typescript
   - Press Enter to choose No CMS
   - Press Enter to choose No Styling System
   - Skip all optional features by pressing Enter on the done button.
   - Confirm the installation by pressing Enter (or typing y)

Installation might take a while. You can look at the next page while you're waiting.


Once installation is finished, enter the directory of your new Gatsby Project


```plain
cd my-gatsby-site
```{{exec}}

Congratulations you've setup the template of a Gatsby project!
