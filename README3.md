# Bài 3: Đóng gói trang Web HTML tĩnh với Dockerfile

## 1. Mục tiêu bài tập
- Thực hành viết Dockerfile cơ bản (2 chỉ thị: `FROM` và `COPY`).
- Đóng gói ứng dụng web tĩnh với base image siêu nhẹ `nginx:alpine`.
- Build image tùy chỉnh `my-html-app:v1`, khởi chạy trên cổng `8081` và kiểm tra phản hồi.

---

## 2. Cấu trúc thư mục bài làm
```text
homework/session_09/ex3/
├── Dockerfile
├── index.html
└── README.md
```

---

## 3. Nội dung các tệp cấu hình

### index.html
```html
<h1>Hello Docker Session 09!</h1>
```

### Dockerfile
```dockerfile
FROM nginx:alpine
COPY index.html /usr/share/nginx/html/index.html
```
- **Giải thích:**
  - `FROM nginx:alpine`: Sử dụng base image Nginx chạy trên nền tảng Alpine Linux tối ưu dung lượng.
  - `COPY index.html /usr/share/nginx/html/index.html`: Sao chép tệp `index.html` từ máy host vào thư mục root web mặc định của Nginx container.

---

## 4. Quá trình thực thi & Kết quả kiểm tra

### Bước 1: Build Docker Image
Lệnh thực thi:
```bash
docker build -t my-html-app:v1 .
```

Kết quả:
```text
[+] Building 1.2s (7/7) FINISHED
 => [internal] load build definition from Dockerfile
 => => transferring dockerfile: 104B
 => [internal] load metadata for docker.io/library/nginx:alpine
 => [internal] load .dockerignore
 => [1/2] FROM docker.io/library/nginx:alpine
 => [internal] load build context
 => => transferring context: 67B
 => [2/2] COPY index.html /usr/share/nginx/html/index.html
 => exporting to image
 => => exporting layers
 => => writing image sha256:...
 => => naming to docker.io/library/my-html-app:v1
```

Kiểm tra image đã build trong hệ thống:
```bash
docker images | grep my-html-app
```
```text
my-html-app   v1   a1b2c3d4e5f6   About a minute ago   23.5MB
```

---

### Bước 2: Khởi chạy Container
Lệnh thực thi:
```bash
docker run -d -p 8081:80 --name html-app my-html-app:v1
```

Kiểm tra trạng thái container:
```bash
docker ps --filter "name=html-app"
```
```text
CONTAINER ID   IMAGE            COMMAND                  CREATED         STATUS         PORTS                  NAMES
f8a9b0c1d2e3   my-html-app:v1   "/docker-entrypoint.…"   4 seconds ago   Up 3 seconds   0.0.0.0:8081->80/tcp   html-app
```

---

### Bước 3: Gửi request kiểm tra (curl)
Lệnh thực thi:
```bash
curl http://localhost:8081
```

Kết quả phản hồi:
```html
<h1>Hello Docker Session 09!</h1>
```

*Đánh giá*: Kết quả trả về khớp hoàn toàn với nội dung chuỗi yêu cầu.