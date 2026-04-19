---
layout: default
title: transfer repositories from GitLab to GitHub
nav_exclude: true
---

# problem

- transfer repositories from GitLab to GitHub

# resolve

- project in gitlab, run:

```sh
    git remote add <name-repo-in-github> <url-repo-in-github>;
    git push --mirror <name-repo-in-github>
```
