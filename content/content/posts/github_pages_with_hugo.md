---
title: "用Hugo、Github、Github Pages建立靜態網站"
draft: false
date: "2020-04-03"
tags: ["hugo","github"]
categories: ["技術"]
---


雖然在 Hugo 的[官方文件](https://gohugo.io/hosting-and-deployment/hosting-on-github/)有寫用 Github 作為 Host 應該怎麼把 Hugo 佈署上去，但實際執行時還是遇到了一點問題，為了避免忘記來做一下紀錄～

## 三種 Github pages 頁面型態

- Github Pages 提供了3種不同型態的頁面 User / Organization / Project Site

  - 用 User / Organization 為主頁一個帳號只能有**一個**

    顯示網址為 ```https://<user/organization>.github.io```

  - Project 頁面能有很多個

    顯示網址為 ```https://<user>.github.io/<project-name>```

而我選用的是用 Project 方式架設

## 1. 安裝 Hugo 並建立專案

在安裝完 Hugo 後（待補），直接建立新的專案

```bash=
# 建立名為 Blog 的 Hugo 新專案
$ hugo new site Blog

# change directory
$ cd Blog

# git initialized
$ git init
$ echo .DS_store >> .gitignore

# add git remote repository
$ git remote add origin git@github.com:<your-github-account>/Blog
```

## 2. 安裝新的 Themes

可以到官方提供的 [Themes 列表](https://themes.gohugo.io/) 找到自己喜歡的主題

建議用 submodule 方式來安裝 themes

```bash=
# add hugo themes to project as submodule
$ git submodule add https://github.com/xiaoheiAh/hugo-theme-pure themes/pure
```

## 3. 編輯設定檔
```bash
baseurl: "https://<your-github-account>.github.io/Blog"
language: "en-us"
title: "Hugo Blog"
theme: "pure"
```

## 4. 建立新的文章
在 content/posts 建立 first-post.md ，根據使用的 themes 不同，有可能會有所差異
```bash=
$ hugo new posts/first-post.md -f yaml
```

編輯 first-post.md
```bash=
---
title: "<your title>"
# 是否為草稿
draft: true 
date: "2020-04-03"
tags: ["1st-tag","2nd-tag"......]
categories: ["1st category"......]
---

my first post
```

## 5. 預覽
```bash=
# -w watch filesystem for changes and recreate as needed
# -D include content marked as draft
# Press Ctrl+C to stop
$ hugo server -w
```

執行後在瀏覽器輸入 localhost:1313/Blog 就會出現目前 Hugo 所產生的網站樣子了

## 6. 把 Hugo 靜態網站發布到 Github Pages
```bash=
# remove public folder, it will recreated later
$ rm -rf public

# add all path and file, and push
$ git add .
$ git commit -m 'hugo project init'
$ git push -u origin master

# Create a new orphand branch (no commit history) named gh-pages
$ git checkout --orphan gh-pages

# Unstage all files
# -rf themes/pure
$ git rm -rf --cached $(git ls-files)

# Add and commit that file
$ git add .
$ git commit -m "INIT: initial commit on gh-pages branch"

# Push to remote gh-pages branch
$ git push origin gh-pages

# Return to master branch
$ git checkout master

# Remove the public folder to make room for the gh-pages subtree
$ rm -rf public

# Add the gh-pages branch of the repository. It will look like a folder named public
$ git subtree add --prefix=public git@github.com:<your-github-account>/Blog.git gh-pages --squash

# Pull down the file we just committed. This helps avoid merge conflicts
$ git subtree pull --prefix=public git@github.com:<your-github-account>/Blog.git gh-pages

# Run hugo. Generated site will be placed in public directory (or omit -t ThemeName if you're not using a theme)
$ hugo

# Add everything
$ git add -A

# Commit and push to master
$ git commit -m "Updating site" && git push origin master

# Push the public subtree to the gh-pages branch
$ git subtree push --prefix=public git@github.com:<your-github-account>/Blog.git gh-pages
```
照著上面一大串慢慢操作就好了，執行完後在瀏覽器輸入 https://<your-github-account>.github.io/Blog 應該就能看到了

## 7. 更新文章
之後如果有修改只須執行前面的最後3個步驟即可，為了方便可以寫成一個 deploy.sh

```bash=
# deploy.sh
echo -e "Deploying updates to GitHub ~"

# Build the project.
hugo

# Add changes to git.
git add -A

# Commit changes.
msg="rebuilding site `date`"
if [ $# -eq 1 ]
  then msg="$1"
fi
git commit -m "$msg"

# Push source and build repos.
git push origin master
git subtree push --prefix=public git@github.com:<your-github-account>/Blog.git gh-pages
```
記得要給該檔案執行權限

## 參考來源網站
- https://kaichu.io/2015/07/12/my-first-post/
