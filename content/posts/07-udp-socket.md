---
title: "Bài 7: Lập Trình Mạng Cho Giao Thức UDP"
date: 2024-05-25T00:00:00+07:00
weight: 7
draft: false
tags: ["Java", "UDP", "Socket"]
categories: ["Java", "JavaScript"]
---

## Mục tiêu bài học
*   **Hiểu rõ về giao thức UDP**: Các khái niệm, cơ chế hoạt động, và các lớp `DatagramPacket`, `DatagramSocket`.
*   **Xác định quy trình**: Nắm vững các bước triển khai ứng dụng mạng UDP (không kết nối).
*   **Lập trình thực tế**: Xây dựng ứng dụng gửi nhận gói tin để hiểu sâu về cách hoạt động.

## Nội dung bài học

### 1. Tổng quan UDP (User Datagram Protocol)
UDP là giao thức không hướng kết nối (connectionless). Nó gửi dữ liệu dưới dạng các gói tin độc lập (Datagram) mà không cần thiết lập đường truyền trước, do đó tốc độ nhanh hơn TCP nhưng không đảm bảo độ tin cậy (có thể mất gói tin).

![Quy trình UDP](/LTM/images/udp-flow-diagram.png)
*(Sơ đồ tuần tự quy trình gửi nhận UDP)*

### 2. Lớp DatagramPacket
Lớp `java.net.DatagramPacket` đại diện cho một gói tin dữ liệu.
*   **Vai trò**: Đóng gói dữ liệu cần gửi hoặc chứa dữ liệu nhận được.
*   **Constructor chính**:
    *   `DatagramPacket(byte[] buf, int length)`: Dùng để nhận dữ liệu.
    *   `DatagramPacket(byte[] buf, int length, InetAddress address, int port)`: Dùng để gửi dữ liệu đi.

### 3. Lớp DatagramSocket
Lớp `java.net.DatagramSocket` là điểm cuối (endpoint) để gửi và nhận các gói tin.
*   **Constructor**:
    *   `DatagramSocket()`: Tạo socket client (cổng ngẫu nhiên).
    *   `DatagramSocket(int port)`: Tạo socket server lắng nghe tại cổng cố định.
*   **Phương thức**:
    *   `send(DatagramPacket p)`: Gửi gói tin.
    *   `receive(DatagramPacket p)`: Chờ nhận gói tin (Blocking).

### 4. Gửi/nhận gói tin
Quy trình giao tiếp UDP đơn giản hơn TCP vì không có bước `accept()` hay `connect()`.

**Ví dụ Server (Nhận tin):**
```java
DatagramSocket socket = new DatagramSocket(9876);
byte[] buffer = new byte[1024];
DatagramPacket packet = new DatagramPacket(buffer, buffer.length);

System.out.println("UDP Server waiting...");
socket.receive(packet); // Chờ nhận

String msg = new String(packet.getData(), 0, packet.getLength());
System.out.println("Received: " + msg);
```

**Ví dụ Client (Gửi tin):**
```java
DatagramSocket socket = new DatagramSocket();
String data = "Hello UDP";
byte[] buffer = data.getBytes();
InetAddress ip = InetAddress.getByName("localhost");

DatagramPacket packet = new DatagramPacket(buffer, buffer.length, ip, 9876);
socket.send(packet);
System.out.println("Packet sent!");
```

![Kết quả chạy UDP](/LTM/images/udp-console.png)
*(Kết quả minh họa giao tiếp UDP)*

## Tài liệu tham khảo
*   [Oracle Docs: Datagrams](https://docs.oracle.com/javase/tutorial/networking/datagrams/)
