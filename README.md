# vi.react.dev

Kho lưu trữ này chứa mã nguồn và tài liệu cho bản dịch tiếng Việt của [react.dev](https://react.dev/).

## Bắt đầu

### Yêu cầu

1. Git
2. Node từ `v16.8.0` trở lên
3. Yarn. Xem hướng dẫn cài đặt trên [website Yarn](https://yarnpkg.com/lang/en/docs/install/)
4. Một fork của repo này nếu bạn muốn đóng góp
5. Bản clone của [tamnd/vi.react.dev](https://github.com/tamnd/vi.react.dev) trên máy của bạn

### Cài đặt

1. `cd vi.react.dev` để vào thư mục gốc của dự án
2. Chạy `yarn` để cài các dependency npm của website

### Chạy cục bộ

1. Chạy `yarn dev` để khởi động development server bằng [Next.js](https://nextjs.org/)
2. Mở `http://localhost:3000` trong trình duyệt

## Đóng góp

### Hướng dẫn chung

Tài liệu được chia thành nhiều phần với mục đích và giọng điệu khác nhau. Nếu bạn định viết nhiều hơn vài câu, hãy đọc trước [hướng dẫn đóng góp của repo gốc](https://github.com/reactjs/react.dev/blob/main/CONTRIBUTING.md#guidelines-for-text) cho đúng loại nội dung.

### Tạo nhánh

1. Chạy `git checkout main` từ bất kỳ thư mục nào trong repo cục bộ của bạn
2. Chạy `git pull origin main` để cập nhật `main`
3. Chạy `git checkout -b ten-nhanh-cua-ban` để tạo nhánh mới

### Thực hiện thay đổi

1. Làm theo phần [Chạy cục bộ](#chạy-cục-bộ)
2. Lưu file và kiểm tra trong trình duyệt
3. Các thay đổi trong `src` sẽ hot-reload
4. Các thay đổi trong `src/content` sẽ hot-reload
5. Nếu làm việc với plugin, bạn có thể cần xóa thư mục `.cache` và khởi động lại server

### Kiểm tra thay đổi

1. Nếu có thể, hãy kiểm tra các thay đổi giao diện trên desktop và mobile, với các trình duyệt phổ biến
2. Chạy `yarn check-all` để chạy Prettier, ESLint, và kiểm tra kiểu

### Đẩy thay đổi

1. Chạy `git add -A && git commit -m "Thông điệp commit"` để tạo commit
2. Chạy `git push origin ten-nhanh-cua-ban`
3. Mở pull request trên [tamnd/vi.react.dev](https://github.com/tamnd/vi.react.dev)
4. Nếu thay đổi giao diện, nên đính kèm ảnh chụp màn hình

## Dịch tài liệu

Nếu bạn muốn tham gia dịch tài liệu React sang tiếng Việt:

1. Đọc [TRANSLATE.md](/Users/apple/github/tamnd/vi.react.dev/TRANSLATE.md)
2. Theo dõi thuật ngữ trong [GLOSSARY.md](/Users/apple/github/tamnd/vi.react.dev/GLOSSARY.md)
3. Ưu tiên dịch từ upstream hiện tại của `reactjs/react.dev`
4. Dùng `zh-hans.react.dev` để đối chiếu độ đầy đủ, không dùng làm nguồn dịch chính

## Giấy phép

Nội dung gửi lên [react.dev](https://react.dev/) được cấp phép theo CC-BY-4.0, như mô tả trong [LICENSE-DOCS.md](https://github.com/reactjs/react.dev/blob/main/LICENSE-DOCS.md).
