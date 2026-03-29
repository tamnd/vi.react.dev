---
title: "API React cũ"
---

<Intro>

Các API này được export từ package `react`, nhưng không được khuyến nghị dùng trong code mới. Hãy xem các trang API riêng lẻ được liên kết để biết những lựa chọn thay thế được đề xuất.

</Intro>

---

## API cũ {/*legacy-apis*/}

* [`Children`](/reference/react/Children) cho phép bạn thao tác và biến đổi JSX nhận được qua prop `children`. [Xem lựa chọn thay thế.](/reference/react/Children#alternatives)
* [`cloneElement`](/reference/react/cloneElement) cho phép bạn tạo một phần tử React bằng cách dùng một phần tử khác làm điểm xuất phát. [Xem lựa chọn thay thế.](/reference/react/cloneElement#alternatives)
* [`Component`](/reference/react/Component) cho phép bạn định nghĩa một component React dưới dạng lớp JavaScript. [Xem lựa chọn thay thế.](/reference/react/Component#alternatives)
* [`createElement`](/reference/react/createElement) cho phép bạn tạo một phần tử React. Thông thường, bạn sẽ dùng JSX thay thế.
* [`createRef`](/reference/react/createRef) tạo một object ref có thể chứa giá trị bất kỳ. [Xem lựa chọn thay thế.](/reference/react/createRef#alternatives)
* [`forwardRef`](/reference/react/forwardRef) cho phép component của bạn để lộ một nút DOM cho component cha thông qua một [ref.](/learn/manipulating-the-dom-with-refs)
* [`isValidElement`](/reference/react/isValidElement) kiểm tra xem một giá trị có phải là phần tử React hay không. Thường được dùng với [`cloneElement`.](/reference/react/cloneElement)
* [`PureComponent`](/reference/react/PureComponent) tương tự [`Component`,](/reference/react/Component) nhưng bỏ qua việc kết xuất lại khi props không đổi. [Xem lựa chọn thay thế.](/reference/react/PureComponent#alternatives)

---

## API đã bị loại bỏ {/*removed-apis*/}

Các API này đã bị loại bỏ trong React 19:

* [`createFactory`](https://18.react.dev/reference/react/createFactory): hãy dùng JSX thay thế.
* Component lớp: [`static contextTypes`](https://18.react.dev//reference/react/Component#static-contexttypes): hãy dùng [`static contextType`](#static-contexttype) thay thế.
* Component lớp: [`static childContextTypes`](https://18.react.dev//reference/react/Component#static-childcontexttypes): hãy dùng [`static contextType`](#static-contexttype) thay thế.
* Component lớp: [`static getChildContext`](https://18.react.dev//reference/react/Component#getchildcontext): hãy dùng [`Context`](/reference/react/createContext#provider) thay thế.
* Component lớp: [`static propTypes`](https://18.react.dev//reference/react/Component#static-proptypes): hãy dùng hệ thống kiểu như [TypeScript](https://www.typescriptlang.org/) thay thế.
* Component lớp: [`this.refs`](https://18.react.dev//reference/react/Component#refs): hãy dùng [`createRef`](/reference/react/createRef) thay thế.
