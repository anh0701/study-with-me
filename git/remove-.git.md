---
layout: default
title: File Nháp
nav_exclude: true
---

# problem

- no push code: maybe child directory have folder .git => move it

# resolve

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
