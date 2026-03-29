---
title: Thành phần đầu tiên của bạn
---

<Intro>

*Thành phần* là một trong những khái niệm cốt lõi của React. Chúng là nền tảng để bạn xây dựng giao diện người dùng (UI), nên đây là nơi hoàn hảo để bắt đầu hành trình học React của bạn!

</Intro>

<YouWillLearn>

* Thành phần là gì
* Vai trò của thành phần trong ứng dụng React
* Cách viết thành phần React đầu tiên của bạn

</YouWillLearn>

## Thành phần: các khối xây dựng UI {/*components-ui-building-blocks*/}

Trên Web, HTML cho phép chúng ta tạo ra những tài liệu có cấu trúc phong phú bằng tập thẻ dựng sẵn như `<h1>` và `<li>`:

```html
<article>
  <h1>My First Component</h1>
  <ol>
    <li>Components: UI Building Blocks</li>
    <li>Defining a Component</li>
    <li>Using a Component</li>
  </ol>
</article>
```

Đoạn markup này biểu diễn bài viết `<article>`, tiêu đề `<h1>`, và mục lục (đã rút gọn) dưới dạng danh sách có thứ tự `<ol>`. Kiểu markup như vậy, kết hợp với CSS để tạo kiểu và JavaScript để thêm tính tương tác, nằm phía sau mọi thanh bên, ảnh đại diện, hộp thoại modal, menu thả xuống, tức là mọi phần UI bạn thấy trên Web.

React cho phép bạn kết hợp markup, CSS và JavaScript thành những "thành phần" tùy chỉnh, tức là **các phần tử UI có thể tái sử dụng cho ứng dụng của bạn.** Đoạn code mục lục ở trên có thể được biến thành một thành phần `<TableOfContents />` mà bạn kết xuất trên mọi trang. Ẩn bên dưới, nó vẫn dùng chính những thẻ HTML như `<article>`, `<h1>`, v.v.

Tương tự như với thẻ HTML, bạn có thể kết hợp, sắp xếp và lồng các thành phần để thiết kế cả trang hoàn chỉnh. Ví dụ, trang tài liệu bạn đang đọc được tạo nên từ các thành phần React:

```js
<PageLayout>
  <NavigationHeader>
    <SearchBar />
    <Link to="/docs">Docs</Link>
  </NavigationHeader>
  <Sidebar />
  <PageContent>
    <TableOfContents />
    <DocumentationText />
  </PageContent>
</PageLayout>
```

Khi dự án lớn dần, bạn sẽ nhận ra nhiều thiết kế có thể được ghép lại bằng cách tái sử dụng những thành phần bạn đã viết, từ đó tăng tốc phát triển. Mục lục ở trên có thể được thêm vào bất kỳ màn hình nào chỉ với `<TableOfContents />`! Bạn thậm chí có thể khởi động dự án nhanh hơn bằng hàng nghìn thành phần mà cộng đồng mã nguồn mở React đã chia sẻ như [Chakra UI](https://chakra-ui.com/) và [Material UI.](https://material-ui.com/)

## Định nghĩa một thành phần {/*defining-a-component*/}

Theo cách truyền thống khi tạo trang web, lập trình viên web viết markup cho nội dung rồi thêm tương tác bằng một ít JavaScript. Cách này hoạt động rất tốt khi tính tương tác chỉ là một thứ "có thì tốt". Còn bây giờ, điều đó được kỳ vọng ở nhiều website và mọi ứng dụng. React đặt tính tương tác lên trước trong khi vẫn dùng cùng công nghệ: **một thành phần React là một hàm JavaScript mà bạn có thể _rắc thêm markup vào_.** Đây là nó trông như thế nào (bạn có thể sửa ví dụ bên dưới):

<Sandpack>

```js
export default function Profile() {
  return (
    <img
      src="https://i.imgur.com/MK3eW3Am.jpg"
      alt="Katherine Johnson"
    />
  )
}
```

```css
img { height: 200px; }
```

</Sandpack>

Và đây là cách xây dựng một thành phần:

### Bước 1: Export thành phần {/*step-1-export-the-component*/}

Tiền tố `export default` là [cú pháp JavaScript tiêu chuẩn](https://developer.mozilla.org/docs/web/javascript/reference/statements/export) (không dành riêng cho React). Nó cho phép bạn đánh dấu hàm chính trong một tệp để sau này có thể import hàm đó từ tệp khác. (Bạn sẽ tìm hiểu thêm về import trong [Import và Export Thành phần](/learn/importing-and-exporting-components)!)

### Bước 2: Định nghĩa hàm {/*step-2-define-the-function*/}

Với `function Profile() { }`, bạn định nghĩa một hàm JavaScript có tên là `Profile`.

<Pitfall>

Thành phần React là các hàm JavaScript thông thường, nhưng **tên của chúng phải bắt đầu bằng chữ cái viết hoa** nếu không chúng sẽ không hoạt động!

</Pitfall>

### Bước 3: Thêm markup {/*step-3-add-markup*/}

Thành phần trả về một thẻ `<img />` với các thuộc tính `src` và `alt`. `<img />` được viết giống HTML, nhưng thực ra ẩn bên dưới nó là JavaScript! Cú pháp này được gọi là [JSX](/learn/writing-markup-with-jsx), và nó cho phép bạn nhúng markup vào bên trong JavaScript.

Câu lệnh `return` có thể được viết trên một dòng, như trong thành phần này:

```js
return <img src="https://i.imgur.com/MK3eW3As.jpg" alt="Katherine Johnson" />;
```

Nhưng nếu markup của bạn không nằm cùng dòng với từ khóa `return`, bạn phải bọc nó trong một cặp dấu ngoặc tròn:

```js
return (
  <div>
    <img src="https://i.imgur.com/MK3eW3As.jpg" alt="Katherine Johnson" />
  </div>
);
```

<Pitfall>

Nếu không có dấu ngoặc, mọi code ở các dòng sau `return` [sẽ bị bỏ qua](https://stackoverflow.com/questions/2846283/what-are-the-rules-for-javascripts-automatic-semicolon-insertion-asi)!

</Pitfall>

## Sử dụng một thành phần {/*using-a-component*/}

Bây giờ khi đã định nghĩa thành phần `Profile`, bạn có thể lồng nó vào trong các thành phần khác. Ví dụ, bạn có thể export một thành phần `Gallery` sử dụng nhiều thành phần `Profile`:

<Sandpack>

```js
function Profile() {
  return (
    <img
      src="https://i.imgur.com/MK3eW3As.jpg"
      alt="Katherine Johnson"
    />
  );
}

export default function Gallery() {
  return (
    <section>
      <h1>Amazing scientists</h1>
      <Profile />
      <Profile />
      <Profile />
    </section>
  );
}
```

```css
img { margin: 0 10px 10px 0; height: 90px; }
```

</Sandpack>

### Trình duyệt nhìn thấy gì {/*what-the-browser-sees*/}

Hãy để ý sự khác nhau giữa chữ hoa và chữ thường:

* `<section>` viết thường, nên React biết rằng ta đang nói đến một thẻ HTML.
* `<Profile />` bắt đầu bằng chữ `P` viết hoa, nên React biết rằng ta muốn dùng thành phần tên là `Profile`.

Và `Profile` còn chứa thêm HTML nữa: `<img />`. Cuối cùng, đây là thứ trình duyệt nhìn thấy:

```html
<section>
  <h1>Amazing scientists</h1>
  <img src="https://i.imgur.com/MK3eW3As.jpg" alt="Katherine Johnson" />
  <img src="https://i.imgur.com/MK3eW3As.jpg" alt="Katherine Johnson" />
  <img src="https://i.imgur.com/MK3eW3As.jpg" alt="Katherine Johnson" />
</section>
```

### Lồng và tổ chức các thành phần {/*nesting-and-organizing-components*/}

Thành phần là các hàm JavaScript thông thường, nên bạn có thể đặt nhiều thành phần trong cùng một tệp. Điều này tiện lợi khi các thành phần khá nhỏ hoặc liên quan chặt chẽ với nhau. Nếu tệp trở nên quá chật chội, bạn luôn có thể chuyển `Profile` sang một tệp riêng. Bạn sẽ sớm học cách làm điều đó trong [trang về import.](/learn/importing-and-exporting-components)

Vì các thành phần `Profile` được kết xuất bên trong `Gallery`, thậm chí nhiều lần, nên ta có thể nói `Gallery` là một **thành phần cha,** kết xuất từng `Profile` như một thành phần "con". Đây là một phần sức mạnh của React: bạn có thể định nghĩa thành phần một lần rồi dùng ở bao nhiêu nơi và bao nhiêu lần tùy thích.

<Pitfall>

Thành phần có thể kết xuất các thành phần khác, nhưng **bạn tuyệt đối không được lồng phần định nghĩa của chúng:**

```js {2-5}
export default function Gallery() {
  // 🔴 Never define a component inside another component!
  function Profile() {
    // ...
  }
  // ...
}
```

Đoạn mã trên [rất chậm và gây ra lỗi.](/learn/preserving-and-resetting-state#different-components-at-the-same-position-reset-state) Thay vào đó, hãy định nghĩa mọi thành phần ở cấp cao nhất:

```js {5-8}
export default function Gallery() {
  // ...
}

// ✅ Khai báo thành phần ở cấp cao nhất
function Profile() {
  // ...
}
```

Khi một thành phần con cần dữ liệu từ thành phần cha, hãy [truyền nó bằng props](/learn/passing-props-to-a-component) thay vì lồng các phần định nghĩa.

</Pitfall>

<DeepDive>

#### Thành phần ở mọi cấp {/*components-all-the-way-down*/}

Ứng dụng React của bạn bắt đầu từ một thành phần "gốc". Thông thường, nó được tạo tự động khi bạn bắt đầu một dự án mới. Ví dụ, nếu bạn dùng [CodeSandbox](https://codesandbox.io/) hoặc framework [Next.js](https://nextjs.org/), thành phần gốc sẽ được định nghĩa trong `pages/index.js`. Trong các ví dụ này, bạn đã export các thành phần gốc.

Hầu hết ứng dụng React đều dùng thành phần ở mọi cấp. Điều đó có nghĩa là bạn không chỉ dùng thành phần cho những phần có thể tái sử dụng như nút bấm, mà còn cho những phần lớn hơn như thanh bên, danh sách, và cuối cùng là cả trang hoàn chỉnh! Thành phần là cách tiện lợi để tổ chức code UI và markup, ngay cả khi một số thành phần chỉ được dùng một lần.

[Các framework dựa trên React](/learn/creating-a-react-app) còn tiến thêm một bước. Thay vì dùng một tệp HTML trống và để React "tiếp quản" việc quản lý trang bằng JavaScript, chúng *còn* tự động tạo HTML từ các thành phần React của bạn. Nhờ vậy, ứng dụng có thể hiển thị một phần nội dung trước khi mã JavaScript tải xong.

Dù vậy, nhiều website chỉ dùng React để [thêm tính tương tác vào những trang HTML có sẵn.](/learn/add-react-to-an-existing-project#using-react-for-a-part-of-your-existing-page) Chúng có nhiều thành phần gốc thay vì chỉ một thành phần cho toàn bộ trang. Bạn có thể dùng React nhiều hay ít tùy nhu cầu.

</DeepDive>

<Recap>

Bạn vừa có trải nghiệm đầu tiên với React! Hãy cùng điểm lại vài ý chính.

* React cho phép bạn tạo thành phần, tức là **các phần tử UI có thể tái sử dụng cho ứng dụng của bạn.**
* Trong một ứng dụng React, mọi phần của UI đều là một thành phần.
* Thành phần React là các hàm JavaScript thông thường, ngoại trừ:

  1. Tên của chúng luôn bắt đầu bằng chữ cái viết hoa.
  2. Chúng trả về markup JSX.

</Recap>



<Challenges>

#### Export thành phần {/*export-the-component*/}

Sandbox này không hoạt động vì thành phần gốc chưa được export:

<Sandpack>

```js
function Profile() {
  return (
    <img
      src="https://i.imgur.com/lICfvbD.jpg"
      alt="Aklilu Lemma"
    />
  );
}
```

```css
img { height: 181px; }
```

</Sandpack>

Hãy thử tự sửa trước khi xem lời giải!

<Solution>

Hãy thêm `export default` trước phần định nghĩa hàm như sau:

<Sandpack>

```js
export default function Profile() {
  return (
    <img
      src="https://i.imgur.com/lICfvbD.jpg"
      alt="Aklilu Lemma"
    />
  );
}
```

```css
img { height: 181px; }
```

</Sandpack>

Có thể bạn sẽ thắc mắc vì sao chỉ viết `export` thôi lại chưa đủ để sửa ví dụ này. Bạn có thể tìm hiểu sự khác nhau giữa `export` và `export default` trong [Import và Export Thành phần.](/learn/importing-and-exporting-components)

</Solution>

#### Sửa câu lệnh return {/*fix-the-return-statement*/}

Có gì đó không đúng với câu lệnh `return` này. Bạn sửa được không?

<Hint>

Bạn có thể gặp lỗi "Unexpected token" khi thử sửa. Nếu vậy, hãy kiểm tra xem dấu chấm phẩy có nằm *sau* dấu ngoặc đóng hay không. Đặt dấu chấm phẩy bên trong `return ( )` sẽ gây lỗi.

</Hint>


<Sandpack>

```js
export default function Profile() {
  return
    <img src="https://i.imgur.com/jA8hHMpm.jpg" alt="Katsuko Saruhashi" />;
}
```

```css
img { height: 180px; }
```

</Sandpack>

<Solution>

Bạn có thể sửa thành phần này bằng cách đưa câu lệnh return lên một dòng như sau:

<Sandpack>

```js
export default function Profile() {
  return <img src="https://i.imgur.com/jA8hHMpm.jpg" alt="Katsuko Saruhashi" />;
}
```

```css
img { height: 180px; }
```

</Sandpack>

Hoặc bọc markup JSX được trả về trong dấu ngoặc tròn, mở ngay sau `return`:

<Sandpack>

```js
export default function Profile() {
  return (
    <img 
      src="https://i.imgur.com/jA8hHMpm.jpg" 
      alt="Katsuko Saruhashi" 
    />
  );
}
```

```css
img { height: 180px; }
```

</Sandpack>

</Solution>

#### Tìm lỗi sai {/*spot-the-mistake*/}

Có gì đó không ổn trong cách thành phần `Profile` được khai báo và sử dụng. Bạn có tìm ra lỗi không? (Hãy nhớ lại cách React phân biệt thành phần với các thẻ HTML thông thường!)

<Sandpack>

```js
function profile() {
  return (
    <img
      src="https://i.imgur.com/QIrZWGIs.jpg"
      alt="Alan L. Hart"
    />
  );
}

export default function Gallery() {
  return (
    <section>
      <h1>Amazing scientists</h1>
      <profile />
      <profile />
      <profile />
    </section>
  );
}
```

```css
img { margin: 0 10px 10px 0; height: 90px; }
```

</Sandpack>

<Solution>

Tên thành phần React phải bắt đầu bằng chữ cái viết hoa.

Hãy đổi `function profile()` thành `function Profile()`, rồi đổi mọi `<profile />` thành `<Profile />`:

<Sandpack>

```js
function Profile() {
  return (
    <img
      src="https://i.imgur.com/QIrZWGIs.jpg"
      alt="Alan L. Hart"
    />
  );
}

export default function Gallery() {
  return (
    <section>
      <h1>Amazing scientists</h1>
      <Profile />
      <Profile />
      <Profile />
    </section>
  );
}
```

```css
img { margin: 0 10px 10px 0; }
```

</Sandpack>

</Solution>

#### Thành phần của riêng bạn {/*your-own-component*/}

Hãy tự viết một thành phần từ đầu. Bạn có thể đặt cho nó bất kỳ tên hợp lệ nào và trả về bất kỳ markup nào. Nếu chưa có ý tưởng, bạn có thể viết một thành phần `Congratulations` hiển thị `<h1>Good job!</h1>`. Đừng quên export nó!

<Sandpack>

```js
// Write your component below!

```

</Sandpack>

<Solution>

<Sandpack>

```js
export default function Congratulations() {
  return (
    <h1>Good job!</h1>
  );
}
```

</Sandpack>

</Solution>

</Challenges>
