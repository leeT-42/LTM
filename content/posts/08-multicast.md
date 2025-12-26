---
title: "Bài 8: Lập Trình Multicast"
date: 2024-05-27T00:00:00+07:00
weight: 8
draft: false
tags: ["Java", "Multicast", "UDP"]
categories: ["Java", "JavaScript"]
---

## Nội dung bài học

### 1. Tổng quan Multicast
Multicast là kỹ thuật gửi tin nhắn từ một nguồn đến một nhóm đích (Group) cụ thể cùng một lúc.
*   **Hiệu quả**: Thay vì gửi N gói tin cho N người nhận (Unicast), Server chỉ gửi 1 gói tin đến địa chỉ đầu mối (Multicast Group IP), và hạ tầng mạng sẽ sao chép gói tin đó cho tất cả thành viên trong nhóm.
*   **Địa chỉ IP Multicast**: Thuộc lớp D, nằm trong dải `224.0.0.0` đến `239.255.255.255`.

```text
       +--------+
       | SERVER |
       +--------+
           | (Gửi 1 gói tin)
           v
    [ Router / Mạng ]
           |
   -----------------
   |       |       |
   v       v       v
+-----+ +-----+ +-----+
| PC1 | | PC2 | | PC3 |
+-----+ +-----+ +-----+
  (Các máy tham gia nhóm nhận được tin)
```

### 2. Kiểu dữ liệu MulticastSocket
Lớp `java.net.MulticastSocket` kế thừa từ `DatagramSocket`, cung cấp thêm các khả năng để gia nhập và rời khỏi nhóm.

*   **Constructor**:
    *   `MulticastSocket(int port)`: Tạo socket và ràng buộc với cổng cục bộ (để nhận tin).
*   **Phương thức quan trọng**:
    *   `joinGroup(InetAddress mcastaddr)`: Gia nhập một nhóm multicast.
    *   `leaveGroup(InetAddress mcastaddr)`: Rời khỏi nhóm.
    *   `send(DatagramPacket p)`: Gửi gói tin (như DatagramSocket thường).
    *   `receive(DatagramPacket p)`: Nhận gói tin.

### 3. Các bước lập trình Multicast

Để tạo một ứng dụng Multicast (ví dụ Chat nhóm), ta thực hiện các bước sau:

**Bước 1: Tạo Socket và Địa chỉ nhóm**
```java
MulticastSocket socket = new MulticastSocket(8888);
InetAddress group = InetAddress.getByName("224.0.0.1");
```

**Bước 2: Gia nhập nhóm (Join)**
```java
socket.joinGroup(group);
System.out.println("Đã tham gia nhóm Chat...");
```

**Bước 3: Nhận hoặc Gửi tin nhắn**
```java
// Nhận tin
byte[] buffer = new byte[1024];
DatagramPacket packet = new DatagramPacket(buffer, buffer.length);
socket.receive(packet);
String msg = new String(packet.getData(), 0, packet.getLength());
System.out.println("Tin nhắn nhận được: " + msg);

// Gửi tin
String sendMsg = "Hello Group!";
DatagramPacket outPacket = new DatagramPacket(
    sendMsg.getBytes(), sendMsg.length(), group, 8888
);
socket.send(outPacket);
```

**Bước 4: Rời nhóm và Đóng Socket**
```java
socket.leaveGroup(group);
socket.close();
```

> [!NOTE]
> Khi lập trình Multicast, cần chắc chắn rằng Firewall hoặc Router không chặn các gói tin UDP trên cổng đang sử dụng.

## Tài liệu tham khảo
*   [Oracle Docs: Broadcasting to Multiple Recipients](https://docs.oracle.com/javase/tutorial/networking/datagrams/broadcasting.html)
