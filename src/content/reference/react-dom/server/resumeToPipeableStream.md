---
title: resumeToPipeableStream
---

<Intro>

`resumeToPipeableStream` truyền theo dạng stream một cây React đã được kết xuất trước tới một [Node.js Stream](https://nodejs.org/api/stream.html) có thể pipe.

```js
const {pipe, abort} = await resumeToPipeableStream(reactNode, postponedState, options?)
```

</Intro>

<InlineToc />

<Note>

API này dành riêng cho Node.js. Những môi trường có [Web Streams](https://developer.mozilla.org/en-US/docs/Web/API/Streams_API), như Deno và các edge runtime hiện đại, nên dùng [`resume`](/reference/react-dom/server/renderToReadableStream) thay thế.

</Note>

---

## Reference {/*reference*/}

### `resumeToPipeableStream(node, postponed, options?)` {/*resume-to-pipeable-stream*/}

Hãy gọi `resume` để tiếp tục kết xuất một cây React đã được kết xuất trước thành HTML vào một [Node.js Stream.](https://nodejs.org/api/stream.html#writable-streams)

```js
import { resume } from 'react-dom/server';
import {getPostponedState} from './storage';

async function handler(request, response) {
  const postponed = await getPostponedState(request);
  const {pipe} = resumeToPipeableStream(<App />, postponed, {
    onShellReady: () => {
      pipe(response);
    }
  });
}
```

[Xem thêm ví dụ ở bên dưới.](#usage)

#### Parameters {/*parameters*/}

* `reactNode`: Nút React mà bạn đã gọi `prerender` với nó. Ví dụ, một phần tử JSX như `<App />`. Nó được kỳ vọng đại diện cho toàn bộ tài liệu, nên component `App` cần kết xuất thẻ `<html>`.
* `postponedState`: Object `postpone` mờ đục được trả về từ một [API prerender](/reference/react-dom/static/index), được tải từ nơi bạn đã lưu nó, ví dụ Redis, một tệp hoặc S3.
* **tùy chọn** `options`: Một object chứa các tùy chọn stream.
  * **tùy chọn** `nonce`: Chuỗi [`nonce`](http://developer.mozilla.org/en-US/docs/Web/HTML/Element/script#nonce) để cho phép script theo [`script-src` Content-Security-Policy](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Security-Policy/script-src).
  * **tùy chọn** `signal`: Một [abort signal](https://developer.mozilla.org/en-US/docs/Web/API/AbortSignal) cho phép bạn [hủy render phía server](#aborting-server-rendering) và render phần còn lại ở phía client.
  * **tùy chọn** `onError`: Callback chạy mỗi khi có lỗi phía server, dù [có thể phục hồi](/reference/react-dom/server/renderToReadableStream#recovering-from-errors-outside-the-shell) hay [không.](/reference/react-dom/server/renderToReadableStream#recovering-from-errors-inside-the-shell) Mặc định, callback này chỉ gọi `console.error`. Nếu bạn ghi đè nó để [ghi log báo cáo crash](/reference/react-dom/server/renderToReadableStream#logging-crashes-on-the-server), hãy chắc chắn vẫn gọi `console.error`.
  * **tùy chọn** `onShellReady`: Callback chạy ngay sau khi [shell](#specifying-what-goes-into-the-shell) hoàn tất. Bạn có thể gọi `pipe` tại đây để bắt đầu stream. React sẽ [stream thêm nội dung](#streaming-more-content-as-it-loads) sau shell cùng với các thẻ `<script>` nội tuyến để thay thế phần fallback HTML đang tải bằng nội dung thực.
  * **tùy chọn** `onShellError`: Callback chạy nếu có lỗi khi render shell. Nó nhận lỗi làm đối số. Chưa có byte nào được phát ra từ stream, và cả `onShellReady` lẫn `onAllReady` đều sẽ không được gọi, nên bạn có thể [xuất ra một shell HTML fallback](#recovering-from-errors-inside-the-shell) hoặc dùng prelude.


#### Returns {/*returns*/}

`resume` trả về một object với hai phương thức:

* `pipe` xuất HTML vào [Writable Node.js Stream](https://nodejs.org/api/stream.html#writable-streams) được cung cấp. Hãy gọi `pipe` trong `onShellReady` nếu bạn muốn bật streaming, hoặc trong `onAllReady` cho crawler và quá trình tạo nội dung tĩnh.
* `abort` cho phép bạn [hủy render phía server](#aborting-server-rendering) và render phần còn lại ở phía client.

#### Caveats {/*caveats*/}

- `resumeToPipeableStream` không chấp nhận các tùy chọn `bootstrapScripts`, `bootstrapScriptContent` hoặc `bootstrapModules`. Thay vào đó, bạn cần truyền các tùy chọn này cho lệnh gọi `prerender` tạo ra `postponedState`. Bạn cũng có thể tự chèn nội dung bootstrap vào writable stream.
- `resumeToPipeableStream` không chấp nhận `identifierPrefix` vì tiền tố phải giống nhau ở cả `prerender` và `resumeToPipeableStream`.
- Vì không thể truyền `nonce` cho prerender, bạn chỉ nên cung cấp `nonce` cho `resumeToPipeableStream` nếu bạn không cung cấp script cho prerender.
- `resumeToPipeableStream` sẽ render lại từ gốc cho tới khi tìm thấy component chưa được prerender hoàn toàn. Chỉ những Component đã được prerender đầy đủ, nghĩa là component đó và các component con của nó đã prerender xong, mới bị bỏ qua hoàn toàn.

## Usage {/*usage*/}

### Đọc thêm {/*further-reading*/}

Việc resume hoạt động tương tự `renderToReadableStream`. Để xem thêm ví dụ, hãy xem [phần hướng dẫn sử dụng của `renderToReadableStream`](/reference/react-dom/server/renderToReadableStream#usage).
Phần [hướng dẫn sử dụng của `prerender`](/reference/react-dom/static/prerender#usage) có các ví dụ về cách dùng riêng `prerenderToNodeStream`.
