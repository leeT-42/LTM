---
title: "Bài 6: Kỹ Thuật Đa Tiến Trình Và Tuần Tự Hóa Đối Tượng"
date: 2024-05-25T00:00:00+07:00
weight: 6
draft: false
tags: ["Java", "Process", "Serialization"]
categories: ["Java", "JavaScript"]
---

## Mục tiêu bài học
*   **Hiểu được khái niệm**: Nắm vững sự khác biệt giữa đa tiến trình (Multi-process) và đa luồng (Multi-thread), cũng như khái niệm tuần tự hóa (Serialization).
*   **Nắm được phương pháp**: Biết cách sử dụng `ProcessBuilder` để tạo tiến trình và `Serializable` để lưu trữ đối tượng.
*   **Áp dụng thực tiễn**: Sử dụng đa tiến trình và tuần tự hóa đối tượng để giải quyết các bài toán trong ứng dụng mạng (truyền object qua socket).

## Nội dung bài học

### 1. Ứng dụng lập trình đa tiến trình
Đa tiến trình là kỹ thuật chạy nhiều ứng dụng độc lập song song. Mỗi tiến trình có không gian bộ nhớ riêng, an toàn và ổn định hơn so với đa luồng (nếu 1 process chết không ảnh hưởng process khác).

![So sánh Process và Thread](/LTM/images/process-vs-thread.png)
*(Sơ đồ so sánh kiến trúc bộ nhớ của Process và Thread)*

**Ví dụ `ProcessBuilder` mở Notepad:**
```java
try {
    ProcessBuilder pb = new ProcessBuilder("notepad.exe");
    Process p = pb.start();
    System.out.println("Đã mở Notepad thành công!");
} catch (IOException e) {
    e.printStackTrace();
}
```

### 2. Tuần tự hóa đối tượng (Serialization)
Tuần tự hóa là quá trình chuyển đổi trạng thái của một đối tượng thành luồng byte (Byte Stream) để có thể lưu xuống file hoặc truyền qua mạng. Quá trình ngược lại gọi là Deserialization.

![Sơ đồ Tuần tự hóa](/LTM/images/serialization-diagram.png)
*(Quy trình Serialize và Deserialize đối tượng)*

**Ví dụ Serialization:**
```java
import java.io.*;

class Student implements Serializable {
    int id;
    String name;
    public Student(int id, String name) { this.id = id; this.name = name; }
}

public class SerializationDemo {
    public static void main(String[] args) {
        Student s1 = new Student(101, "John");
        
        // Ghi đối tượng vào file
        try (ObjectOutputStream out = new ObjectOutputStream(new FileOutputStream("student.ser"))) {
            out.writeObject(s1);
            System.out.println("Student Object created: ID=101, Name=John");
            System.out.println("Serializing object to student.ser...");
        } catch (IOException e) { e.printStackTrace(); }

        // Đọc đối tượng từ file
        try (ObjectInputStream in = new ObjectInputStream(new FileInputStream("student.ser"))) {
            System.out.println("Deserializing object...");
            Student s2 = (Student) in.readObject();
            System.out.println("Student Object restored: ID=" + s2.id + ", Name=" + s2.name);
        } catch (IOException | ClassNotFoundException e) { e.printStackTrace(); }
    }
}
```

![Kết quả chạy Serialization](/LTM/images/serialization-console.png)
*(Kết quả chạy thử chương trình ghi và đọc đối tượng)*

## Tài liệu tham khảo
*   [Oracle Docs: Object Serialization](https://docs.oracle.com/javase/tutorial/jndi/objects/serial.html)
