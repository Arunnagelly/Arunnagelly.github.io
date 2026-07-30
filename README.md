# Rasa Art & GharGharGita GitHub Pages Website

This repository hosts the static website files for **Rasa Art** and **GharGharGita**, configured for hosting on **GitHub Pages**.

## Structure

```text
/
├── index.html          # Main hub linking to both apps
├── styles.css          # Premium shared stylesheet (Apple inspired)
├── README.md           # Deployment documentation
└── rasaart/            # Rasa Art sub-directory
    ├── index.html      # Rasa Art landing page
    ├── privacy.html    # Rasa Art privacy policy
    ├── support.html    # Rasa Art support & FAQ
    ├── terms.html      # Rasa Art terms of use
    └── assets/
        └── logo.png    # Rasa Art app icon
```

## How to Publish to GitHub Pages

To make these pages live under your GitHub Pages URL (e.g., `https://<username>.github.io/` or `https://<username>.github.io/Rasa-Art-github/` depending on repository setup):

### Step 1: Initialize Git Repository

If you haven't initialized git in this directory yet:

```bash
git init
git add .
git commit -m "Initial commit of Rasa Art and GharGharGita portal website"
```

### Step 2: Connect to GitHub

Create a new repository on GitHub (for example, named `rasa-art-web` or similar) and push your files:

```bash
# Rename the default branch to main
git branch -M main

# Link to your GitHub remote (replace with your actual repository URL)
git remote add origin https://github.com/arunkumarnagelly/<repository-name>.git

# Push the code
git push -u origin main
```

### Step 3: Enable GitHub Pages

1. Navigate to your repository on **GitHub.com**.
2. Click on **Settings** (tab at the top).
3. Scroll down or click **Pages** in the left sidebar.
4. Under **Build and deployment** -> **Source**, select **Deploy from a branch**.
5. Choose the branch **`main`** and folder **`/ (root)`**.
6. Click **Save**.

Your website will be built and deployed by GitHub within a few minutes! You will see the live URL printed at the top of the Settings -> Pages screen.
