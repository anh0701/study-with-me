---
layout: default
title: 25. Backend Roadmap
description: ""
---

## Nền tảng lập trình (Programming Fundametals)

### 1. Syntax cơ bản

- biến
- kiêủ dữ liệu
- điều kiện
- vòng lặp
- function
- array/list
- string

### 2. Tư duy lập trình

- decomposition (chia nhỏ bài toán)
- debugging
- đọc track trace

### 3. OOP cơ bản

- class
- object
- encapsulation
- inheritance
- polymorphism
- abstraction

### 4. Clean code

- naming
- function nhỏ
- tách module

### 5. Chọn ngôn ngữ

| Language   | Backend framework |
| ---------- | ----------------- |
| Java       | Spring Boot       |
| C#         | ASP.NET           |
| Python     | FastAPI / Django  |
| Go         | Gin               |
| JavaScript | Node.js           |

## Data Structures & Algorithms

### 1. Data structures

- Array
- Linked List
- Queue
- Hash Table
- Tree
- Graph

### 2. Algorithms

- searching
- sorting
- recusion
- backtracking
- BFS/DFS
- dynamic programming (basic)

## Computer Science Foundations

### 1. Operating System

- process
- thread
- context switching
- memory management
- deadlock
- concurrency

### 2. Networking

- TCP/IP: [see more ...](TCP.md)
- HTTP: [see more ...](HTTPvsHTTPS.md)
- DNS: [see more ...](Hosting_Domain_DNS.md)
- load balancing

### 3. Database theory

- relational model
- normalization
- index
- query optimization
- ACID
- transaction

## Backend Fundamentals

### 1. HTTP API

- REST
- request/response
- headers
- status code
- JSON

[API](APIs.md)

### 2. Authentication

- session
- cookie
- JWT
- OAuth

### 3. Caching

- Redis
- cache aside
- TTL

[Catching](Caching.md)

### 4. Message Queue

- producer
- consumer
- queue
- pub/sub

[Message brokers](MessageBrokers.md)

## Database

### 1. SQL

- join
- subquery
- index
- execution plan

### 2. Database phổ biến

| Type       | Example            |
| ---------- | ------------------ |
| relational | MySQL / PostgreSQL |
| key-value  | Redis              |
| document   | MongoDB            |
| search     | Elasticsearch      |

## System Design

### Topics

- monolith vs microservices: [Monolithic Apps]({{ site.baseurl }}/monolithic-apps/), [Microservices]({{ site.baseurl }}/microservices/)
- load balancer
- horizontal scaling
- caching layer
- CDN
- database replication
- sharding

### Ví dụ design

- URL shortener
- chat system
- notification system
- banking transfer

## DevOps basics

### 1. Linux

- process
- port
- log
- permissions

### 2. Docker

- container
- image
- docker compose

### 3. CI/CD

- pipeline
- build
- deploy

[see more ...](CI_CD.md)

## Kiến thức nâng cao

### 1. Distributed system

- consensus
- CAP theorem
- eventual consistency

### 2. High concurrency

- rate limiting
- circuit breaker
- idempotency

### 3. Data pipeline

- ETL
- stream processing

## Một số project nhỏ nên làm

### 1. Rest API Todo

feature

- auth
- CRUD
- pagination
- search

### 2. Blog system

- comment
- tagging
- like
- search

### 3. mini ecommerce

- cart
- order
- payment mock
- inventory
