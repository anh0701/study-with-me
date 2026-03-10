---
layout: default
title: File Nháp
nav_exclude: true
---

1. gen key:

```sh
    ssh-keygen -t rsa -f ~/.ssh ghk_aya                         
```

2. Add public key to github/gitlab

```sh
    cat ~/.ssh/ghk_aya.pub 
```

3.  Similar to other accounts (step 1, 2)

4. Config file

```sh
    nvim ~/.ssh/config 
```

content file:

```sh
    # github account
    Host aya
    HostName github.com
    IdentityFile ~/.ssh/ghk_aya
    IdentitiesOnly yes

    # github account other...
    Host anh
    HostName gitlab.com
    IdentityFile ~/.ssh/ghk_anh
    IdentitiesOnly yes
```

5. Add private key to agent & test connect

```sh
    ssh-add ~/.ssh/ghk_aya
    ...
    ssh-keyscan github.com >> ~/.ssh/known_hosts
    ssh git@aya
    ....
```

6. Notes

- Before add changes to staging area, you must config .gitconfig: username, email.
