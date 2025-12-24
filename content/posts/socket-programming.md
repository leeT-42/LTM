---
title: "Lập Trình Socket Trong Java"
date: 2024-05-28T00:00:00+07:00
draft: false
tags: ["Java", "Socket", "Network"]
categories: ["Networking"]
---

## 1. Socket là gì?
Là điểm cuối (endpoint) trong liên kết giao tiếp 2 chiều giữa 2 chương trình chạy trên mạng.

## 2. Mô hình Client-Server
*   **Server**: Lắng nghe yêu cầu tại một Port cụ thể.
*   **Client**: Gửi yêu cầu kết nối đến IP và Port của Server.

## 3. Code Ví Dụ (Server)
```java
ServerSocket server = new ServerSocket(5000);
Socket socket = server.accept(); // Chờ kết nối
// Đọc/Ghi dữ liệu qua InputStream/OutputStream
```

## 4. Code Ví Dụ (Client)
```java
Socket socket = new Socket("localhost", 5000);
// Gửi yêu cầu
```
