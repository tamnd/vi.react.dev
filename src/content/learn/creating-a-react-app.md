---
title: Tạo một ứng dụng React
---

<Intro>

Nếu bạn muốn xây dựng một ứng dụng hoặc website mới với React, chúng tôi khuyên bạn nên bắt đầu bằng một framework.

</Intro>

Nếu ứng dụng của bạn có những ràng buộc mà các framework hiện có chưa phục vụ tốt, bạn muốn tự xây dựng framework riêng, hoặc chỉ muốn học những điều cơ bản của một ứng dụng React, bạn có thể [xây dựng ứng dụng React từ đầu](/learn/build-a-react-app-from-scratch).

## Framework full-stack {/*full-stack-frameworks*/}

Những framework được khuyến nghị này hỗ trợ đầy đủ các tính năng bạn cần để triển khai và mở rộng ứng dụng trong môi trường production. Chúng đã tích hợp những tính năng React mới nhất và tận dụng kiến trúc của React.

<Note>

#### Framework full-stack không bắt buộc phải có server. {/*react-frameworks-do-not-require-a-server*/}

Mọi framework trên trang này đều hỗ trợ client-side rendering ([CSR](https://developer.mozilla.org/en-US/docs/Glossary/CSR)), single-page app ([SPA](https://developer.mozilla.org/en-US/docs/Glossary/SPA)) và static-site generation ([SSG](https://developer.mozilla.org/en-US/docs/Glossary/SSG)). Những ứng dụng này có thể được triển khai lên [CDN](https://developer.mozilla.org/en-US/docs/Glossary/CDN) hoặc dịch vụ hosting tĩnh mà không cần server. Ngoài ra, các framework này cho phép bạn thêm server-side rendering theo từng route khi phù hợp với nhu cầu của mình.

Điều này cho phép bạn bắt đầu với một ứng dụng chỉ có client, rồi sau này nếu nhu cầu thay đổi, bạn có thể chọn bật các tính năng phía server trên từng route mà không phải viết lại toàn bộ ứng dụng. Hãy xem tài liệu của framework bạn dùng để cấu hình chiến lược kết xuất.

</Note>

### Next.js (App Router) {/*nextjs-app-router*/}

**[App Router của Next.js](https://nextjs.org/docs) là một framework React tận dụng đầy đủ kiến trúc của React để hỗ trợ các ứng dụng React full-stack.**

<TerminalBlock>
npx create-next-app@latest
</TerminalBlock>

Next.js được duy trì bởi [Vercel](https://vercel.com/). Bạn có thể [triển khai ứng dụng Next.js](https://nextjs.org/docs/app/building-your-application/deploying) lên bất kỳ nhà cung cấp hosting nào hỗ trợ Node.js hoặc container Docker, hoặc lên server riêng của bạn. Next.js cũng hỗ trợ [static export](https://nextjs.org/docs/app/building-your-application/deploying/static-exports), không yêu cầu server.

### React Router (v7) {/*react-router-v7*/}

**[React Router](https://reactrouter.com/start/framework/installation) là thư viện routing phổ biến nhất cho React và có thể kết hợp với Vite để tạo thành một framework React full-stack**. Nó nhấn mạnh các Web API tiêu chuẩn và có nhiều [template sẵn sàng để triển khai](https://github.com/remix-run/react-router-templates) cho nhiều runtime và nền tảng JavaScript khác nhau.

Để tạo một dự án framework React Router mới, hãy chạy:

<TerminalBlock>
npx create-react-router@latest
</TerminalBlock>

React Router được duy trì bởi [Shopify](https://www.shopify.com).

### Expo (dành cho ứng dụng native) {/*expo*/}

**[Expo](https://expo.dev/) là một framework React cho phép bạn tạo ứng dụng Android, iOS và web dùng chung với UI thực sự native.** Nó cung cấp một SDK cho [React Native](https://reactnative.dev/) giúp các phần native dễ dùng hơn. Để tạo một dự án Expo mới, hãy chạy:

<TerminalBlock>
npx create-expo-app@latest
</TerminalBlock>

Nếu bạn chưa quen với Expo, hãy xem [hướng dẫn Expo](https://docs.expo.dev/tutorial/introduction/).

Expo được duy trì bởi [Expo (công ty)](https://expo.dev/about). Xây dựng ứng dụng với Expo là miễn phí và bạn có thể gửi chúng lên Google Play và App Store mà không bị hạn chế. Expo cũng cung cấp các dịch vụ đám mây trả phí theo lựa chọn.


## Các framework khác {/*other-frameworks*/}

Ngoài ra còn có một số framework mới nổi đang hướng tới tầm nhìn React full-stack của chúng tôi:

- [TanStack Start (Beta)](https://tanstack.com/start/): TanStack Start là một framework React full-stack được xây dựng trên TanStack Router. Nó cung cấp SSR cho toàn bộ tài liệu, streaming, server functions, bundling và nhiều hơn nữa bằng các công cụ như Nitro và Vite.
- [RedwoodSDK](https://rwsdk.com/): Redwood là một framework React full-stack với nhiều gói và cấu hình được cài sẵn, giúp việc xây dựng ứng dụng web full-stack trở nên dễ dàng.

<DeepDive>

#### Những tính năng nào tạo nên tầm nhìn kiến trúc full-stack của nhóm React? {/*which-features-make-up-the-react-teams-full-stack-architecture-vision*/}

Trình bundler của App Router trong Next.js hiện thực đầy đủ [đặc tả React Server Components chính thức](https://github.com/reactjs/rfcs/blob/main/text/0188-server-components.md). Điều này cho phép bạn kết hợp các thành phần chạy ở thời điểm build, chỉ chạy trên server và thành phần tương tác trong cùng một cây React.

Ví dụ, bạn có thể viết một thành phần React chỉ chạy trên server dưới dạng hàm `async` đọc dữ liệu từ cơ sở dữ liệu hoặc từ tệp. Sau đó bạn có thể truyền dữ liệu từ nó xuống các thành phần tương tác:

```js
// This component runs *only* on the server (or during the build).
async function Talks({ confId }) {
  // 1. You're on the server, so you can talk to your data layer. API endpoint not required.
  const talks = await db.Talks.findAll({ confId });

  // 2. Add any amount of rendering logic. It won't make your JavaScript bundle larger.
  const videos = talks.map(talk => talk.video);

  // 3. Pass the data down to the components that will run in the browser.
  return <SearchableVideoList videos={videos} />;
}
```

App Router của Next.js cũng tích hợp [data fetching với Suspense](/blog/2022/03/29/react-v18#suspense-in-data-frameworks). Điều này cho phép bạn chỉ định trạng thái tải, chẳng hạn skeleton placeholder, cho những phần khác nhau của giao diện người dùng trực tiếp trong cây React:

```js
<Suspense fallback={<TalksLoading />}>
  <Talks confId={conf.id} />
</Suspense>
```

Server Components và Suspense là các tính năng của React chứ không phải của riêng Next.js. Tuy nhiên, để áp dụng chúng ở cấp framework cần có sự đầu tư và công sức triển khai đáng kể. Hiện tại, App Router của Next.js là hiện thực đầy đủ nhất. Nhóm React đang làm việc với các nhà phát triển bundler để giúp những tính năng này dễ triển khai hơn trong thế hệ framework tiếp theo.

</DeepDive>

## Bắt đầu từ đầu {/*start-from-scratch*/}

Nếu ứng dụng của bạn có những ràng buộc mà các framework hiện có chưa phục vụ tốt, bạn muốn tự xây dựng framework riêng hoặc chỉ muốn học những điều cơ bản của một ứng dụng React, vẫn có những lựa chọn khác để bắt đầu một dự án React từ đầu.

Bắt đầu từ đầu cho bạn nhiều linh hoạt hơn, nhưng cũng đòi hỏi bạn phải tự chọn công cụ cho routing, data fetching và các mẫu sử dụng phổ biến khác. Nó gần giống như tự xây dựng framework của riêng mình thay vì dùng một framework đã tồn tại. [Những framework chúng tôi khuyên dùng](#full-stack-frameworks) đã có sẵn giải pháp cho các vấn đề này.

Nếu bạn muốn xây dựng giải pháp riêng, hãy xem hướng dẫn [xây dựng ứng dụng React từ đầu](/learn/build-a-react-app-from-scratch) của chúng tôi để biết cách thiết lập một dự án React mới với công cụ build như [Vite](https://vite.dev/), [Parcel](https://parceljs.org/) hoặc [RSbuild](https://rsbuild.dev/).

-----

_Nếu bạn là tác giả của một framework và muốn được đưa vào trang này, [hãy cho chúng tôi biết](https://github.com/reactjs/react.dev/issues/new?assignees=&labels=type%3A+framework&projects=&template=3-framework.yml&title=%5BFramework%5D%3A+)_
