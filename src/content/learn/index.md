---
title: Bắt đầu nhanh
---

<Intro>

Chào mừng bạn đến với tài liệu React! Trang này sẽ giúp bạn làm quen với 80% các khái niệm React mà bạn sẽ dùng hằng ngày.

</Intro>

<YouWillLearn>

- Cách tạo và lồng component
- Cách thêm markup và style
- Cách hiển thị dữ liệu
- Cách kết xuất điều kiện và danh sách
- Cách phản hồi sự kiện và cập nhật màn hình
- Cách chia sẻ dữ liệu giữa các component

</YouWillLearn>

## Tạo và lồng component {/*components*/}

Ứng dụng React được tạo nên từ các *component*. Một component là một phần của UI (giao diện người dùng) có logic và giao diện riêng. Component có thể nhỏ như một nút bấm, hoặc lớn như cả một trang hoàn chỉnh.

Component React là các hàm JavaScript trả về markup:

```js
function MyButton() {
  return (
    <button>I'm a button</button>
  );
}
```

Sau khi khai báo `MyButton`, bạn có thể lồng nó vào trong một component khác:

```js {5}
export default function MyApp() {
  return (
    <div>
      <h1>Welcome to my app</h1>
      <MyButton />
    </div>
  );
}
```

Hãy để ý rằng `<MyButton />` bắt đầu bằng chữ in hoa. Đó là cách bạn nhận ra đây là một component React. Tên component React luôn phải bắt đầu bằng chữ in hoa, còn thẻ HTML thì phải viết thường.

Hãy xem kết quả:

<Sandpack>

```js
function MyButton() {
  return (
    <button>
      I'm a button
    </button>
  );
}

export default function MyApp() {
  return (
    <div>
      <h1>Welcome to my app</h1>
      <MyButton />
    </div>
  );
}
```

</Sandpack>

Từ khóa `export default` chỉ định component chính trong tệp. Nếu bạn chưa quen với một số cú pháp JavaScript, [MDN](https://developer.mozilla.org/en-US/docs/web/javascript/reference/statements/export) và [javascript.info](https://javascript.info/import-export) là những tài liệu tham khảo rất tốt.

## Viết markup với JSX {/*writing-markup-with-jsx*/}

Cú pháp markup bạn vừa thấy ở trên được gọi là *JSX*. JSX là tùy chọn, nhưng phần lớn dự án React đều dùng JSX vì nó tiện lợi. Tất cả [các công cụ chúng tôi khuyên dùng để phát triển cục bộ](/learn/installation) đều hỗ trợ JSX ngay từ đầu.

JSX chặt chẽ hơn HTML. Bạn phải đóng các thẻ như `<br />`. Component của bạn cũng không thể trả về nhiều thẻ JSX cùng lúc. Bạn phải bọc chúng trong một phần tử cha chung như `<div>...</div>` hoặc bộ bọc rỗng `<>...</>`:

```js {3,6}
function AboutPage() {
  return (
    <>
      <h1>About</h1>
      <p>Hello there.<br />How do you do?</p>
    </>
  );
}
```

Nếu bạn có nhiều HTML cần chuyển sang JSX, bạn có thể dùng [trình chuyển đổi trực tuyến.](https://transform.tools/html-to-jsx)

## Thêm style {/*adding-styles*/}

Trong React, bạn khai báo một lớp CSS bằng `className`. Nó hoạt động tương tự thuộc tính [`class`](https://developer.mozilla.org/en-US/docs/Web/HTML/Global_attributes/class) của HTML:

```js
<img className="avatar" />
```

Sau đó, bạn viết các quy tắc CSS cho nó trong một tệp CSS riêng:

```css
/* In your CSS */
.avatar {
  border-radius: 50%;
}
```

React không áp đặt cách bạn thêm tệp CSS. Trong trường hợp đơn giản nhất, bạn sẽ thêm thẻ [`<link>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/link) vào HTML. Nếu bạn dùng một công cụ build hoặc framework, hãy xem tài liệu của nó để biết cách thêm tệp CSS vào dự án.

## Hiển thị dữ liệu {/*displaying-data*/}

JSX cho phép bạn đặt markup vào trong JavaScript. Dấu ngoặc nhọn cho phép bạn "thoát ra" JavaScript để nhúng một biến từ code và hiển thị nó cho người dùng. Ví dụ, đoạn này sẽ hiển thị `user.name`:

```js {3}
return (
  <h1>
    {user.name}
  </h1>
);
```

Bạn cũng có thể "đi vào JavaScript" từ các thuộc tính JSX, nhưng bạn phải dùng ngoặc nhọn *thay cho* dấu nháy. Ví dụ, `className="avatar"` truyền chuỗi `"avatar"` làm lớp CSS, còn `src={user.imageUrl}` sẽ đọc giá trị của biến JavaScript `user.imageUrl`, rồi truyền giá trị đó làm thuộc tính `src`:

```js {3,4}
return (
  <img
    className="avatar"
    src={user.imageUrl}
  />
);
```

Bạn cũng có thể đặt những biểu thức phức tạp hơn vào trong ngoặc nhọn JSX, ví dụ như [nối chuỗi](https://javascript.info/operators#string-concatenation-with-binary):

<Sandpack>

```js
const user = {
  name: 'Hedy Lamarr',
  imageUrl: 'https://i.imgur.com/yXOvdOSs.jpg',
  imageSize: 90,
};

export default function Profile() {
  return (
    <>
      <h1>{user.name}</h1>
      <img
        className="avatar"
        src={user.imageUrl}
        alt={'Photo of ' + user.name}
        style={{
          width: user.imageSize,
          height: user.imageSize
        }}
      />
    </>
  );
}
```

```css
.avatar {
  border-radius: 50%;
}

.large {
  border: 4px solid gold;
}
```

</Sandpack>

Trong ví dụ trên, `style={{}}` không phải là cú pháp đặc biệt mà là một object `{}` thông thường nằm trong ngoặc nhọn JSX của `style={ }`. Bạn có thể dùng thuộc tính `style` khi style của bạn phụ thuộc vào các biến JavaScript.

## Kết xuất có điều kiện {/*conditional-rendering*/}

Trong React, không có cú pháp đặc biệt nào để viết điều kiện. Thay vào đó, bạn sẽ dùng chính những kỹ thuật như khi viết JavaScript thông thường. Ví dụ, bạn có thể dùng câu lệnh [`if`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/if...else) để bao gồm JSX theo điều kiện:

```js
let content;
if (isLoggedIn) {
  content = <AdminPanel />;
} else {
  content = <LoginForm />;
}
return (
  <div>
    {content}
  </div>
);
```

Nếu thích code gọn hơn, bạn có thể dùng [toán tử điều kiện `?`.](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Conditional_Operator) Khác với `if`, nó dùng được ngay bên trong JSX:

```js
<div>
  {isLoggedIn ? (
    <AdminPanel />
  ) : (
    <LoginForm />
  )}
</div>
```

Khi bạn không cần nhánh `else`, bạn cũng có thể dùng [cú pháp logic `&&`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Logical_AND#short-circuit_evaluation) ngắn gọn hơn:

```js
<div>
  {isLoggedIn && <AdminPanel />}
</div>
```

Tất cả các cách tiếp cận này cũng dùng được để chỉ định thuộc tính theo điều kiện. Nếu bạn chưa quen với một số cú pháp JavaScript ở đây, bạn có thể bắt đầu bằng cách luôn dùng `if...else`.

## Kết xuất danh sách {/*rendering-lists*/}

Bạn sẽ dùng các tính năng JavaScript như [vòng lặp `for`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/for) và [hàm `map()` của mảng](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/map) để kết xuất danh sách component.

Ví dụ, giả sử bạn có một mảng các sản phẩm:

```js
const products = [
  { title: 'Cabbage', id: 1 },
  { title: 'Garlic', id: 2 },
  { title: 'Apple', id: 3 },
];
```

Bên trong component, hãy dùng hàm `map()` để biến mảng sản phẩm thành một mảng các phần tử `<li>`:

```js
const listItems = products.map(product =>
  <li key={product.id}>
    {product.title}
  </li>
);

return (
  <ul>{listItems}</ul>
);
```

Hãy để ý `<li>` có thuộc tính `key`. Với mỗi phần tử trong danh sách, bạn nên truyền một chuỗi hoặc số để định danh duy nhất phần tử đó trong số các phần tử cùng cấp. Thông thường, key nên đến từ dữ liệu của bạn, chẳng hạn như ID trong cơ sở dữ liệu. React dùng key để biết điều gì đã xảy ra nếu sau này bạn chèn, xóa hoặc sắp xếp lại các phần tử.

<Sandpack>

```js
const products = [
  { title: 'Cabbage', isFruit: false, id: 1 },
  { title: 'Garlic', isFruit: false, id: 2 },
  { title: 'Apple', isFruit: true, id: 3 },
];

export default function ShoppingList() {
  const listItems = products.map(product =>
    <li
      key={product.id}
      style={{
        color: product.isFruit ? 'magenta' : 'darkgreen'
      }}
    >
      {product.title}
    </li>
  );

  return (
    <ul>{listItems}</ul>
  );
}
```

</Sandpack>

## Phản hồi sự kiện {/*responding-to-events*/}

Bạn có thể phản hồi sự kiện bằng cách khai báo các hàm *trình xử lý sự kiện* bên trong component:

```js {2-4,7}
function MyButton() {
  function handleClick() {
    alert('You clicked me!');
  }

  return (
    <button onClick={handleClick}>
      Click me
    </button>
  );
}
```

Hãy để ý `onClick={handleClick}` không có dấu ngoặc ở cuối! Đừng _gọi_ hàm trình xử lý sự kiện; bạn chỉ cần *truyền nó xuống*. React sẽ gọi trình xử lý sự kiện của bạn khi người dùng nhấp vào nút.

## Cập nhật màn hình {/*updating-the-screen*/}

Thông thường, bạn sẽ muốn component của mình "ghi nhớ" một số thông tin rồi hiển thị nó. Ví dụ, có thể bạn muốn đếm số lần một nút được nhấp. Để làm điều đó, hãy thêm *state* vào component.

Trước tiên, hãy import [`useState`](/reference/react/useState) từ React:

```js
import { useState } from 'react';
```

Bây giờ bạn có thể khai báo một *biến state* bên trong component:

```js
function MyButton() {
  const [count, setCount] = useState(0);
  // ...
```

Bạn sẽ nhận được hai thứ từ `useState`: state hiện tại (`count`) và hàm cho phép bạn cập nhật nó (`setCount`). Bạn có thể đặt cho chúng bất kỳ tên nào, nhưng quy ước là viết theo dạng `[something, setSomething]`.

Lần đầu nút được hiển thị, `count` sẽ là `0` vì bạn đã truyền `0` vào `useState()`. Khi muốn thay đổi state, hãy gọi `setCount()` và truyền giá trị mới cho nó. Nhấp vào nút này sẽ tăng bộ đếm lên:

```js {5}
function MyButton() {
  const [count, setCount] = useState(0);

  function handleClick() {
    setCount(count + 1);
  }

  return (
    <button onClick={handleClick}>
      Clicked {count} times
    </button>
  );
}
```

React sẽ gọi lại hàm component của bạn. Lần này `count` sẽ là `1`. Sau đó là `2`. Và cứ thế tiếp tục.

Nếu bạn kết xuất cùng một component nhiều lần, mỗi bản sao sẽ có state riêng. Hãy nhấp từng nút riêng biệt:

<Sandpack>

```js
import { useState } from 'react';

export default function MyApp() {
  return (
    <div>
      <h1>Counters that update separately</h1>
      <MyButton />
      <MyButton />
    </div>
  );
}

function MyButton() {
  const [count, setCount] = useState(0);

  function handleClick() {
    setCount(count + 1);
  }

  return (
    <button onClick={handleClick}>
      Clicked {count} times
    </button>
  );
}
```

```css
button {
  display: block;
  margin-bottom: 5px;
}
```

</Sandpack>

Hãy để ý mỗi nút đều "ghi nhớ" state `count` riêng của nó và không ảnh hưởng đến các nút khác.

## Sử dụng Hooks {/*using-hooks*/}

Các hàm bắt đầu bằng `use` được gọi là *Hook*. `useState` là Hook dựng sẵn do React cung cấp. Bạn có thể tìm các Hook dựng sẵn khác trong [tài liệu tham chiếu API.](/reference/react) Bạn cũng có thể tự viết Hook bằng cách kết hợp các Hook sẵn có.

Hook bị ràng buộc chặt hơn các hàm khác. Bạn chỉ có thể gọi Hook *ở đầu* component của mình (hoặc đầu một Hook khác). Nếu muốn dùng `useState` trong một điều kiện hoặc vòng lặp, hãy tách ra thành component mới và đặt nó vào đó.

## Chia sẻ dữ liệu giữa các component {/*sharing-data-between-components*/}

Trong ví dụ trước, mỗi `MyButton` có `count` độc lập riêng, và khi từng nút được nhấp thì chỉ `count` của nút đó thay đổi:

<DiagramGroup>

<Diagram name="sharing_data_child" height={367} width={407} alt="Sơ đồ hiển thị một cây gồm ba component, một component cha tên MyApp và hai component con tên MyButton. Cả hai component MyButton đều có count bằng 0.">

Ban đầu, state `count` của mỗi `MyButton` là `0`

</Diagram>

<Diagram name="sharing_data_child_clicked" height={367} width={407} alt="Sơ đồ giống như trước, nhưng count của component con MyButton đầu tiên được làm nổi bật để biểu thị một lần nhấp và giá trị count đã tăng lên 1. Component MyButton thứ hai vẫn có giá trị 0." >

`MyButton` đầu tiên cập nhật `count` của nó lên `1`

</Diagram>

</DiagramGroup>

Tuy nhiên, trong nhiều trường hợp bạn sẽ cần các component *chia sẻ dữ liệu và luôn cập nhật cùng nhau*.

Để cả hai component `MyButton` hiển thị cùng một `count` và cập nhật cùng nhau, bạn cần chuyển state từ các nút riêng lẻ "lên trên" tới component gần nhất chứa tất cả chúng.

Trong ví dụ này, đó là `MyApp`:

<DiagramGroup>

<Diagram name="sharing_data_parent" height={385} width={410} alt="Sơ đồ hiển thị một cây gồm ba component, một component cha tên MyApp và hai component con tên MyButton. MyApp chứa giá trị count bằng 0 và truyền nó xuống cả hai component MyButton, mỗi component cũng hiển thị giá trị 0." >

Ban đầu, state `count` của `MyApp` là `0` và được truyền xuống cho cả hai component con

</Diagram>

<Diagram name="sharing_data_parent_clicked" height={385} width={410} alt="Sơ đồ giống như trước, nhưng count của component cha MyApp được làm nổi bật để biểu thị một lần nhấp và giá trị đã tăng lên 1. Luồng truyền xuống cả hai component con MyButton cũng được làm nổi bật, và giá trị count trong mỗi component con được đặt thành 1 để cho thấy giá trị đã được truyền xuống." >

Khi nhấp, `MyApp` cập nhật state `count` của nó lên `1` rồi truyền xuống cho cả hai component con

</Diagram>

</DiagramGroup>

Bây giờ khi bạn nhấp vào một trong hai nút, `count` trong `MyApp` sẽ thay đổi, và điều đó sẽ làm thay đổi cả hai giá trị count trong `MyButton`. Đây là cách bạn biểu diễn điều đó trong code.

Trước tiên, hãy *nâng state lên* từ `MyButton` vào `MyApp`:

```js {2-6,18}
export default function MyApp() {
  const [count, setCount] = useState(0);

  function handleClick() {
    setCount(count + 1);
  }

  return (
    <div>
      <h1>Counters that update separately</h1>
      <MyButton />
      <MyButton />
    </div>
  );
}

function MyButton() {
  // ... we're moving code from here ...
}

```

Sau đó, hãy *truyền state xuống* từ `MyApp` tới từng `MyButton`, cùng với trình xử lý nhấp dùng chung. Bạn có thể truyền thông tin vào `MyButton` bằng ngoặc nhọn JSX, giống như cách trước đó bạn đã làm với các thẻ dựng sẵn như `<img>`:

```js {11-12}
export default function MyApp() {
  const [count, setCount] = useState(0);

  function handleClick() {
    setCount(count + 1);
  }

  return (
    <div>
      <h1>Counters that update together</h1>
      <MyButton count={count} onClick={handleClick} />
      <MyButton count={count} onClick={handleClick} />
    </div>
  );
}
```

Thông tin bạn truyền xuống theo cách này được gọi là _props_. Bây giờ component `MyApp` chứa state `count` và trình xử lý sự kiện `handleClick`, rồi *truyền cả hai xuống dưới dưới dạng props* cho từng nút.

Cuối cùng, hãy sửa `MyButton` để *đọc* các props mà bạn đã truyền từ component cha của nó:

```js {1,3}
function MyButton({ count, onClick }) {
  return (
    <button onClick={onClick}>
      Clicked {count} times
    </button>
  );
}
```

Khi bạn nhấp vào nút, trình xử lý `onClick` sẽ chạy. Prop `onClick` của mỗi nút đều được đặt thành hàm `handleClick` bên trong `MyApp`, nên code bên trong hàm đó sẽ được thực thi. Đoạn code đó gọi `setCount(count + 1)`, làm tăng biến state `count`. Giá trị `count` mới được truyền làm prop tới từng nút, nên tất cả chúng đều hiển thị giá trị mới. Điều này được gọi là "lifting state up". Bằng cách nâng state lên trên, bạn đã chia sẻ nó giữa các component.

<Sandpack>

```js
import { useState } from 'react';

export default function MyApp() {
  const [count, setCount] = useState(0);

  function handleClick() {
    setCount(count + 1);
  }

  return (
    <div>
      <h1>Counters that update together</h1>
      <MyButton count={count} onClick={handleClick} />
      <MyButton count={count} onClick={handleClick} />
    </div>
  );
}

function MyButton({ count, onClick }) {
  return (
    <button onClick={onClick}>
      Clicked {count} times
    </button>
  );
}
```

```css
button {
  display: block;
  margin-bottom: 5px;
}
```

</Sandpack>

## Bước tiếp theo {/*next-steps*/}

Đến đây, bạn đã nắm được những điều cơ bản về cách viết code React!

Hãy xem [Hướng dẫn](/learn/tutorial-tic-tac-toe) để thực hành những kiến thức này và xây dựng ứng dụng mini đầu tiên của bạn với React.
