---
title: preconnect
---

<Intro>

`preconnect` cho phép bạn chủ động kết nối sớm tới một server mà bạn dự kiến sẽ tải tài nguyên từ đó.

```js
preconnect("https://example.com");
```

</Intro>

<InlineToc />

---

## Reference {/*reference*/}

### `preconnect(href)` {/*preconnect*/}

Để preconnect tới một host, hãy gọi hàm `preconnect` từ `react-dom`.

```js
import { preconnect } from 'react-dom';

function AppRoot() {
  preconnect("https://example.com");
  // ...
}

```

[Xem thêm ví dụ ở bên dưới.](#usage)

Hàm `preconnect` cung cấp cho trình duyệt một gợi ý rằng nó nên mở kết nối tới server được chỉ định. Nếu trình duyệt chọn làm như vậy, việc này có thể tăng tốc độ tải tài nguyên từ server đó.

#### Parameters {/*parameters*/}

* `href`: một chuỗi. URL của server mà bạn muốn kết nối tới.


#### Returns {/*returns*/}

`preconnect` không trả về gì.

#### Caveats {/*caveats*/}

* Gọi `preconnect` nhiều lần với cùng một server có cùng hiệu ứng như một lần gọi duy nhất.
* Trong trình duyệt, bạn có thể gọi `preconnect` ở bất kỳ đâu: khi render component, trong một Effect, trong event handler, v.v.
* Trong server-side rendering hoặc khi render Server Components, `preconnect` chỉ có tác dụng nếu bạn gọi nó trong lúc render một component hoặc trong một ngữ cảnh async bắt nguồn từ việc render component. Mọi lời gọi khác sẽ bị bỏ qua.
* Nếu bạn biết tài nguyên cụ thể mình sẽ cần, bạn có thể gọi [các hàm khác](/reference/react-dom/#resource-preloading-apis) để bắt đầu tải chúng ngay lập tức.
* Không có lợi ích gì khi preconnect tới cùng một server đang host chính trang web, vì tới lúc gợi ý được đưa ra thì kết nối đó đã tồn tại rồi.

---

## Usage {/*usage*/}

### Preconnect khi render {/*preconnecting-when-rendering*/}

Hãy gọi `preconnect` khi render một component nếu bạn biết rằng các component con của nó sẽ tải tài nguyên bên ngoài từ host đó.

```js
import { preconnect } from 'react-dom';

function AppRoot() {
  preconnect("https://example.com");
  return ...;
}
```

### Preconnect trong event handler {/*preconnecting-in-an-event-handler*/}

Hãy gọi `preconnect` trong event handler trước khi chuyển sang một trang hoặc trạng thái cần đến tài nguyên bên ngoài. Việc này khởi động quá trình sớm hơn so với việc gọi nó trong lúc render trang hoặc trạng thái mới.

```js
import { preconnect } from 'react-dom';

function CallToAction() {
  const onClick = () => {
    preconnect('http://example.com');
    startWizard();
  }
  return (
    <button onClick={onClick}>Start Wizard</button>
  );
}
```
