# THG Internal Training Hub

Đây là một bộ tài liệu training nội bộ dưới dạng site tĩnh. Mục tiêu của repo là deploy lên server và hiển thị như một trang training, ví dụ `training.thgfulfill.com`.

## Nội dung repo

- `index.html` - Trang tổng hợp chính, chứa sidebar và liên kết đến tất cả các tài liệu con.
- `onboarding.html` - Tài liệu onboarding.
- `search.html` - Tài liệu hướng dẫn về tìm kiếm.
- `pod.html` - Tài liệu liên quan đến POD.
- `dropship.html` - Tài liệu Dropship.
- `fulfill.html` - Tài liệu Fulfillment.
- `express.html` - Tài liệu Express.
- `sop-sale.html` - SOP bộ phận Sale.
- `sop-cskh.html` - SOP bộ phận CSKH.
- `sop-finance.html` - SOP bộ phận Finance.
- `sop-cross.html` - SOP bộ phận Cross.
- `trouble.html` - Tài liệu xử lý sự cố.
- `trouble_data.json` - Dữ liệu phụ trợ cho `trouble.html`.

> Lưu ý: các file HTML không bị chỉnh sửa theo yêu cầu.

## Mô tả cách hoạt động

- `index.html` là trang entry point.
- Khi người dùng truy cập vào `training.thgfulfill.com`, server chỉ cần trả về `index.html`.
- Tại `index.html`, người dùng có thể nhấn vào các liên kết để mở các file HTML con.
- Mỗi file HTML con được trình bày độc lập và có thể mở trực tiếp bằng URL tương ứng.

## Các điều kiện cần để triển khai

1. Triển khai toàn bộ file hiện có lên thư mục gốc của site.
2. Thiết lập document root trỏ đến `index.html`.
3. Giữ nguyên cấu trúc file và liên kết tương đối, vì các trang HTML hiện tại sử dụng liên kết nội bộ.
4. Nếu dùng hosting tĩnh như GitHub Pages hoặc nginx, chỉ cần đảm bảo `index.html` là trang mặc định.

## Ví dụ cấu hình

### Với domain `training.thgfulfill.com`

- `https://training.thgfulfill.com/` -> `index.html`
- `https://training.thgfulfill.com/fulfill.html` -> `fulfill.html`
- `https://training.thgfulfill.com/sop-sale.html` -> `sop-sale.html`

### Nếu dùng GitHub Pages

1. Push toàn bộ file lên repository.
2. Bật GitHub Pages ở nhánh `main` (hoặc `master`) và để root repository làm source.
3. Domain sẽ hiển thị `index.html` làm trang landing.

## Gợi ý cho bộ phận IT

- Đây là một site tài liệu nội bộ tĩnh, không cần backend phức tạp.
- Chỉ cần hosting tĩnh, server web trả về file HTML và các tài nguyên liên quan.
- `index.html` hiện đã chịu trách nhiệm tổng hợp và liên kết đến tất cả phần học.
- Nếu cần, có thể dùng reverse proxy hoặc route domain để ánh xạ `training.thgfulfill.com` đến thư mục chứa repo.

## Kết luận

Repo này đã sẵn sàng để deploy như một trang training nội bộ.

- `index.html` là trang tổng hợp chính.
- Các tài liệu con nằm trong các file HTML riêng.
- Không cần chỉnh sửa thêm HTML để chạy được site.

Nếu cần, tôi có thể hỗ trợ thêm phần hướng dẫn cấu hình web server cho deployment.
