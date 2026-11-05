# Bài 6: Ngăn chặn rò rỉ thông tin bí mật trên GitHub

## 1. Pre-push Checklist

Trước khi đẩy mã nguồn lên GitHub Public, nhóm cần kiểm tra:

- [ ] Không hardcode API Key, mật khẩu, Access Token trong source code.
- [ ] Không đưa file `.env` lên GitHub.
- [ ] Đã thêm `.env` vào file `.gitignore`.
- [ ] Đã tạo file `.env.example` không chứa thông tin bí mật.
- [ ] Sử dụng công cụ quét mã nguồn như Gitleaks để phát hiện Secret bị lộ.
- [ ] Kiểm tra lại các file bằng lệnh `git status`.
- [ ] Chỉ push những file cần thiết lên GitHub.

## 2. Cấu trúc file .env.example

Tạo file `.env.example` để cung cấp mẫu cấu hình cho các thành viên mà không làm lộ thông tin bí mật.

Cấu trúc đề xuất:

```text
project/
├── .env
├── .env.example
├── .gitignore
├── src/
└── README.md
```

Nội dung file `.env.example`:

```env
# DEVELOPMENT
DEV_API_URL=http://localhost:3000
DEV_API_KEY=your_dev_api_key

# TEST
TEST_API_URL=https://test.example.com
TEST_API_KEY=your_test_api_key

# PRODUCTION
PROD_API_URL=https://api.example.com
PROD_API_KEY=your_production_api_key
```

Nội dung file `.gitignore`:

```gitignore
.env
.env.*
!.env.example
```

Lưu ý: File `.env` chứa thông tin thật phải được giữ riêng và không đưa lên GitHub.

## 3. Kích hoạt xác thực hai yếu tố (2FA)

Yêu cầu tất cả thành viên bật 2FA cho tài khoản GitHub.

Các bước thực hiện:

1. Đăng nhập GitHub.
2. Chọn ảnh đại diện → Settings.
3. Chọn Password and authentication.
4. Tìm mục Two-factor authentication.
5. Chọn Enable two-factor authentication.
6. Thiết lập ứng dụng xác thực như Google Authenticator.
7. Lưu Backup Codes ở nơi an toàn.

Đối với quản trị viên repository:

- Kiểm tra các thành viên đã bật 2FA.
- Thiết lập yêu cầu 2FA cho tổ chức GitHub nếu sử dụng GitHub Organization.
- Loại bỏ quyền truy cập của tài khoản không đáp ứng yêu cầu bảo mật.

## 4. Kết luận

Để tránh rò rỉ thông tin bí mật khi đưa dự án lên GitHub Public, nhóm cần kiểm tra mã nguồn trước khi push, sử dụng `.env.example` thay cho thông tin thật, dùng Gitleaks để quét API Keys và bắt buộc các thành viên bật 2FA. Những biện pháp này giúp giảm nguy cơ bị đánh cắp thông tin và truy cập trái phép vào hệ thống.
