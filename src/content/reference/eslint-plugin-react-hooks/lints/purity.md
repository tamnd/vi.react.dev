---
title: purity
---

<Intro>

Kiểm tra rằng [component/Hook là thuần](/reference/rules/components-and-hooks-must-be-pure) bằng cách xác nhận chúng không gọi những hàm đã biết là không thuần.

</Intro>

## Chi tiết quy tắc {/*rule-details*/}

Component React phải là hàm thuần. Với cùng một props, chúng phải luôn trả về cùng một JSX. Khi component dùng các hàm như `Math.random()` hoặc `Date.now()` trong lúc render, chúng tạo ra kết quả khác nhau ở mỗi lần render, làm phá vỡ các giả định của React và gây ra lỗi như hydration mismatch, memoization không chính xác và hành vi khó đoán.

## Vi phạm thường gặp {/*common-violations*/}

Nói chung, bất kỳ API nào trả về giá trị khác nhau cho cùng một đầu vào đều vi phạm quy tắc này. Những ví dụ thường gặp gồm:

- `Math.random()`
- `Date.now()` / `new Date()`
- `crypto.randomUUID()`
- `performance.now()`

### Invalid {/*invalid*/}

Ví dụ về code không đúng với quy tắc này:

```js
// ❌ Math.random() trong render
function Component() {
  const id = Math.random(); // Khác nhau ở mỗi lần render
  return <div key={id}>Content</div>;
}

// ❌ Date.now() để lấy giá trị
function Component() {
  const timestamp = Date.now(); // Thay đổi ở mỗi lần render
  return <div>Được tạo lúc: {timestamp}</div>;
}
```

### Valid {/*valid*/}

Ví dụ về code đúng với quy tắc này:

```js
// ✅ ID ổn định từ state ban đầu
function Component() {
  const [id] = useState(() => crypto.randomUUID());
  return <div key={id}>Content</div>;
}
```

## Khắc phục sự cố {/*troubleshooting*/}

### Tôi cần hiển thị thời gian hiện tại {/*current-time*/}

Việc gọi `Date.now()` trong lúc render sẽ khiến component của bạn không còn thuần:

```js {expectedErrors: {'react-compiler': [3]}}
// ❌ Sai: thời gian thay đổi ở mỗi lần render
function Clock() {
  return <div>Thời gian hiện tại: {Date.now()}</div>;
}
```

Thay vào đó, hãy [chuyển hàm không thuần ra ngoài render](/reference/rules/components-and-hooks-must-be-pure#components-and-hooks-must-be-idempotent):

```js
function Clock() {
  const [time, setTime] = useState(() => Date.now());

  useEffect(() => {
    const interval = setInterval(() => {
      setTime(Date.now());
    }, 1000);

    return () => clearInterval(interval);
  }, []);

  return <div>Thời gian hiện tại: {time}</div>;
}
```
