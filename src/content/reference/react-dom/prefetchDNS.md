---
title: prefetchDNS
---

<Intro>

`prefetchDNS` cho phép bạn chủ động tra cứu sớm địa chỉ IP của một server mà bạn dự kiến sẽ tải tài nguyên từ đó.

```js
prefetchDNS("https://example.com");
```

</Intro>

<InlineToc />

---

## Reference {/*reference*/}

### `prefetchDNS(href)` {/*prefetchdns*/}

Để tra cứu một host, hãy gọi hàm `prefetchDNS` từ `react-dom`.

```js
import { prefetchDNS } from 'react-dom';

function AppRoot() {
  prefetchDNS("https://example.com");
  // ...
}

```

[Xem thêm ví dụ ở bên dưới.](#usage)

Hàm `prefetchDNS` cung cấp cho trình duyệt một gợi ý rằng nó nên tra cứu địa chỉ IP của server được chỉ định. Nếu trình duyệt chọn làm như vậy, việc này có thể tăng tốc độ tải tài nguyên từ server đó.

#### Parameters {/*parameters*/}

* `href`: một chuỗi. URL của server mà bạn muốn kết nối tới.

#### Returns {/*returns*/}

`prefetchDNS` không trả về gì.

#### Caveats {/*caveats*/}

* Gọi `prefetchDNS` nhiều lần với cùng một server có cùng hiệu ứng như một lần gọi duy nhất.
* Trong trình duyệt, bạn có thể gọi `prefetchDNS` ở bất kỳ đâu: khi render component, trong một Effect, trong event handler, v.v.
* Trong server-side rendering hoặc khi render Server Components, `prefetchDNS` chỉ có tác dụng nếu bạn gọi nó trong lúc render một component hoặc trong một ngữ cảnh async bắt nguồn từ việc render component. Mọi lời gọi khác sẽ bị bỏ qua.
* Nếu bạn biết tài nguyên cụ thể mình sẽ cần, bạn có thể gọi [các hàm khác](/reference/react-dom/#resource-preloading-apis) để bắt đầu tải chúng ngay lập tức.
* Không có lợi ích gì khi prefetch cùng một server đang host chính trang web, vì tới lúc gợi ý được đưa ra thì nó đã được tra cứu rồi.
* So với [`preconnect`](/reference/react-dom/preconnect), `prefetchDNS` có thể phù hợp hơn nếu bạn đang suy đoán kết nối tới một số lượng lớn domain, trong trường hợp đó chi phí mở preconnection có thể lớn hơn lợi ích mang lại.

---

## Usage {/*usage*/}

### Prefetch DNS khi render {/*prefetching-dns-when-rendering*/}

Hãy gọi `prefetchDNS` khi render một component nếu bạn biết rằng các component con của nó sẽ tải tài nguyên bên ngoài từ host đó.

```js
import { prefetchDNS } from 'react-dom';

function AppRoot() {
  prefetchDNS("https://example.com");
  return ...;
}
```

### Prefetch DNS trong event handler {/*prefetching-dns-in-an-event-handler*/}

Hãy gọi `prefetchDNS` trong event handler trước khi chuyển sang một trang hoặc trạng thái cần đến tài nguyên bên ngoài. Việc này khởi động quá trình sớm hơn so với việc gọi nó trong lúc render trang hoặc trạng thái mới.

```js
import { prefetchDNS } from 'react-dom';

function CallToAction() {
  const onClick = () => {
    prefetchDNS('http://example.com');
    startWizard();
  }
  return (
    <button onClick={onClick}>Start Wizard</button>
  );
}
```
