---
title: API React DOM phía server
---

<Intro>

Các API `react-dom/server` cho phép bạn kết xuất component React thành HTML ở phía server. Những API này chỉ được dùng trên server ở tầng cao nhất của ứng dụng để tạo ra HTML ban đầu. Một [framework](/learn/creating-a-react-app#full-stack-frameworks) có thể gọi chúng thay bạn. Phần lớn component của bạn không cần import hay sử dụng chúng.

</Intro>

---

## API server cho Web Streams {/*server-apis-for-web-streams*/}

Các phương thức này chỉ khả dụng trong những môi trường có [Web Streams](https://developer.mozilla.org/en-US/docs/Web/API/Streams_API), bao gồm trình duyệt, Deno và một số edge runtime hiện đại:

* [`renderToReadableStream`](/reference/react-dom/server/renderToReadableStream) kết xuất một cây React thành [Readable Web Stream.](https://developer.mozilla.org/en-US/docs/Web/API/ReadableStream)
* [`resume`](/reference/react-dom/server/renderToPipeableStream) tiếp tục [`prerender`](/reference/react-dom/static/prerender) thành một [Readable Web Stream](https://developer.mozilla.org/en-US/docs/Web/API/ReadableStream).


<Note>

Node.js cũng có các phương thức này để tương thích, nhưng chúng không được khuyến nghị do hiệu năng kém hơn. Hãy dùng [API Node.js chuyên biệt](#server-apis-for-nodejs-streams) thay thế.

</Note>
---

## API server cho Node.js Streams {/*server-apis-for-nodejs-streams*/}

Các phương thức này chỉ khả dụng trong những môi trường có [Node.js Streams:](https://nodejs.org/api/stream.html)

* [`renderToPipeableStream`](/reference/react-dom/server/renderToPipeableStream) kết xuất một cây React thành [Node.js Stream](https://nodejs.org/api/stream.html) có thể pipe.
* [`resumeToPipeableStream`](/reference/react-dom/server/renderToPipeableStream) tiếp tục [`prerenderToNodeStream`](/reference/react-dom/static/prerenderToNodeStream) thành [Node.js Stream](https://nodejs.org/api/stream.html) có thể pipe.

---

## API server cũ cho môi trường không hỗ trợ stream {/*legacy-server-apis-for-non-streaming-environments*/}

Những phương thức này có thể được dùng trong các môi trường không hỗ trợ stream:

* [`renderToString`](/reference/react-dom/server/renderToString) kết xuất một cây React thành chuỗi.
* [`renderToStaticMarkup`](/reference/react-dom/server/renderToStaticMarkup) kết xuất một cây React không tương tác thành chuỗi.

Chúng có chức năng hạn chế hơn so với các API stream.
