---
title: config
---

<Intro>

Kiểm tra các [tùy chọn cấu hình](/reference/react-compiler/configuration) của compiler.

</Intro>

## Chi tiết quy tắc {/*rule-details*/}

React Compiler chấp nhận nhiều [tùy chọn cấu hình](/reference/react-compiler/configuration) để kiểm soát hành vi của nó. Quy tắc này kiểm tra rằng cấu hình của bạn dùng đúng tên tùy chọn và kiểu giá trị, nhờ đó ngăn những lỗi âm thầm do gõ sai hoặc thiết lập sai.

### Invalid {/*invalid*/}

Ví dụ về code không đúng với quy tắc này:

```js
// ❌ Tên tùy chọn không xác định
module.exports = {
  plugins: [
    ['babel-plugin-react-compiler', {
      compileMode: 'all' // Gõ sai: phải là compilationMode
    }]
  ]
};

// ❌ Giá trị tùy chọn không hợp lệ
module.exports = {
  plugins: [
    ['babel-plugin-react-compiler', {
      compilationMode: 'everything' // Không hợp lệ: hãy dùng 'all' hoặc 'infer'
    }]
  ]
};
```

### Valid {/*valid*/}

Ví dụ về code đúng với quy tắc này:

```js
// ✅ Cấu hình compiler hợp lệ
module.exports = {
  plugins: [
    ['babel-plugin-react-compiler', {
      compilationMode: 'infer',
      panicThreshold: 'critical_errors'
    }]
  ]
};
```

## Khắc phục sự cố {/*troubleshooting*/}

### Cấu hình không hoạt động như mong đợi {/*config-not-working*/}

Cấu hình compiler của bạn có thể đang có lỗi gõ sai hoặc giá trị không đúng:

```js
// ❌ Sai: Những lỗi cấu hình thường gặp
module.exports = {
  plugins: [
    ['babel-plugin-react-compiler', {
      // Gõ sai tên tùy chọn
      compilationMod: 'all',
      // Sai kiểu giá trị
      panicThreshold: true,
      // Tùy chọn không xác định
      optimizationLevel: 'max'
    }]
  ]
};
```

Hãy kiểm tra [tài liệu cấu hình](/reference/react-compiler/configuration) để biết các tùy chọn hợp lệ:

```js
// ✅ Tốt hơn: Cấu hình hợp lệ
module.exports = {
  plugins: [
    ['babel-plugin-react-compiler', {
      compilationMode: 'all', // hoặc 'infer'
      panicThreshold: 'none', // hoặc 'critical_errors', 'all_errors'
      // Chỉ dùng những tùy chọn đã được tài liệu hóa
    }]
  ]
};
```
