---
title: Viết Markup với JSX
---

<Intro>

*JSX* là một phần mở rộng cú pháp cho JavaScript, cho phép bạn viết markup giống HTML bên trong tệp JavaScript. Dù vẫn có những cách khác để viết thành phần, đa số lập trình viên React thích sự ngắn gọn của JSX, và phần lớn codebase đều dùng nó.

</Intro>

<YouWillLearn>

* Vì sao React trộn markup với logic kết xuất
* JSX khác HTML ở điểm nào
* Cách hiển thị thông tin bằng JSX

</YouWillLearn>

## JSX: đưa markup vào JavaScript {/*jsx-putting-markup-into-javascript*/}

Web được xây dựng trên HTML, CSS và JavaScript. Trong nhiều năm, lập trình viên web giữ nội dung trong HTML, thiết kế trong CSS, và logic trong JavaScript, thường là ở các tệp riêng biệt! Nội dung được viết bằng markup trong HTML, còn logic của trang nằm riêng trong JavaScript:

<DiagramGroup>

<Diagram name="writing_jsx_html" height={237} width={325} alt="HTML markup with purple background and a div with two child tags: p and form. ">

HTML

</Diagram>

<Diagram name="writing_jsx_js" height={237} width={325} alt="Three JavaScript handlers with yellow background: onSubmit, onLogin, and onClick.">

JavaScript

</Diagram>

</DiagramGroup>

Nhưng khi Web ngày càng tương tác hơn, logic càng quyết định nội dung nhiều hơn. JavaScript bắt đầu điều khiển HTML! Đó là lý do **trong React, logic kết xuất và markup nằm cùng một chỗ, đó là các thành phần.**

<DiagramGroup>

<Diagram name="writing_jsx_sidebar" height={330} width={325} alt="React component with HTML and JavaScript from previous examples mixed. Function name is Sidebar which calls the function isLoggedIn, highlighted in yellow. Nested inside the function highlighted in purple is the p tag from before, and a Form tag referencing the component shown in the next diagram.">

`Sidebar.js` React component

</Diagram>

<Diagram name="writing_jsx_form" height={330} width={325} alt="React component with HTML and JavaScript from previous examples mixed. Function name is Form containing two handlers onClick and onSubmit highlighted in yellow. Following the handlers is HTML highlighted in purple. The HTML contains a form element with a nested input element, each with an onClick prop.">

`Form.js` React component

</Diagram>

</DiagramGroup>

Việc giữ logic kết xuất và markup của một nút bấm ở cùng nhau giúp chúng luôn đồng bộ với nhau sau mỗi lần chỉnh sửa. Ngược lại, những chi tiết không liên quan, như markup của nút bấm và markup của thanh bên, được tách khỏi nhau, giúp bạn an toàn hơn khi thay đổi từng phần riêng lẻ.

Mỗi thành phần React là một hàm JavaScript có thể chứa một ít markup mà React sẽ kết xuất vào trình duyệt. Thành phần React dùng một phần mở rộng cú pháp gọi là JSX để biểu diễn markup đó. JSX trông rất giống HTML, nhưng chặt chẽ hơn một chút và có thể hiển thị thông tin động. Cách tốt nhất để hiểu điều này là chuyển một đoạn markup HTML sang markup JSX.

<Note>

JSX và React là hai thứ riêng biệt. Chúng thường được dùng cùng nhau, nhưng bạn *có thể* [dùng chúng độc lập](https://reactjs.org/blog/2020/09/22/introducing-the-new-jsx-transform.html#whats-a-jsx-transform) với nhau. JSX là một phần mở rộng cú pháp, còn React là thư viện JavaScript.

</Note>

## Chuyển HTML thành JSX {/*converting-html-to-jsx*/}

Giả sử bạn có một đoạn HTML (hoàn toàn hợp lệ):

```html
<h1>Hedy Lamarr's Todos</h1>
<img 
  src="https://i.imgur.com/yXOvdOSs.jpg" 
  alt="Hedy Lamarr" 
  class="photo"
>
<ul>
    <li>Invent new traffic lights
    <li>Rehearse a movie scene
    <li>Improve the spectrum technology
</ul>
```

Và bạn muốn đưa nó vào thành phần của mình:

```js
export default function TodoList() {
  return (
    // ???
  )
}
```

Nếu bạn sao chép và dán nguyên như vậy, nó sẽ không hoạt động:


<Sandpack>

```js
export default function TodoList() {
  return (
    // Cách này chưa chạy được!
    <h1>Hedy Lamarr's Todos</h1>
    <img 
      src="https://i.imgur.com/yXOvdOSs.jpg" 
      alt="Hedy Lamarr" 
      class="photo"
    >
    <ul>
      <li>Invent new traffic lights
      <li>Rehearse a movie scene
      <li>Improve the spectrum technology
    </ul>
  );
}
```

```css
img { height: 90px }
```

</Sandpack>

Đó là vì JSX chặt chẽ hơn và có thêm một vài quy tắc so với HTML! Nếu đọc các thông báo lỗi ở trên, chúng sẽ hướng dẫn bạn sửa markup, hoặc bạn có thể làm theo hướng dẫn bên dưới.

<Note>

Phần lớn thời gian, thông báo lỗi hiển thị trên màn hình của React sẽ giúp bạn tìm ra vấn đề nằm ở đâu. Hãy đọc chúng nếu bạn bị mắc kẹt!

</Note>

## Các quy tắc của JSX {/*the-rules-of-jsx*/}

### 1. Trả về một phần tử gốc duy nhất {/*1-return-a-single-root-element*/}

Để trả về nhiều phần tử từ một thành phần, **hãy bọc chúng trong một thẻ cha duy nhất.**

Ví dụ, bạn có thể dùng một `<div>`:

```js {1,11}
<div>
  <h1>Hedy Lamarr's Todos</h1>
  <img 
    src="https://i.imgur.com/yXOvdOSs.jpg" 
    alt="Hedy Lamarr" 
    class="photo"
  >
  <ul>
    ...
  </ul>
</div>
```


Nếu không muốn thêm một `<div>` dư thừa vào markup, bạn có thể viết `<>` và `</>` thay thế:

```js {1,11}
<>
  <h1>Hedy Lamarr's Todos</h1>
  <img 
    src="https://i.imgur.com/yXOvdOSs.jpg" 
    alt="Hedy Lamarr" 
    class="photo"
  >
  <ul>
    ...
  </ul>
</>
```

Thẻ rỗng này được gọi là *[Fragment.](/reference/react/Fragment)* Fragment cho phép bạn nhóm mọi thứ lại mà không để lại dấu vết nào trong cây HTML của trình duyệt.

<DeepDive>

#### Vì sao nhiều thẻ JSX phải được bọc lại? {/*why-do-multiple-jsx-tags-need-to-be-wrapped*/}

JSX trông giống HTML, nhưng ẩn bên dưới nó được chuyển thành các đối tượng JavaScript thuần. Bạn không thể trả về hai đối tượng từ một hàm nếu không bọc chúng trong một mảng. Điều này giải thích vì sao bạn cũng không thể trả về hai thẻ JSX mà không bọc chúng trong một thẻ khác hoặc một Fragment.

</DeepDive>

### 2. Đóng mọi thẻ {/*2-close-all-the-tags*/}

JSX yêu cầu các thẻ phải được đóng rõ ràng: các thẻ tự đóng như `<img>` phải trở thành `<img />`, và các thẻ bao bọc như `<li>oranges` phải được viết thành `<li>oranges</li>`.

Đây là cách đóng thẻ đúng cho ảnh và các mục danh sách của Hedy Lamarr:

```js {2-6,8-10}
<>
  <img 
    src="https://i.imgur.com/yXOvdOSs.jpg" 
    alt="Hedy Lamarr" 
    class="photo"
   />
  <ul>
    <li>Invent new traffic lights</li>
    <li>Rehearse a movie scene</li>
    <li>Improve the spectrum technology</li>
  </ul>
</>
```

### 3. Viết <s>mọi thứ</s> hầu hết mọi thứ theo camelCase! {/*3-camelcase-salls-most-of-the-things*/}

JSX sẽ chuyển thành JavaScript, và các thuộc tính viết trong JSX trở thành các khóa của đối tượng JavaScript. Trong các thành phần của riêng bạn, bạn thường sẽ muốn đọc các thuộc tính đó thành biến. Nhưng JavaScript có giới hạn đối với tên biến. Ví dụ, tên của chúng không thể chứa dấu gạch ngang hoặc là từ khóa dành riêng như `class`.

Đó là lý do trong React, nhiều thuộc tính HTML và SVG được viết theo camelCase. Ví dụ, thay vì `stroke-width` bạn dùng `strokeWidth`. Vì `class` là từ khóa dành riêng, trong React bạn sẽ viết `className`, được đặt tên theo [thuộc tính DOM tương ứng](https://developer.mozilla.org/en-US/docs/Web/API/Element/className):

```js {4}
<img 
  src="https://i.imgur.com/yXOvdOSs.jpg" 
  alt="Hedy Lamarr" 
  className="photo"
/>
```

Bạn có thể [tìm thấy toàn bộ các thuộc tính này trong danh sách props của thành phần DOM.](/reference/react-dom/components/common) Nếu viết sai một cái, đừng lo, React sẽ in ra một thông báo kèm gợi ý sửa trong [bảng điều khiển của trình duyệt.](https://developer.mozilla.org/docs/Tools/Browser_Console)

<Pitfall>

Vì lý do lịch sử, các thuộc tính [`aria-*`](https://developer.mozilla.org/docs/Web/Accessibility/ARIA) và [`data-*`](https://developer.mozilla.org/docs/Learn/HTML/Howto/Use_data_attributes) vẫn được viết như trong HTML, có dấu gạch ngang.

</Pitfall>

### Mẹo nhỏ: Dùng trình chuyển đổi JSX {/*pro-tip-use-a-jsx-converter*/}

Việc chuyển đổi toàn bộ các thuộc tính này trong markup có sẵn có thể khá tẻ nhạt! Chúng tôi khuyên bạn dùng một [trình chuyển đổi](https://transform.tools/html-to-jsx) để chuyển HTML và SVG hiện có sang JSX. Trình chuyển đổi rất hữu ích trong thực tế, nhưng bạn vẫn nên hiểu chuyện gì đang diễn ra để có thể tự tin viết JSX bằng chính mình.

Đây là kết quả cuối cùng của bạn:

<Sandpack>

```js
export default function TodoList() {
  return (
    <>
      <h1>Hedy Lamarr's Todos</h1>
      <img 
        src="https://i.imgur.com/yXOvdOSs.jpg" 
        alt="Hedy Lamarr" 
        className="photo" 
      />
      <ul>
        <li>Invent new traffic lights</li>
        <li>Rehearse a movie scene</li>
        <li>Improve the spectrum technology</li>
      </ul>
    </>
  );
}
```

```css
img { height: 90px }
```

</Sandpack>

<Recap>

Bây giờ bạn đã biết vì sao JSX tồn tại và cách dùng nó trong thành phần:

* Thành phần React gom logic kết xuất với markup vào cùng một chỗ vì chúng có liên quan với nhau.
* JSX khá giống HTML, nhưng có một vài điểm khác biệt. Bạn có thể dùng [trình chuyển đổi](https://transform.tools/html-to-jsx) nếu cần.
* Thông báo lỗi thường sẽ chỉ cho bạn đúng hướng để sửa markup.

</Recap>



<Challenges>

#### Chuyển một ít HTML sang JSX {/*convert-some-html-to-jsx*/}

Đoạn HTML này đã được dán vào một thành phần, nhưng nó chưa phải JSX hợp lệ. Hãy sửa nó:

<Sandpack>

```js
export default function Bio() {
  return (
    <div class="intro">
      <h1>Welcome to my website!</h1>
    </div>
    <p class="summary">
      You can find my thoughts here.
      <br><br>
      <b>And <i>pictures</b></i> of scientists!
    </p>
  );
}
```

```css
.intro {
  background-image: linear-gradient(to left, violet, indigo, blue, green, yellow, orange, red);
  background-clip: text;
  color: transparent;
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
}

.summary {
  padding: 20px;
  border: 10px solid gold;
}
```

</Sandpack>

Bạn muốn làm thủ công hay dùng trình chuyển đổi đều được!

<Solution>

<Sandpack>

```js
export default function Bio() {
  return (
    <div>
      <div className="intro">
        <h1>Welcome to my website!</h1>
      </div>
      <p className="summary">
        You can find my thoughts here.
        <br /><br />
        <b>And <i>pictures</i></b> of scientists!
      </p>
    </div>
  );
}
```

```css
.intro {
  background-image: linear-gradient(to left, violet, indigo, blue, green, yellow, orange, red);
  background-clip: text;
  color: transparent;
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
}

.summary {
  padding: 20px;
  border: 10px solid gold;
}
```

</Sandpack>

</Solution>

</Challenges>
