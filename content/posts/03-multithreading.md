---
title: "Bài 3: Lập Trình Đa Tuyến"
date: 2024-05-26T00:00:00+07:00
weight: 3
draft: false
tags: ["Java", "Thread"]
categories: ["Java", "JavaScript"]
---

## Mục tiêu bài học
*   Hiểu khái niệm **Process** (Tiến trình) và **Thread** (Luồng).
*   Phân biệt 2 cách tạo Thread: `extends Thread` và `implements Runnable`.
*   Hiểu về vòng đời của Thread và các vấn đề đồng bộ hóa (`synchronized`).

## Nội dung bài học

### 1. Tại sao cần Đa tuyến (Multithreading)?
Trong lập trình mạng, Server cần phục vụ nhiều Client cùng lúc (**Concurrent Socket Server**). Nếu không có đa luồng, Client B sẽ phải đợi Client A ngắt kết nối mới được phục vụ.

### 2. Vòng đời của một Thread
Một Thread trải qua các trạng thái: `New` -> `Runnable` -> `Running` -> `Blocked/Waiting` -> `Terminated`.

![Sơ đồ vòng đời Thread](/LTM/images/thread-lifecycle.png)
*(Sơ đồ minh họa các trạng thái New, Runnable, Running...)*

### 3. Ví dụ thực hành: Đua luồng (Race Condition)
Ví dụ minh họa việc 2 luồng cùng truy cập một biến đếm mà không đồng bộ hóa, dẫn đến kết quả sai.

```java
class Counter {
    private int count = 0;
    
    // Thêm từ khóa 'synchronized' để sửa lỗi Race Condition
    public synchronized void increment() {
        count++;
    }
    
    public int getCount() { return count; }
}

public class RaceConditionDemo {
    public static void main(String[] args) throws InterruptedException {
        Counter c = new Counter();
        
        Thread t1 = new Thread(() -> {
            for(int i=0; i<1000; i++) c.increment();
        });
        
        Thread t2 = new Thread(() -> {
            for(int i=0; i<1000; i++) c.increment();
        });
        
        t1.start();
        t2.start();
        
        t1.join();
        t2.join();
        
        System.out.println("Kết quả cuối cùng: " + c.getCount());
    }
}
```

### 4. Kết quả mong đợi
*   Nếu **không có** `synchronized`: Kết quả < 2000 (ngẫu nhiên).
*   Nếu **có** `synchronized`: Kết quả = 2000.

![Kết quả chạy thử](/LTM/images/thread-output.png)
*(Hình minh họa )*

## Hướng dẫn tự học
*   Chạy thử đoạn code trên, bỏ từ khóa `synchronized` và quan sát kết quả.
*   Tìm hiểu về `ExecutorService` (Thread Pool) cho các ứng dụng Server lớn.
