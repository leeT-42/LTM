---
title: "Bài 2: Quản Lý Các Luồng Nhập Xuất"
date: 2024-05-22T00:00:00+07:00
weight: 2
draft: false
tags: ["Java", "IO", "Stream"]
categories: ["Java", "JavaScript"]
---

## Nội dung bài học

### 1. Giới thiệu
Stream (Luồng) trong Java là một khái niệm trừu tượng dùng để biểu diễn một dòng dữ liệu tuần tự chảy từ nguồn (Source) đến đích (Destination). Nguồn có thể là file, bàn phím, hoặc socket mạng.

![Sơ đồ phân cấp Java IO](/LTM/images/java-io-hierarchy.png)

### 2. Các luồng byte (Byte Streams)
Dùng để xử lý dữ liệu nhị phân (binary data) như hình ảnh, âm thanh, video. Đơn vị nhỏ nhất là **byte (8-bit)**.
*   **InputStream**: Lớp cha trừu tượng cho tất cả các luồng nhập byte.
*   **OutputStream**: Lớp cha trừu tượng cho tất cả các luồng xuất byte.
*   *Ví dụ*: `FileInputStream`, `FileOutputStream`.

**Ví dụ Copy ảnh (Đọc/Ghi từng byte):**
```java
try (FileInputStream in = new FileInputStream("image.png");
     FileOutputStream out = new FileOutputStream("image_copy.png")) {
    
    int c;
    while ((c = in.read()) != -1) {
        out.write(c);
    }
}
```

### 3. Các luồng ký tự (Character Streams)
Dùng để xử lý dữ liệu văn bản (text, Unicode). Đơn vị nhỏ nhất là **char (16-bit)**. Tự động xử lý encoding (UTF-8,...) giúp tránh lỗi phông chữ.
*   **Reader**: Lớp cha cho luồng nhập ký tự.
*   **Writer**: Lớp cha cho luồng xuất ký tự.
*   *Ví dụ*: `FileReader`, `FileWriter`.

**Ví dụ đọc file văn bản:**
```java
try (FileReader reader = new FileReader("baiviet.txt")) {
    int data;
    while ((data = reader.read()) != -1) {
        System.out.print((char) data); // Ép kiểu int sang char
    }
}
```

### 4. Các luồng lọc dữ liệu (Filter Streams)
Là các luồng bao bọc (wrapper) các luồng khác để cung cấp thêm tính năng xử lý dữ liệu trước khi đọc/ghi (ví dụ: đếm số dòng, nén dữ liệu).
*   Classes: `FilterInputStream`, `FilterOutputStream`.

**Ví dụ nén dữ liệu với GZIP (Wrapper):**
```java
// FileOutputStream (Ghi file) -> GZIPOutputStream (Nén) -> Ghi dữ liệu
try (FileOutputStream fos = new FileOutputStream("data.gz");
     GZIPOutputStream gzip = new GZIPOutputStream(fos)) {
    
    String data = "Dữ liệu này sẽ được nén";
    gzip.write(data.getBytes());
}
```

### 5. Các luồng đệm dữ liệu (Buffered Streams)
Giúp tối ưu hóa hiệu năng I/O bằng cách giảm số lần truy cập trực tiếp vào đĩa cứng hoặc mạng. Dữ liệu được đọc/ghi vào một vùng nhớ đệm (buffer) trước.

**Ví dụ BufferedStream:**
```java
try (BufferedInputStream bis = new BufferedInputStream(new FileInputStream("source.jpg"));
     BufferedOutputStream bos = new BufferedOutputStream(new FileOutputStream("dest.jpg"))) {
    
    byte[] buffer = new byte[1024];
    int length;
    while ((length = bis.read(buffer)) > 0) {
        bos.write(buffer, 0, length);
    }
}
```



### 6. Các lớp nhập/xuất định kiểu dữ liệu (Data Streams)
Cho phép đọc/ghi các kiểu dữ liệu nguyên thủy của Java (`int`, `double`, `boolean`, `String` UTF-8) một cách thuận tiện thay vì xử lý từng byte thô.
*   Classes: `DataInputStream`, `DataOutputStream`.

**Ví dụ ghi và đọc dữ liệu:**
```java
// Ghi dữ liệu
DataOutputStream dos = new DataOutputStream(new FileOutputStream("data.bin"));
dos.writeInt(100);
dos.writeDouble(9.5);
dos.writeUTF("Hello Java IO");
dos.close();

// Đọc dữ liệu (Phải đọc đúng thứ tự đã ghi)
DataInputStream dis = new DataInputStream(new FileInputStream("data.bin"));
int num = dis.readInt();
double score = dis.readDouble();
String text = dis.readUTF();
```

## Tài liệu tham khảo
*   [Oracle Docs: Java I/O Tutorial](https://docs.oracle.com/javase/tutorial/essential/io/)
