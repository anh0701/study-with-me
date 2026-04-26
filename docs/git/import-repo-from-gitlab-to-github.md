---
layout: default
title: 6.6 transfer repositories from GitLab to GitHub
parent: 06. Git
description: ""
has_toc: side_bar 
---

# Transfer repositories from GitLab to GitHub

## 1. problem

- transfer repositories from GitLab to GitHub

## 2. resolve

- project in gitlab, run:

```sh
    git remote add <name-repo-in-github> <url-repo-in-github>;
    git push --mirror <name-repo-in-github>
```
