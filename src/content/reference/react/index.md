---
title: Tổng quan tài liệu tham chiếu React
---

<Intro>

Phần này cung cấp tài liệu tham chiếu chi tiết để làm việc với React. Nếu bạn cần phần giới thiệu về React, hãy xem mục [Tìm hiểu](/learn).

</Intro>

Tài liệu tham chiếu React được chia thành các mục con theo chức năng:

## React {/*react*/}

Các tính năng React dùng bằng code:

* [Hooks](/reference/react/hooks) - Dùng các tính năng React khác nhau từ trong component của bạn.
* [Components](/reference/react/components) - Các component dựng sẵn mà bạn có thể dùng trong JSX.
* [APIs](/reference/react/apis) - Các API hữu ích để định nghĩa component.
* [Directives](/reference/rsc/directives) - Cung cấp chỉ dẫn cho các bundler tương thích với React Server Components.

## React DOM {/*react-dom*/}

React DOM chứa các tính năng chỉ được hỗ trợ cho ứng dụng web, tức là chạy trong môi trường DOM của trình duyệt. Mục này được chia thành các phần sau:

* [Hooks](/reference/react-dom/hooks) - Hook cho ứng dụng web chạy trong môi trường DOM của trình duyệt.
* [Components](/reference/react-dom/components) - React hỗ trợ toàn bộ component HTML và SVG dựng sẵn của trình duyệt.
* [APIs](/reference/react-dom) - Package `react-dom` chứa các phương thức chỉ được hỗ trợ trong ứng dụng web.
* [Client APIs](/reference/react-dom/client) - Các API `react-dom/client` cho phép bạn kết xuất component React ở phía client, tức là trong trình duyệt.
* [Server APIs](/reference/react-dom/server) - Các API `react-dom/server` cho phép bạn kết xuất component React thành HTML ở phía server.
* [Static APIs](/reference/react-dom/static) - Các API `react-dom/static` cho phép bạn tạo HTML tĩnh cho component React.

## React Compiler {/*react-compiler*/}

React Compiler là một công cụ tối ưu hóa ở thời điểm build, tự động ghi nhớ kết quả cho component React và các giá trị của bạn:

* [Configuration](/reference/react-compiler/configuration) - Các tùy chọn cấu hình cho React Compiler.
* [Directives](/reference/react-compiler/directives) - Các directive ở cấp hàm để kiểm soát việc biên dịch.
* [Compiling Libraries](/reference/react-compiler/compiling-libraries) - Hướng dẫn phân phối mã thư viện đã được biên dịch trước.

## ESLint Plugin React Hooks {/*eslint-plugin-react-hooks*/}

[Plugin ESLint cho React Hooks](/reference/eslint-plugin-react-hooks) giúp áp dụng Các quy tắc của React:

* [Lints](/reference/eslint-plugin-react-hooks) - Tài liệu chi tiết cho từng lint kèm ví dụ.

## Rules of React {/*rules-of-react*/}

React có những thành ngữ riêng, hay nói cách khác là các quy tắc, về cách biểu đạt mẫu theo hướng dễ hiểu và tạo ra ứng dụng chất lượng cao:

* [Components and Hooks must be pure](/reference/rules/components-and-hooks-must-be-pure) – Tính thuần giúp code của bạn dễ hiểu, dễ gỡ lỗi hơn, đồng thời cho phép React tự động tối ưu hóa component và Hook một cách chính xác.
* [React calls Components and Hooks](/reference/rules/react-calls-components-and-hooks) – React chịu trách nhiệm kết xuất component và Hook khi cần thiết để tối ưu trải nghiệm người dùng.
* [Rules of Hooks](/reference/rules/rules-of-hooks) – Hook được định nghĩa bằng các hàm JavaScript, nhưng đại diện cho một loại logic UI có thể tái sử dụng đặc biệt với các giới hạn về nơi có thể gọi chúng.

## Legacy APIs {/*legacy-apis*/}

* [Legacy APIs](/reference/react/legacy) - Được export từ package `react`, nhưng không được khuyến nghị dùng trong code mới.
