---
title: set-state-in-render
---

<Intro>

Kiểm tra để ngăn việc đặt state vô điều kiện trong lúc kết xuất, vì điều này có thể kích hoạt thêm các lần kết xuất và các vòng lặp kết xuất vô hạn tiềm ẩn.

</Intro>

## Chi tiết luật {/*rule-details*/}

Việc gọi `setState` trong lúc kết xuất một cách vô điều kiện sẽ kích hoạt thêm một lần kết xuất khác trước khi lần hiện tại kết thúc. Điều này tạo ra một vòng lặp vô hạn làm ứng dụng của bạn bị crash.

## Các vi phạm thường gặp {/*common-violations*/}

### Không hợp lệ {/*invalid*/}

```js {expectedErrors: {'react-compiler': [4]}}
// ❌ Unconditional setState directly in render
function Component({value}) {
  const [count, setCount] = useState(0);
  setCount(value); // Infinite loop!
  return <div>{count}</div>;
}
```

### Hợp lệ {/*valid*/}

```js
// ✅ Derive during render
function Component({items}) {
  const sorted = [...items].sort(); // Just calculate it in render
  return <ul>{sorted.map(/*...*/)}</ul>;
}

// ✅ Set state in event handler
function Component() {
  const [count, setCount] = useState(0);
  return (
    <button onClick={() => setCount(count + 1)}>
      {count}
    </button>
  );
}

// ✅ Derive from props instead of setting state
function Component({user}) {
  const name = user?.name || '';
  const email = user?.email || '';
  return <div>{name}</div>;
}

// ✅ Conditionally derive state from props and state from previous renders
function Component({ items }) {
  const [isReverse, setIsReverse] = useState(false);
  const [selection, setSelection] = useState(null);

  const [prevItems, setPrevItems] = useState(items);
  if (items !== prevItems) { // This condition makes it valid
    setPrevItems(items);
    setSelection(null);
  }
  // ...
}
```

## Khắc phục sự cố {/*troubleshooting*/}

### Tôi muốn đồng bộ state với một prop {/*clamp-state-to-prop*/}

Một vấn đề phổ biến là cố "sửa" state sau khi nó đã được kết xuất. Giả sử bạn muốn giữ cho bộ đếm không vượt quá prop `max`:

```js
// ❌ Wrong: clamps during render
function Counter({max}) {
  const [count, setCount] = useState(0);

  if (count > max) {
    setCount(max);
  }

  return (
    <button onClick={() => setCount(count + 1)}>
      {count}
    </button>
  );
}
```

Ngay khi `count` vượt quá `max`, một vòng lặp vô hạn sẽ bị kích hoạt.

Thay vào đó, thường tốt hơn nếu chuyển logic này vào sự kiện, tức nơi state được đặt lần đầu. Ví dụ, bạn có thể ép giá trị tối đa ngay tại thời điểm cập nhật state:

```js
// ✅ Clamp when updating
function Counter({max}) {
  const [count, setCount] = useState(0);

  const increment = () => {
    setCount(current => Math.min(current + 1, max));
  };

  return <button onClick={increment}>{count}</button>;
}
```

Giờ setter chỉ chạy khi phản hồi click, React hoàn tất kết xuất bình thường, và `count` sẽ không bao giờ vượt quá `max`.

Trong một số trường hợp hiếm gặp, bạn có thể cần điều chỉnh state dựa trên thông tin từ các lần kết xuất trước. Với các trường hợp đó, hãy làm theo [mẫu này](https://react.dev/reference/react/useState#storing-information-from-previous-renders) để đặt state có điều kiện.
