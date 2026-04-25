---
layout: default
title: clone repo submodule
nav_exclude: true
has_toc: side_bar 
---

## problem

- when clone repo workspace, submodule folder null

## resolve

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
