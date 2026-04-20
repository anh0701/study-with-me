---
layout: default
title: clone repo submodule
nav_exclude: true
---

<div class="my-right-toc" markdown="1">
1. TOC
{:toc}
</div>

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
