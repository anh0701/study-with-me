---
layout: default
title: 6.5 clone repo submodule
parent: 06. Git
description: ""
has_toc: side_bar 
---

# Clone repo submodule

## 1. problem

- when clone repo workspace, submodule folder null

## 2. resolve

- run command:

```sh
    git clone --recurse-submodules [link_clone]
    git submodule init
    git submodule update
```

hoặc sử dụng câu lệnh:

```sh
    git submodule update --init --recursive
```
