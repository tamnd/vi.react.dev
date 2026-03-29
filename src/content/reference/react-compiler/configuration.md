---
title: Cấu hình
---

<Intro>

Trang này liệt kê toàn bộ tùy chọn cấu hình có sẵn trong React Compiler.

</Intro>

<Note>

Với hầu hết ứng dụng, các tùy chọn mặc định sẽ hoạt động ngay. Nếu bạn có nhu cầu đặc biệt, có thể dùng các tùy chọn nâng cao này.

</Note>

```js
// babel.config.js
module.exports = {
  plugins: [
    [
      'babel-plugin-react-compiler', {
        // compiler options
      }
    ]
  ]
};
```

---

## Kiểm soát biên dịch {/*compilation-control*/}

Những tùy chọn này điều khiển *những gì* compiler tối ưu và *cách* nó chọn component cùng Hook để biên dịch.

* [`compilationMode`](/reference/react-compiler/compilationMode) điều khiển chiến lược chọn hàm để biên dịch, ví dụ tất cả hàm, chỉ các hàm có chú thích, hoặc phát hiện thông minh.

```js
{
  compilationMode: 'annotation' // Only compile "use memo" functions
}
```

---

## Tương thích phiên bản {/*version-compatibility*/}

Cấu hình phiên bản React bảo đảm compiler sinh ra mã tương thích với phiên bản React của bạn.

[`target`](/reference/react-compiler/target) chỉ định phiên bản React bạn đang dùng, 17, 18 hoặc 19.

```js
// For React 18 projects
{
  target: '18' // Also requires react-compiler-runtime package
}
```

---

## Xử lý lỗi {/*error-handling*/}

Những tùy chọn này điều khiển cách compiler phản ứng với code không tuân theo [Các quy tắc của React](/reference/rules).

[`panicThreshold`](/reference/react-compiler/panicThreshold) quyết định nên làm build thất bại hay bỏ qua các component có vấn đề.

```js
// Recommended for production
{
  panicThreshold: 'none' // Skip components with errors instead of failing the build
}
```

---

## Gỡ lỗi {/*debugging*/}

Các tùy chọn ghi log và phân tích giúp bạn hiểu compiler đang làm gì.

[`logger`](/reference/react-compiler/logger) cung cấp cơ chế ghi log tùy chỉnh cho các sự kiện biên dịch.

```js
{
  logger: {
    logEvent(filename, event) {
      if (event.kind === 'CompileSuccess') {
        console.log('Compiled:', filename);
      }
    }
  }
}
```

---

## Cờ tính năng {/*feature-flags*/}

Biên dịch có điều kiện cho phép bạn kiểm soát thời điểm dùng mã đã được tối ưu.

[`gating`](/reference/react-compiler/gating) bật cờ tính năng ở thời gian chạy cho A/B testing hoặc rollout dần.

```js
{
  gating: {
    source: 'my-feature-flags',
    importSpecifierName: 'isCompilerEnabled'
  }
}
```

---

## Các mẫu cấu hình phổ biến {/*common-patterns*/}

### Cấu hình mặc định {/*default-configuration*/}

Với hầu hết ứng dụng React 19, compiler hoạt động mà không cần cấu hình:

```js
// babel.config.js
module.exports = {
  plugins: [
    'babel-plugin-react-compiler'
  ]
};
```

### Dự án React 17/18 {/*react-17-18*/}

Các phiên bản React cũ hơn cần gói runtime và cấu hình target:

```bash
npm install react-compiler-runtime@latest
```

```js
{
  target: '18' // or '17'
}
```

### Áp dụng dần {/*incremental-adoption*/}

Bắt đầu với các thư mục cụ thể rồi mở rộng dần:

```js
{
  compilationMode: 'annotation' // Only compile "use memo" functions
}
```
