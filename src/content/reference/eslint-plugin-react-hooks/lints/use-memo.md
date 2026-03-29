---
title: use-memo
---

<Intro>

Kiểm tra để bảo đảm Hook `useMemo` được dùng cùng với một giá trị trả về. Xem [tài liệu `useMemo`](/reference/react/useMemo) để biết thêm chi tiết.

</Intro>

## Chi tiết luật {/*rule-details*/}

`useMemo` dùng để tính toán và lưu nhớ đệm các giá trị tốn kém, không phải để tạo side effect. Nếu không có giá trị trả về, `useMemo` sẽ trả về `undefined`, làm mất mục đích của nó và thường cho thấy bạn đang dùng nhầm Hook.

### Không hợp lệ {/*invalid*/}

Ví dụ về mã không đúng cho luật này:

```js {expectedErrors: {'react-compiler': [3]}}
// ❌ No return value
function Component({ data }) {
  const processed = useMemo(() => {
    data.forEach(item => console.log(item));
    // Missing return!
  }, [data]);

  return <div>{processed}</div>; // Always undefined
}
```

### Hợp lệ {/*valid*/}

Ví dụ về mã đúng cho luật này:

```js
// ✅ Returns computed value
function Component({ data }) {
  const processed = useMemo(() => {
    return data.map(item => item * 2);
  }, [data]);

  return <div>{processed}</div>;
}
```

## Khắc phục sự cố {/*troubleshooting*/}

### Tôi cần chạy side effect khi dependencies thay đổi {/*side-effects*/}

Bạn có thể sẽ thử dùng `useMemo` cho side effect:

{/* TODO(@poteto) fix compiler validation to check for unassigned useMemos */}
```js {expectedErrors: {'react-compiler': [4]}}
// ❌ Wrong: Side effects in useMemo
function Component({user}) {
  // No return value, just side effect
  useMemo(() => {
    analytics.track('UserViewed', {userId: user.id});
  }, [user.id]);

  // Not assigned to a variable
  useMemo(() => {
    return analytics.track('UserViewed', {userId: user.id});
  }, [user.id]);
}
```

Nếu side effect cần xảy ra khi người dùng tương tác, tốt nhất là đặt side effect cùng với sự kiện:

```js
// ✅ Good: Side effects in event handlers
function Component({user}) {
  const handleClick = () => {
    analytics.track('ButtonClicked', {userId: user.id});
    // Other click logic...
  };

  return <button onClick={handleClick}>Click me</button>;
}
```

Nếu side effect đồng bộ state React với một state bên ngoài nào đó, hãy dùng `useEffect`:

```js
// ✅ Good: Synchronization in useEffect
function Component({theme}) {
  useEffect(() => {
    localStorage.setItem('preferredTheme', theme);
    document.body.className = theme;
  }, [theme]);

  return <div>Current theme: {theme}</div>;
}
```
