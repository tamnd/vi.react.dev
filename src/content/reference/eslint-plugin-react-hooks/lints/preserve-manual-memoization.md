---
title: preserve-manual-memoization
---

<Intro>

Kiểm tra rằng phần memoization thủ công hiện có được compiler giữ nguyên. React Compiler sẽ chỉ biên dịch component và Hook nếu suy luận của nó [phù hợp hoặc tốt hơn phần memoization thủ công hiện có](/learn/react-compiler/introduction#what-should-i-do-about-usememo-usecallback-and-reactmemo).

</Intro>

## Chi tiết quy tắc {/*rule-details*/}

React Compiler giữ nguyên các lời gọi `useMemo`, `useCallback` và `React.memo` hiện có của bạn. Nếu bạn đã tự memoize một thứ gì đó, compiler sẽ giả định rằng bạn có lý do chính đáng và sẽ không xóa nó đi. Tuy nhiên, dependency không đầy đủ sẽ khiến compiler không thể hiểu luồng dữ liệu trong code của bạn và áp dụng thêm các tối ưu hóa.

### Invalid {/*invalid*/}

Ví dụ về code không đúng với quy tắc này:

```js
// ❌ Thiếu dependency trong useMemo
function Component({ data, filter }) {
  const filtered = useMemo(
    () => data.filter(filter),
    [data] // Thiếu dependency 'filter'
  );

  return <List items={filtered} />;
}

// ❌ Thiếu dependency trong useCallback
function Component({ onUpdate, value }) {
  const handleClick = useCallback(() => {
    onUpdate(value);
  }, [onUpdate]); // Thiếu 'value'

  return <button onClick={handleClick}>Update</button>;
}
```

### Valid {/*valid*/}

Ví dụ về code đúng với quy tắc này:

```js
// ✅ Dependency đầy đủ
function Component({ data, filter }) {
  const filtered = useMemo(
    () => data.filter(filter),
    [data, filter] // Đã bao gồm mọi dependency
  );

  return <List items={filtered} />;
}

// ✅ Hoặc để compiler tự xử lý
function Component({ data, filter }) {
  // Không cần memoization thủ công
  const filtered = data.filter(filter);
  return <List items={filtered} />;
}
```

## Khắc phục sự cố {/*troubleshooting*/}

### Tôi có nên xóa phần memoization thủ công không? {/*remove-manual-memoization*/}

Bạn có thể tự hỏi liệu React Compiler có khiến memoization thủ công trở nên không cần thiết nữa hay không:

```js
// Tôi còn cần đoạn này không?
function Component({items, sortBy}) {
  const sorted = useMemo(() => {
    return [...items].sort((a, b) => {
      return a[sortBy] - b[sortBy];
    });
  }, [items, sortBy]);

  return <List items={sorted} />;
}
```

Bạn có thể xóa nó một cách an toàn nếu đang dùng React Compiler:

```js
// ✅ Tốt hơn: để compiler tự tối ưu
function Component({items, sortBy}) {
  const sorted = [...items].sort((a, b) => {
    return a[sortBy] - b[sortBy];
  });

  return <List items={sorted} />;
}
```
