BTVN - Nguyễn Xuân Hải
### Khởi chạy hệ thống

Mở CMD hoặc PowerShell tại thư mục dự án:

```cmd
docker compose config
docker compose up -d
docker compose ps
```

### Truy cập ứng dụng

- Juice Shop trực tiếp: http://localhost:3000
- Juice Shop qua WAF: http://localhost:8080

## Kiểm thử bảo mật

### SQL Injection

Truy cập trực tiếp:

```bash
curl -i "http://localhost:3000/rest/products/search?q=')%20OR%201=1--"
```

Truy cập qua WAF:

```bash
curl -i "http://localhost:8080/rest/products/search?q=')%20OR%201=1--"
```

### Cross-Site Scripting (XSS)

Truy cập trực tiếp:

```bash
curl -i --get "http://localhost:3000/rest/products/search" --data-urlencode "q=<script>alert(1)</script>"
```

Truy cập qua WAF:

```bash
curl -i --get "http://localhost:8080/rest/products/search" --data-urlencode "q=<script>alert(1)</script>"
```

### Path Traversal

Truy cập trực tiếp:

```bash
curl -i "http://localhost:3000/?file=../../etc/passwd"
```

Truy cập qua WAF:

```bash
curl -i "http://localhost:8080/?file=../../etc/passwd"
```