---
title: "Bất Đồng Bộ: Promises và Async/Await"
date: 2024-05-26T00:00:00+07:00
draft: false
tags: ["JavaScript", "Async"]
categories: ["Frontend"]
---

## 1. Tại sao cần Async?
JS là đơn luồng (single-threaded). Các tác vụ lâu (I/O, API) cần chạy bất đồng bộ để không chặn giao diện.

## 2. Promise
Đại diện cho một giá trị trong tương lai.
```javascript
fetchData().then(data => console.log(data));
```

## 3. Async/Await
Cú pháp hiện đại giúp viết code async trông như sync.
```javascript
async function getData() {
    try {
        const res = await fetch(url);
        const data = await res.json();
    } catch (err) {
        console.error(err);
    }
}
```
