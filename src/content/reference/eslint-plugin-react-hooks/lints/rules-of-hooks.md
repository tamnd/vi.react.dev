---
title: rules-of-hooks
---

<Intro>

Kiểm tra để bảo đảm component và Hook tuân theo [Các quy tắc của Hook](/reference/rules/rules-of-hooks).

</Intro>

## Chi tiết luật {/*rule-details*/}

React dựa vào thứ tự các Hook được gọi để giữ state chính xác giữa các lần kết xuất. Mỗi lần component của bạn kết xuất, React kỳ vọng đúng cùng các Hook được gọi theo đúng cùng thứ tự. Khi Hook được gọi có điều kiện hoặc trong vòng lặp, React mất dấu state nào ứng với lời gọi Hook nào, dẫn đến lỗi như lệch state và thông báo "Rendered fewer/more hooks than expected".

## Các vi phạm thường gặp {/*common-violations*/}

Những mẫu sau vi phạm Các quy tắc của Hook:

- **Hook trong điều kiện** (`if`/`else`, toán tử ba ngôi, `&&`/`||`)
- **Hook trong vòng lặp** (`for`, `while`, `do-while`)
- **Hook sau lệnh return sớm**
- **Hook trong callback hoặc event handler**
- **Hook trong hàm async**
- **Hook trong phương thức của class**
- **Hook ở cấp module**

<Note>

### Hook `use` {/*use-hook*/}

Hook `use` khác với các Hook React khác. Bạn có thể gọi nó có điều kiện và trong vòng lặp:

```js
// ✅ `use` can be conditional
if (shouldFetch) {
  const data = use(fetchPromise);
}

// ✅ `use` can be in loops
for (const promise of promises) {
  results.push(use(promise));
}
```

Tuy nhiên, `use` vẫn có những hạn chế:
- Không thể được bọc trong try/catch
- Phải được gọi bên trong component hoặc Hook

Tìm hiểu thêm: [API Reference của `use`](/reference/react/use)

</Note>

### Không hợp lệ {/*invalid*/}

Ví dụ về mã không đúng cho luật này:

```js
// ❌ Hook in condition
if (isLoggedIn) {
  const [user, setUser] = useState(null);
}

// ❌ Hook after early return
if (!data) return <Loading />;
const [processed, setProcessed] = useState(data);

// ❌ Hook in callback
<button onClick={() => {
  const [clicked, setClicked] = useState(false);
}}/>

// ❌ `use` in try/catch
try {
  const data = use(promise);
} catch (e) {
  // error handling
}

// ❌ Hook at module level
const globalState = useState(0); // Outside component
```

### Hợp lệ {/*valid*/}

Ví dụ về mã đúng cho luật này:

```js
function Component({ isSpecial, shouldFetch, fetchPromise }) {
  // ✅ Hooks at top level
  const [count, setCount] = useState(0);
  const [name, setName] = useState('');

  if (!isSpecial) {
    return null;
  }

  if (shouldFetch) {
    // ✅ `use` can be conditional
    const data = use(fetchPromise);
    return <div>{data}</div>;
  }

  return <div>{name}: {count}</div>;
}
```

## Khắc phục sự cố {/*troubleshooting*/}

### Tôi muốn lấy dữ liệu dựa trên một điều kiện nào đó {/*conditional-data-fetching*/}

Bạn đang cố gọi `useEffect` có điều kiện:

```js
// ❌ Conditional hook
if (isLoggedIn) {
  useEffect(() => {
    fetchUserData();
  }, []);
}
```

Hãy gọi Hook vô điều kiện và kiểm tra điều kiện ở bên trong:

```js
// ✅ Condition inside hook
useEffect(() => {
  if (isLoggedIn) {
    fetchUserData();
  }
}, [isLoggedIn]);
```

<Note>

Có những cách tốt hơn `useEffect` để lấy dữ liệu. Hãy cân nhắc TanStack Query, useSWR hoặc React Router 6.4+ cho data fetching. Những giải pháp này xử lý việc khử trùng lặp request, cache phản hồi và tránh network waterfall.

Tìm hiểu thêm: [Lấy dữ liệu](/learn/synchronizing-with-effects#fetching-data)

</Note>

### Tôi cần state khác nhau cho các tình huống khác nhau {/*conditional-state-initialization*/}

Bạn đang cố khởi tạo state có điều kiện:

```js
// ❌ Conditional state
if (userType === 'admin') {
  const [permissions, setPermissions] = useState(adminPerms);
} else {
  const [permissions, setPermissions] = useState(userPerms);
}
```

Hãy luôn gọi `useState`, rồi đặt giá trị khởi tạo có điều kiện:

```js
// ✅ Conditional initial value
const [permissions, setPermissions] = useState(
  userType === 'admin' ? adminPerms : userPerms
);
```

## Tùy chọn {/*options*/}

Bạn có thể cấu hình các custom effect hook bằng cài đặt ESLint dùng chung, khả dụng từ `eslint-plugin-react-hooks` 6.1.1 trở lên:

```js
{
  "settings": {
    "react-hooks": {
      "additionalEffectHooks": "(useMyEffect|useCustomEffect)"
    }
  }
}
```

- `additionalEffectHooks`: Mẫu regex khớp các custom Hook nên được coi là effect. Cấu hình này cho phép `useEffectEvent` và các hàm sự kiện tương tự được gọi từ custom effect hook của bạn.

Cấu hình dùng chung này được dùng bởi cả luật `rules-of-hooks` và `exhaustive-deps`, giúp bảo đảm hành vi nhất quán trên mọi luật lint liên quan đến Hook.
