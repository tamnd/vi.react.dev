---
title: Import và Export Thành phần
---

<Intro>

Sức mạnh của thành phần nằm ở khả năng tái sử dụng: bạn có thể tạo các thành phần được ghép từ những thành phần khác. Nhưng khi bạn lồng ngày càng nhiều thành phần, thường sẽ hợp lý hơn nếu bắt đầu tách chúng ra các tệp khác nhau. Điều này giúp tệp của bạn dễ theo dõi hơn và cho phép tái sử dụng thành phần ở nhiều nơi hơn.

</Intro>

<YouWillLearn>

* Tệp thành phần gốc là gì
* Cách import và export một thành phần
* Khi nào nên dùng import và export mặc định hoặc có tên
* Cách import và export nhiều thành phần từ cùng một tệp
* Cách tách thành phần thành nhiều tệp

</YouWillLearn>

## Tệp thành phần gốc {/*the-root-component-file*/}

Trong [Thành phần đầu tiên của bạn](/learn/your-first-component), bạn đã tạo một thành phần `Profile` và một thành phần `Gallery` để kết xuất nó:

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

Hiện tại chúng nằm trong **tệp thành phần gốc,** có tên là `App.js` trong ví dụ này. Tuy vậy, tùy vào cách bạn thiết lập mà thành phần gốc có thể nằm ở một tệp khác. Nếu bạn dùng framework có định tuyến dựa trên tệp, chẳng hạn Next.js, thành phần gốc của bạn sẽ khác nhau ở mỗi trang.

## Export và import một thành phần {/*exporting-and-importing-a-component*/}

Nếu sau này bạn muốn thay đổi màn hình đầu tiên và đặt một danh sách sách khoa học ở đó thì sao? Hoặc muốn đặt toàn bộ hồ sơ ở nơi khác? Khi đó, sẽ hợp lý nếu chuyển `Gallery` và `Profile` ra khỏi tệp thành phần gốc. Cách này giúp chúng mô-đun hơn và có thể tái sử dụng trong các tệp khác. Bạn có thể chuyển một thành phần theo ba bước:

1. **Tạo** một tệp JS mới để đặt các thành phần vào đó.
2. **Export** thành phần hàm của bạn từ tệp đó (dùng [default](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Statements/export#using_the_default_export) hoặc [named](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Statements/export#using_named_exports) exports).
3. **Import** nó trong tệp nơi bạn sẽ dùng thành phần đó (bằng cách import tương ứng với [default](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Statements/import#importing_defaults) hoặc [named](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Statements/import#import_a_single_export_from_a_module) exports).

Ở đây cả `Profile` và `Gallery` đã được chuyển ra khỏi `App.js` vào một tệp mới tên là `Gallery.js`. Bây giờ bạn có thể thay đổi `App.js` để import `Gallery` từ `Gallery.js`:

<Sandpack>

```js src/App.js
import Gallery from './Gallery.js';

export default function App() {
  return (
    <Gallery />
  );
}
```

```js src/Gallery.js
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
img { margin: 0 10px 10px 0; height: 90px; }
```

</Sandpack>

Hãy để ý rằng ví dụ này giờ đã được tách thành hai tệp thành phần:

1. `Gallery.js`:
   - Định nghĩa thành phần `Profile`, chỉ được dùng trong cùng tệp nên không được export.
   - Export thành phần `Gallery` dưới dạng **default export.**
2. `App.js`:
   - Import `Gallery` dưới dạng **default import** từ `Gallery.js`.
   - Export thành phần gốc `App` dưới dạng **default export.**


<Note>

Bạn có thể gặp những tệp không ghi phần mở rộng `.js` như sau:

```js 
import Gallery from './Gallery';
```

`'./Gallery.js'` hoặc `'./Gallery'` đều hoạt động với React, dù cách thứ nhất gần với cách [ES Modules gốc](https://developer.mozilla.org/docs/Web/JavaScript/Guide/Modules) vận hành hơn.

</Note>

<DeepDive>

#### `default` so với export có tên {/*default-vs-named-exports*/}

Có hai cách chính để export giá trị trong JavaScript: default exports và named exports. Cho đến lúc này, các ví dụ của chúng ta chỉ dùng default exports. Nhưng bạn có thể dùng một hoặc cả hai kiểu trong cùng một tệp. **Một tệp chỉ có tối đa một _default_ export, nhưng có thể có bao nhiêu _named_ exports cũng được.**

![Default and named exports](/images/docs/illustrations/i_import-export.svg)

Cách bạn export thành phần sẽ quyết định cách bạn phải import nó. Bạn sẽ gặp lỗi nếu cố import một default export giống như cách import named export! Bảng này sẽ giúp bạn dễ theo dõi hơn:

| Syntax           | Export statement                           | Import statement                          |
| -----------      | -----------                                | -----------                               |
| Default  | `export default function Button() {}` | `import Button from './Button.js';`     |
| Named    | `export function Button() {}`         | `import { Button } from './Button.js';` |

Khi viết một _default_ import, bạn có thể đặt bất kỳ tên nào mình muốn sau `import`. Ví dụ, bạn có thể viết `import Banana from './Button.js'` và nó vẫn nhận cùng một default export. Ngược lại, với named imports, tên phải khớp ở cả hai phía. Đó là lý do chúng được gọi là _named_ imports!

**Mọi người thường dùng default exports nếu tệp chỉ export một thành phần, và dùng named exports nếu tệp export nhiều thành phần hoặc giá trị.** Dù bạn thích phong cách code nào, hãy luôn đặt tên có ý nghĩa cho các hàm thành phần và những tệp chứa chúng. Các thành phần không có tên, như `export default () => {}`, không được khuyến khích vì khiến việc gỡ lỗi khó hơn.

</DeepDive>

## Export và import nhiều thành phần từ cùng một tệp {/*exporting-and-importing-multiple-components-from-the-same-file*/}

Nếu bạn chỉ muốn hiển thị một `Profile` thay vì cả gallery thì sao? Bạn cũng có thể export thành phần `Profile`. Nhưng `Gallery.js` đã có một *default* export rồi, và bạn không thể có _hai_ default exports. Bạn có thể tạo một tệp mới với default export, hoặc thêm một *named* export cho `Profile`. **Một tệp chỉ có thể có một default export, nhưng có thể có rất nhiều named exports!**

<Note>

Để giảm khả năng nhầm lẫn giữa default và named exports, một số đội chọn chỉ dùng một kiểu (default hoặc named), hoặc tránh trộn cả hai trong cùng một tệp. Hãy làm theo cách phù hợp nhất với bạn!

</Note>

Trước tiên, hãy **export** `Profile` từ `Gallery.js` bằng named export (không dùng từ khóa `default`):

```js
export function Profile() {
  // ...
}
```

Sau đó, **import** `Profile` từ `Gallery.js` vào `App.js` bằng named import (có dấu ngoặc nhọn):

```js
import { Profile } from './Gallery.js';
```

Cuối cùng, hãy **kết xuất** `<Profile />` từ thành phần `App`:

```js
export default function App() {
  return <Profile />;
}
```

Bây giờ `Gallery.js` chứa hai exports: một default export là `Gallery`, và một named export là `Profile`. `App.js` import cả hai. Hãy thử sửa `<Profile />` thành `<Gallery />` rồi đổi lại trong ví dụ này:

<Sandpack>

```js src/App.js
import Gallery from './Gallery.js';
import { Profile } from './Gallery.js';

export default function App() {
  return (
    <Profile />
  );
}
```

```js src/Gallery.js
export function Profile() {
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
img { margin: 0 10px 10px 0; height: 90px; }
```

</Sandpack>

Bây giờ bạn đang dùng kết hợp default exports và named exports:

* `Gallery.js`:
  - Export thành phần `Profile` dưới dạng **named export tên là `Profile`.**
  - Export thành phần `Gallery` dưới dạng **default export.**
* `App.js`:
  - Import `Profile` dưới dạng **named import tên là `Profile`** từ `Gallery.js`.
  - Import `Gallery` dưới dạng **default import** từ `Gallery.js`.
  - Export thành phần gốc `App` dưới dạng **default export.**

<Recap>

Trên trang này bạn đã học được:

* Tệp thành phần gốc là gì
* Cách import và export một thành phần
* Khi nào và cách dùng import và export mặc định hoặc có tên
* Cách export nhiều thành phần từ cùng một tệp

</Recap>



<Challenges>

#### Tách các thành phần thêm nữa {/*split-the-components-further*/}

Hiện tại, `Gallery.js` export cả `Profile` và `Gallery`, điều này hơi dễ gây nhầm lẫn.

Hãy chuyển thành phần `Profile` sang tệp `Profile.js` riêng của nó, rồi thay đổi thành phần `App` để kết xuất cả `<Profile />` và `<Gallery />` lần lượt.

Bạn có thể dùng default export hoặc named export cho `Profile`, nhưng hãy đảm bảo rằng bạn dùng cú pháp import tương ứng trong cả `App.js` lẫn `Gallery.js`! Bạn có thể tham khảo bảng trong phần đọc sâu bên trên:

| Syntax           | Export statement                           | Import statement                          |
| -----------      | -----------                                | -----------                               |
| Default  | `export default function Button() {}` | `import Button from './Button.js';`     |
| Named    | `export function Button() {}`         | `import { Button } from './Button.js';` |

<Hint>

Đừng quên import các thành phần ở nơi chúng được gọi đến. `Gallery` cũng dùng `Profile`, đúng không?

</Hint>

<Sandpack>

```js src/App.js
import Gallery from './Gallery.js';
import { Profile } from './Gallery.js';

export default function App() {
  return (
    <div>
      <Profile />
    </div>
  );
}
```

```js src/Gallery.js active
// Move me to Profile.js!
export function Profile() {
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

```js src/Profile.js
```

```css
img { margin: 0 10px 10px 0; height: 90px; }
```

</Sandpack>

Sau khi làm cho nó chạy được với một kiểu export, hãy thử làm cho nó chạy với kiểu còn lại.

<Solution>

Đây là lời giải với named exports:

<Sandpack>

```js src/App.js
import Gallery from './Gallery.js';
import { Profile } from './Profile.js';

export default function App() {
  return (
    <div>
      <Profile />
      <Gallery />
    </div>
  );
}
```

```js src/Gallery.js
import { Profile } from './Profile.js';

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

```js src/Profile.js
export function Profile() {
  return (
    <img
      src="https://i.imgur.com/QIrZWGIs.jpg"
      alt="Alan L. Hart"
    />
  );
}
```

```css
img { margin: 0 10px 10px 0; height: 90px; }
```

</Sandpack>

Đây là lời giải với default exports:

<Sandpack>

```js src/App.js
import Gallery from './Gallery.js';
import Profile from './Profile.js';

export default function App() {
  return (
    <div>
      <Profile />
      <Gallery />
    </div>
  );
}
```

```js src/Gallery.js
import Profile from './Profile.js';

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

```js src/Profile.js
export default function Profile() {
  return (
    <img
      src="https://i.imgur.com/QIrZWGIs.jpg"
      alt="Alan L. Hart"
    />
  );
}
```

```css
img { margin: 0 10px 10px 0; height: 90px; }
```

</Sandpack>

</Solution>

</Challenges>
