---
title: error-boundaries
---

<Intro>

Kiểm tra việc dùng Error Boundaries thay vì try/catch cho lỗi xảy ra trong component con.

</Intro>

## Chi tiết quy tắc {/*rule-details*/}

Khối try/catch không thể bắt lỗi xảy ra trong quá trình React render. Những lỗi được ném ra trong phương thức render hoặc Hook sẽ nổi lên qua cây component. Chỉ [Error Boundaries](/reference/react/Component#catching-rendering-errors-with-an-error-boundary) mới có thể bắt được các lỗi này.

### Invalid {/*invalid*/}

Ví dụ về code không đúng với quy tắc này:

```js {expectedErrors: {'react-compiler': [4]}}
// ❌ Try/catch sẽ không bắt được lỗi render
function Parent() {
  try {
    return <ChildComponent />; // Nếu chỗ này ném lỗi, catch cũng không giúp được
  } catch (error) {
    return <div>Đã xảy ra lỗi</div>;
  }
}
```

### Valid {/*valid*/}

Ví dụ về code đúng với quy tắc này:

```js
// ✅ Dùng error boundary
function Parent() {
  return (
    <ErrorBoundary>
      <ChildComponent />
    </ErrorBoundary>
  );
}
```

## Khắc phục sự cố {/*troubleshooting*/}

### Tại sao linter bảo tôi không nên bọc `use` trong `try`/`catch`? {/*why-is-the-linter-telling-me-not-to-wrap-use-in-trycatch*/}

Hook `use` không ném lỗi theo nghĩa truyền thống, mà nó tạm ngưng việc thực thi component. Khi `use` gặp một promise đang chờ, nó sẽ tạm ngưng component và để React hiển thị fallback. Chỉ Suspense và Error Boundaries mới có thể xử lý các trường hợp này. Linter cảnh báo việc bọc `use` trong `try`/`catch` để tránh gây nhầm lẫn vì khối `catch` sẽ không bao giờ chạy.

```js {expectedErrors: {'react-compiler': [5]}}
// ❌ Try/catch quanh hook `use`
function Component({promise}) {
  try {
    const data = use(promise); // Sẽ không bắt được - `use` tạm ngưng chứ không ném lỗi
    return <div>{data}</div>;
  } catch (error) {
    return <div>Tải thất bại</div>; // Không thể chạy tới đây
  }
}

// ✅ Error boundary bắt lỗi từ `use`
function App() {
  return (
    <ErrorBoundary fallback={<div>Tải thất bại</div>}>
      <Suspense fallback={<div>Đang tải...</div>}>
        <DataComponent promise={fetchData()} />
      </Suspense>
    </ErrorBoundary>
  );
}
```
