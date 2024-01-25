 [简体中文](README_zhcn.md)



# Hexo-Issue-Blog-Automation

This is a workflow designed for Hexo blogs, which converts `GitHub Issues` into blog posts and automatically deploys them to `GitHub Pages`. This allows you to write articles online. I spent a night putting this project together, and it might still be imperfect (for example, it currently only supports publishing without modifications). I plan to refine it later when I have time, and you are welcome to make modifications and submit PRs.

## Features

- **Automatic Content Conversion**: Automatically converts content from GitHub Issues into Hexo blog posts.

- **Deployment**: Automatically deploys the generated static website content to GitHub Pages.

## How to Use

### Preparation

1. Fork this repository and create another repository named `username.github.io` (this will store the generated static files).

2. Clone the forked repository to your local machine.

3. Modify your Hexo blog style as needed.

4. Modify `convert-issues-to-posts.js`:
   
   ```javascript
   const GITHUB_TOKEN = process.env.GITHUB_TOKEN;
   const REPO_OWNER = 'meteorOSS';  // Replace with your GitHub username
   const REPO_NAME = 'hexo-source';  // Replace with your repository name
   const ISSUES_API_URL = `https://api.github.com/repos/${REPO_OWNER}/${REPO_NAME}/issues?state=open`;
   
   ```

### Configuring GitHub Actions

1. Generate a Personal Access Token (PAT) with the appropriate permissions and add it to your repository's Secrets with the key `HEXO_TOKEN`.

2. Modify the GitHub Actions workflow file in `github/workflows`:
   
   ```yaml
   - name: Deploy to GitHub Pages
     uses: peaceiris/actions-gh-pages@v3
     with:
       personal_token: ${{ secrets.HEXO_TOKEN }}
       publish_dir: ./public
       branch: main
       # Change to your own repository
       external_repository: meteorOSS/meteorOSS.github.io
   
   ```

### Writing and Publishing

1. Create new blog posts by writing content in GitHub Issues.

2. Whenever a new Issue is created or there is a new commit to the repository, GitHub Actions will automatically run, converting the Issues into blog posts and deploying them to GitHub Pages.

## Contribution

Contributions of any kind are welcome, whether it's feature improvements, documentation enhancements, or issue reports. Feel free to fork this repository and submit a Pull Request.
