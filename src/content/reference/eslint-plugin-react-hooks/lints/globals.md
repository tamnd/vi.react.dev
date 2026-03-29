---
title: globals
---

<Intro>

Kiểm tra việc gán/thay đổi giá trị toàn cục trong lúc render, như một phần của việc bảo đảm [tác dụng phụ phải chạy bên ngoài render](/reference/rules/components-and-hooks-must-be-pure#side-effects-must-run-outside-of-render).

</Intro>

## Chi tiết quy tắc {/*rule-details*/}

Biến toàn cục tồn tại ngoài sự kiểm soát của React. Khi bạn sửa đổi chúng trong lúc render, bạn phá vỡ giả định của React rằng quá trình render là thuần. Điều này có thể khiến component hoạt động khác nhau giữa môi trường phát triển và production, làm hỏng Fast Refresh, và khiến ứng dụng của bạn không thể được tối ưu bằng các tính năng như React Compiler.

### Invalid {/*invalid*/}

Ví dụ về code không đúng với quy tắc này:

```js
// ❌ Bộ đếm toàn cục
let renderCount = 0;
function Component() {
  renderCount++; // Thay đổi biến toàn cục
  return <div>Count: {renderCount}</div>;
}

// ❌ Sửa đổi thuộc tính trên window
function Component({userId}) {
  window.currentUser = userId; // Thay đổi giá trị toàn cục
  return <div>User: {userId}</div>;
}

// ❌ push vào mảng toàn cục
const events = [];
function Component({event}) {
  events.push(event); // Thay đổi mảng toàn cục
  return <div>Events: {events.length}</div>;
}

// ❌ Thao tác với cache
const cache = {};
function Component({id}) {
  if (!cache[id]) {
    cache[id] = fetchData(id); // Sửa đổi cache trong lúc render
  }
  return <div>{cache[id]}</div>;
}
```

### Valid {/*valid*/}

Ví dụ về code đúng với quy tắc này:

```js
// ✅ Dùng state cho bộ đếm
function Component() {
  const [clickCount, setClickCount] = useState(0);

  const handleClick = () => {
    setClickCount(c => c + 1);
  };

  return (
    <button onClick={handleClick}>
      Đã nhấp: {clickCount} lần
    </button>
  );
}

// ✅ Dùng context cho giá trị toàn cục
function Component() {
  const user = useContext(UserContext);
  return <div>User: {user.id}</div>;
}

// ✅ Đồng bộ trạng thái bên ngoài với React
function Component({title}) {
  useEffect(() => {
    document.title = title; // OK trong effect
  }, [title]);

  return <div>Trang: {title}</div>;
}
```
