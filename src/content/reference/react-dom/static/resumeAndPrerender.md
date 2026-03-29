---
title: resumeAndPrerender
---

<Intro>

`resumeAndPrerender` tiếp tục một cây React đã được prerender thành chuỗi HTML tĩnh bằng [Web Stream](https://developer.mozilla.org/en-US/docs/Web/API/Streams_API).

```js
const { prelude,postpone } = await resumeAndPrerender(reactNode, postponedState, options?)
```

</Intro>

<InlineToc />

<Note>

API này phụ thuộc vào [Web Streams.](https://developer.mozilla.org/en-US/docs/Web/API/Streams_API) Với Node.js, hãy dùng [`resumeAndPrerenderToNodeStream`](/reference/react-dom/static/resumeAndPrerenderToNodeStream) thay thế.

</Note>

---

## Reference {/*reference*/}

### `resumeAndPrerender(reactNode, postponedState, options?)` {/*resumeandprerender*/}

Hãy gọi `resumeAndPrerender` để tiếp tục một cây React đã được prerender thành chuỗi HTML tĩnh.

```js
import { resumeAndPrerender } from 'react-dom/static';
import { getPostponedState } from 'storage';

async function handler(request, response) {
  const postponedState = getPostponedState(request);
  const { prelude } = await resumeAndPrerender(<App />, postponedState, {
    bootstrapScripts: ['/main.js']
  });
  return new Response(prelude, {
    headers: { 'content-type': 'text/html' },
  });
}
```

Ở phía client, hãy gọi [`hydrateRoot`](/reference/react-dom/client/hydrateRoot) để biến HTML do server tạo ra thành có tương tác.

[Xem thêm ví dụ ở bên dưới.](#usage)

#### Parameters {/*parameters*/}

* `reactNode`: Nút React mà bạn đã gọi `prerender` hoặc `resumeAndPrerender` trước đó với nó. Ví dụ, một phần tử JSX như `<App />`. Nó được kỳ vọng đại diện cho toàn bộ tài liệu, nên component `App` cần kết xuất thẻ `<html>`.
* `postponedState`: Object `postpone` mờ đục được trả về từ một [API prerender](/reference/react-dom/static/index), được tải từ nơi bạn đã lưu nó, ví dụ Redis, một tệp hoặc S3.
* **tùy chọn** `options`: Một object chứa các tùy chọn stream.
  * **tùy chọn** `signal`: Một [abort signal](https://developer.mozilla.org/en-US/docs/Web/API/AbortSignal) cho phép bạn [hủy render phía server](#aborting-server-rendering) và render phần còn lại ở phía client.
  * **tùy chọn** `onError`: Callback chạy mỗi khi có lỗi phía server, dù [có thể phục hồi](#recovering-from-errors-outside-the-shell) hay [không.](/reference/react-dom/server/renderToReadableStream#recovering-from-errors-inside-the-shell) Mặc định callback này chỉ gọi `console.error`. Nếu bạn ghi đè nó để [ghi log báo cáo crash](#logging-crashes-on-the-server), hãy chắc chắn vẫn gọi `console.error`.

#### Returns {/*returns*/}

`prerender` trả về một Promise:
- Nếu render thành công, Promise sẽ resolve thành một object chứa:
  - `prelude`: một [Web Stream](https://developer.mozilla.org/en-US/docs/Web/API/Streams_API) của HTML. Bạn có thể dùng stream này để gửi phản hồi theo từng phần, hoặc đọc toàn bộ stream thành chuỗi.
  - `postponed`: một object mờ đục, có thể JSON-serialize, có thể truyền cho [`resume`](/reference/react-dom/server/resume) hoặc [`resumeAndPrerender`](/reference/react-dom/static/resumeAndPrerender) nếu `prerender` bị hủy.
- Nếu render thất bại, Promise sẽ bị reject. [Hãy dùng điều này để xuất ra một shell fallback.](/reference/react-dom/server/renderToReadableStream#recovering-from-errors-inside-the-shell)

#### Caveats {/*caveats*/}

`nonce` không phải là tùy chọn khả dụng khi prerender. Nonce phải là duy nhất cho mỗi request, và nếu bạn dùng nonce để bảo vệ ứng dụng với [CSP](https://developer.mozilla.org/en-US/docs/Web/HTTP/Guides/CSP), sẽ không phù hợp và thiếu an toàn nếu đưa giá trị nonce vào ngay trong nội dung prerender.

<Note>

### Khi nào tôi nên dùng `resumeAndPrerender`? {/*when-to-use-prerender*/}

API tĩnh `resumeAndPrerender` được dùng cho static server-side generation, tức SSG. Không giống `renderToString`, `resumeAndPrerender` chờ toàn bộ dữ liệu tải xong trước khi resolve. Điều này khiến nó phù hợp để tạo HTML tĩnh cho cả một trang, bao gồm cả dữ liệu cần được lấy thông qua Suspense. Để stream nội dung trong lúc nó đang tải, hãy dùng API server-side render dạng stream như [renderToReadableStream](/reference/react-dom/server/renderToReadableStream).

`resumeAndPrerender` có thể bị hủy và sau đó hoặc được tiếp tục bằng một `resumeAndPrerender` khác, hoặc được resume bằng `resume` để hỗ trợ pre-render từng phần.

</Note>

---

## Usage {/*usage*/}

### Đọc thêm {/*further-reading*/}

`resumeAndPrerender` hoạt động tương tự [`prerender`](/reference/react-dom/static/prerender) nhưng có thể dùng để tiếp tục một quá trình prerender đã bắt đầu trước đó rồi bị hủy.
Để biết thêm về việc resume một cây đã được prerender, hãy xem [tài liệu về resume](/reference/react-dom/server/resume#resuming-a-prerender).
