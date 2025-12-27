# Lê Minh Thanh - Personal Blog

Chào mừng đến với mã nguồn blog cá nhân của **Lê Minh Thanh**.
Đây là nơi mình chia sẻ kiến thức về **Lập trình Mạng**, **Hệ thống**, và các dự án công nghệ của mình.

## 🚀 Giới thiệu
Blog được xây dựng bằng [Hugo](https://gohugo.io/) - một Static Site Generator siêu nhanh, sử dụng theme [PaperMod](https://github.com/adityatelange/hugo-PaperMod) được tùy biến lại.

- **Author**: Lê Minh Thanh
- **Email**: leminhthanh931@gmail.com
- **Website**: [https://leeT-42.github.io/LTM/](https://leeT-42.github.io/LTM/)

## 📂 Cấu trúc thư mục chính
- `content/`: Chứa nội dung bài viết (Markdown).
  - `content/posts`: Các bài viết blog.
  - `content/projects`: Thông tin các dự án.
- `layouts/`: Chứa các file giao diện tùy chỉnh (HTML).
- `static/`: Chứa tài nguyên tĩnh (ảnh, file css tùy chỉnh...).
- `hugo.toml`: File cấu hình chính của dự án.

## 🛠️ Cài đặt và Chạy dự án

### 1. Yêu cầu
- Đã cài đặt [Hugo](https://gohugo.io/installation/) (phiên bản Extended càng tốt).
- Git.

### 2. Chạy server local (Development)
Để xem trước trang web trên máy local (bao gồm cả bài viết nhá - draft):
```bash
hugo server -D
```
Truy cập: `http://localhost:1313/LTM/`

### 3. Build ra file tĩnh (Production)
Để tạo ra thư mục `public` chứa web tĩnh để upload lên host (GitHub Pages):
```bash
hugo
```

## 📝 Cách viết bài mới
Tạo một file markdown mới trong thư mục `content/posts`:
```bash
hugo new posts/tên-bai-viet-moi.md
```
Sau đó mở file vừa tạo để chỉnh sửa nội dung.

---
*© 2025 Lê Minh Thanh*
