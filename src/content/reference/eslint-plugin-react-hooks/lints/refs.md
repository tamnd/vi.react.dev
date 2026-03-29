---
title: refs
---

<Intro>

Kiểm tra cách dùng ref đúng, không đọc hoặc ghi trong lúc kết xuất. Xem phần "pitfalls" trong [cách dùng `useRef()`](/reference/react/useRef#usage).

</Intro>

## Chi tiết luật {/*rule-details*/}

Ref giữ những giá trị không được dùng để kết xuất. Khác với state, thay đổi ref không kích hoạt kết xuất lại. Việc đọc hoặc ghi `ref.current` trong lúc kết xuất sẽ phá vỡ kỳ vọng của React. Ref có thể chưa được khởi tạo khi bạn cố đọc nó, và giá trị của chúng có thể cũ hoặc không nhất quán.

## Cách luật này phát hiện ref {/*how-it-detects-refs*/}

Lint này chỉ áp dụng các quy tắc đó cho những giá trị mà nó biết là ref. Một giá trị được suy ra là ref khi compiler thấy bất kỳ mẫu nào sau đây:

- Được trả về từ `useRef()` hoặc `React.createRef()`.

  ```js
  const scrollRef = useRef(null);
  ```

- Một định danh có tên `ref` hoặc kết thúc bằng `Ref` mà đọc từ hoặc ghi vào `.current`.

  ```js
  buttonRef.current = node;
  ```

- Được truyền qua prop JSX `ref`, ví dụ `<div ref={someRef} />`.

  ```jsx
  <input ref={inputRef} />
  ```

Khi một giá trị đã được đánh dấu là ref, suy luận đó sẽ đi theo giá trị qua các phép gán, destructuring hoặc lời gọi hàm trợ giúp. Điều này cho phép lint nêu ra vi phạm ngay cả khi `ref.current` được truy cập bên trong một hàm khác nhận ref làm đối số.

## Các vi phạm thường gặp {/*common-violations*/}

- Đọc `ref.current` trong lúc kết xuất
- Cập nhật `refs` trong lúc kết xuất
- Dùng `refs` cho các giá trị đáng lẽ nên là state

### Không hợp lệ {/*invalid*/}

Ví dụ về mã không đúng cho luật này:

```js
// ❌ Reading ref during render
function Component() {
  const ref = useRef(0);
  const value = ref.current; // Don't read during render
  return <div>{value}</div>;
}

// ❌ Modifying ref during render
function Component({value}) {
  const ref = useRef(null);
  ref.current = value; // Don't modify during render
  return <div />;
}
```

### Hợp lệ {/*valid*/}

Ví dụ về mã đúng cho luật này:

```js
// ✅ Read ref in effects/handlers
function Component() {
  const ref = useRef(null);

  useEffect(() => {
    if (ref.current) {
      console.log(ref.current.offsetWidth); // OK in effect
    }
  });

  return <div ref={ref} />;
}

// ✅ Use state for UI values
function Component() {
  const [count, setCount] = useState(0);

  return (
    <button onClick={() => setCount(count + 1)}>
      {count}
    </button>
  );
}

// ✅ Lazy initialization of ref value
function Component() {
  const ref = useRef(null);

  // Initialize only once on first use
  if (ref.current === null) {
    ref.current = expensiveComputation(); // OK - lazy initialization
  }

  const handleClick = () => {
    console.log(ref.current); // Use the initialized value
  };

  return <button onClick={handleClick}>Click</button>;
}
```

## Khắc phục sự cố {/*troubleshooting*/}

### Lint đã đánh dấu object thường của tôi có `.current` {/*plain-object-current*/}

Heuristic về tên cố ý coi `ref.current` và `fooRef.current` là ref thực sự. Nếu bạn đang mô hình hóa một object bao chứa tùy biến, hãy chọn tên khác, ví dụ `box`, hoặc chuyển giá trị có thể thay đổi đó sang state. Việc đổi tên sẽ tránh lint này vì compiler sẽ ngừng suy luận nó là ref.
