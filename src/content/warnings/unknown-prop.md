---
title: Cảnh báo prop không xác định
---

Cảnh báo unknown-prop sẽ xuất hiện nếu bạn cố kết xuất một phần tử DOM với một prop mà React không nhận ra là thuộc tính/property DOM hợp lệ. Bạn nên bảo đảm rằng các phần tử DOM của mình không mang theo những prop thừa không cần thiết.

Có một vài nguyên nhân phổ biến khiến cảnh báo này xuất hiện:

1. Bạn có đang dùng `{...props}` hoặc `cloneElement(element, props)` không? Khi sao chép props sang component con, bạn nên bảo đảm rằng mình không vô tình chuyển tiếp những props vốn chỉ dành cho component cha. Hãy xem các cách khắc phục phổ biến cho vấn đề này ở bên dưới.

2. Bạn đang dùng một thuộc tính DOM không chuẩn trên một nút DOM gốc, có thể để biểu diễn dữ liệu tùy chỉnh. Nếu bạn đang cố đính kèm dữ liệu tùy chỉnh vào một phần tử DOM chuẩn, hãy cân nhắc dùng thuộc tính dữ liệu tùy chỉnh như mô tả [trên MDN](https://developer.mozilla.org/en-US/docs/Web/Guide/HTML/Using_data_attributes).

3. React chưa nhận ra thuộc tính mà bạn chỉ định. Điều này có thể sẽ được sửa trong một phiên bản React tương lai. React sẽ cho phép bạn truyền thuộc tính đó mà không cảnh báo nếu bạn viết tên thuộc tính ở dạng chữ thường.

4. Bạn đang dùng một component React mà không viết hoa, ví dụ `<myButton />`. React sẽ hiểu nó là thẻ DOM vì phép biến đổi JSX của React dùng quy ước chữ hoa và chữ thường để phân biệt component do người dùng định nghĩa với thẻ DOM. Với component React của riêng bạn, hãy dùng PascalCase. Ví dụ, hãy viết `<MyButton />` thay vì `<myButton />`.

---

Nếu bạn gặp cảnh báo này vì truyền props kiểu `{...props}`, component cha của bạn cần "tiêu thụ" mọi prop được dành cho component cha chứ không phải component con. Ví dụ:

**Không tốt:** Prop `layout` ngoài dự kiến được chuyển tiếp xuống thẻ `div`.

```js
function MyDiv(props) {
  if (props.layout === 'horizontal') {
    // KHÔNG TỐT! Vì bạn biết chắc "layout" không phải là prop mà <div> hiểu.
    return <div {...props} style={getHorizontalStyle()} />
  } else {
    // KHÔNG TỐT! Vì bạn biết chắc "layout" không phải là prop mà <div> hiểu.
    return <div {...props} style={getVerticalStyle()} />
  }
}
```

**Tốt:** Có thể dùng cú pháp spread để tách các biến ra khỏi props và đưa phần props còn lại vào một biến.

```js
function MyDiv(props) {
  const { layout, ...rest } = props
  if (layout === 'horizontal') {
    return <div {...rest} style={getHorizontalStyle()} />
  } else {
    return <div {...rest} style={getVerticalStyle()} />
  }
}
```

**Tốt:** Bạn cũng có thể gán props vào một object mới rồi xóa các khóa mà bạn đang dùng khỏi object mới đó. Hãy chắc chắn không xóa props khỏi object `this.props` gốc, vì object đó nên được xem là bất biến.

```js
function MyDiv(props) {
  const divProps = Object.assign({}, props);
  delete divProps.layout;

  if (props.layout === 'horizontal') {
    return <div {...divProps} style={getHorizontalStyle()} />
  } else {
    return <div {...divProps} style={getVerticalStyle()} />
  }
}
```
