---
title: "Thao Tác DOM với JavaScript"
date: 2024-05-25T00:00:00+07:00
draft: false
tags: ["JavaScript", "DOM"]
categories: ["Frontend"]
---

## 1. DOM là gì?
DOM (Document Object Model) là biểu diễn dạng cây của trang HTML giúp JS có thể thay đổi cấu trúc, nội dung và kiểu dáng.

## 2. Truy cập phần tử
```javascript
const el = document.getElementById("myId");
const items = document.querySelectorAll(".item");
```

## 3. Thay đổi nội dung
```javascript
el.textContent = "Nội dung mới";
el.style.color = "red";
```

## 4. Event Listener
```javascript
btn.addEventListener("click", () => {
    alert("Clicked!");
});
```
