---
layout: default
title: create folder/project in local before create repo in github
nav_exclude: true
---

<div class="my-right-toc" markdown="1">
1. TOC
{:toc}
</div>

# create folder/project in local before create repo in github

1. Problem
   - create folder/project in computer
   - after create new repo
2. Resolve

```sh
   git init
   git remote add origin  URL-REPO
   git remote -v # to check
   git checkout -b main # switch to branch main
   git pull origin main
   git add .
   git commit -m "..{messgae}.."
   git push origin main
```
