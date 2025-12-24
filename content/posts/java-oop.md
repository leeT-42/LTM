---
title: "Lập Trình Hướng Đối Tượng (OOP) trong Java"
date: 2024-05-21T00:00:00+07:00
draft: false
tags: ["Java", "OOP"]
categories: ["Programming"]
---

## 1. Giới thiệu
Lập trình hướng đối tượng (OOP) là một mô hình lập trình dựa trên khái niệm "đối tượng", chứa đựng dữ liệu và mã lệnh.

## 2. 4 Tính chất cơ bản
1.  **Tính đóng gói (Encapsulation)**: Che giấu dữ liệu, chỉ cho phép truy cập qua method public.
2.  **Tính kế thừa (Inheritance)**: Class con kế thừa thuộc tính/phương thức từ class cha.
3.  **Tính đa hình (Polymorphism)**: Một hành động có thể thực hiện theo nhiều cách khác nhau.
4.  **Tính trừu tượng (Abstraction)**: Ẩn chi tiết cài đặt, chỉ hiển thị tính năng.

## 3. Ví dụ Code
```java
class Animal {
    void speak() {
        System.out.println("Animal speaks");
    }
}

class Dog extends Animal {
    @Override
    void speak() {
        System.out.println("Woof");
    }
}
```
