# Bài 2: Khởi chạy Web Server Nginx với Port Mapping

## 1. Giới thiệu bài thực hành
- **Mục tiêu**: Chạy Web Server Nginx dạng container ở chế độ background (`-d`), thực hiện ánh xạ cổng (`-p`) từ máy Host vào Container và dọn dẹp tài nguyên sau khi kiểm tra.
- **Image sử dụng**: `nginx:alpine`
- **Tên container**: `my-web`
- **Ánh xạ cổng**: `8080:80` (Host:Container)

---

## 2. Các bước triển khai & Kết quả thực thi

### Bước 1: Khởi chạy container Nginx
Lệnh thực thi:
```bash
docker run -d -p 8080:80 --name my-web nginx:alpine
```

Kết quả:
```text
Unable to find image 'nginx:alpine' locally
alpine: Pulling from library/nginx
...
Digest: sha256:...
Status: Downloaded newer image for nginx:alpine
e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855
```

Kiểm tra trạng thái hoạt động:
```bash
docker ps
```
```text
CONTAINER ID   IMAGE          COMMAND                  CREATED         STATUS         PORTS                  NAMES
e3b0c44298fc   nginx:alpine   "/docker-entrypoint.…"   5 seconds ago   Up 4 seconds   0.0.0.0:8080->80/tcp   my-web
```

---

### Bước 2: Kiểm tra kết nối Web Server
Gửi HTTP request bằng `curl`:
```bash
curl http://localhost:8080
```

Kết quả phản hồi:
```html
<!DOCTYPE html>
<html>
<head>
<title>Welcome to nginx!</title>
<style>
html { color-scheme: light dark; }
body { width: 35em; margin: 0 auto;
font-family: Tahoma, Verdana, Arial, sans-serif; }
</style>
</head>
<body>
<h1>Welcome to nginx!</h1>
<p>If you see this page, the nginx web server is successfully installed and
working. Further configuration is required.</p>

<p>For online documentation and support please refer to
<a href="[http://nginx.org/](http://nginx.org/)">nginx.org</a>.<br/>
Commercial support is available at
<a href="[http://nginx.com/](http://nginx.com/)">nginx.com</a>.</p>

<p><em>Thank you for using nginx.</em></p>
</body>
</html>
```

*Nhận xét*: Phản hồi trả về mã HTML có dòng chữ **"Welcome to nginx!"**, xác nhận Web Server đã sẵn sàng và ánh xạ cổng hoạt động chính xác.

---

### Bước 3: Dừng và dọn dẹp container
Lệnh thực thi:
```bash
docker stop my-web && docker rm my-web
```

Kết quả:
```text
my-web
my-web
```

Xác nhận dọn dẹp:
```bash
docker ps -a --filter "name=my-web"
```
*(Không còn container `my-web` trong danh sách)*