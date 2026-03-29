---
title: React gọi Component và Hook
---

<Intro>
React chịu trách nhiệm kết xuất component và Hook khi cần để tối ưu trải nghiệm người dùng. Nó mang tính khai báo: bạn nói cho React biết cần kết xuất gì trong logic component, và React sẽ tự tìm cách hiển thị tốt nhất cho người dùng.
</Intro>

<InlineToc />

---

## Không bao giờ gọi trực tiếp hàm component {/*never-call-component-functions-directly*/}

Component chỉ nên được dùng trong JSX. Đừng gọi chúng như các hàm thông thường. React phải là bên gọi chúng.

React phải quyết định khi nào hàm component của bạn được gọi [trong quá trình kết xuất](/reference/rules/components-and-hooks-must-be-pure#how-does-react-run-your-code). Trong React, bạn làm điều đó bằng JSX.

```js {2}
function BlogPost() {
  return <Layout><Article /></Layout>; // ✅ Good: Only use components in JSX
}
```

```js {expectedErrors: {'react-compiler': [2]}} {2}
function BlogPost() {
  return <Layout>{Article()}</Layout>; // 🔴 Bad: Never call them directly
}
```

Nếu component chứa Hook, rất dễ vi phạm [Các quy tắc của Hook](/reference/rules/rules-of-hooks) khi component bị gọi trực tiếp trong vòng lặp hoặc điều kiện.

Để React điều phối kết xuất còn mang lại nhiều lợi ích:

* **Component trở thành nhiều hơn một hàm.** React có thể tăng cường chúng bằng các tính năng như *state cục bộ* thông qua Hook gắn với danh tính của component trong cây.
* **Kiểu component tham gia vào quá trình đối soát.** Bằng cách để React gọi component, bạn cũng cho nó biết thêm về cấu trúc khái niệm của cây. Ví dụ, khi chuyển từ kết xuất `<Feed>` sang trang `<Profile>`, React sẽ không cố tái sử dụng chúng.
* **React có thể cải thiện trải nghiệm người dùng.** Ví dụ, nó có thể cho trình duyệt làm một phần công việc giữa các lần gọi component để việc kết xuất lại cây component lớn không chặn luồng chính.
* **Trải nghiệm gỡ lỗi tốt hơn.** Nếu component là công dân hạng nhất mà thư viện biết đến, chúng tôi có thể xây dựng những công cụ phát triển giàu thông tin để quan sát trong lúc phát triển.
* **Đối soát hiệu quả hơn.** React có thể quyết định chính xác component nào trong cây cần kết xuất lại và bỏ qua những component không cần. Điều đó làm ứng dụng nhanh và mượt hơn.

---

## Không bao giờ truyền Hook như các giá trị thông thường {/*never-pass-around-hooks-as-regular-values*/}

Hook chỉ nên được gọi bên trong component hoặc Hook. Đừng bao giờ truyền nó như một giá trị thông thường.

Hook cho phép bạn tăng cường component bằng các tính năng của React. Chúng luôn phải được gọi như hàm, và không bao giờ được truyền như giá trị thông thường. Điều này cho phép *suy luận cục bộ*, tức khả năng để lập trình viên hiểu mọi thứ một component có thể làm chỉ bằng cách nhìn component đó một cách cô lập.

Phá vỡ quy tắc này sẽ khiến React không thể tự động tối ưu component của bạn.

### Đừng biến đổi Hook một cách động {/*dont-dynamically-mutate-a-hook*/}

Hook nên "tĩnh" nhất có thể. Điều này nghĩa là bạn không nên biến đổi chúng một cách động. Ví dụ, đừng viết các Hook bậc cao:

```js {expectedErrors: {'react-compiler': [2, 3]}} {2}
function ChatInput() {
  const useDataWithLogging = withLogging(useData); // 🔴 Bad: don't write higher order Hooks
  const data = useDataWithLogging();
}
```

Hook nên là bất biến và không bị thay đổi. Thay vì biến đổi Hook động, hãy tạo một phiên bản Hook tĩnh với chức năng mong muốn.

```js {2,6}
function ChatInput() {
  const data = useDataWithLogging(); // ✅ Good: Create a new version of the Hook
}

function useDataWithLogging() {
  // ... Create a new version of the Hook and inline the logic here
}
```

### Đừng dùng Hook một cách động {/*dont-dynamically-use-hooks*/}

Hook cũng không nên bị dùng một cách động. Ví dụ, thay vì làm dependency injection trong component bằng cách truyền Hook làm giá trị:

```js {expectedErrors: {'react-compiler': [2]}} {2}
function ChatInput() {
  return <Button useData={useDataWithLogging} /> // 🔴 Bad: don't pass Hooks as props
}
```

Bạn nên luôn inline lời gọi Hook vào bên trong component đó và xử lý mọi logic ở đó.

```js {6}
function ChatInput() {
  return <Button />
}

function Button() {
  const data = useDataWithLogging(); // ✅ Good: Use the Hook directly
}

function useDataWithLogging() {
  // If there's any conditional logic to change the Hook's behavior, it should be inlined into
  // the Hook
}
```

Theo cách này, `<Button />` dễ hiểu và dễ gỡ lỗi hơn nhiều. Khi Hook được dùng theo cách động, độ phức tạp của ứng dụng tăng lên đáng kể và làm suy yếu suy luận cục bộ, khiến nhóm của bạn kém hiệu quả hơn về lâu dài. Nó cũng làm tăng nguy cơ vô tình phá vỡ [Các quy tắc của Hook](/reference/rules/rules-of-hooks), vốn yêu cầu Hook không được gọi có điều kiện. Nếu bạn thấy mình cần mock component cho test, thường tốt hơn là mock server để trả về dữ liệu dựng sẵn. Nếu có thể, kiểm thử đầu cuối cũng thường hiệu quả hơn để kiểm tra ứng dụng.
