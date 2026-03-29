---
title: "Các API tích hợp sẵn của React"
---

<Intro>

Ngoài [Hooks](/reference/react/hooks) và [Components](/reference/react/components), gói `react` còn export một số API khác hữu ích cho việc định nghĩa component. Trang này liệt kê toàn bộ các API React hiện đại còn lại.

</Intro>

---

* [`createContext`](/reference/react/createContext) cho phép bạn định nghĩa và cung cấp context cho các component con. Dùng cùng với [`useContext`.](/reference/react/useContext)
* [`lazy`](/reference/react/lazy) cho phép bạn trì hoãn việc tải mã của component cho đến lần đầu nó được render.
* [`memo`](/reference/react/memo) cho phép component của bạn bỏ qua việc re-render khi prop không đổi. Dùng cùng với [`useMemo`](/reference/react/useMemo) và [`useCallback`.](/reference/react/useCallback)
* [`startTransition`](/reference/react/startTransition) cho phép bạn đánh dấu một cập nhật state là không khẩn cấp. Tương tự [`useTransition`.](/reference/react/useTransition)
* [`act`](/reference/react/act) cho phép bạn bọc các lần render và tương tác trong bài kiểm thử để đảm bảo các cập nhật đã được xử lý trước khi đưa ra assertion.

---

## API tài nguyên {/*resource-apis*/}

*Tài nguyên* có thể được một component truy cập mà không cần là một phần trong state của nó. Ví dụ, component có thể đọc một thông điệp từ Promise hoặc đọc thông tin style từ context.

Để đọc một giá trị từ tài nguyên, hãy dùng API này:

* [`use`](/reference/react/use) cho phép bạn đọc giá trị của một tài nguyên như [Promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise) hoặc [context](/learn/passing-data-deeply-with-context).
```js
function MessageComponent({ messagePromise }) {
  const message = use(messagePromise);
  const theme = use(ThemeContext);
  // ...
}
```
