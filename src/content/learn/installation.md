---
title: Cài đặt
---

<Intro>

React ngay từ đầu đã được thiết kế để có thể áp dụng dần dần. Bạn có thể dùng ít hay nhiều React tùy theo nhu cầu. Dù bạn muốn thử React cho biết, thêm chút tính tương tác vào một trang HTML hay bắt đầu một ứng dụng phức tạp chạy bằng React, phần này sẽ giúp bạn bắt đầu.

</Intro>

## Thử React {/*try-react*/}

Bạn không cần cài đặt gì để thử React. Hãy thử chỉnh sửa sandbox này!

<Sandpack>

```js
function Greeting({ name }) {
  return <h1>Hello, {name}</h1>;
}

export default function App() {
  return <Greeting name="world" />
}
```

</Sandpack>

Bạn có thể chỉnh sửa trực tiếp hoặc mở nó trong tab mới bằng cách nhấn nút "Fork" ở góc trên bên phải.

Phần lớn các trang trong tài liệu React đều có sandbox như thế này. Ngoài tài liệu React ra, cũng có nhiều sandbox trực tuyến hỗ trợ React, ví dụ như [CodeSandbox](https://codesandbox.io/s/new), [StackBlitz](https://stackblitz.com/fork/react) hoặc [CodePen.](https://codepen.io/pen?template=QWYVwWN)

Để thử React cục bộ trên máy tính của bạn, [hãy tải trang HTML này xuống.](https://gist.githubusercontent.com/gaearon/0275b1e1518599bbeafcde4722e79ed1/raw/db72dcbf3384ee1708c4a07d3be79860db04bff0/example.html) Hãy mở nó trong trình soạn thảo và trên trình duyệt của bạn!

## Tạo ứng dụng React {/*creating-a-react-app*/}

Nếu bạn muốn bắt đầu một ứng dụng React mới, bạn có thể [tạo ứng dụng React](/learn/creating-a-react-app) bằng một framework được khuyến nghị.

## Xây dựng ứng dụng React từ đầu {/*build-a-react-app-from-scratch*/}

Nếu framework không phù hợp với dự án của bạn, bạn muốn tự xây framework của riêng mình, hoặc chỉ đơn giản muốn học những điều cơ bản về một ứng dụng React, bạn có thể [xây dựng ứng dụng React từ đầu](/learn/build-a-react-app-from-scratch).

## Thêm React vào dự án hiện có {/*add-react-to-an-existing-project*/}

Nếu muốn thử dùng React trong ứng dụng hoặc website hiện có, bạn có thể [thêm React vào một dự án hiện có.](/learn/add-react-to-an-existing-project)


<Note>

#### Tôi có nên dùng Create React App không? {/*should-i-use-create-react-app*/}

Không. Create React App đã bị ngừng hỗ trợ. Để biết thêm thông tin, hãy xem [Khai tử Create React App](/blog/2025/02/14/sunsetting-create-react-app).

</Note>

## Bước tiếp theo {/*next-steps*/}

Hãy chuyển đến hướng dẫn [Bắt đầu nhanh](/learn) để khám phá những khái niệm React quan trọng nhất mà bạn sẽ gặp hằng ngày.
