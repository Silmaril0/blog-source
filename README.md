## 

## Hexo-Issue-Blog-Automation



这是一个为Hexo博客编写的工作流程，它将 `Github Issue` 转换为博客文章并自动部署到`GithubPages` 。从而你可以做到在线编写文章，该项目是我花了一晚上时间折腾出来的，它可能还并不完善 (例如只有发布没有修改)，在稍后我会抽空完善它，如果你愿意，也可以修改后提交PR



## 特点

- 自动内容转换: 将 GitHub Issues 中的内容自动转换为 Hexo 博客文章。

- 部署: 自动将生成的静态网站内容部署到 GitHub Pages。
  
  

## 使用方法

### 准备工作

- 1. fork本仓库，并再创建一个 `用户名.github.io` 仓库 (这里会存放生成后的静态文件)
  
  2. 克隆fork后的代码到本地
  
  3. 按需修改你的hexo博客样式
  
  4. 修改  `convert-issues-to-posts.js`
     
     - ```js
       const GITHUB_TOKEN = process.env.GITHUB_TOKEN;
       const REPO_OWNER = 'meteorOSS';  // 替换为你的 GitHub 用户名
       const REPO_NAME = 'hexo-source';  // 替换为你的仓库名
       const ISSUES_API_URL = `https://api.github.com/repos/${REPO_OWNER}/${REPO_NAME}/issues?state=open`;
       ```

### 配置Github Action

- 1. 生成一个具有适当权限的 Personal Access Token (PAT)，并将其添加到你的仓库 Secrets 中，键为 HEXO_TOKEN
  
  2. 修改 `github\workflows\github\workflows`
     
     - ```yaml
         - name: Deploy to GitHub Pages
             uses: peaceiris/actions-gh-pages@v3
             with:
               personal_token: ${{ secrets.HEXO_TOKEN }}
               publish_dir: ./public
               branch: main
               # 改为你自己的仓库
               external_repository: meteorOSS/meteorOSS.github.io
               publ
       ```

### 写作和发布

- 1. 通过在 GitHub Issues 中编写内容来创建新的博客文章。
  
  2. 每当有新的 Issue 被创建或仓库有新的提交时，GitHub Actions 会自动运行，将 Issues 转换为博客文章，并部署到 GitHub Pages。



## 贡献

欢迎任何形式的贡献，无论是功能改进、文档补充还是问题反馈。请随时 Fork 本仓库并提交 Pull Request。
