---
title: "Bài 4: Quản Lý Địa Chỉ Kết Nối Mạng"
date: 2024-05-23T00:00:00+07:00
weight: 4
draft: false
tags: ["Java", "InetAddress", "URL", "URLConnection"]
categories: ["Java", "JavaScript"]
---

## Nội dung bài học

### 1. Lớp InetAddress
Lớp `java.net.InetAddress` được sử dụng để đại diện cho địa chỉ IP (Internet Protocol). Nó cung cấp các phương thức để làm việc với Hostname và IP Address mà không cần tạo ra socket.

*   **Các phương thức chính**:
    *   `getByName(String host)`: Trả về đối tượng InetAddress của host chỉ định.
    *   `getLocalHost()`: Trả về thông tin của máy trạm hiện tại.
    *   `getHostName()`: Lấy tên host.
    *   `getHostAddress()`: Lấy địa chỉ IP.

**Ví dụ Code:**
```java
try {
    InetAddress ip = InetAddress.getByName("www.google.com");
    System.out.println("Host Name: " + ip.getHostName());
    System.out.println("IP Address: " + ip.getHostAddress());
    
    InetAddress local = InetAddress.getLocalHost();
    System.out.println("Local Host: " + local);
} catch (UnknownHostException e) {
    e.printStackTrace();
}
```

![Kết quả InetAddress](/LTM/images/inetaddress-output.png)
*(Kết quả chạy demo lấy IP của Google)*

### 2. Lớp URL
URL (Uniform Resource Locator) là con trỏ tới tài nguyên trên WWW (World Wide Web). Một URL bao gồm: Protocol, Hostname, Port và File name.

*   **Cấu trúc**: `protocol://hostname:port/path/file`

![Cấu trúc URL](/LTM/images/url-structure.png)
*(Sơ đồ các thành phần của một URL)*

**Ví dụ phân tích URL:**
```java
URL url = new URL("https://www.example.com:80/pages/index.html");
System.out.println("Protocol: " + url.getProtocol());
System.out.println("Host: " + url.getHost());
System.out.println("Port: " + url.getPort());
System.out.println("File: " + url.getFile());
```

### 3. Lớp URLConnection
Lớp `URLConnection` đại diện cho một kết nối truyền thông giữa ứng dụng Java và URL. Nó có thể được sử dụng để đọc nội dung từ một trang web hoặc gửi dữ liệu (POST request).

**Ví dụ đọc mã nguồn trang Web:**
```java
try {
    URL url = new URL("http://www.google.com");
    URLConnection urlCon = url.openConnection();
    
    BufferedReader br = new BufferedReader(
        new InputStreamReader(urlCon.getInputStream())
    );
    
    String line;
    while ((line = br.readLine()) != null) {
        System.out.println(line);
    }
    br.close();
} catch (Exception e) {
    e.printStackTrace();
}
```

![Kết quả URLConnection](/LTM/images/urlconnection-output.png)
*(Kết quả đọc thử nội dung HTML từ URL)*

## Tài liệu tham khảo
*   [Oracle Docs: Working with URLs](https://docs.oracle.com/javase/tutorial/networking/urls/)
