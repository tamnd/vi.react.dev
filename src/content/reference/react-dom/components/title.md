---
title: "<title>"
---

<Intro>

[Component `<title>` dựng sẵn của trình duyệt](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/title) cho phép bạn chỉ định tiêu đề của tài liệu.

```js
<title>My Blog</title>
```

</Intro>

<InlineToc />

---

## Reference {/*reference*/}

### `<title>` {/*title*/}

Để chỉ định tiêu đề của tài liệu, hãy kết xuất [component `<title>` dựng sẵn của trình duyệt](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/title). Bạn có thể kết xuất `<title>` từ bất kỳ component nào và React sẽ luôn đặt phần tử DOM tương ứng vào phần head của tài liệu.

```js
<title>My Blog</title>
```

[Xem thêm ví dụ ở bên dưới.](#usage)

#### Props {/*props*/}

`<title>` hỗ trợ toàn bộ [prop phần tử thông dụng.](/reference/react-dom/components/common#common-props)

* `children`: `<title>` chỉ chấp nhận văn bản làm phần tử con. Văn bản này sẽ trở thành tiêu đề của tài liệu. Bạn cũng có thể truyền component riêng của mình miễn là chúng chỉ kết xuất văn bản.

#### Special rendering behavior {/*special-rendering-behavior*/}

React sẽ luôn đặt phần tử DOM tương ứng với component `<title>` vào trong phần `<head>` của tài liệu, bất kể nó được kết xuất ở đâu trong cây React. `<head>` là nơi hợp lệ duy nhất để `<title>` tồn tại trong DOM, nhưng sẽ rất tiện và giữ được tính kết hợp nếu component đại diện cho một trang cụ thể có thể tự kết xuất `<title>` của chính nó.

Có hai ngoại lệ cho điều này:
* Nếu `<title>` nằm trong một component `<svg>`, sẽ không có hành vi đặc biệt nào, vì trong ngữ cảnh đó nó không đại diện cho tiêu đề của tài liệu mà là [chú thích trợ năng cho đồ họa SVG đó](https://developer.mozilla.org/en-US/docs/Web/SVG/Element/title).
* Nếu `<title>` có prop [`itemProp`](https://developer.mozilla.org/en-US/docs/Web/HTML/Global_attributes/itemprop), sẽ không có hành vi đặc biệt nào, vì khi đó nó không đại diện cho tiêu đề tài liệu mà là metadata về một phần cụ thể của trang.

<Pitfall>

Chỉ nên kết xuất một `<title>` tại một thời điểm. Nếu nhiều component cùng kết xuất thẻ `<title>`, React sẽ đặt tất cả các tiêu đề đó vào phần head của tài liệu. Khi điều đó xảy ra, hành vi của trình duyệt và công cụ tìm kiếm là không xác định.

</Pitfall>

---

## Usage {/*usage*/}

### Đặt tiêu đề tài liệu {/*set-the-document-title*/}

Hãy kết xuất component `<title>` từ bất kỳ component nào với văn bản làm phần tử con. React sẽ đặt một nút DOM `<title>` vào phần `<head>` của tài liệu.

<SandpackWithHTMLOutput>

```js src/App.js active
import ShowRenderedHTML from './ShowRenderedHTML.js';

export default function ContactUsPage() {
  return (
    <ShowRenderedHTML>
      <title>My Site: Contact Us</title>
      <h1>Contact Us</h1>
      <p>Email us at support@example.com</p>
    </ShowRenderedHTML>
  );
}
```

</SandpackWithHTMLOutput>

### Dùng biến trong tiêu đề {/*use-variables-in-the-title*/}

Phần tử con của component `<title>` phải là một chuỗi văn bản duy nhất. Hoặc một số duy nhất, hoặc một object duy nhất có phương thức `toString`. Có thể không dễ nhận ra, nhưng dùng ngoặc nhọn JSX như sau:

```js
<title>Trang kết quả {pageNumber}</title> // 🔴 Vấn đề: Đây không phải một chuỗi duy nhất
```

... thực ra sẽ khiến component `<title>` nhận một mảng gồm hai phần tử làm children, chuỗi `"Trang kết quả"` và giá trị của `pageNumber`. Điều này sẽ gây lỗi. Thay vào đó, hãy dùng nội suy chuỗi để truyền cho `<title>` một chuỗi duy nhất:

```js
<title>{`Results page ${pageNumber}`}</title>
```
