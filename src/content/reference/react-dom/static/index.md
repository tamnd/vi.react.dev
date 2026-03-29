---
title: API React DOM tĩnh
---

<Intro>

Các API `react-dom/static` cho phép bạn tạo HTML tĩnh cho component React. So với các API streaming, khả năng của chúng bị giới hạn hơn. Một [framework](/learn/creating-a-react-app#full-stack-frameworks) có thể gọi chúng thay cho bạn. Phần lớn component của bạn không cần import hay dùng trực tiếp các API này.

</Intro>

---

## API tĩnh cho Web Streams {/*static-apis-for-web-streams*/}

Các phương thức này chỉ khả dụng trong những môi trường có [Web Streams](https://developer.mozilla.org/en-US/docs/Web/API/Streams_API), bao gồm trình duyệt, Deno và một số edge runtime hiện đại:

* [`prerender`](/reference/react-dom/static/prerender) render một cây React thành HTML tĩnh bằng [Readable Web Stream.](https://developer.mozilla.org/en-US/docs/Web/API/ReadableStream)
* <ExperimentalBadge /> [`resumeAndPrerender`](/reference/react-dom/static/resumeAndPrerender) tiếp tục một cây React đã được prerender thành HTML tĩnh bằng [Readable Web Stream](https://developer.mozilla.org/en-US/docs/Web/API/ReadableStream).

Node.js cũng có các phương thức này để tương thích, nhưng không được khuyến nghị vì hiệu năng kém hơn. Hãy dùng [các API chuyên biệt cho Node.js](#static-apis-for-nodejs-streams) thay thế.

---

## API tĩnh cho Node.js Streams {/*static-apis-for-nodejs-streams*/}

Các phương thức này chỉ khả dụng trong những môi trường có [Node.js Streams](https://nodejs.org/api/stream.html):

* [`prerenderToNodeStream`](/reference/react-dom/static/prerenderToNodeStream) render một cây React thành HTML tĩnh bằng [Node.js Stream.](https://nodejs.org/api/stream.html)
* <ExperimentalBadge /> [`resumeAndPrerenderToNodeStream`](/reference/react-dom/static/resumeAndPrerenderToNodeStream) tiếp tục một cây React đã được prerender thành HTML tĩnh bằng [Node.js Stream.](https://nodejs.org/api/stream.html)
