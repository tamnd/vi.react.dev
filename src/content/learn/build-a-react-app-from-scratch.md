---
title: Xây dựng ứng dụng React từ đầu
---

<Intro>

Nếu ứng dụng của bạn có những ràng buộc mà các framework hiện có chưa phục vụ tốt, bạn muốn tự xây dựng framework riêng, hoặc chỉ muốn học những điều cơ bản của một ứng dụng React, bạn có thể xây dựng ứng dụng React từ đầu.

</Intro>

<DeepDive>

#### Hãy cân nhắc dùng framework {/*consider-using-a-framework*/}

Bắt đầu từ đầu là một cách dễ để làm quen với React, nhưng đánh đổi lớn là con đường này thường tương đương với việc tự xây một framework tạm thời của riêng bạn. Khi yêu cầu của bạn thay đổi, bạn có thể phải giải quyết thêm nhiều vấn đề giống framework mà các framework chúng tôi khuyên dùng đã có lời giải chín muồi và được hỗ trợ tốt.

Ví dụ, nếu sau này ứng dụng của bạn cần hỗ trợ server-side rendering (SSR), static site generation (SSG) và/hoặc React Server Components (RSC), bạn sẽ phải tự triển khai chúng. Tương tự, những tính năng React trong tương lai đòi hỏi tích hợp ở cấp framework cũng sẽ phải do bạn tự triển khai nếu muốn dùng.

Các framework được chúng tôi khuyên dùng cũng giúp bạn xây dựng ứng dụng có hiệu năng tốt hơn. Chẳng hạn, việc giảm hoặc loại bỏ các waterfall từ network request mang lại trải nghiệm người dùng tốt hơn. Điều này có thể chưa phải ưu tiên khi bạn đang làm dự án nhỏ, nhưng nếu ứng dụng có thêm người dùng, bạn có thể sẽ muốn cải thiện hiệu năng.

Đi theo hướng này cũng khiến việc nhận hỗ trợ trở nên khó hơn, vì cách bạn phát triển routing, data fetching và các tính năng khác sẽ mang tính riêng biệt với tình huống của bạn. Bạn chỉ nên chọn cách này nếu thấy thoải mái khi tự giải quyết các vấn đề đó, hoặc nếu chắc chắn rằng mình sẽ không bao giờ cần những tính năng này.

Để xem danh sách framework được khuyên dùng, hãy xem [Tạo một ứng dụng React](/learn/creating-a-react-app).

</DeepDive>


## Bước 1: Cài công cụ build {/*step-1-install-a-build-tool*/}

Bước đầu tiên là cài một công cụ build như `vite`, `parcel` hoặc `rsbuild`. Các công cụ build này cung cấp khả năng đóng gói và chạy source code, máy chủ phát triển cho môi trường cục bộ và lệnh build để triển khai ứng dụng lên server production.

### Vite {/*vite*/}

[Vite](https://vite.dev/) là một công cụ build hướng tới trải nghiệm phát triển nhanh hơn và gọn hơn cho các dự án web hiện đại.

<TerminalBlock>
npm create vite@latest my-app -- --template react-ts
</TerminalBlock>

Vite có tính quy ước và đi kèm các mặc định hợp lý ngay từ đầu. Vite có hệ sinh thái plugin phong phú để hỗ trợ fast refresh, JSX, Babel/SWC và các tính năng phổ biến khác. Hãy xem [plugin React của Vite](https://vite.dev/plugins/#vitejs-plugin-react) hoặc [plugin React SWC](https://vite.dev/plugins/#vitejs-plugin-react-swc) cùng [dự án ví dụ React SSR](https://vite.dev/guide/ssr.html#example-projects) để bắt đầu.

Vite đã được dùng làm công cụ build trong một trong các [framework được chúng tôi khuyên dùng](/learn/creating-a-react-app): [React Router](https://reactrouter.com/start/framework/installation).

### Parcel {/*parcel*/}

[Parcel](https://parceljs.org/) kết hợp trải nghiệm phát triển tuyệt vời ngay khi bắt đầu với một kiến trúc có thể mở rộng, đủ sức đưa dự án của bạn từ giai đoạn đầu đến các ứng dụng production quy mô lớn.

<TerminalBlock>
npm install --save-dev parcel
</TerminalBlock>

Parcel hỗ trợ fast refresh, JSX, TypeScript, Flow và styling ngay từ đầu. Hãy xem [công thức React của Parcel](https://parceljs.org/recipes/react/#getting-started) để bắt đầu.

### Rsbuild {/*rsbuild*/}

[Rsbuild](https://rsbuild.dev/) là công cụ build dựa trên Rspack, mang lại trải nghiệm phát triển liền mạch cho ứng dụng React. Nó đi kèm các cấu hình mặc định đã được tinh chỉnh cẩn thận và tối ưu hiệu năng sẵn sàng để dùng.

<TerminalBlock>
npx create-rsbuild --template react
</TerminalBlock>

Rsbuild có hỗ trợ tích hợp cho các tính năng React như fast refresh, JSX, TypeScript và styling. Hãy xem [hướng dẫn React của Rsbuild](https://rsbuild.dev/guide/framework/react) để bắt đầu.

<Note>

#### Metro cho React Native {/*react-native*/}

Nếu bạn bắt đầu từ đầu với React Native, bạn sẽ cần dùng [Metro](https://metrobundler.dev/), trình bundler JavaScript cho React Native. Metro hỗ trợ đóng gói cho các nền tảng như iOS và Android, nhưng thiếu nhiều tính năng so với các công cụ ở đây. Chúng tôi khuyên bạn nên bắt đầu với Vite, Parcel hoặc Rsbuild trừ khi dự án của bạn cần hỗ trợ React Native.

</Note>

## Bước 2: Xây dựng các mẫu ứng dụng phổ biến {/*step-2-build-common-application-patterns*/}

Các công cụ build ở trên bắt đầu với một ứng dụng chỉ có client, kiểu single-page app (SPA), nhưng không bao gồm các giải pháp tiếp theo cho những chức năng phổ biến như routing, data fetching hay styling.

Hệ sinh thái React có nhiều công cụ cho các vấn đề này. Chúng tôi liệt kê một vài công cụ được dùng rộng rãi để bạn bắt đầu, nhưng bạn hoàn toàn có thể chọn công cụ khác nếu phù hợp hơn.

### Routing {/*routing*/}

Routing quyết định nội dung hoặc trang nào sẽ hiển thị khi người dùng truy cập một URL cụ thể. Bạn cần thiết lập router để ánh xạ URL tới các phần khác nhau trong ứng dụng. Bạn cũng sẽ phải xử lý nested routes, route parameters và query parameters. Router có thể được cấu hình trong code hoặc được định nghĩa dựa trên cấu trúc thư mục và tệp của component.

Router là phần cốt lõi của ứng dụng hiện đại, và thường được tích hợp với data fetching, bao gồm cả prefetch dữ liệu cho cả một trang để tải nhanh hơn, code splitting để giảm kích thước bundle ở client, và các cách kết xuất trang để quyết định cách mỗi trang được tạo ra.

Chúng tôi gợi ý dùng:

- [React Router](https://reactrouter.com/start/data/custom)
- [Tanstack Router](https://tanstack.com/router/latest)


### Data fetching {/*data-fetching*/}

Lấy dữ liệu từ server hoặc nguồn dữ liệu khác là phần quan trọng của hầu hết ứng dụng. Làm điều đó đúng cách đòi hỏi phải xử lý trạng thái tải, trạng thái lỗi và bộ nhớ đệm cho dữ liệu đã lấy, điều này có thể khá phức tạp.

Các thư viện data fetching chuyên dụng làm giúp bạn phần khó trong việc lấy và cache dữ liệu, để bạn tập trung vào việc ứng dụng cần dữ liệu gì và hiển thị nó như thế nào. Những thư viện này thường được dùng trực tiếp trong component, nhưng cũng có thể tích hợp vào routing loader để prefetch nhanh hơn, hiệu năng tốt hơn, và cả trong server rendering.

Lưu ý rằng việc lấy dữ liệu trực tiếp trong component có thể dẫn đến thời gian tải chậm hơn do waterfall từ network request, vì vậy chúng tôi khuyên bạn nên prefetch dữ liệu trong routing loader hoặc trên server càng nhiều càng tốt. Cách này cho phép dữ liệu của trang được lấy cùng lúc khi trang đang hiển thị.

Nếu bạn lấy dữ liệu từ phần lớn backend hoặc API kiểu REST, chúng tôi gợi ý dùng:

- [TanStack Query](https://tanstack.com/query/)
- [SWR](https://swr.vercel.app/)
- [RTK Query](https://redux-toolkit.js.org/rtk-query/overview)

Nếu bạn lấy dữ liệu từ GraphQL API, chúng tôi gợi ý dùng:

- [Apollo](https://www.apollographql.com/docs/react)
- [Relay](https://relay.dev/)


### Code splitting {/*code-splitting*/}

Code splitting là quá trình chia ứng dụng thành những bundle nhỏ hơn có thể tải theo nhu cầu. Kích thước code của ứng dụng tăng lên với mỗi tính năng mới và dependency bổ sung. Ứng dụng có thể tải chậm vì toàn bộ mã cho cả ứng dụng phải được gửi xuống trước khi dùng được. Cache, giảm bớt tính năng/dependency và chuyển một phần code sang chạy trên server có thể giúp giảm chậm tải, nhưng đó vẫn là những giải pháp chưa trọn vẹn và có thể hy sinh chức năng nếu lạm dụng.

Tương tự, nếu bạn phụ thuộc vào việc các ứng dụng dùng framework của bạn phải tự tách code, có thể sẽ có lúc thời gian tải còn chậm hơn cả khi không tách code. Ví dụ, [lazy loading](/reference/react/lazy) một biểu đồ sẽ trì hoãn việc gửi code cần thiết để kết xuất biểu đồ, tức tách code của biểu đồ khỏi phần còn lại của ứng dụng. [Parcel hỗ trợ code splitting với React.lazy](https://parceljs.org/recipes/react/#code-splitting). Tuy nhiên, nếu biểu đồ tải dữ liệu *sau khi* đã được kết xuất lần đầu, giờ bạn phải chờ hai lần. Đây là waterfall: thay vì vừa lấy dữ liệu cho biểu đồ vừa gửi code để kết xuất nó cùng lúc, bạn phải đợi từng bước hoàn thành lần lượt.

Việc tách code theo route, khi được tích hợp với bundling và data fetching, có thể giảm thời gian tải ban đầu của ứng dụng cũng như thời gian để phần nội dung lớn nhất hiển thị trên màn hình được kết xuất ([Largest Contentful Paint](https://web.dev/articles/lcp)).

Để biết hướng dẫn code splitting, hãy xem tài liệu của công cụ build bạn dùng:
- [Tối ưu build trong Vite](https://vite.dev/guide/features.html#build-optimizations)
- [Code splitting trong Parcel](https://parceljs.org/features/code-splitting/)
- [Code splitting trong Rsbuild](https://rsbuild.dev/guide/optimization/code-splitting)

### Cải thiện hiệu năng ứng dụng {/*improving-application-performance*/}

Vì công cụ build bạn chọn chỉ hỗ trợ single-page app (SPA), bạn sẽ cần tự triển khai các [mẫu kết xuất](https://www.patterns.dev/vanilla/rendering-patterns) khác như server-side rendering (SSR), static site generation (SSG) và/hoặc React Server Components (RSC). Ngay cả khi ban đầu bạn chưa cần những tính năng này, trong tương lai có thể sẽ có một số route hưởng lợi từ SSR, SSG hoặc RSC.

* **Single-page app (SPA)** tải một trang HTML duy nhất và cập nhật trang một cách động khi người dùng tương tác. SPA dễ bắt đầu hơn nhưng có thể có thời gian tải ban đầu chậm hơn. SPA là kiến trúc mặc định của hầu hết công cụ build.

* **Streaming server-side rendering (SSR)** kết xuất trang trên server rồi gửi trang đã kết xuất hoàn chỉnh về cho client. SSR có thể cải thiện hiệu năng, nhưng việc thiết lập và bảo trì phức tạp hơn so với single-page app. Với streaming, SSR có thể trở nên rất phức tạp trong cả thiết lập lẫn bảo trì. Hãy xem [hướng dẫn SSR của Vite]( https://vite.dev/guide/ssr).

* **Static site generation (SSG)** tạo các tệp HTML tĩnh cho ứng dụng ở thời điểm build. SSG có thể cải thiện hiệu năng, nhưng cũng phức tạp hơn để thiết lập và bảo trì so với server-side rendering. Hãy xem [hướng dẫn SSG của Vite](https://vite.dev/guide/ssr.html#pre-rendering-ssg).

* **React Server Components (RSC)** cho phép bạn kết hợp các thành phần chạy ở thời điểm build, chỉ chạy trên server và thành phần tương tác trong cùng một cây React. RSC có thể cải thiện hiệu năng, nhưng hiện tại việc thiết lập và bảo trì đòi hỏi chuyên môn sâu. Hãy xem [các ví dụ RSC của Parcel](https://github.com/parcel-bundler/rsc-examples).

Chiến lược kết xuất của bạn cần tích hợp với router để ứng dụng xây dựng bằng framework của bạn có thể chọn chiến lược kết xuất theo từng route. Điều này cho phép dùng nhiều chiến lược kết xuất khác nhau mà không phải viết lại toàn bộ ứng dụng. Ví dụ, landing page của ứng dụng có thể hưởng lợi từ static generation (SSG), trong khi trang có news feed có thể hoạt động tốt nhất với server-side rendering.

Sử dụng đúng chiến lược kết xuất cho đúng route có thể giảm thời gian tải byte nội dung đầu tiên ([Time to First Byte](https://web.dev/articles/ttfb)), thời gian kết xuất phần nội dung đầu tiên ([First Contentful Paint](https://web.dev/articles/fcp)) và thời gian kết xuất phần nội dung lớn nhất nhìn thấy trên màn hình ([Largest Contentful Paint](https://web.dev/articles/lcp)).

### Và còn nữa... {/*and-more*/}

Đây chỉ là vài ví dụ về những tính năng mà một ứng dụng mới cần cân nhắc khi xây dựng từ đầu. Nhiều giới hạn bạn gặp phải có thể khó giải quyết vì mỗi vấn đề đều liên kết với các vấn đề khác và có thể đòi hỏi chuyên môn sâu ở những lĩnh vực bạn chưa quen.

Nếu bạn không muốn tự giải quyết các vấn đề này, bạn có thể [bắt đầu với một framework](/learn/creating-a-react-app) đã cung cấp sẵn các tính năng đó.
