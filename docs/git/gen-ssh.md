---
layout: default
title: gen ssh in windows
nav_exclude: true
---

<div class="my-right-toc" markdown="1">
1. TOC
{:toc}
</div>

- B1:

    ```sh
        ssh-keygen -t rsa
    ```

- B2: service -> openssh athen....-> chuot phai -> properties -> manual -> apply -> start -> ok
- B3:  

    ```sh
        ssh-add .\.ssh\id_rsa
    ```

- B4:

    ```sh
        notepad .\.ssh\id_rsa.pub
    ```

 -> copy add vao github, gitlab

- B5:

    ```sh
        code .\.ssh\config
    ```

    ```sh
    Host *
        IdentityFile ~/.ssh/id_rsa
        IdentitiesOnly yes
    ```

- B6:

    ```sh
        ssh git@github.com;
        ssh git@gitlab.com;
    ```
