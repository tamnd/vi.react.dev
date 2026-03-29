---
title: renderToStaticMarkup
---

<Intro>

`renderToStaticMarkup` kết xuất một cây React không tương tác thành một chuỗi HTML.

```js
const html = renderToStaticMarkup(reactNode, options?)
```

</Intro>

<InlineToc />

---

## Reference {/*reference*/}

### `renderToStaticMarkup(reactNode, options?)` {/*rendertostaticmarkup*/}

Trên server, hãy gọi `renderToStaticMarkup` để kết xuất ứng dụng của bạn thành HTML.

```js
import { renderToStaticMarkup } from 'react-dom/server';

const html = renderToStaticMarkup(<Page />);
```

Nó sẽ tạo ra đầu ra HTML không tương tác cho các component React của bạn.

[Xem thêm ví dụ ở bên dưới.](#usage)

#### Parameters {/*parameters*/}

* `reactNode`: Một nút React mà bạn muốn kết xuất thành HTML. Ví dụ, một nút JSX như `<Page />`.
* **tùy chọn** `options`: Một object cho việc render phía server.
  * **tùy chọn** `identifierPrefix`: Tiền tố chuỗi mà React dùng cho các ID được tạo bởi [`useId`.](/reference/react/useId) Hữu ích để tránh xung đột khi dùng nhiều root trên cùng một trang.

#### Returns {/*returns*/}

Một chuỗi HTML.

#### Caveats {/*caveats*/}

* Đầu ra của `renderToStaticMarkup` không thể được hydrate.

* `renderToStaticMarkup` có hỗ trợ Suspense hạn chế. Nếu một component bị tạm ngưng, `renderToStaticMarkup` sẽ ngay lập tức gửi fallback của nó dưới dạng HTML.

* `renderToStaticMarkup` hoạt động trong trình duyệt, nhưng không được khuyến nghị dùng trong code phía client. Nếu bạn cần kết xuất một component thành HTML trong trình duyệt, hãy [lấy HTML bằng cách kết xuất nó vào một nút DOM.](/reference/react-dom/server/renderToString#removing-rendertostring-from-the-client-code)

---

## Usage {/*usage*/}

### Kết xuất một cây React không tương tác thành HTML dưới dạng chuỗi {/*rendering-a-non-interactive-react-tree-as-html-to-a-string*/}

Hãy gọi `renderToStaticMarkup` để kết xuất ứng dụng của bạn thành một chuỗi HTML mà bạn có thể gửi đi trong phản hồi từ server:

```js {5-6}
import { renderToStaticMarkup } from 'react-dom/server';

// Cú pháp route handler phụ thuộc vào framework backend của bạn
app.use('/', (request, response) => {
  const html = renderToStaticMarkup(<Page />);
  response.send(html);
});
```

Điều này sẽ tạo ra đầu ra HTML ban đầu không tương tác cho các component React của bạn.

<Pitfall>

Phương thức này kết xuất **HTML không tương tác và không thể hydrate.** Điều này hữu ích nếu bạn muốn dùng React như một công cụ tạo trang tĩnh đơn giản, hoặc nếu bạn đang kết xuất nội dung hoàn toàn tĩnh như email.

Ứng dụng tương tác nên dùng [`renderToString`](/reference/react-dom/server/renderToString) ở phía server và [`hydrateRoot`](/reference/react-dom/client/hydrateRoot) ở phía client.

</Pitfall>
