---
title: React Developer Tools
---

<Intro>

Dùng React Developer Tools để kiểm tra [component](/learn/your-first-component) React, chỉnh sửa [props](/learn/passing-props-to-a-component) và [state](/learn/state-a-components-memory), cũng như xác định các vấn đề về hiệu năng.

</Intro>

<YouWillLearn>

* Cách cài đặt React Developer Tools

</YouWillLearn>

## Tiện ích mở rộng trình duyệt {/*browser-extension*/}

Cách dễ nhất để gỡ lỗi các website được xây bằng React là cài tiện ích mở rộng React Developer Tools cho trình duyệt. Nó có sẵn cho một số trình duyệt phổ biến:

* [Cài cho **Chrome**](https://chrome.google.com/webstore/detail/react-developer-tools/fmkadmapgofadopljbjfkapdkoienihi?hl=en)
* [Cài cho **Firefox**](https://addons.mozilla.org/en-US/firefox/addon/react-devtools/)
* [Cài cho **Edge**](https://microsoftedge.microsoft.com/addons/detail/react-developer-tools/gpphkfbcpidddadnkolkpfckpihlkkil)

Bây giờ, nếu bạn truy cập một website **được xây bằng React,** bạn sẽ thấy các bảng _Components_ và _Profiler_.

![React Developer Tools extension](/images/docs/react-devtools-extension.png)

### Safari và các trình duyệt khác {/*safari-and-other-browsers*/}
Với các trình duyệt khác, ví dụ Safari, hãy cài package npm [`react-devtools`](https://www.npmjs.com/package/react-devtools):
```bash
# Yarn
yarn global add react-devtools

# Npm
npm install -g react-devtools
```

Tiếp theo, mở developer tools từ terminal:
```bash
react-devtools
```

Sau đó kết nối website của bạn bằng cách thêm thẻ `<script>` sau vào đầu phần `<head>` của website:
```html {3}
<html>
  <head>
    <script src="http://localhost:8097"></script>
```

Hãy tải lại website trong trình duyệt để xem nó trong developer tools.

![React Developer Tools standalone](/images/docs/react-devtools-standalone.png)

## Di động (React Native) {/*mobile-react-native*/}

Để kiểm tra các ứng dụng được xây bằng [React Native](https://reactnative.dev/), bạn có thể dùng [React Native DevTools](https://reactnative.dev/docs/react-native-devtools), trình gỡ lỗi tích hợp sẵn được tích hợp sâu với React Developer Tools. Mọi tính năng đều hoạt động giống hệt tiện ích trình duyệt, bao gồm tô sáng và chọn phần tử native.

[Tìm hiểu thêm về gỡ lỗi trong React Native.](https://reactnative.dev/docs/debugging)

> Với các phiên bản React Native cũ hơn 0.76, hãy dùng bản dựng độc lập của React DevTools bằng cách làm theo hướng dẫn [Safari và các trình duyệt khác](#safari-and-other-browsers) ở trên.
