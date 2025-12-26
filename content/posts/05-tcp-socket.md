---
title: "Bài 5: Lập Trình Socket Cho Giao Thức TCP"
date: 2024-05-24T00:00:00+07:00
weight: 5
draft: false
tags: ["Java", "TCP", "Socket", "Client-Server"]
categories: ["Java", "JavaScript"]
---

## Nội dung bài học

### 1. Mô hình Khách/Chủ (Client/Server)
Mô hình Client-Server là kiến trúc mạng phổ biến nhất, trong đó:
*   **Server (Máy chủ)**: Cung cấp dịch vụ, luôn ở trạng thái chờ đợi yêu cầu.
*   **Client (Máy khách)**: Gửi yêu cầu đến Server và chờ phản hồi.

![Mô hình Client-Server](/LTM/images/client-server-model.png)
*(Sơ đồ tổng quan mô hình Client-Server)*

### 2. Mô hình truyền tin socket
Socket là giao diện lập trình ứng dụng (API) mạng, cho phép hai chương trình giao tiếp với nhau. Trong TCP:
1.  Server tạo **ServerSocket**, gán địa chỉ IP/Port và lắng nghe.
2.  Client tạo **Socket**, kết nối đến IP/Port của Server.
3.  Khi kết nối thiết lập, cả hai bên giao tiếp qua **InputStream/OutputStream**.
4.  Đóng kết nối khi hoàn tất.

![Quy trình giao tiếp Socket](/LTM/images/tcp-socket-flow.png)
*(Sơ đồ tuần tự các bước kết nối TCP Socket)*

### 3. Lớp Socket (Dùng cho Client)
Lớp `java.net.Socket` đại diện cho một kênh kết nối phía Client.

*   **Constructor**: `Socket(String host, int port)` - Tạo kết nối đến Server.
*   **Phương thức chính**:
    *   `getInputStream()`: Nhận dữ liệu từ Server.
    *   `getOutputStream()`: Gửi dữ liệu lên Server.
    *   `close()`: Đóng kết nối.

**Ví dụ Client:**
```java
// Tạo kết nối đến Server tại cổng 5000
Socket socket = new Socket("localhost", 5000);

// Gửi dữ liệu
PrintWriter out = new PrintWriter(socket.getOutputStream(), true);
out.println("Hello Server");

// Đóng kết nối
socket.close();
```

### 4. Lớp ServerSocket (Dùng cho Server)
Lớp `java.net.ServerSocket` dùng để chờ đợi và chấp nhận các kết nối từ Client.

*   **Constructor**: `ServerSocket(int port)` - Mở cổng lắng nghe.
*   **Phương thức chính**:
    *   `accept()`: Chặn (block) chương trình cho đến khi có Client kết nối. Trả về một đối tượng `Socket` để giao tiếp với Client đó.

**Ví dụ Server:**
```java
ServerSocket server = new ServerSocket(5000);
System.out.println("Server started...");

// Chờ Client kết nối
Socket client = server.accept(); 
System.out.println("Client connected!");

// Nhận dữ liệu
BufferedReader in = new BufferedReader(new InputStreamReader(client.getInputStream()));
String msg = in.readLine();
System.out.println("Client says: " + msg);

server.close();
```

![Kết quả chạy thử](/LTM/images/tcp-terminal-output.png)
*(Minh họa Server và Client đang giao tiếp)*

## Tài liệu tham khảo
*   [Oracle Docs: Sockets](https://docs.oracle.com/javase/tutorial/networking/sockets/)
