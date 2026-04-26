---
layout: default
title: 6.8 remove git
parent: 06. Git
description: ""
has_toc: side_bar 
---

# Remove git

## 1. problem

- no push code: maybe child directory have folder .git => move it

## 2. resolve

- B1: check:
    + 1.

    ```sh
        cd .\.git
    ```

    + 2.

    ```sh
        ls -la
    ```

- B2: if having folder .git:

```sh
    git remote -v
    Remove-Item -Path .\.git -Force
```

=> Finish
