---
title: API React DOM
---

<Intro>

Package `react-dom` chứa các phương thức chỉ được hỗ trợ cho ứng dụng web, tức là chạy trong môi trường DOM của trình duyệt. Chúng không được hỗ trợ cho React Native.

</Intro>

---

## API {/*apis*/}

Các API này có thể được import từ component của bạn. Chúng hiếm khi được dùng:

* [`createPortal`](/reference/react-dom/createPortal) cho phép bạn kết xuất component con ở một phần khác của cây DOM.
* [`flushSync`](/reference/react-dom/flushSync) cho phép bạn buộc React flush một cập nhật state và cập nhật DOM theo cách đồng bộ.

## API tải trước tài nguyên {/*resource-preloading-apis*/}

Những API này có thể được dùng để làm ứng dụng nhanh hơn bằng cách tải trước các tài nguyên như script, stylesheet và font ngay khi bạn biết mình sẽ cần đến chúng, ví dụ trước khi điều hướng sang một trang khác nơi các tài nguyên đó sẽ được dùng.

[Framework dựa trên React](/learn/creating-a-react-app) thường xử lý việc tải tài nguyên thay bạn, nên có thể bạn sẽ không cần tự gọi các API này. Hãy xem tài liệu của framework để biết chi tiết.

* [`prefetchDNS`](/reference/react-dom/prefetchDNS) cho phép bạn tìm nạp trước địa chỉ IP của một tên miền DNS mà bạn dự kiến sẽ kết nối tới.
* [`preconnect`](/reference/react-dom/preconnect) cho phép bạn kết nối tới một server mà bạn dự kiến sẽ yêu cầu tài nguyên từ đó, ngay cả khi bạn chưa biết mình sẽ cần tài nguyên gì.
* [`preload`](/reference/react-dom/preload) cho phép bạn tìm nạp một stylesheet, font, hình ảnh hoặc script bên ngoài mà bạn dự kiến sẽ dùng.
* [`preloadModule`](/reference/react-dom/preloadModule) cho phép bạn tìm nạp một module ESM mà bạn dự kiến sẽ dùng.
* [`preinit`](/reference/react-dom/preinit) cho phép bạn tìm nạp và đánh giá một script bên ngoài hoặc tìm nạp và chèn một stylesheet.
* [`preinitModule`](/reference/react-dom/preinitModule) cho phép bạn tìm nạp và đánh giá một module ESM.

---

## Điểm vào {/*entry-points*/}

Package `react-dom` cung cấp thêm hai điểm vào:

* [`react-dom/client`](/reference/react-dom/client) chứa các API để kết xuất component React ở phía client, tức là trong trình duyệt.
* [`react-dom/server`](/reference/react-dom/server) chứa các API để kết xuất component React ở phía server.

---

## API đã bị loại bỏ {/*removed-apis*/}

Các API này đã bị loại bỏ trong React 19:

* [`findDOMNode`](https://18.react.dev/reference/react-dom/findDOMNode): xem [các lựa chọn thay thế](https://18.react.dev/reference/react-dom/findDOMNode#alternatives).
* [`hydrate`](https://18.react.dev/reference/react-dom/hydrate): hãy dùng [`hydrateRoot`](/reference/react-dom/client/hydrateRoot) thay thế.
* [`render`](https://18.react.dev/reference/react-dom/render): hãy dùng [`createRoot`](/reference/react-dom/client/createRoot) thay thế.
* [`unmountComponentAtNode`](/reference/react-dom/unmountComponentAtNode): hãy dùng [`root.unmount()`](/reference/react-dom/client/createRoot#root-unmount) thay thế.
* [`renderToNodeStream`](https://18.react.dev/reference/react-dom/server/renderToNodeStream): hãy dùng các API [`react-dom/server`](/reference/react-dom/server) thay thế.
* [`renderToStaticNodeStream`](https://18.react.dev/reference/react-dom/server/renderToStaticNodeStream): hãy dùng các API [`react-dom/server`](/reference/react-dom/server) thay thế.
