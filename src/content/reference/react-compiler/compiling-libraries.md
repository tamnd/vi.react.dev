---
title: Biên dịch thư viện
---

<Intro>
Hướng dẫn này giúp tác giả thư viện hiểu cách dùng React Compiler để phát hành mã thư viện đã được tối ưu cho người dùng của họ.
</Intro>

<InlineToc />

## Vì sao nên phát hành mã đã biên dịch? {/*why-ship-compiled-code*/}

Là tác giả thư viện, bạn có thể biên dịch mã thư viện trước khi phát hành lên npm. Điều này mang lại một số lợi ích:

- **Cải thiện hiệu năng cho mọi người dùng** - Người dùng thư viện của bạn sẽ nhận được mã đã tối ưu kể cả khi họ chưa dùng React Compiler
- **Người dùng không cần cấu hình gì thêm** - Các tối ưu hóa hoạt động ngay lập tức
- **Hành vi nhất quán** - Mọi người dùng đều nhận cùng một phiên bản tối ưu bất kể cách họ build

## Thiết lập biên dịch {/*setting-up-compilation*/}

Hãy thêm React Compiler vào quy trình build của thư viện:

<TerminalBlock>
npm install -D babel-plugin-react-compiler@latest
</TerminalBlock>

Cấu hình công cụ build để biên dịch thư viện. Ví dụ với Babel:

```js
// babel.config.js
module.exports = {
  plugins: [
    'babel-plugin-react-compiler',
  ],
  // ... other config
};
```

## Tương thích ngược {/*backwards-compatibility*/}

Nếu thư viện của bạn hỗ trợ các phiên bản React thấp hơn 19, bạn sẽ cần cấu hình bổ sung:

### 1. Cài gói runtime {/*install-runtime-package*/}

Chúng tôi khuyên bạn cài `react-compiler-runtime` như một dependency trực tiếp:

<TerminalBlock>
npm install react-compiler-runtime@latest
</TerminalBlock>

```json
{
  "dependencies": {
    "react-compiler-runtime": "^1.0.0"
  },
  "peerDependencies": {
    "react": "^17.0.0 || ^18.0.0 || ^19.0.0"
  }
}
```

### 2. Cấu hình phiên bản đích {/*configure-target-version*/}

Đặt phiên bản React tối thiểu mà thư viện của bạn hỗ trợ:

```js
{
  target: '17', // Minimum supported React version
}
```

## Chiến lược kiểm thử {/*testing-strategy*/}

Hãy kiểm thử thư viện của bạn cả khi có biên dịch lẫn khi không có biên dịch để bảo đảm tính tương thích. Chạy bộ test hiện có trên mã đã biên dịch, đồng thời tạo một cấu hình test riêng bỏ qua compiler. Cách này giúp phát hiện các vấn đề có thể phát sinh từ quá trình biên dịch và bảo đảm thư viện hoạt động đúng trong mọi tình huống.

## Khắc phục sự cố {/*troubleshooting*/}

### Thư viện không hoạt động với các phiên bản React cũ hơn {/*library-doesnt-work-with-older-react-versions*/}

Nếu thư viện đã biên dịch của bạn ném lỗi trong React 17 hoặc 18:

1. Xác minh bạn đã cài `react-compiler-runtime` làm dependency
2. Kiểm tra cấu hình `target` có khớp với phiên bản React tối thiểu mà bạn hỗ trợ không
3. Bảo đảm gói runtime được đưa vào bundle bạn phát hành

### Biên dịch xung đột với các plugin Babel khác {/*compilation-conflicts-with-other-babel-plugins*/}

Một số plugin Babel có thể xung đột với React Compiler:

1. Đặt `babel-plugin-react-compiler` ở vị trí sớm trong danh sách plugin
2. Tắt các tối ưu hóa xung đột trong những plugin khác
3. Kiểm thử kỹ đầu ra build của bạn

### Không tìm thấy module runtime {/*runtime-module-not-found*/}

Nếu người dùng thấy lỗi "Cannot find module 'react-compiler-runtime'":

1. Bảo đảm runtime được liệt kê trong `dependencies`, không phải `devDependencies`
2. Kiểm tra bundler của bạn có đưa runtime vào đầu ra không
3. Xác minh gói đã được phát hành lên npm cùng với thư viện

## Bước tiếp theo {/*next-steps*/}

- Tìm hiểu các [kỹ thuật gỡ lỗi](/learn/react-compiler/debugging) cho mã đã biên dịch
- Xem [các tùy chọn cấu hình](/reference/react-compiler/configuration) để biết đầy đủ tùy chọn của compiler
- Khám phá [các chế độ biên dịch](/reference/react-compiler/compilationMode) cho tối ưu hóa có chọn lọc
