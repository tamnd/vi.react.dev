---
title: "<option>"
---

<Intro>

[Component `<option>` dựng sẵn của trình duyệt](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/option) cho phép bạn kết xuất một lựa chọn bên trong hộp [`<select>`](/reference/react-dom/components/select).

```js
<select>
  <option value="someOption">Some option</option>
  <option value="otherOption">Other option</option>
</select>
```

</Intro>

<InlineToc />

---

## Reference {/*reference*/}

### `<option>` {/*option*/}

[Component `<option>` dựng sẵn của trình duyệt](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/option) cho phép bạn kết xuất một lựa chọn bên trong hộp [`<select>`](/reference/react-dom/components/select).

```js
<select>
  <option value="someOption">Some option</option>
  <option value="otherOption">Other option</option>
</select>
```

[Xem thêm ví dụ ở bên dưới.](#usage)

#### Props {/*props*/}

`<option>` hỗ trợ toàn bộ [prop phần tử thông dụng.](/reference/react-dom/components/common#common-props)

Ngoài ra, `<option>` còn hỗ trợ các prop sau:

* [`disabled`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/option#disabled): Một giá trị boolean. Nếu là `true`, lựa chọn này sẽ không thể được chọn và sẽ hiện mờ đi.
* [`label`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/option#label): Một chuỗi. Chỉ định ý nghĩa của lựa chọn. Nếu không được chỉ định, văn bản bên trong lựa chọn sẽ được dùng.
* [`value`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/option#value): Giá trị sẽ được dùng [khi gửi `<select>` cha trong một form](/reference/react-dom/components/select#reading-the-select-box-value-when-submitting-a-form) nếu lựa chọn này được chọn.

#### Caveats {/*caveats*/}

* React không hỗ trợ thuộc tính `selected` trên `<option>`. Thay vào đó, hãy truyền `value` của lựa chọn này tới [`<select defaultValue>`](/reference/react-dom/components/select#providing-an-initially-selected-option) ở component cha cho hộp chọn không kiểm soát, hoặc [`<select value>`](/reference/react-dom/components/select#controlling-a-select-box-with-a-state-variable) cho hộp chọn có kiểm soát.

---

## Usage {/*usage*/}

### Hiển thị hộp chọn với các lựa chọn {/*displaying-a-select-box-with-options*/}

Hãy kết xuất một `<select>` với danh sách các component `<option>` bên trong để hiển thị hộp chọn. Gán cho mỗi `<option>` một `value` đại diện cho dữ liệu sẽ được gửi cùng form.

[Đọc thêm về cách hiển thị một `<select>` với danh sách các component `<option>`.](/reference/react-dom/components/select)

<Sandpack>

```js
export default function FruitPicker() {
  return (
    <label>
      Pick a fruit:
      <select name="selectedFruit">
        <option value="apple">Apple</option>
        <option value="banana">Banana</option>
        <option value="orange">Orange</option>
      </select>
    </label>
  );
}
```

```css
select { margin: 5px; }
```

</Sandpack>  
