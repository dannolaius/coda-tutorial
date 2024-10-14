# Setting Up a Gatsby Project

In this section, we will set up a new Gatsby project and configure it with Tailwind for styling.

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
    git config --global user.email "you@example.com"
    ```{{exec}}

2. Set your Git username:

    ```plain
    git config --global user.name "Your Name"
    ```{{exec}}

### Initializing a Gatsby Project

To create a new Gatsby project, follow these steps:

1. Run the following command to initialize a new Gatsby project:

    ```plain
    npm init gatsby
    ```{{exec}}

2. Follow the prompts:
   - Press Enter or type Y to install the necessary package.
   - Press Enter for the default project name.
   - Press Enter for the default folder name.
   - Press Enter to choose Javascript over Typescript
   - Press Enter to choose No CMS
   - Press Enter to choose No Styling System
   - Skip all optional features by pressing Enter on the done button.
   - Confirm the installation by pressing Enter or typing Y

Enter the directory of your new Gatsby Project

    ```plain
    cd my-gatsby-site
    ```{{exec}}


Congratulations you've setup the template of a Gatsby project!
