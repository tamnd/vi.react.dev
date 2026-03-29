---
title: Mô tả UI
---

<Intro>

React là một thư viện JavaScript để kết xuất giao diện người dùng (UI). UI được tạo nên từ những đơn vị nhỏ như nút bấm, văn bản và hình ảnh. React cho phép bạn kết hợp chúng thành các *thành phần* có thể tái sử dụng và lồng vào nhau. Từ trang web đến ứng dụng điện thoại, mọi thứ trên màn hình đều có thể được chia nhỏ thành các thành phần. Trong chương này, bạn sẽ học cách tạo, tùy chỉnh và hiển thị có điều kiện các thành phần React.

</Intro>

<YouWillLearn isChapter={true}>

* [Cách viết thành phần React đầu tiên của bạn](/learn/your-first-component)
* [Khi nào và cách tạo tệp chứa nhiều thành phần](/learn/importing-and-exporting-components)
* [Cách thêm markup vào JavaScript bằng JSX](/learn/writing-markup-with-jsx)
* [Cách dùng dấu ngoặc nhọn với JSX để truy cập khả năng của JavaScript từ thành phần của bạn](/learn/javascript-in-jsx-with-curly-braces)
* [Cách cấu hình thành phần bằng props](/learn/passing-props-to-a-component)
* [Cách kết xuất có điều kiện các thành phần](/learn/conditional-rendering)
* [Cách kết xuất nhiều thành phần cùng lúc](/learn/rendering-lists)
* [Cách tránh những lỗi khó hiểu bằng việc giữ thành phần thuần](/learn/keeping-components-pure)
* [Vì sao việc hiểu UI của bạn như những cây lại hữu ích](/learn/understanding-your-ui-as-a-tree)

</YouWillLearn>

## Thành phần đầu tiên của bạn {/*your-first-component*/}

Ứng dụng React được xây dựng từ các phần UI tách biệt gọi là *thành phần*. Một thành phần React là một hàm JavaScript mà bạn có thể rắc thêm markup vào. Thành phần có thể nhỏ như một nút bấm, hoặc lớn như cả một trang hoàn chỉnh. Đây là thành phần `Gallery` đang kết xuất ba thành phần `Profile`:

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

<LearnMore path="/learn/your-first-component">

Đọc **[Thành phần đầu tiên của bạn](/learn/your-first-component)** để tìm hiểu cách khai báo và sử dụng thành phần React.

</LearnMore>

## Import và export thành phần {/*importing-and-exporting-components*/}

Bạn có thể khai báo nhiều thành phần trong một tệp, nhưng các tệp lớn sẽ khó theo dõi. Để giải quyết điều này, bạn có thể *export* một thành phần ra tệp riêng, rồi *import* thành phần đó từ một tệp khác:


<Sandpack>

```js src/App.js hidden
import Gallery from './Gallery.js';

export default function App() {
  return (
    <Gallery />
  );
}
```

```js src/Gallery.js active
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
img { margin: 0 10px 10px 0; }
```

</Sandpack>

<LearnMore path="/learn/importing-and-exporting-components">

Đọc **[Import và Export Thành phần](/learn/importing-and-exporting-components)** để tìm hiểu cách tách thành phần ra các tệp riêng.

</LearnMore>

## Viết markup với JSX {/*writing-markup-with-jsx*/}

Mỗi thành phần React là một hàm JavaScript có thể chứa một ít markup mà React sẽ kết xuất vào trình duyệt. Thành phần React dùng một phần mở rộng cú pháp có tên JSX để biểu diễn markup đó. JSX trông khá giống HTML, nhưng chặt chẽ hơn một chút và có thể hiển thị thông tin động.

Nếu dán markup HTML sẵn có vào một thành phần React, không phải lúc nào nó cũng hoạt động:

<Sandpack>

```js
export default function TodoList() {
  return (
    // This doesn't quite work!
    <h1>Hedy Lamarr's Todos</h1>
    <img
      src="https://i.imgur.com/yXOvdOSs.jpg"
      alt="Hedy Lamarr"
      class="photo"
    >
    <ul>
      <li>Invent new traffic lights
      <li>Rehearse a movie scene
      <li>Improve spectrum technology
    </ul>
  );
}
```

```css
img { height: 90px; }
```

</Sandpack>

Nếu bạn có HTML sẵn như vậy, bạn có thể sửa nó bằng [trình chuyển đổi](https://transform.tools/html-to-jsx):

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
        <li>Improve spectrum technology</li>
      </ul>
    </>
  );
}
```

```css
img { height: 90px; }
```

</Sandpack>

<LearnMore path="/learn/writing-markup-with-jsx">

Đọc **[Viết Markup với JSX](/learn/writing-markup-with-jsx)** để tìm hiểu cách viết JSX hợp lệ.

</LearnMore>

## JavaScript trong JSX với dấu ngoặc nhọn {/*javascript-in-jsx-with-curly-braces*/}

JSX cho phép bạn viết markup giống HTML bên trong tệp JavaScript, giữ logic kết xuất và nội dung ở cùng một chỗ. Đôi khi bạn sẽ muốn thêm một ít logic JavaScript hoặc tham chiếu tới một thuộc tính động trong markup đó. Khi đó, bạn có thể dùng dấu ngoặc nhọn trong JSX để "mở một cửa sổ" sang JavaScript:

<Sandpack>

```js
const person = {
  name: 'Gregorio Y. Zara',
  theme: {
    backgroundColor: 'black',
    color: 'pink'
  }
};

export default function TodoList() {
  return (
    <div style={person.theme}>
      <h1>{person.name}'s Todos</h1>
      <img
        className="avatar"
        src="https://i.imgur.com/7vQD0fPs.jpg"
        alt="Gregorio Y. Zara"
      />
      <ul>
        <li>Improve the videophone</li>
        <li>Prepare aeronautics lectures</li>
        <li>Work on the alcohol-fuelled engine</li>
      </ul>
    </div>
  );
}
```

```css
body { padding: 0; margin: 0 }
body > div > div { padding: 20px; }
.avatar { border-radius: 50%; height: 90px; }
```

</Sandpack>

<LearnMore path="/learn/javascript-in-jsx-with-curly-braces">

Đọc **[JavaScript trong JSX với Dấu ngoặc nhọn](/learn/javascript-in-jsx-with-curly-braces)** để tìm hiểu cách truy cập dữ liệu JavaScript từ JSX.

</LearnMore>

## Truyền props cho thành phần {/*passing-props-to-a-component*/}

Các thành phần React dùng *props* để giao tiếp với nhau. Mỗi thành phần cha có thể truyền một ít thông tin cho các thành phần con bằng cách cung cấp props cho chúng. Props có thể khiến bạn liên tưởng đến thuộc tính HTML, nhưng bạn có thể truyền qua đó bất kỳ giá trị JavaScript nào, bao gồm đối tượng, mảng, hàm và cả JSX!

<Sandpack>

```js
import { getImageUrl } from './utils.js'

export default function Profile() {
  return (
    <Card>
      <Avatar
        size={100}
        person={{
          name: 'Katsuko Saruhashi',
          imageId: 'YfeOqp2'
        }}
      />
    </Card>
  );
}

function Avatar({ person, size }) {
  return (
    <img
      className="avatar"
      src={getImageUrl(person)}
      alt={person.name}
      width={size}
      height={size}
    />
  );
}

function Card({ children }) {
  return (
    <div className="card">
      {children}
    </div>
  );
}

```

```js src/utils.js
export function getImageUrl(person, size = 's') {
  return (
    'https://i.imgur.com/' +
    person.imageId +
    size +
    '.jpg'
  );
}
```

```css
.card {
  width: fit-content;
  margin: 5px;
  padding: 5px;
  font-size: 20px;
  text-align: center;
  border: 1px solid #aaa;
  border-radius: 20px;
  background: #fff;
}
.avatar {
  margin: 20px;
  border-radius: 50%;
}
```

</Sandpack>

<LearnMore path="/learn/passing-props-to-a-component">

Đọc **[Truyền Props cho Thành phần](/learn/passing-props-to-a-component)** để tìm hiểu cách truyền và đọc props.

</LearnMore>

## Kết xuất có điều kiện {/*conditional-rendering*/}

Các thành phần của bạn thường sẽ cần hiển thị những thứ khác nhau tùy theo điều kiện khác nhau. Trong React, bạn có thể kết xuất JSX có điều kiện bằng cú pháp JavaScript như câu lệnh `if`, toán tử `&&` và `? :`.

Trong ví dụ này, toán tử JavaScript `&&` được dùng để kết xuất dấu kiểm một cách có điều kiện:

<Sandpack>

```js
function Item({ name, isPacked }) {
  return (
    <li className="item">
      {name} {isPacked && '✅'}
    </li>
  );
}

export default function PackingList() {
  return (
    <section>
      <h1>Sally Ride's Packing List</h1>
      <ul>
        <Item
          isPacked={true}
          name="Space suit"
        />
        <Item
          isPacked={true}
          name="Helmet with a golden leaf"
        />
        <Item
          isPacked={false}
          name="Photo of Tam"
        />
      </ul>
    </section>
  );
}
```

</Sandpack>

<LearnMore path="/learn/conditional-rendering">

Đọc **[Kết xuất Có điều kiện](/learn/conditional-rendering)** để tìm hiểu các cách khác nhau để kết xuất nội dung có điều kiện.

</LearnMore>

## Kết xuất danh sách {/*rendering-lists*/}

Bạn sẽ thường muốn hiển thị nhiều thành phần tương tự nhau từ một tập dữ liệu. Bạn có thể dùng `filter()` và `map()` của JavaScript cùng với React để lọc và biến đổi mảng dữ liệu của mình thành một mảng các thành phần.

Với mỗi phần tử trong mảng, bạn cần chỉ định một `key`. Thông thường, bạn sẽ muốn dùng một ID từ cơ sở dữ liệu làm `key`. Key cho phép React theo dõi vị trí của từng phần tử trong danh sách ngay cả khi danh sách thay đổi.

<Sandpack>

```js src/App.js
import { people } from './data.js';
import { getImageUrl } from './utils.js';

export default function List() {
  const listItems = people.map(person =>
    <li key={person.id}>
      <img
        src={getImageUrl(person)}
        alt={person.name}
      />
      <p>
        <b>{person.name}:</b>
        {' ' + person.profession + ' '}
        known for {person.accomplishment}
      </p>
    </li>
  );
  return (
    <article>
      <h1>Scientists</h1>
      <ul>{listItems}</ul>
    </article>
  );
}
```

```js src/data.js
export const people = [{
  id: 0,
  name: 'Creola Katherine Johnson',
  profession: 'mathematician',
  accomplishment: 'spaceflight calculations',
  imageId: 'MK3eW3A'
}, {
  id: 1,
  name: 'Mario José Molina-Pasquel Henríquez',
  profession: 'chemist',
  accomplishment: 'discovery of Arctic ozone hole',
  imageId: 'mynHUSa'
}, {
  id: 2,
  name: 'Mohammad Abdus Salam',
  profession: 'physicist',
  accomplishment: 'electromagnetism theory',
  imageId: 'bE7W1ji'
}, {
  id: 3,
  name: 'Percy Lavon Julian',
  profession: 'chemist',
  accomplishment: 'pioneering cortisone drugs, steroids and birth control pills',
  imageId: 'IOjWm71'
}, {
  id: 4,
  name: 'Subrahmanyan Chandrasekhar',
  profession: 'astrophysicist',
  accomplishment: 'white dwarf star mass calculations',
  imageId: 'lrWQx8l'
}];
```

```js src/utils.js
export function getImageUrl(person) {
  return (
    'https://i.imgur.com/' +
    person.imageId +
    's.jpg'
  );
}
```

```css
ul { list-style-type: none; padding: 0px 10px; }
li {
  margin-bottom: 10px;
  display: grid;
  grid-template-columns: 1fr 1fr;
  align-items: center;
}
img { width: 100px; height: 100px; border-radius: 50%; }
h1 { font-size: 22px; }
h2 { font-size: 20px; }
```

</Sandpack>

<LearnMore path="/learn/rendering-lists">

Đọc **[Kết xuất Danh sách](/learn/rendering-lists)** để tìm hiểu cách kết xuất danh sách thành phần và cách chọn `key`.

</LearnMore>

## Giữ thành phần thuần {/*keeping-components-pure*/}

Một số hàm JavaScript là *thuần*. Một hàm thuần:

* **Chỉ lo việc của nó.** Nó không thay đổi bất kỳ đối tượng hoặc biến nào đã tồn tại trước khi được gọi.
* **Cùng đầu vào, cùng đầu ra.** Với cùng đầu vào, một hàm thuần phải luôn trả về cùng một kết quả.

Bằng cách nghiêm ngặt chỉ viết các thành phần của bạn như những hàm thuần, bạn có thể tránh được cả một nhóm lỗi khó hiểu và hành vi khó đoán khi codebase ngày càng lớn. Đây là một ví dụ về thành phần không thuần:

<Sandpack>

```js {expectedErrors: {'react-compiler': [5]}}
let guest = 0;

function Cup() {
  // Bad: changing a preexisting variable!
  guest = guest + 1;
  return <h2>Tea cup for guest #{guest}</h2>;
}

export default function TeaSet() {
  return (
    <>
      <Cup />
      <Cup />
      <Cup />
    </>
  );
}
```

</Sandpack>

Bạn có thể làm cho thành phần này trở nên thuần bằng cách truyền một prop thay vì sửa đổi một biến đã tồn tại từ trước:

<Sandpack>

```js
function Cup({ guest }) {
  return <h2>Tea cup for guest #{guest}</h2>;
}

export default function TeaSet() {
  return (
    <>
      <Cup guest={1} />
      <Cup guest={2} />
      <Cup guest={3} />
    </>
  );
}
```

</Sandpack>

<LearnMore path="/learn/keeping-components-pure">

Đọc **[Giữ Thành phần thuần](/learn/keeping-components-pure)** để tìm hiểu cách viết thành phần như những hàm thuần, dễ đoán.

</LearnMore>

## UI của bạn như một cái cây {/*your-ui-as-a-tree*/}

React dùng cây để mô hình hóa mối quan hệ giữa các thành phần và module.

Cây kết xuất của React là biểu diễn mối quan hệ cha con giữa các thành phần.

<Diagram name="generic_render_tree" height={250} width={500} alt="Một sơ đồ cây có năm nút, mỗi nút đại diện cho một thành phần. Nút gốc nằm ở đỉnh sơ đồ cây và được gắn nhãn 'Root Component'. Từ đó có hai mũi tên kéo xuống hai nút mang nhãn 'Component A' và 'Component C'. Mỗi mũi tên đều có nhãn 'renders'. 'Component A' có một mũi tên 'renders' trỏ tới nút mang nhãn 'Component B'. 'Component C' có một mũi tên 'renders' trỏ tới nút mang nhãn 'Component D'.">

Ví dụ về cây kết xuất React.

</Diagram>

Các thành phần ở gần đỉnh cây, gần thành phần gốc, được xem là các thành phần cấp cao nhất. Những thành phần không có thành phần con là các thành phần lá. Việc phân loại này hữu ích để hiểu luồng dữ liệu và hiệu năng kết xuất.

Mô hình hóa mối quan hệ giữa các module JavaScript là một cách hữu ích khác để hiểu ứng dụng của bạn. Chúng tôi gọi đó là cây phụ thuộc module.

<Diagram name="generic_dependency_tree" height={250} width={500} alt="Một sơ đồ cây có năm nút. Mỗi nút đại diện cho một module JavaScript. Nút trên cùng được gắn nhãn 'RootModule.js'. Từ đó có ba mũi tên trỏ tới các nút: 'ModuleA.js', 'ModuleB.js' và 'ModuleC.js'. Mỗi mũi tên đều có nhãn 'imports'. Nút 'ModuleC.js' có một mũi tên 'imports' trỏ tới nút mang nhãn 'ModuleD.js'.">

Ví dụ về cây phụ thuộc module.

</Diagram>

Cây phụ thuộc thường được các công cụ build dùng để đóng gói toàn bộ mã JavaScript liên quan để client tải về và kết xuất. Kích thước bundle lớn làm suy giảm trải nghiệm người dùng của ứng dụng React. Hiểu cây phụ thuộc module sẽ giúp bạn gỡ lỗi những vấn đề như vậy.

<LearnMore path="/learn/understanding-your-ui-as-a-tree">

Đọc **[UI của bạn như một Cái cây](/learn/understanding-your-ui-as-a-tree)** để tìm hiểu cách tạo cây kết xuất và cây phụ thuộc module cho ứng dụng React, cũng như vì sao chúng là những mô hình tư duy hữu ích để cải thiện trải nghiệm người dùng và hiệu năng.

</LearnMore>


## Tiếp theo là gì? {/*whats-next*/}

Hãy chuyển sang [Thành phần đầu tiên của bạn](/learn/your-first-component) để bắt đầu đọc chương này theo từng trang!

Hoặc, nếu bạn đã quen với những chủ đề này, hãy đọc [Thêm tính tương tác](/learn/adding-interactivity).
