---
title: exhaustive-deps
---

<Intro>

Kiểm tra để bảo đảm mảng dependency của các React Hook chứa đầy đủ mọi dependency cần thiết.

</Intro>

## Chi tiết luật {/*rule-details*/}

Các React Hook như `useEffect`, `useMemo` và `useCallback` chấp nhận mảng dependency. Khi một giá trị được tham chiếu bên trong các Hook đó không được đưa vào mảng dependency, React sẽ không chạy lại effect hoặc tính lại giá trị khi dependency đó thay đổi. Điều này gây ra stale closure, nơi Hook dùng các giá trị đã cũ.

## Các vi phạm thường gặp {/*common-violations*/}

Lỗi này thường xảy ra khi bạn cố "đánh lừa" React về dependency để kiểm soát thời điểm effect chạy. Effect phải đồng bộ component của bạn với các hệ thống bên ngoài. Mảng dependency cho React biết effect dùng những giá trị nào để React biết khi nào cần đồng bộ lại.

Nếu bạn thấy mình đang vật lộn với linter, rất có thể bạn cần tổ chức lại code. Hãy xem [Loại bỏ Dependency của Effect](/learn/removing-effect-dependencies) để tìm hiểu cách làm.

### Không hợp lệ {/*invalid*/}

Ví dụ về mã không đúng cho luật này:

```js
// ❌ Missing dependency
useEffect(() => {
  console.log(count);
}, []); // Missing 'count'

// ❌ Missing prop
useEffect(() => {
  fetchUser(userId);
}, []); // Missing 'userId'

// ❌ Incomplete dependencies
useMemo(() => {
  return items.sort(sortOrder);
}, [items]); // Missing 'sortOrder'
```

### Hợp lệ {/*valid*/}

Ví dụ về mã đúng cho luật này:

```js
// ✅ All dependencies included
useEffect(() => {
  console.log(count);
}, [count]);

// ✅ All dependencies included
useEffect(() => {
  fetchUser(userId);
}, [userId]);
```

## Khắc phục sự cố {/*troubleshooting*/}

### Việc thêm dependency là hàm gây ra vòng lặp vô hạn {/*function-dependency-loops*/}

Bạn có một effect nhưng lại tạo một hàm mới ở mỗi lần kết xuất:

```js
// ❌ Causes infinite loop
const logItems = () => {
  console.log(items);
};

useEffect(() => {
  logItems();
}, [logItems]); // Infinite loop!
```

Trong hầu hết trường hợp, bạn không cần effect. Hãy gọi hàm ở nơi hành động xảy ra:

```js
// ✅ Call it from the event handler
const logItems = () => {
  console.log(items);
};

return <button onClick={logItems}>Log</button>;

// ✅ Or derive during render if there's no side effect
items.forEach(item => {
  console.log(item);
});
```

Nếu bạn thực sự cần effect, ví dụ để subscribe vào thứ gì đó bên ngoài, hãy làm cho dependency ổn định:

```js
// ✅ useCallback keeps the function reference stable
const logItems = useCallback(() => {
  console.log(items);
}, [items]);

useEffect(() => {
  logItems();
}, [logItems]);

// ✅ Or move the logic straight into the effect
useEffect(() => {
  console.log(items);
}, [items]);
```

### Chỉ chạy effect đúng một lần {/*effect-on-mount*/}

Bạn muốn chạy effect một lần khi mount, nhưng linter phàn nàn về dependency bị thiếu:

```js
// ❌ Missing dependency
useEffect(() => {
  sendAnalytics(userId);
}, []); // Missing 'userId'
```

Hoặc là thêm dependency, được khuyên dùng, hoặc dùng ref nếu bạn thật sự cần chỉ chạy một lần:

```js
// ✅ Include dependency
useEffect(() => {
  sendAnalytics(userId);
}, [userId]);

// ✅ Or use a ref guard inside an effect
const sent = useRef(false);

useEffect(() => {
  if (sent.current) {
    return;
  }

  sent.current = true;
  sendAnalytics(userId);
}, [userId]);
```

## Tùy chọn {/*options*/}

Bạn có thể cấu hình custom effect hook bằng cài đặt ESLint dùng chung, khả dụng từ `eslint-plugin-react-hooks` 6.1.1 trở lên:

```js
{
  "settings": {
    "react-hooks": {
      "additionalEffectHooks": "(useMyEffect|useCustomEffect)"
    }
  }
}
```

- `additionalEffectHooks`: Mẫu regex khớp với các custom Hook nên được kiểm tra exhaustive dependencies. Cấu hình này được chia sẻ cho mọi luật `react-hooks`.

Để tương thích ngược, luật này cũng chấp nhận tùy chọn ở cấp luật:

```js
{
  "rules": {
    "react-hooks/exhaustive-deps": ["warn", {
      "additionalHooks": "(useMyCustomHook|useAnotherHook)"
    }]
  }
}
```

- `additionalHooks`: Regex cho các Hook nên được kiểm tra exhaustive dependencies. **Lưu ý:** Nếu tùy chọn ở cấp luật này được chỉ định, nó sẽ được ưu tiên hơn cấu hình `settings` dùng chung.
