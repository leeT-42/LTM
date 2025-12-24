---
title: "Làm chủ Java Collections Framework"
date: 2024-05-22T00:00:00+07:00
draft: false
tags: ["Java", "Collections"]
categories: ["Programming"]
---

## 1. Tổng quan
Java Collections Framework cung cấp kiến trúc để lưu trữ và thao tác nhóm các đối tượng.

## 2. Các Interface chính
*   **List**: Lưu trữ danh sách có thứ tự, chấp nhận trùng lặp. (ArrayList, LinkedList)
*   **Set**: Lưu trữ tập hợp không trùng lặp. (HashSet, TreeSet)
*   **Map**: Lưu trữ cặp Key-Value. (HashMap, TreeMap)

## 3. ArrayList vs LinkedList
*   **ArrayList**: Dùng mảng động. Truy xuất nhanh (get), thêm/xoá chậm.
*   **LinkedList**: Dùng danh sách liên kết. Truy xuất chậm, thêm/xoá nhanh.

```java
List<String> list = new ArrayList<>();
list.add("Java");
list.add("Network");
```
