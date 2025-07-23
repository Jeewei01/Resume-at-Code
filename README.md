# Resume as Code

This repository is a "Resume as Code" implementation, managing my professional resume as a simple JSON file (`resume.json`). It leverages the [JSON Resume](https://jsonresume.org/) open-source initiative, the `jsonresume-theme-engineering` [theme](https://github.com/skoenig/jsonresume-theme-engineering), and GitHub Actions to automate the build and deployment process.

The live version of the resume is available on GitHub Pages. Any changes pushed to the `resume.json` file in the `main` branch will automatically trigger a rebuild and update the live resume which is hosted on the `gh-pages` branch.

## Key Features

- **Single Source of Truth**: The `resume.json` file is the master document for all resume data.
- **Automated Builds**: A GitHub Actions workflow renders the resume into an HTML page and a PDF file.
- **Custom PDF Export**: Uses a custom Node.js script with **Playwright** for a more reliable PDF export, instead of the default Puppeteer implementation.
- **Live Deployment**: The latest version of the resume is always available via GitHub Pages.

## How It Works

1.  **Edit**: Make changes to your professional information in the `resume.json` file.
2.  **Commit & Push**: Commit the changes to the `main` branch and push them to GitHub.
3.  **Automate**: A GitHub Action is triggered on push, which:
    - Installs dependencies (`npm install`).
    - Renders the `resume.json` to `index.html` using the `jsonresume-theme-engineering` theme.
    - Runs the `export-pdf.js` script to generate `resume.pdf` from the HTML file using Playwright.
    - Commits the updated `index.html` and `resume.pdf` files to the `gh-pages` branch, making them live.

## Setting Up Your Own GitResume

To replicate this setup for your own resume:

1.  **Create your repository:** Click the "Use this template" button at the top of this repository page to create a new repository based on this one. And include the additional branch as well. 

2.  **Configure GitHub Pages:** In your new repository's settings, navigate to the "Pages" section. Set the source to "Deploy from a branch" and select the `gh-pages` branch as the source.

With this configuration, the GitHub Actions workflow will automatically build and deploy your resume to GitHub Pages whenever you update `resume.json` on the `main` branch. 

Typically the link to your github pages will be `https://<your_github_username>.github.io/<repo_name>` and its available on the deployment status. 

## Local Usage

To run this project locally, you'll need to have Node.js and npm installed.

1.  **Clone the repository:**
    ```bash
    git clone <your-new-repository-url>
    cd <your-repository-name>
    ```

2.  **Install dependencies:**
    ```bash
    npm install
    npx playwright install chromium
    ```

3.  **Copy sample-resume.json & update resume.json:**
    ```bash
    cp sample-resume.json resume.json
    ```

4.  **Render the HTML:**
    This command uses the `resumed` [CLI](https://github.com/rbardini/resumed) to render your `resume.json` into an `index.html` file.
    ```bash
    npm run export-html
    ```

5.  **Export the PDF:**
    This command runs the custom Playwright script to generate `resume.pdf` from the `index.html` file.
    ```bash
    npm run export-pdf
    ```

After running these commands, you will have `index.html` and `resume.pdf` in your project directory.
