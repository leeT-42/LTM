---
title: "Đa Luồng (Multithreading) trong Java"
date: 2024-05-23T00:00:00+07:00
draft: false
tags: ["Java", "Concurrency"]
categories: ["Programming"]
---

## 1. Thread là gì?
Thread (luồng) là đơn vị nhỏ nhất của việc thực thi trong một quy trình.

## 2. Cách tạo Thread
Có 2 cách chính:
1.  Kế thừa class `Thread`.
2.  Implement interface `Runnable`.

```java
// Cách 2 (Khuyên dùng)
class MyToask implements Runnable {
    public void run() {
        System.out.println("Running...");
    }
}
Thread t1 = new Thread(new MyTask());
t1.start();
```

## 3. Vòng đời Thread
New -> Runnable -> Running -> Blocked/Waiting -> Terminated.
