---
title: Các quy tắc của React
---

<Intro>
Cũng giống như mỗi ngôn ngữ lập trình có cách biểu đạt khái niệm riêng, React có các thành ngữ riêng, hay nói cách khác là các quy tắc, về cách biểu đạt mẫu theo hướng dễ hiểu và tạo ra ứng dụng chất lượng cao.
</Intro>

<InlineToc />

---

<Note>
Để tìm hiểu thêm về cách biểu đạt UI bằng React, chúng tôi khuyến nghị bạn đọc [Suy nghĩ theo React](/learn/thinking-in-react).
</Note>

Phần này mô tả những quy tắc bạn cần tuân theo để viết code React đúng tinh thần của React. Viết code React đúng tinh thần có thể giúp bạn xây dựng những ứng dụng được tổ chức tốt, an toàn và có tính kết hợp cao. Những đặc tính này giúp ứng dụng của bạn bền vững hơn trước thay đổi và dễ cộng tác hơn với các nhà phát triển khác, thư viện và công cụ.

Những quy tắc này được gọi là **Các quy tắc của React**. Chúng là các quy tắc chứ không chỉ là khuyến nghị, theo nghĩa nếu bạn vi phạm chúng thì ứng dụng của bạn rất có thể sẽ có lỗi. Code của bạn cũng sẽ không còn đúng tinh thần React và trở nên khó hiểu, khó suy luận hơn.

Chúng tôi đặc biệt khuyến nghị dùng [Strict Mode](/reference/react/StrictMode) cùng với [plugin ESLint](https://www.npmjs.com/package/eslint-plugin-react-hooks) của React để giúp codebase của bạn tuân theo Các quy tắc của React. Bằng cách tuân theo các quy tắc này, bạn sẽ có thể tìm ra và xử lý những lỗi đó, đồng thời giữ cho ứng dụng dễ bảo trì.

---

## Component và Hook phải thuần {/*components-and-hooks-must-be-pure*/}

[Tính thuần trong Component và Hook](/reference/rules/components-and-hooks-must-be-pure) là một quy tắc quan trọng của React, giúp ứng dụng của bạn dễ dự đoán, dễ gỡ lỗi và cho phép React tự động tối ưu hóa code.

* [Component phải có tính idempotent](/reference/rules/components-and-hooks-must-be-pure#components-and-hooks-must-be-idempotent) – Component React được giả định là luôn trả về cùng một kết quả đầu ra tương ứng với đầu vào của chúng như props, state và context.
* [Tác dụng phụ phải chạy bên ngoài render](/reference/rules/components-and-hooks-must-be-pure#side-effects-must-run-outside-of-render) – Tác dụng phụ không nên chạy trong render, vì React có thể render component nhiều lần để tạo ra trải nghiệm người dùng tốt nhất có thể.
* [Props và state là bất biến](/reference/rules/components-and-hooks-must-be-pure#props-and-state-are-immutable) – Props và state của component là những ảnh chụp bất biến đối với một lần render duy nhất. Đừng bao giờ thay đổi trực tiếp chúng.
* [Giá trị trả về và đối số truyền vào Hook là bất biến](/reference/rules/components-and-hooks-must-be-pure#return-values-and-arguments-to-hooks-are-immutable) – Một khi giá trị đã được truyền vào Hook, bạn không nên sửa đổi chúng. Tương tự props trong JSX, các giá trị trở thành bất biến khi được truyền vào Hook.
* [Giá trị là bất biến sau khi được truyền vào JSX](/reference/rules/components-and-hooks-must-be-pure#values-are-immutable-after-being-passed-to-jsx) – Đừng thay đổi giá trị sau khi chúng đã được dùng trong JSX. Hãy chuyển thao tác thay đổi lên trước khi JSX được tạo ra.

---

## React gọi Component và Hook {/*react-calls-components-and-hooks*/}

[React chịu trách nhiệm kết xuất component và Hook khi cần thiết để tối ưu trải nghiệm người dùng.](/reference/rules/react-calls-components-and-hooks) Cách tiếp cận này là khai báo: bạn nói cho React biết cần kết xuất gì trong logic của component, và React sẽ tự tìm cách hiển thị điều đó tốt nhất cho người dùng.

* [Đừng bao giờ gọi trực tiếp hàm component](/reference/rules/react-calls-components-and-hooks#never-call-component-functions-directly) – Component chỉ nên được dùng trong JSX. Đừng gọi chúng như các hàm thông thường.
* [Đừng bao giờ truyền Hook như giá trị thông thường](/reference/rules/react-calls-components-and-hooks#never-pass-around-hooks-as-regular-values) – Hook chỉ nên được gọi bên trong component. Đừng truyền chúng đi như giá trị thông thường.

---

## Rules of Hooks {/*rules-of-hooks*/}

Hook được định nghĩa bằng các hàm JavaScript, nhưng chúng đại diện cho một loại logic UI có thể tái sử dụng đặc biệt với những giới hạn về nơi có thể gọi. Bạn cần tuân theo [Rules of Hooks](/reference/rules/rules-of-hooks) khi sử dụng chúng.

* [Chỉ gọi Hook ở cấp cao nhất](/reference/rules/rules-of-hooks#only-call-hooks-at-the-top-level) – Đừng gọi Hook bên trong vòng lặp, điều kiện hoặc hàm lồng nhau. Thay vào đó, hãy luôn dùng Hook ở cấp cao nhất trong hàm React của bạn, trước mọi lệnh return sớm.
* [Chỉ gọi Hook từ hàm React](/reference/rules/rules-of-hooks#only-call-hooks-from-react-functions) – Đừng gọi Hook từ các hàm JavaScript thông thường.
