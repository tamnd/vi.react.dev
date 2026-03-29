---
title: Import và Export Thành Phần
---

<Intro>

Điều kỳ diệu của các thành phần nằm ở khả năng tái sử dụng: bạn có thể tạo ra những thành phần được ghép từ các thành phần khác. Nhưng khi bạn lồng ngày càng nhiều thành phần vào nhau, việc tách chúng ra các tệp khác nhau thường sẽ hợp lý hơn. Cách này giúp tệp của bạn dễ quét hơn và cho phép tái sử dụng thành phần ở nhiều nơi hơn.

</Intro>

<YouWillLearn>

* Root component file là gì
* Cách import và export một thành phần
* Khi nào nên dùng default import/export và named import/export
* Cách import và export nhiều thành phần từ cùng một tệp
* Cách tách các thành phần thành nhiều tệp

</YouWillLearn>

## Root component file {/*the-root-component-file*/}

Trong [Thành Phần Đầu Tiên Của Bạn](/learn/your-first-component), bạn đã tạo một thành phần `Profile` và một thành phần `Gallery` để kết xuất nó:

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

Hiện tại chúng cùng nằm trong một **root component file**, trong ví dụ này là `App.js`. Tùy vào cách bạn thiết lập, root component của bạn cũng có thể nằm ở một tệp khác. Ví dụ, nếu bạn dùng framework có file-based routing như Next.js, thì mỗi trang sẽ có một root component khác nhau.

## Export và import một thành phần {/*exporting-and-importing-a-component*/}

Điều gì sẽ xảy ra nếu sau này bạn muốn thay đổi màn hình đầu và đặt một danh sách sách khoa học ở đó? Hoặc đặt tất cả các hồ sơ sang nơi khác? Khi đó, việc chuyển `Gallery` và `Profile` ra khỏi root component file sẽ rất hợp lý. Điều này giúp chúng mô-đun hơn và tái sử dụng được ở các tệp khác. Bạn có thể di chuyển một thành phần theo ba bước:

1. **Tạo** một tệp JS mới để chứa các thành phần.
2. **Export** function component của bạn từ tệp đó bằng [default](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Statements/export#using_the_default_export) hoặc [named](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Statements/export#using_named_exports) exports.
3. **Import** nó vào tệp nơi bạn sẽ dùng thành phần bằng kỹ thuật import tương ứng cho [default](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Statements/import#importing_defaults) hoặc [named](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Statements/import#import_a_single_export_from_a_module) exports.

Ở đây, cả `Profile` lẫn `Gallery` đều đã được chuyển khỏi `App.js` sang một tệp mới tên là `Gallery.js`. Bây giờ bạn có thể đổi `App.js` để import `Gallery` từ `Gallery.js`:

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
   - Định nghĩa thành phần `Profile`, thành phần này chỉ được dùng trong cùng tệp và không được export.
   - Export thành phần `Gallery` dưới dạng **default export.**
2. `App.js`:
   - Import `Gallery` dưới dạng **default import** từ `Gallery.js`.
   - Export root component `App` dưới dạng **default export.**


<Note>

Bạn có thể gặp những tệp bỏ phần mở rộng `.js`, ví dụ như sau:

```js
import Gallery from './Gallery';
```

Cả `'./Gallery.js'` lẫn `'./Gallery'` đều hoạt động với React, nhưng cách đầu tiên gần với cách [native ES Modules](https://developer.mozilla.org/docs/Web/JavaScript/Guide/Modules) hoạt động hơn.

</Note>

<DeepDive>

#### Default export và named export {/*default-vs-named-exports*/}

JavaScript có hai cách chính để export giá trị: default export và named export. Từ đầu đến giờ, các ví dụ của chúng ta chỉ dùng default export. Nhưng bạn có thể dùng một hoặc cả hai kiểu trong cùng một tệp. **Một tệp chỉ được có tối đa một _default_ export, nhưng có thể có bao nhiêu _named_ exports tùy ý.**

![Default and named exports](/images/docs/illustrations/i_import-export.svg)

Cách bạn export thành phần quyết định cách bạn phải import nó. Bạn sẽ gặp lỗi nếu cố import một default export theo cách dành cho named export. Bảng sau sẽ giúp bạn theo dõi:

| Cú pháp | Câu lệnh export | Câu lệnh import |
| ----------- | ----------- | ----------- |
| Default | `export default function Button() {}` | `import Button from './Button.js';` |
| Named | `export function Button() {}` | `import { Button } from './Button.js';` |

Khi viết _default_ import, bạn có thể đặt bất kỳ tên nào bạn muốn sau `import`. Ví dụ, bạn có thể viết `import Banana from './Button.js'` và nó vẫn nhận đúng default export đó. Ngược lại, với named import, tên phải khớp ở cả hai phía. Đó là lý do chúng được gọi là _named_ imports.

**Mọi người thường dùng default export nếu tệp chỉ export một thành phần, và dùng named export nếu tệp export nhiều thành phần hoặc giá trị.** Dù bạn thích phong cách nào, hãy luôn đặt tên có ý nghĩa cho function component và cho các tệp chứa chúng. Những thành phần không có tên, chẳng hạn `export default () => {}`, thường không được khuyến khích vì chúng khiến việc gỡ lỗi khó hơn.

</DeepDive>

## Export và import nhiều thành phần từ cùng một tệp {/*exporting-and-importing-multiple-components-from-the-same-file*/}

Nếu bạn chỉ muốn hiển thị một `Profile` thay vì cả một gallery thì sao? Bạn cũng có thể export thành phần `Profile`. Nhưng `Gallery.js` đã có một *default* export rồi, và bạn không thể có _hai_ default exports. Bạn có thể tạo một tệp mới với default export, hoặc thêm một *named* export cho `Profile`. **Một tệp chỉ có thể có một default export, nhưng có thể có rất nhiều named exports!**

<Note>

Để giảm bớt sự nhầm lẫn giữa default export và named export, một số đội chọn chỉ dùng một kiểu duy nhất hoặc tránh trộn cả hai kiểu trong cùng một tệp. Hãy chọn cách phù hợp nhất với bạn.

</Note>

Đầu tiên, hãy **export** `Profile` từ `Gallery.js` bằng named export, không có từ khóa `default`:

```js
export function Profile() {
  // ...
}
```

Sau đó, hãy **import** `Profile` từ `Gallery.js` vào `App.js` bằng named import, với dấu ngoặc nhọn:

```js
import { Profile } from './Gallery.js';
```

Cuối cùng, hãy **kết xuất** `<Profile />` từ thành phần `App`:

```js
export default function App() {
  return <Profile />;
}
```

Bây giờ `Gallery.js` chứa hai export: default export là `Gallery`, và named export là `Profile`. `App.js` import cả hai. Hãy thử sửa `<Profile />` thành `<Gallery />` rồi đổi lại trong ví dụ này:

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

Bây giờ bạn đang dùng kết hợp cả default export lẫn named export:

* `Gallery.js`:
  - Export thành phần `Profile` dưới dạng **named export có tên `Profile`.**
  - Export thành phần `Gallery` dưới dạng **default export.**
* `App.js`:
  - Import `Profile` dưới dạng **named import có tên `Profile`** từ `Gallery.js`.
  - Import `Gallery` dưới dạng **default import** từ `Gallery.js`.
  - Export root component `App` dưới dạng **default export.**

<Recap>

Trên trang này bạn đã học được:

* Root component file là gì
* Cách import và export một thành phần
* Khi nào và cách dùng default import/export và named import/export
* Cách export nhiều thành phần từ cùng một tệp

</Recap>



<Challenges>

#### Tách các thành phần xa hơn nữa {/*split-the-components-further*/}

Hiện tại `Gallery.js` export cả `Profile` lẫn `Gallery`, điều này hơi gây nhầm lẫn.

Hãy chuyển thành phần `Profile` sang tệp riêng `Profile.js`, rồi thay đổi thành phần `App` để kết xuất cả `<Profile />` và `<Gallery />` lần lượt.

Bạn có thể dùng default export hoặc named export cho `Profile`, nhưng hãy chắc chắn rằng bạn dùng cú pháp import tương ứng trong cả `App.js` lẫn `Gallery.js`. Bạn có thể xem lại bảng trong phần đào sâu ở trên:

| Cú pháp | Câu lệnh export | Câu lệnh import |
| ----------- | ----------- | ----------- |
| Default | `export default function Button() {}` | `import Button from './Button.js';` |
| Named | `export function Button() {}` | `import { Button } from './Button.js';` |

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
