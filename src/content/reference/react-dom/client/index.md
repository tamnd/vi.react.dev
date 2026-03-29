---
title: API React DOM phía client
---

<Intro>

Các API `react-dom/client` cho phép bạn render component React ở phía client, tức trong trình duyệt. Những API này thường được dùng ở tầng cao nhất của ứng dụng để khởi tạo cây React. Một [framework](/learn/creating-a-react-app#full-stack-frameworks) có thể gọi chúng thay cho bạn. Phần lớn component của bạn không cần import hay dùng trực tiếp các API này.

</Intro>

---

## API phía client {/*client-apis*/}

* [`createRoot`](/reference/react-dom/client/createRoot) cho phép bạn tạo một root để hiển thị component React bên trong một nút DOM của trình duyệt.
* [`hydrateRoot`](/reference/react-dom/client/hydrateRoot) cho phép bạn hiển thị component React bên trong một nút DOM của trình duyệt mà nội dung HTML của nó trước đó đã được tạo bởi [`react-dom/server`.](/reference/react-dom/server)

---

## Hỗ trợ trình duyệt {/*browser-support*/}

React hỗ trợ tất cả các trình duyệt phổ biến, bao gồm Internet Explorer 9 trở lên. Một số polyfill là cần thiết cho các trình duyệt cũ như IE 9 và IE 10.
