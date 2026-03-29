---
title: "Hook React DOM dựng sẵn"
---

<Intro>

Package `react-dom` chứa các Hook chỉ được hỗ trợ cho ứng dụng web, tức là chạy trong môi trường DOM của trình duyệt. Những Hook này không được hỗ trợ trong các môi trường không phải trình duyệt như ứng dụng iOS, Android hoặc Windows. Nếu bạn đang tìm các Hook được hỗ trợ trong trình duyệt web *và các môi trường khác*, hãy xem [trang React Hooks](/reference/react/hooks). Trang này liệt kê tất cả Hook trong package `react-dom`.

</Intro>

---

## Hook cho form {/*form-hooks*/}

*Form* cho phép bạn tạo các điều khiển tương tác để gửi thông tin. Để quản lý form trong component, hãy dùng một trong các Hook sau:

* [`useFormStatus`](/reference/react-dom/hooks/useFormStatus) cho phép bạn cập nhật UI dựa trên trạng thái của một form.

```js
function Form({ action }) {
  async function increment(n) {
    return n + 1;
  }
  const [count, incrementFormAction] = useActionState(increment, 0);
  return (
    <form action={action}>
      <button formAction={incrementFormAction}>Count: {count}</button>
      <Button />
    </form>
  );
}

function Button() {
  const { pending } = useFormStatus();
  return (
    <button disabled={pending} type="submit">
      Submit
    </button>
  );
}
```
