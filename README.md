# How to Deploy a Website on GitHub

Deploying a static website consisting of HTML, CSS, and JavaScript on GitHub Pages is a straightforward process. GitHub Pages allows you to host static websites directly from your GitHub repository. Follow these steps to deploy your website:

## Step 1: Create a GitHub Repository

1. Go to GitHub and log in to your account.
2. Click on the `+` icon in the upper-right corner and select `New repository`.
3. Name your repository (e.g., `my-website`).
4. Add a description (optional).
5. Choose `Public` as the visibility.
6. Initialize the repository with a `README.md` file (optional but recommended).
7. Click `Create repository`.

## Step 2: Add Your Website Files to the Repository

1. On your local machine, create a new directory for your website files if you haven't already.
2. Place your HTML, CSS, and JavaScript files in this directory.
3. Open a terminal (or Git Bash on Windows) and navigate to the directory containing your website files.
4. Initialize a new Git repository:

    ```sh
    git init
    ```

5. Add the GitHub repository as a remote:

    ```sh
    git remote add origin https://github.com/your-username/my-website.git
    ```

6. Add all your files to the repository:

    ```sh
    git add .
    ```

7. Commit the changes:

    ```sh
    git commit -m "Initial commit"
    ```

8. Push the changes to GitHub:

    ```sh
    git push -u origin master
    ```

## Step 3: Configure GitHub Pages

1. Go to your repository on GitHub.
2. Click on `Settings` in the top menu.
3. Scroll down to the `GitHub Pages` section.
4. Under `Source`, select the branch you want to use (e.g., `master` or `main`). If you have your website files in a specific folder (e.g., `docs`), select the branch and specify the folder.
5. Click `Save`.

## Step 4: Access Your Deployed Website

After configuring GitHub Pages, GitHub will automatically deploy your website. It usually takes a few minutes. You can access your website using the URL:

```
https://your-username.github.io/my-website/
```

## Example Directory Structure

Your project directory might look like this:

```
my-website/
├── index.html
├── style.css
├── script.js
└── README.md
```

## Example `index.html`

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>My Website</title>
    <link rel="stylesheet" href="style.css">
</head>
<body>
    <h1>Welcome to My Website</h1>
    <p>This is a simple static website hosted on GitHub Pages.</p>
    <script src="script.js"></script>
</body>
</html>
```

## Example `style.css`

```css
body {
    font-family: Arial, sans-serif;
    text-align: center;
    margin-top: 50px;
}
```

## Example `script.js`

```javascript
console.log('Hello, world!');
```

## Additional Tips

- **Custom Domain**: If you want to use a custom domain, create a `CNAME` file in your repository with your custom domain name and configure your DNS settings accordingly.
- **Continuous Deployment**: To automate deployment, you can set up a GitHub Actions workflow. Create a `.github/workflows/deploy.yml` file in your repository:

    ```yaml
    name: Deploy to GitHub Pages

    on:
      push:
        branches:
          - master  # Change this to your default branch if necessary

    jobs:
      deploy:
        runs-on: ubuntu-latest

        steps:
          - name: Checkout repository
            uses: actions/checkout@v2

          - name: Setup Node.js
            uses: actions/setup-node@v2
            with:
              node-version: '14'

          - name: Install dependencies and build
            run: |
              npm install
              npm run build

          - name: Deploy to GitHub Pages
            uses: peaceiris/actions-gh-pages@v3
            with:
              github_token: ${{ secrets.GITHUB_TOKEN }}
              publish_dir: ./build  # Change this to your build output directory if necessary
    ```

  This example assumes you have a build step (e.g., using a static site generator or bundler). If your site doesn't need a build step, you can simplify the workflow.

By following these steps, you should be able to deploy your static website on GitHub Pages easily.
