---
title: "Các Hook React tích hợp sẵn"
---

<Intro>

*Hook* cho phép bạn dùng các tính năng khác nhau của React từ bên trong thành phần. Bạn có thể dùng các Hook tích hợp sẵn hoặc kết hợp chúng để xây dựng Hook riêng. Trang này liệt kê toàn bộ Hook tích hợp sẵn trong React.

</Intro>

---

## Hook state {/*state-hooks*/}

*State* giúp thành phần ["ghi nhớ" thông tin như dữ liệu nhập của người dùng.](/learn/state-a-components-memory) Ví dụ, một thành phần biểu mẫu có thể dùng state để lưu giá trị đầu vào, trong khi một thành phần thư viện ảnh có thể dùng state để lưu chỉ số của ảnh đang được chọn.

Để thêm state vào thành phần, hãy dùng một trong các Hook sau:

* [`useState`](/reference/react/useState) khai báo một biến state mà bạn có thể cập nhật trực tiếp.
* [`useReducer`](/reference/react/useReducer) khai báo một biến state với logic cập nhật nằm trong một [hàm reducer.](/learn/extracting-state-logic-into-a-reducer)

```js
function ImageGallery() {
  const [index, setIndex] = useState(0);
  // ...
```

---

## Hook context {/*context-hooks*/}

*Context* cho phép một thành phần [nhận thông tin từ các thành phần cha ở xa mà không cần truyền nó dưới dạng props.](/learn/passing-props-to-a-component) Ví dụ, thành phần cấp cao nhất của ứng dụng có thể truyền theme UI hiện tại cho mọi thành phần bên dưới, bất kể chúng nằm sâu đến đâu.

* [`useContext`](/reference/react/useContext) đọc và đăng ký theo dõi một context.

```js
function Button() {
  const theme = useContext(ThemeContext);
  // ...
```

---

## Hook ref {/*ref-hooks*/}

*Ref* cho phép thành phần [lưu giữ một số thông tin không dùng để kết xuất,](/learn/referencing-values-with-refs) chẳng hạn như một nút DOM hoặc ID timeout. Khác với state, cập nhật ref sẽ không kết xuất lại thành phần. Ref là một "lối thoát" khỏi mô hình React. Chúng hữu ích khi bạn cần làm việc với các hệ thống không phải React, ví dụ như các API tích hợp sẵn của trình duyệt.

* [`useRef`](/reference/react/useRef) khai báo một ref. Bạn có thể giữ bất kỳ giá trị nào trong đó, nhưng thường nhất là để giữ một nút DOM.
* [`useImperativeHandle`](/reference/react/useImperativeHandle) cho phép bạn tùy chỉnh ref mà thành phần của bạn phơi ra. Hook này hiếm khi được dùng.

```js
function Form() {
  const inputRef = useRef(null);
  // ...
```

---

## Hook Effect {/*effect-hooks*/}

*Effect* cho phép thành phần [kết nối và đồng bộ với các hệ thống bên ngoài.](/learn/synchronizing-with-effects) Điều này bao gồm mạng, DOM của trình duyệt, animation, widget được viết bằng thư viện UI khác và các đoạn code không phải React.

* [`useEffect`](/reference/react/useEffect) kết nối một thành phần với hệ thống bên ngoài.

```js
function ChatRoom({ roomId }) {
  useEffect(() => {
    const connection = createConnection(roomId);
    connection.connect();
    return () => connection.disconnect();
  }, [roomId]);
  // ...
```

Effect là một "lối thoát" khỏi mô hình React. Đừng dùng Effect để điều phối luồng dữ liệu của ứng dụng. Nếu bạn không tương tác với một hệ thống bên ngoài, [bạn có thể không cần Effect.](/learn/you-might-not-need-an-effect)

`useEffect` có hai biến thể hiếm dùng với sự khác biệt về thời điểm chạy:

* [`useLayoutEffect`](/reference/react/useLayoutEffect) chạy trước khi trình duyệt vẽ lại màn hình. Bạn có thể đo layout ở đây.
* [`useInsertionEffect`](/reference/react/useInsertionEffect) chạy trước khi React thay đổi DOM. Thư viện có thể chèn CSS động ở đây.

Bạn cũng có thể tách sự kiện khỏi Effect:

- [`useEffectEvent`](/reference/react/useEffectEvent) tạo ra một sự kiện không phản ứng để gọi từ bất kỳ Effect hook nào.
---

## Hook hiệu năng {/*performance-hooks*/}

Một cách phổ biến để tối ưu hiệu năng kết xuất lại là bỏ qua công việc không cần thiết. Ví dụ, bạn có thể yêu cầu React tái sử dụng một phép tính đã được lưu nhớ đệm hoặc bỏ qua việc kết xuất lại nếu dữ liệu không thay đổi kể từ lần kết xuất trước.

Để bỏ qua phép tính và các lần kết xuất lại không cần thiết, hãy dùng một trong các Hook sau:

- [`useMemo`](/reference/react/useMemo) cho phép bạn lưu nhớ đệm kết quả của một phép tính tốn kém.
- [`useCallback`](/reference/react/useCallback) cho phép bạn lưu nhớ đệm định nghĩa hàm trước khi truyền nó xuống một thành phần đã được tối ưu.

```js
function TodoList({ todos, tab, theme }) {
  const visibleTodos = useMemo(() => filterTodos(todos, tab), [todos, tab]);
  // ...
}
```

Đôi khi bạn không thể bỏ qua việc kết xuất lại vì màn hình thực sự cần cập nhật. Khi đó, bạn có thể cải thiện hiệu năng bằng cách tách các cập nhật chặn buộc phải đồng bộ, như gõ vào ô nhập liệu, khỏi các cập nhật không chặn vốn không cần chặn giao diện người dùng, như cập nhật biểu đồ.

Để ưu tiên kết xuất, hãy dùng một trong các Hook sau:

- [`useTransition`](/reference/react/useTransition) cho phép bạn đánh dấu một chuyển tiếp state là không chặn và cho phép các cập nhật khác ngắt nó.
- [`useDeferredValue`](/reference/react/useDeferredValue) cho phép bạn trì hoãn cập nhật một phần không quan trọng của UI và để các phần khác cập nhật trước.

---

## Các Hook khác {/*other-hooks*/}

Các Hook này chủ yếu hữu ích với tác giả thư viện và không thường được dùng trong code ứng dụng.

- [`useDebugValue`](/reference/react/useDebugValue) cho phép bạn tùy chỉnh nhãn mà React DevTools hiển thị cho Hook tùy biến của bạn.
- [`useId`](/reference/react/useId) cho phép một thành phần liên kết với chính nó một ID duy nhất. Thường dùng với các API trợ năng.
- [`useSyncExternalStore`](/reference/react/useSyncExternalStore) cho phép một thành phần đăng ký theo dõi một store bên ngoài.
* [`useActionState`](/reference/react/useActionState) cho phép bạn quản lý state của các action.

---

## Hook của riêng bạn {/*your-own-hooks*/}

Bạn cũng có thể [định nghĩa Hook tùy biến của riêng mình](/learn/reusing-logic-with-custom-hooks#extracting-your-own-custom-hook-from-a-component) dưới dạng các hàm JavaScript.
