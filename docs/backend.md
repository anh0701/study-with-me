---
layout: default
title: 25. Backend Roadmap
description: ""
has_toc: side_bar 
---

# Backend Roadmap

## 1. Nền tảng lập trình (Programming Fundametals)

### 1.1. Syntax cơ bản

- biến
- kiêủ dữ liệu
- điều kiện
- vòng lặp
- function
- array/list
- string

### 1.2. Tư duy lập trình

- decomposition (chia nhỏ bài toán)
- debugging
- đọc track trace

### 1.3. OOP cơ bản

- class
- object
- encapsulation
- inheritance
- polymorphism
- abstraction

### 1.4. Clean code

- naming
- function nhỏ
- tách module

### 1.5. Chọn ngôn ngữ

| Language   | Backend framework |
| ---------- | ----------------- |
| Java       | Spring Boot       |
| C#         | ASP.NET           |
| Python     | FastAPI / Django  |
| Go         | Gin               |
| JavaScript | Node.js           |

## 2. Data Structures & Algorithms

### 2.1. Data structures

- Array
- Linked List
- Queue
- Hash Table
- Tree
- Graph

### 2.2. Algorithms

- searching
- sorting
- recusion
- backtracking
- BFS/DFS
- dynamic programming (basic)

## 3. Computer Science Foundations

### 3.1. Operating System

- process
- thread
- context switching
- memory management
- deadlock
- concurrency

### 3.2. Networking

- TCP/IP: [see more ...](TCP.md)
- HTTP: [see more ...](HTTPvsHTTPS.md)
- DNS: [see more ...](Hosting_Domain_DNS.md)
- load balancing

### 3.3. Database theory

- relational model
- normalization
- index
- query optimization
- ACID
- transaction

## 4. Backend Fundamentals

### 4. 1. HTTP API

- REST
- request/response
- headers
- status code
- JSON

[API](APIs.md)

### 4.2. Authentication

- session
- cookie
- JWT
- OAuth

### 4.3. Caching

- Redis
- cache aside
- TTL

[Catching](Caching.md)

### 4.4. Message Queue

- producer
- consumer
- queue
- pub/sub

[Message brokers](MessageBrokers.md)

## 5. Database

### 5.1. SQL

- join
- subquery
- index
- execution plan

### 5.2. Database phổ biến

| Type       | Example            |
| ---------- | ------------------ |
| relational | MySQL / PostgreSQL |
| key-value  | Redis              |
| document   | MongoDB            |
| search     | Elasticsearch      |

## 6. System Design

### 6.1. Topics

- monolith vs microservices: [Monolithic Apps]({{ site.baseurl }}/monolithic-apps/), [Microservices]({{ site.baseurl }}/microservices/)
- load balancer
- horizontal scaling
- caching layer
- CDN
- database replication
- sharding

### 6.2. Ví dụ design

- URL shortener
- chat system
- notification system
- banking transfer

## 7. DevOps basics

### 7.1. Linux

- process
- port
- log
- permissions

### 7.2. Docker

- container
- image
- docker compose

### 7.3. CI/CD

- pipeline
- build
- deploy

[see more ...](CI_CD.md)

## 8. Kiến thức nâng cao

### 8.1. Distributed system

- consensus
- CAP theorem
- eventual consistency

### 8.2. High concurrency

- rate limiting
- circuit breaker
- idempotency

### 8.3. Data pipeline

- ETL
- stream processing

## 9. Một số project nhỏ nên làm

### 9.1. Rest API Todo

feature

- auth
- CRUD
- pagination
- search

### 9.2. Blog system

- comment
- tagging
- like
- search

### 9.3. mini ecommerce

- cart
- order
- payment mock
- inventory
