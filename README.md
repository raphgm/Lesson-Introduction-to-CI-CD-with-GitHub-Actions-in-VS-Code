# Lesson: Introduction to CI/CD with GitHub Actions in VS Code

Learn to set up a basic CI/CD pipeline using GitHub Actions directly from VS Code. By the end, you’ll automate testing and deployment of a simple project.

## 1. What is CI/CD?

- **CI (Continuous Integration)**: Automatically test code changes when pushed to a repository.
- **CD (Continuous Delivery/Deployment)**: Automatically deploy code after passing tests.
- **GitHub Actions**: A tool to automate workflows (CI/CD) directly in your GitHub repository.

## Setup Your Project

### Create a Project in VS Code

Open VS Code and create a new folder (e.g., `github-actions-demo`).

Add a simple file (e.g., `index.html` you can add your resume in index.html and push instead of the simple content below):

```html
<!DOCTYPE html>
<html>
  <body>
    <h1>Hello CI/CD!</h1>
  </body>
</html>
```

### 2. Initialize Git & Connect to GitHub


Create a new GitHub repository (e.g., `github-actions-demo`).

Link your local project to GitHub:

```bash
git remote add origin YOUR_GITHUB_REPO_URL
git push -u origin main
```

## 3. Create a CI Workflow

### Add a GitHub Actions Workflow File

In VS Code, create a folder `.github/workflows` at your project root.

Create a file `ci.yml` inside `.github/workflows`:

```yaml
name: CI Pipeline

on: 
  push:
    branches: [ "main" ]

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout code
        uses: actions/checkout@v4

      - name: Run tests (simulated)
        run: echo "Running tests... Success!"
```

### 4.: Commit and Push

Commit the workflow file:

```bash
git add .github/workflows/ci.yml
git commit -m "Add CI workflow"
git push origin main
```

### 5.  Check GitHub Actions

Go to your GitHub repository → Actions tab.

You’ll see the workflow running. Click to view logs and confirm the simulated test passes.

## 6. Add CD (Deployment)

Let’s deploy the `index.html` to GitHub Pages.

###7.  Update the Workflow

Modify `ci.yml` to add a deployment job:

```yaml
name: CI/CD Pipeline

on:
  push:
    branches: [ "main" ]

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout code
        uses: actions/checkout@v4
      - name: Test
        run: echo "Tests passed!"

  deploy:
    needs: test
    runs-on: ubuntu-latest
    steps:
      - name: Checkout code
        uses: actions/checkout@v4
      - name: Deploy to GitHub Pages
        uses: actions/upload-pages-artifact@v2
        with:
          path: ./
      - name: Deploy
        uses: actions/deploy-pages@v3
```

### 8. Enable GitHub Pages

Go to your GitHub repo → Settings → Pages.

Set Source to GitHub Actions.

### 9. Push Changes

Commit and push the updated workflow:

```bash
git add .github/workflows/ci.yml
git commit -m "Add deployment"
git push origin main
```

Check the Actions tab again. After the workflow runs, your site will be live at:
`https://YOUR_GITHUB_USERNAME.github.io/REPO_NAME/`.

## 10. Best Practices

- **Cache Dependencies**: Speed up workflows by caching tools (e.g., npm packages).
- **Use Secrets**: Store sensitive data (e.g., API keys) in GitHub Secrets.
- **Matrix Testing**: Test across multiple OS/platforms.

## 11. Troubleshooting

- **Workflow Errors**: Check logs in the Actions tab.
- **YAML Syntax**: Use VS Code’s YAML extension for validation. Microsoft's learn-yaml extension would be perfect for this
- **Paths**: Ensure file paths in workflows match your project structure.

