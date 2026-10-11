# Bài 3: Dockerfile đóng gói trang Web HTML tĩnh

## 1. Mục tiêu

- Tạo trang web HTML tĩnh đơn giản.
- Sử dụng Dockerfile để đóng gói trang web vào Nginx Alpine.
- Build Docker Image và chạy Container trên cổng 8081.
- Kiểm tra nội dung trang web bằng curl và trình duyệt.

## 2. Cấu trúc thư mục

```text
bt03/
├── Dockerfile
├── index.html
└── README.md
```

## 3. Nội dung file index.html

```html
<h1>Hello Docker Session 09!</h1>
```

## 4. Nội dung Dockerfile

```dockerfile
FROM nginx:alpine
COPY index.html /usr/share/nginx/html/index.html
```

### Giải thích

- `FROM nginx:alpine`: Sử dụng image Nginx Alpine làm image cơ sở.
- `COPY index.html /usr/share/nginx/html/index.html`: Sao chép file HTML vào thư mục mặc định phục vụ web của Nginx trong container.

## 5. Các bước thực hiện

### Bước 1: Build Docker Image

```bash
docker build -t my-html-app:v1 .
```

Image được tạo với tên `my-html-app` và tag `v1`.

### Bước 2: Khởi chạy Container

```bash
docker run -d -p 8081:80 --name html-app my-html-app:v1
```

Giải thích:

- `-d`: Chạy container ở chế độ nền.
- `-p 8081:80`: Ánh xạ cổng 8081 của máy host tới cổng 80 trong container.
- `--name html-app`: Đặt tên container là `html-app`.

### Bước 3: Kiểm tra Container

```bash
docker ps
```

Kiểm tra container `html-app` đang chạy với trạng thái `Up`.

### Bước 4: Kiểm tra nội dung trang web

Trên Windows PowerShell, chạy:

```powershell
curl.exe http://localhost:8081
```

Kết quả mong đợi:

```html
<h1>Hello Docker Session 09!</h1>
```

### Bước 5: Truy cập bằng trình duyệt

Mở địa chỉ:

http://localhost:8081

Trang web hiển thị nội dung:

**Hello Docker Session 09!**

## 6. Kết quả

- Tạo thành công Docker Image `my-html-app:v1`.
- Khởi chạy thành công container `html-app`.
- Trang HTML tĩnh được phục vụ bởi Nginx Alpine trên cổng 8081.
- Kiểm tra nội dung HTML trả về đúng yêu cầu bài tập.

## 7. Lệnh quản lý Container

Dừng container:

```bash
docker stop html-app
```

Khởi chạy lại container đã dừng:

```bash
docker start html-app
```

Xóa container:

```bash
docker rm -f html-app
```

## 8. Kết luận

Hoàn thành bài tập đóng gói trang web HTML tĩnh bằng Docker với Dockerfile gồm hai câu lệnh. Image `my-html-app:v1` chạy Nginx Alpine và phục vụ trang web tại cổng 8081.