# Deployment Guide cho Bộ phận IT

Đây là hướng dẫn triển khai site training nội bộ tĩnh từ repo hiện tại.

## Mục tiêu

- Triển khai toàn bộ file HTML và tài nguyên có sẵn lên một site nội bộ.
- Domain chính là `training.thgfulfill.com` (hoặc một domain tương đương do IT định nghĩa).
- `index.html` là trang tổng hợp chính, các file HTML khác mở trực tiếp qua liên kết.
- Không cần backend phức tạp hay server side rendering.

## Những gì cần deploy

- `index.html`
- `onboarding.html`
- `search.html`
- `pod.html`
- `dropship.html`
- `fulfill.html`
- `express.html`
- `sop-sale.html`
- `sop-cskh.html`
- `sop-finance.html`
- `sop-cross.html`
- `trouble.html`
- `trouble_data.json`

> Lưu ý: Các file HTML được giữ nguyên, không chỉnh sửa nội dung.

## Yêu cầu cơ bản

1. Document root phải trỏ đến thư mục chứa `index.html`.
2. `index.html` cần là trang mặc định khi vào `training.thgfulfill.com`.
3. Các file HTML con phải truy cập được bằng URL tương ứng, ví dụ `training.thgfulfill.com/fulfill.html`.
4. Nếu site được đặt làm trang tĩnh, không cần cấu hình route server đặc biệt ngoài trả về file tĩnh.

## Triển khai với các môi trường phổ biến

### 1. Web server tĩnh (nginx)

- Document root: thư mục chứa repo
- `index.html` là file mặc định

Ví dụ cấu hình nginx:

```
server {
    listen 80;
    server_name training.thgfulfill.com;

    root /path/to/repo;
    index index.html;

    location / {
        try_files $uri $uri/ =404;
    }
}
```

### 2. Apache HTTP Server

- Đặt `DocumentRoot` trỏ tới thư mục chứa repo
- Bật `DirectoryIndex index.html`

Ví dụ cấu hình Apache:

```
<VirtualHost *:80>
    ServerName training.thgfulfill.com
    DocumentRoot "/path/to/repo"

    <Directory "/path/to/repo">
        Options Indexes FollowSymLinks
        AllowOverride None
        Require all granted
    </Directory>

    DirectoryIndex index.html
</VirtualHost>
```

### 3. IIS (Windows)

- Tạo site mới hoặc ứng dụng mới với physical path trỏ tới thư mục chứa repo.
- Đảm bảo `index.html` nằm trong Default Document list.
- Cho phép truy cập file tĩnh `.html` và `.json`.

### 4. GitHub Pages

- Push toàn bộ file lên nhánh `main` hoặc `gh-pages`.
- Bật GitHub Pages và chọn source là `root` repository.
- GitHub Pages sẽ tự động phục vụ `index.html` và các file HTML khác.

### 5. AWS S3 + CloudFront

- Upload toàn bộ file vào bucket S3.
- Thiết lập bucket làm static website hosting.
- Đặt `index.html` là trang index.
- Nếu dùng CloudFront, cấu hình origin trỏ tới bucket và ánh xạ domain `training.thgfulfill.com`.

### 6. Netlify / Vercel / other static hosts

- Chọn repo hoặc upload code.
- Chọn build command không cần thiết (site tĩnh), directory xuất bản là root repository.
- Đảm bảo `index.html` được phục vụ làm landing page.

## Gợi ý cấu hình route cho domain

- `https://training.thgfulfill.com/` -> `index.html`
- `https://training.thgfulfill.com/onboarding.html` -> `onboarding.html`
- `https://training.thgfulfill.com/fulfill.html` -> `fulfill.html`
- `https://training.thgfulfill.com/trouble.html` -> `trouble.html`

Vì site tĩnh chỉ dùng các liên kết tương đối, nên không cần xử lý route phức tạp.

## Kết luận

Repo hiện tại đã sẵn sàng để deploy dưới dạng một site tĩnh nội bộ.

- Không cần backend
- Không cần sửa file HTML
- Tất cả trang đều có thể mở trực tiếp từ domain hoặc thông qua `index.html`

Nếu cần, bộ phận IT có thể sử dụng cấu hình trên để triển khai với nginx, Apache, IIS, GitHub Pages, S3 hoặc các static hosting khác.