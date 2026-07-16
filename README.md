# Git cơ bản cho người mới

> Mục tiêu: nắm quy trình **sửa file → `git add` → `git commit` → `git push`**.

Git giúp quản lý lịch sử thay đổi của dự án. Lệnh quan trọng nhất khi mới học là `git status`.

---

## 1. Khái niệm nhanh

```text
Working Directory  →  Staging Area  →  Local Repository  →  Remote (GitHub)
     nơi sửa file       nơi chọn file      nơi lưu commit       nơi đồng bộ online
```

| Khu vực | Ý nghĩa |
|---|---|
| **Working Directory** | Các file bạn đang tạo hoặc chỉnh sửa |
| **Staging Area** | Các thay đổi đã chọn để chuẩn bị commit |
| **Local Repository** | Lịch sử commit được lưu trên máy |
| **Remote Repository** | Repository trực tuyến, ví dụ GitHub |

---

## 2. Cài đặt và cấu hình

### Kiểm tra Git

```bash
git --version
```

### Cấu hình tên và email

> Chỉ cần chạy một lần trên mỗi máy.

```bash
git config --global user.name "Huynh Hoang"
git config --global user.email "email@example.com"
```

### Xem cấu hình hiện tại

```bash
git config --global --list
```

---

## 3. Bắt đầu dự án

### Cách 1: Tạo Git cho thư mục mới

```bash
cd duong-dan/toi/du-an
git init
```

Ví dụ:

```bash
mkdir git-demo
cd git-demo
git init
```

### Cách 2: Tải dự án từ GitHub

```bash
git clone https://github.com/ten-user/ten-repo.git
cd ten-repo
```

---

## 4. Kiểm tra trạng thái

```bash
git status
```

| Trạng thái | Nghĩa là |
|---|---|
| `Untracked files` | File mới, Git chưa theo dõi |
| `Changes not staged` | File đã sửa nhưng chưa `git add` |
| `Changes to be committed` | File đã staging và sẵn sàng commit |

---

## 5. Lưu thay đổi

### Thêm file vào staging

```bash
# Chỉ thêm một file
git add README.md

# Thêm toàn bộ thay đổi
git add .
```

### Tạo commit

```bash
git commit -m "Thêm nội dung giới thiệu dự án"
```

Ví dụ thông điệp commit tốt:

```bash
git commit -m "Thêm chức năng đăng nhập"
git commit -m "Sửa lỗi tính tổng đơn hàng"
git commit -m "Cập nhật hướng dẫn cài đặt"
```

---

## 6. Xem lịch sử commit

```bash
# Xem đầy đủ lịch sử
git log

# Xem dạng ngắn
git log --oneline
```

Ví dụ:

```text
a1b2c3d Thêm chức năng đăng nhập
e4f5g6h Khởi tạo dự án
```

---

## 7. Kết nối GitHub

### Kiểm tra remote

```bash
git remote -v
```

### Thêm remote GitHub

```bash
git remote add origin https://github.com/ten-user/ten-repo.git
```

### Đẩy code lần đầu

```bash
git branch -M main
git push -u origin main
```

### Đẩy code các lần sau

```bash
git push
```

### Lấy thay đổi từ GitHub

```bash
git pull
```

---

## 8. Làm việc với nhánh

```bash
# Xem các nhánh
git branch

# Tạo và chuyển sang nhánh mới
git switch -c feature-login

# Chuyển nhánh
git switch main

# Gộp nhánh feature-login vào nhánh hiện tại
git merge feature-login

# Xóa nhánh đã gộp
git branch -d feature-login
```

> Cú pháp cũ vẫn phổ biến: `git checkout -b feature-login`.

---

## 9. Xem nội dung đã thay đổi

```bash
# Thay đổi chưa staging
git diff

# Thay đổi đã staging nhưng chưa commit
git diff --staged
```

---

## 10. Hoàn tác cơ bản

### Bỏ file khỏi staging

> Nội dung file vẫn được giữ nguyên.

```bash
git restore --staged README.md
```

### Hủy thay đổi chưa staging

> **Cẩn thận:** thay đổi trong file sẽ mất.

```bash
git restore README.md
```

### Sửa commit gần nhất

> Chỉ nên dùng khi commit chưa được `git push`.

```bash
git commit --amend -m "Thông điệp commit mới"
```

### Lệnh nguy hiểm

```bash
git reset --hard
```

> Lệnh này có thể xóa toàn bộ thay đổi chưa commit.

---

## 11. Tạo `.gitignore`

Tạo file `.gitignore` tại thư mục gốc dự án:

```gitignore
# Thư viện Node.js
node_modules/

# Biến môi trường và thông tin nhạy cảm
.env

# File log
*.log

# File build
dist/
```

Lưu file này vào Git:

```bash
git add .gitignore
git commit -m "Thêm gitignore"
```

> Không commit mật khẩu, API key, token hoặc file `.env` lên GitHub.

---

## 12. Khi bị conflict

Khi hai người sửa cùng phần nội dung trong một file, Git có thể tạo conflict.

```bash
git pull
```

Trong file có thể xuất hiện:

```text
<<<<<<< HEAD
Nội dung của bạn
=======
Nội dung từ GitHub
>>>>>>> main
```

Sửa file để giữ nội dung cuối cùng, xóa các dòng đánh dấu, sau đó:

```bash
git add ten-file-bi-conflict.txt
git commit -m "Giải quyết xung đột"
git push
```

---

## 13. Quy trình mỗi ngày

```bash
# 1. Đi vào thư mục dự án
cd ten-du-an

# 2. Lấy thay đổi mới nhất
git pull

# 3. Kiểm tra trạng thái
git status

# 4. Chỉnh sửa code hoặc tài liệu

# 5. Xem lại thay đổi
git diff

# 6. Đưa thay đổi vào staging
git add .

# 7. Kiểm tra phần sắp commit
git status
git diff --staged

# 8. Tạo commit
git commit -m "Mô tả rõ thay đổi"

# 9. Đẩy lên GitHub
git push
```

---

## 14. Cheat sheet

| Mục đích | Lệnh |
|---|---|
| Kiểm tra trạng thái | `git status` |
| Tạo repository mới | `git init` |
| Tải repository về máy | `git clone <url>` |
| Thêm một file | `git add <ten-file>` |
| Thêm tất cả thay đổi | `git add .` |
| Tạo commit | `git commit -m "Mô tả"` |
| Xem lịch sử ngắn | `git log --oneline` |
| Xem thay đổi chưa staging | `git diff` |
| Xem thay đổi đã staging | `git diff --staged` |
| Kết nối GitHub | `git remote add origin <url>` |
| Đẩy code lên GitHub | `git push` |
| Lấy code mới từ GitHub | `git pull` |
| Xem nhánh | `git branch` |
| Tạo và chuyển nhánh | `git switch -c <ten-nhanh>` |
| Chuyển nhánh | `git switch <ten-nhanh>` |
| Gộp nhánh | `git merge <ten-nhanh>` |
| Bỏ file khỏi staging | `git restore --staged <file>` |
| Hủy thay đổi của file | `git restore <file>` |
| Xem trợ giúp | `git <lenh> --help` |

---

## 15. Ví dụ hoàn chỉnh

```bash
# Tạo thư mục dự án
mkdir git-practice
cd git-practice

# Khởi tạo Git
git init

# Tạo file
echo "Xin chao Git" > hello.txt

# Kiểm tra file mới
git status

# Đưa file vào staging
git add hello.txt

# Tạo commit đầu tiên
git commit -m "Thêm file hello đầu tiên"

# Đặt nhánh chính là main
git branch -M main

# Kết nối với GitHub
git remote add origin https://github.com/ten-user/git-practice.git

# Đẩy source code lần đầu
git push -u origin main
```

---

## Mẹo ghi nhớ

```text
Không biết Git đang thế nào?     → git status
Muốn lưu thay đổi?               → git add → git commit
Muốn đưa code lên GitHub?        → git push
Muốn lấy code mới từ GitHub?     → git pull
Muốn làm tính năng riêng?        → git switch -c ten-nhanh
```
