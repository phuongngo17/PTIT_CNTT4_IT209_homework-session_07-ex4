# Bài 4: Cấu hình Reverse Proxy Nginx cho ứng dụng Spring Boot

## 1. Mục tiêu

Cấu hình Nginx làm Reverse Proxy:

* `/` phục vụ trang HTML tĩnh.
* `/api/` chuyển tiếp đến ứng dụng Spring Boot tại port `8082`.

## 2. Trang web tĩnh

Thư mục:

```text
/var/www/html/
```

File:

```text
/var/www/html/index.html
```

Trang web hiển thị:

* PTIT DevOps
* Chào mừng đến với website của tôi!
* Server: Ubuntu 24.04
* Web Server: Nginx

## 3. Reverse Proxy

File cấu hình:

```text
/etc/nginx/sites-available/spring-proxy.conf
```

Nginx được cấu hình:

```text
/       → /var/www/html/
/api/   → http://127.0.0.1:8082/
```

Cấu hình được kích hoạt bằng symbolic link:

```text
/etc/nginx/sites-enabled/spring-proxy.conf
```

## 4. Kiểm tra cấu hình

Lệnh:

```bash
sudo nginx -t
```

Kết quả:

```text
syntax is ok
test is successful
```

## 5. Kiểm tra trang chủ

Lệnh:

```bash
curl -I http://localhost/
```

Kết quả:

```text
HTTP/1.1 200 OK
```

## 6. Kiểm tra API

Lệnh:

```bash
curl -I http://localhost/api/health
```

Request `/api/health` được Nginx chuyển tiếp đến Spring Boot tại port `8082`.
