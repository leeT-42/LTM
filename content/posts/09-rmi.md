---
title: "Bài 9: Phân Tán Đối Tượng Trong Java Bằng RMI"
date: 2024-05-28T00:00:00+07:00
weight: 9
draft: false
tags: ["Java", "RMI", "Distributed"]
categories: ["Java", "JavaScript"]
---

## Nội dung bài học

### 1. Tổng quan
RMI (Remote Method Invocation) là cơ chế cho phép một đối tượng Java đang chạy trên máy ảo này (Client) có thể gọi các phương thức của một đối tượng đang chạy trên máy ảo khác (Server).

**Kiến trúc RMI:**
*   **Stub**: Nằm ở phía Client, đóng vai trò như một đại diện (proxy). Nó nhận lệnh gọi hàm, gói dữ liệu (Marshalling) và gửi đi.
*   **Skeleton**: Nằm ở phía Server, nhận yêu cầu, giải gói (Unmarshalling) và gọi hàm thực thi trên đối tượng thật.
*   **RMI Registry**: Quyển danh bạ để Server đăng ký tên đối tượng và Client tìm kiếm.

```text
    Client Machine              Server Machine
   +-------------+             +-------------+
   |  Client App |             |  Server Obj |
   +-----+-------+             +------+------+
         |                            ^
      [Stub]                      [Skeleton]
         |                            |
         +----------- Network --------+
               (Gửi yêu cầu / Nhận kết quả)
```

### 2. Lập trình RMI
Để xây dựng ứng dụng RMI, ta cần tuân thủ các quy tắc:
1.  **Remote Interface**: Phải kế thừa từ `java.rmi.Remote`. Mọi phương thức phải ném ra ngoại lệ `java.rmi.RemoteException`.
2.  **Remote Object**: Lớp cài đặt interface phải kế thừa `UnicastRemoteObject` (thường dùng).
3.  **RMI Registry**: Server phải chạy dịch vụ Registry (mặc định port 1099) để quảng bá đối tượng.

### 3. Cài đặt chương trình RMI
Dưới đây là ví dụ xây dựng ứng dụng **Máy tính (Calculator)** đơn giản.

**Bước 1: Tạo Remote Interface**
```java
import java.rmi.Remote;
import java.rmi.RemoteException;

public interface Calculator extends Remote {
    // Phương thức cộng 2 số
    int add(int a, int b) throws RemoteException;
}
```

**Bước 2: Cài đặt Remote Object (Server)**
```java
import java.rmi.server.UnicastRemoteObject;
import java.rmi.RemoteException;
import java.rmi.registry.LocateRegistry;
import java.rmi.registry.Registry;

public class CalculatorImpl extends UnicastRemoteObject implements Calculator {
    
    public CalculatorImpl() throws RemoteException { super(); }

    @Override
    public int add(int a, int b) throws RemoteException {
        System.out.println("Processing: " + a + " + " + b);
        return a + b;
    }

    public static void main(String[] args) {
        try {
            // 1. Tạo thanh ghi tại cổng 1099
            Registry registry = LocateRegistry.createRegistry(1099);
            
            // 2. Tạo đối tượng
            CalculatorImpl obj = new CalculatorImpl();
            
            // 3. Đăng ký tên định danh
            registry.rebind("CalcuService", obj);
            
            System.out.println("Server is running...");
        } catch (Exception e) { e.printStackTrace(); }
    }
}
```

**Bước 3: Viết Client gọi hàm**
```java
import java.rmi.registry.LocateRegistry;
import java.rmi.registry.Registry;

public class Client {
    public static void main(String[] args) {
        try {
            // 1. Kết nối đến Registry Server
            Registry registry = LocateRegistry.getRegistry("localhost", 1099);
            
            // 2. Tìm kiếm đối tượng bằng tên
            Calculator stub = (Calculator) registry.lookup("CalcuService");
            
            // 3. Gọi hàm từ xa
            int result = stub.add(10, 20);
            System.out.println("Kết quả 10 + 20 = " + result);
            
        } catch (Exception e) { e.printStackTrace(); }
    }
}
```

## Tài liệu tham khảo
*   [Oracle Docs: Getting Started with RMI](https://docs.oracle.com/javase/8/docs/technotes/guides/rmi/hello/hello-world.html)
