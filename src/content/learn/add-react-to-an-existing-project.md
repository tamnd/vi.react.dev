---
title: Thêm React vào dự án hiện có
---

<Intro>

Nếu bạn muốn thêm một ít tính tương tác vào dự án hiện có, bạn không cần phải viết lại toàn bộ nó bằng React. Hãy thêm React vào stack hiện tại của bạn và kết xuất các thành phần React tương tác ở bất cứ đâu.

</Intro>

<Note>

**Bạn cần cài [Node.js](https://nodejs.org/en/) để phát triển cục bộ.** Dù bạn có thể [thử React](/learn/installation#try-react) trực tuyến hoặc với một trang HTML đơn giản, trên thực tế phần lớn công cụ JavaScript bạn muốn dùng để phát triển đều cần Node.js.

</Note>

## Dùng React cho toàn bộ một subroute của website hiện có {/*using-react-for-an-entire-subroute-of-your-existing-website*/}

Giả sử bạn có một ứng dụng web tại `example.com` được xây bằng công nghệ server khác, như Rails, và bạn muốn triển khai toàn bộ các route bắt đầu bằng `example.com/some-app/` hoàn toàn bằng React.

Đây là cách chúng tôi khuyên bạn nên thiết lập:

1. **Xây dựng phần React của ứng dụng** bằng một trong các [framework dựa trên React](/learn/creating-a-react-app).
2. **Chỉ định `/some-app` làm *base path*** trong cấu hình của framework (xem cách làm với [Next.js](https://nextjs.org/docs/app/api-reference/config/next-config-js/basePath), [Gatsby](https://www.gatsbyjs.com/docs/how-to/previews-deploys-hosting/path-prefix/)).
3. **Cấu hình server hoặc proxy** để mọi yêu cầu dưới `/some-app/` đều được ứng dụng React của bạn xử lý.

Điều này bảo đảm phần React trong ứng dụng của bạn có thể [hưởng lợi từ các thực hành tốt nhất](/learn/build-a-react-app-from-scratch#consider-using-a-framework) được tích hợp sẵn trong các framework đó.

Nhiều framework dựa trên React là full-stack và cho phép ứng dụng React của bạn tận dụng server. Tuy nhiên, bạn vẫn có thể dùng cách tiếp cận tương tự ngay cả khi không thể hoặc không muốn chạy JavaScript trên server. Trong trường hợp đó, hãy phục vụ bản export HTML/CSS/JS ([đầu ra của `next export`](https://nextjs.org/docs/advanced-features/static-html-export) với Next.js, mặc định của Gatsby) tại `/some-app/`.

## Dùng React cho một phần của trang hiện có {/*using-react-for-a-part-of-your-existing-page*/}

Giả sử bạn có một trang hiện có được xây bằng công nghệ khác, có thể ở phía server như Rails hoặc phía client như Backbone, và bạn muốn kết xuất các thành phần React tương tác ở đâu đó trên trang đó. Đây là một cách tích hợp React rất phổ biến. Thực tế, đó cũng là cách phần lớn việc dùng React ở Meta diễn ra trong nhiều năm.

Bạn có thể làm điều này qua hai bước:

1. **Thiết lập môi trường JavaScript** cho phép bạn dùng [cú pháp JSX](/learn/writing-markup-with-jsx), chia code thành module bằng cú pháp [`import`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/import) / [`export`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/export), và dùng các package, ví dụ React, từ registry [npm](https://www.npmjs.com/).
2. **Kết xuất các thành phần React của bạn** ở nơi bạn muốn chúng xuất hiện trên trang.

Cách làm chính xác phụ thuộc vào cách trang hiện tại của bạn được thiết lập, vì vậy hãy đi qua một vài chi tiết.

### Bước 1: Thiết lập môi trường JavaScript dạng module {/*step-1-set-up-a-modular-javascript-environment*/}

Môi trường JavaScript dạng module cho phép bạn viết các thành phần React trong từng tệp riêng thay vì nhét toàn bộ code vào một tệp duy nhất. Nó cũng cho phép bạn dùng toàn bộ những package tuyệt vời mà các nhà phát triển khác đã xuất bản lên registry [npm](https://www.npmjs.com/), bao gồm cả React! Cách thực hiện điều này phụ thuộc vào cấu hình hiện tại của bạn:

* **Nếu ứng dụng của bạn đã được tách thành các tệp dùng câu lệnh `import`,** hãy thử tận dụng thiết lập hiện có. Kiểm tra xem việc viết `<div />` trong code JS có gây lỗi cú pháp không. Nếu có, bạn có thể cần [biến đổi code JavaScript bằng Babel](https://babeljs.io/setup), và bật [Babel React preset](https://babeljs.io/docs/babel-preset-react) để dùng JSX.

* **Nếu ứng dụng của bạn chưa có thiết lập biên dịch module JavaScript,** hãy thiết lập bằng [Vite](https://vite.dev/). Cộng đồng Vite duy trì [nhiều tích hợp với framework backend](https://github.com/vitejs/awesome-vite#integrations-with-backends), bao gồm Rails, Django và Laravel. Nếu framework backend của bạn không có trong danh sách, hãy [làm theo hướng dẫn này](https://vite.dev/guide/backend-integration.html) để tích hợp thủ công build của Vite với backend của bạn.

Để kiểm tra xem thiết lập của bạn có hoạt động không, hãy chạy lệnh này trong thư mục dự án:

<TerminalBlock>
npm install react react-dom
</TerminalBlock>

Sau đó thêm những dòng code sau vào đầu tệp JavaScript chính của bạn, có thể tên là `index.js` hoặc `main.js`:

<Sandpack>

```html public/index.html hidden
<!DOCTYPE html>
<html>
  <head><title>My app</title></head>
  <body>
    <!-- Your existing page content (in this example, it gets replaced) -->
    <div id="root"></div>
  </body>
</html>
```

```js src/index.js active
import { createRoot } from 'react-dom/client';

// Clear the existing HTML content
document.body.innerHTML = '<div id="app"></div>';

// Render your React component instead
const root = createRoot(document.getElementById('app'));
root.render(<h1>Hello, world</h1>);
```

</Sandpack>

Nếu toàn bộ nội dung trên trang được thay bằng "Hello, world!", tức là mọi thứ đã hoạt động. Hãy đọc tiếp.

<Note>

Việc tích hợp môi trường JavaScript dạng module vào một dự án hiện có lần đầu có thể khiến bạn thấy ngợp, nhưng nó rất đáng. Nếu bị mắc kẹt, hãy thử dùng [tài nguyên cộng đồng](/community) hoặc [Vite Chat](https://chat.vite.dev/).

</Note>

### Bước 2: Kết xuất các thành phần React ở bất cứ đâu trên trang {/*step-2-render-react-components-anywhere-on-the-page*/}

Ở bước trước, bạn đã đặt đoạn code này ở đầu tệp chính:

```js
import { createRoot } from 'react-dom/client';

// Clear the existing HTML content
document.body.innerHTML = '<div id="app"></div>';

// Render your React component instead
const root = createRoot(document.getElementById('app'));
root.render(<h1>Hello, world</h1>);
```

Dĩ nhiên, trên thực tế bạn sẽ không muốn xóa toàn bộ nội dung HTML hiện có.

Hãy xóa đoạn code đó.

Thay vào đó, có lẽ bạn muốn kết xuất các thành phần React của mình tại những vị trí cụ thể trong HTML. Hãy mở trang HTML của bạn, hoặc các template server tạo ra nó, rồi thêm một thuộc tính [`id`](https://developer.mozilla.org/en-US/docs/Web/HTML/Global_attributes/id) duy nhất vào bất kỳ thẻ nào, ví dụ:

```html
<!-- ... somewhere in your html ... -->
<nav id="navigation"></nav>
<!-- ... more html ... -->
```

Điều này cho phép bạn tìm phần tử HTML đó bằng [`document.getElementById`](https://developer.mozilla.org/en-US/docs/Web/API/Document/getElementById) và truyền nó vào [`createRoot`](/reference/react-dom/client/createRoot) để có thể kết xuất thành phần React của riêng bạn bên trong:

<Sandpack>

```html public/index.html
<!DOCTYPE html>
<html>
  <head><title>My app</title></head>
  <body>
    <p>This paragraph is a part of HTML.</p>
    <nav id="navigation"></nav>
    <p>This paragraph is also a part of HTML.</p>
  </body>
</html>
```

```js src/index.js active
import { createRoot } from 'react-dom/client';

function NavigationBar() {
  // TODO: Actually implement a navigation bar
  return <h1>Hello from React!</h1>;
}

const domNode = document.getElementById('navigation');
const root = createRoot(domNode);
root.render(<NavigationBar />);
```

</Sandpack>

Hãy để ý rằng nội dung HTML gốc từ `index.html` vẫn được giữ nguyên, nhưng thành phần React `NavigationBar` của riêng bạn giờ xuất hiện bên trong `<nav id="navigation">` trong HTML. Hãy đọc [tài liệu sử dụng `createRoot`](/reference/react-dom/client/createRoot#rendering-a-page-partially-built-with-react) để tìm hiểu thêm về cách kết xuất các thành phần React bên trong một trang HTML hiện có.

Khi áp dụng React vào một dự án hiện có, bạn thường sẽ bắt đầu với các thành phần tương tác nhỏ, chẳng hạn nút bấm, rồi dần dần "đi lên" cho tới khi cuối cùng toàn bộ trang được xây bằng React. Nếu bạn đạt đến điểm đó, chúng tôi khuyên bạn nên chuyển sang [một framework React](/learn/creating-a-react-app) ngay sau đó để tận dụng React tối đa.

## Dùng React Native trong ứng dụng mobile native hiện có {/*using-react-native-in-an-existing-native-mobile-app*/}

[React Native](https://reactnative.dev/) cũng có thể được tích hợp dần vào các ứng dụng native hiện có. Nếu bạn đã có một ứng dụng native hiện có cho Android (Java hoặc Kotlin) hoặc iOS (Objective-C hoặc Swift), hãy [làm theo hướng dẫn này](https://reactnative.dev/docs/integration-with-existing-apps) để thêm một màn hình React Native vào đó.
