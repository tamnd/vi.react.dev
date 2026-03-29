---
title: panicThreshold
---

<Intro>

Tùy chọn `panicThreshold` kiểm soát cách React Compiler xử lý lỗi trong quá trình biên dịch.

</Intro>

```js
{
  panicThreshold: 'none' // Recommended
}
```

<InlineToc />

---

## Reference {/*reference*/}

### `panicThreshold` {/*panicthreshold*/}

Xác định xem lỗi biên dịch có làm build thất bại hay chỉ bỏ qua tối ưu hóa.

#### Type {/*type*/}

```
'none' | 'critical_errors' | 'all_errors'
```

#### Giá trị mặc định {/*default-value*/}

`'none'`

#### Options {/*options*/}

- **`'none'`** (mặc định, được khuyến nghị): Bỏ qua những component không thể biên dịch và tiếp tục build
- **`'critical_errors'`**: Chỉ làm build thất bại với các lỗi compiler nghiêm trọng
- **`'all_errors'`**: Làm build thất bại với mọi chẩn đoán từ compiler

#### Caveats {/*caveats*/}

- Bản build production luôn nên dùng `'none'`
- Việc build thất bại sẽ ngăn ứng dụng của bạn được build
- Compiler sẽ tự động phát hiện và bỏ qua code có vấn đề khi dùng `'none'`
- Ngưỡng cao hơn chỉ hữu ích trong quá trình phát triển để gỡ lỗi

---

## Usage {/*usage*/}

### Cấu hình production (khuyến nghị) {/*production-configuration*/}

Với bản build production, luôn dùng `'none'`. Đây là giá trị mặc định:

```js
{
  panicThreshold: 'none'
}
```

Điều này bảo đảm:
- Bản build của bạn không bao giờ thất bại vì vấn đề từ compiler
- Những component không thể tối ưu vẫn chạy bình thường
- Số lượng component được tối ưu là tối đa
- Việc triển khai production ổn định

### Gỡ lỗi khi phát triển {/*development-debugging*/}

Hãy tạm thời dùng ngưỡng nghiêm ngặt hơn để tìm ra vấn đề:

```js
const isDevelopment = process.env.NODE_ENV === 'development';

{
  panicThreshold: isDevelopment ? 'critical_errors' : 'none',
  logger: {
    logEvent(filename, event) {
      if (isDevelopment && event.kind === 'CompileError') {
        // ...
      }
    }
  }
}
```
