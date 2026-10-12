Bài 2: Khởi chạy Web Server Nginx với Port Mapping
Mục tiêu
Khởi chạy Web Server Nginx dạng container ở chế độ ngầm (-d).
Ánh xạ cổng (Port Mapping) từ máy chủ sang container (8080:80).
Kiểm tra truy cập và dọn dẹp tài nguyên container sau khi hoàn thành.
1. Khởi chạy Container Nginx
Lệnh chạy:
docker run -d -p 8080:80 --name my-web nginx:alpine
Giải thích tham số:
-d: Chạy container ở chế độ chạy ngầm (detached mode).
-p 8080:80: Ánh xạ cổng 8080 của máy Host vào cổng 80 của Container.
--name my-web: Đặt tên tường minh cho container là my-web.
nginx:alpine: Sử dụng base image Nginx bản rút gọn Alpine siêu nhẹ (~23MB).
2. Kiểm tra Kết quả Hoạt động
1. Kiểm tra danh sách container đang chạy (docker ps):
$ docker ps
CONTAINER ID   IMAGE          COMMAND                  CREATED         STATUS         PORTS                  NAMES
a1b2c3d4e5f6   nginx:alpine   "/docker-entrypoint.…"   5 seconds ago   Up 4 seconds   0.0.0.0:8080->80/tcp   my-web
2. Gửi yêu cầu HTTP kiểm tra qua curl:
$ curl -I http://localhost:8080
HTTP/1.1 200 OK
Server: nginx/1.25.5
Date: Sun, 11 Oct 2026 03:20:00 GMT
Content-Type: text/html
Content-Length: 615
Last-Modified: Tue, 16 Apr 2024 14:29:59 GMT
Connection: keep-alive
ETag: "661e8c27-267"
Accept-Ranges: bytes
3. Dọn dẹp Container
# Dừng container
docker stop my-web

# Xóa container
docker rm my-web
