---
title: gating
---

<Intro>

Kiểm tra cấu hình của [chế độ gating](/reference/react-compiler/gating).

</Intro>

## Chi tiết quy tắc {/*rule-details*/}

Chế độ gating cho phép bạn áp dụng dần React Compiler bằng cách đánh dấu những component cụ thể để tối ưu hóa. Quy tắc này bảo đảm cấu hình gating của bạn hợp lệ để compiler biết cần xử lý component nào.

### Invalid {/*invalid*/}

Ví dụ về code không đúng với quy tắc này:

```js
// ❌ Thiếu trường bắt buộc
module.exports = {
  plugins: [
    ['babel-plugin-react-compiler', {
      gating: {
        importSpecifierName: '__experimental_useCompiler'
        // Thiếu trường 'source'
      }
    }]
  ]
};

// ❌ Kiểu gating không hợp lệ
module.exports = {
  plugins: [
    ['babel-plugin-react-compiler', {
      gating: '__experimental_useCompiler' // Phải là object
    }]
  ]
};
```

### Valid {/*valid*/}

Ví dụ về code đúng với quy tắc này:

```js
// ✅ Cấu hình gating đầy đủ
module.exports = {
  plugins: [
    ['babel-plugin-react-compiler', {
      gating: {
        importSpecifierName: 'isCompilerEnabled', // tên hàm được export
        source: 'featureFlags' // tên module
      }
    }]
  ]
};

// featureFlags.js
export function isCompilerEnabled() {
  // ...
}

// ✅ Không dùng gating (biên dịch mọi component)
module.exports = {
  plugins: [
    ['babel-plugin-react-compiler', {
      // Không có trường gating - biên dịch tất cả component
    }]
  ]
};
```
