---
title: "React Labs: Những gì chúng tôi đang thực hiện - Tháng 6 năm 2022"
author:  Andrew Clark, Dan Abramov, Jan Kassens, Joseph Savona, Josh Story, Lauren Tan, Luna Ruan, Mengdi Chen, Rick Hanlon, Robert Zhang, Sathya Gunasekaran, Sebastian Markbage, and Xuan Huang
date: 2022/06/15
description: React 18 là thành quả của nhiều năm thực hiện, và cùng với nó là những bài học quý giá cho đội ngũ React. Bản phát hành này là kết quả của nhiều năm nghiên cứu và khám phá nhiều hướng đi. Một số hướng đi đã thành công; nhiều hướng khác là ngõ cụt nhưng lại dẫn đến những hiểu biết mới. Một điều chúng tôi rút ra là cộng đồng sẽ thấy khó chịu khi phải chờ các tính năng mới mà không có góc nhìn về những hướng đi mà chúng tôi đang khám phá.
---

Ngày 15 tháng 6 năm 2022 bởi [Andrew Clark](https://twitter.com/acdlite), [Dan Abramov](https://bsky.app/profile/danabra.mov), [Jan Kassens](https://twitter.com/kassens), [Joseph Savona](https://twitter.com/en_JS), [Josh Story](https://twitter.com/joshcstory), [Lauren Tan](https://twitter.com/potetotes), [Luna Ruan](https://twitter.com/lunaruan), [Mengdi Chen](https://twitter.com/mengdi_en), [Rick Hanlon](https://twitter.com/rickhanlonii), [Robert Zhang](https://twitter.com/jiaxuanzhang01), [Sathya Gunasekaran](https://twitter.com/_gsathya), [Sebastian Markbåge](https://twitter.com/sebmarkbage), và [Xuan Huang](https://twitter.com/Huxpro)

---

<Intro>

[React 18](/blog/2022/03/29/react-v18) là thành quả của nhiều năm thực hiện, và cùng với nó là những bài học quý giá cho đội ngũ React. Bản phát hành này là kết quả của nhiều năm nghiên cứu và khám phá nhiều hướng đi. Một số hướng đi đã thành công; nhiều hướng khác là ngõ cụt nhưng lại dẫn đến những hiểu biết mới. Một điều chúng tôi rút ra là cộng đồng sẽ thấy khó chịu khi phải chờ các tính năng mới mà không có góc nhìn về những hướng đi mà chúng tôi đang khám phá.

</Intro>

---

Thông thường tại bất kỳ thời điểm nào chúng tôi cũng có một số dự án đang được thực hiện, từ thử nghiệm nhiều hơn cho tới đã được xác định rõ ràng. Trong thời gian tới, chúng tôi muốn bắt đầu chia sẻ đều đặn hơn với cộng đồng về những gì mình đang thực hiện trong các dự án này.

Để đặt kỳ vọng đúng, đây không phải là một lộ trình với mốc thời gian rõ ràng. Nhiều dự án trong số này vẫn đang được nghiên cứu tích cực và rất khó để gắn cho chúng một ngày phát hành cụ thể. Thậm chí có thể chúng sẽ không bao giờ được phát hành ở dạng hiện tại tùy thuộc vào những gì chúng tôi học được. Thay vào đó, chúng tôi muốn chia sẻ với bạn những không gian vấn đề mà chúng tôi đang suy nghĩ tích cực, cùng với những gì đã học được cho tới nay.

## Server Components {/*server-components*/}

Chúng tôi đã công bố [bản demo thử nghiệm của React Server Components](https://legacy.reactjs.org/blog/2020/12/21/data-fetching-with-react-server-components.html), RSC, vào tháng 12 năm 2020. Kể từ đó, chúng tôi đã hoàn thiện các phần phụ thuộc của nó trong React 18 và thực hiện những thay đổi lấy cảm hứng từ phản hồi thử nghiệm.

Cụ thể, chúng tôi đang từ bỏ ý tưởng dùng các thư viện I/O đã fork, ví dụ react-fetch, và thay vào đó áp dụng mô hình async/await để có khả năng tương thích tốt hơn. Về mặt kỹ thuật điều này không chặn việc phát hành RSC vì bạn cũng có thể dùng router để lấy dữ liệu. Một thay đổi khác là chúng tôi cũng đang rời khỏi cách tiếp cận dựa trên phần mở rộng tệp để chuyển sang [đánh dấu ranh giới](https://github.com/reactjs/rfcs/pull/189#issuecomment-1116482278).

Chúng tôi đang làm việc cùng Vercel và Shopify để thống nhất hỗ trợ từ bundler cho cùng một ngữ nghĩa trên cả webpack và Vite. Trước khi ra mắt, chúng tôi muốn chắc chắn rằng ngữ nghĩa của RSC là giống nhau trên toàn bộ hệ sinh thái React. Đây là trở ngại lớn nhất để đạt tới trạng thái ổn định.

## Asset Loading {/*asset-loading*/}

Hiện nay, các tài sản như script, stylesheet bên ngoài, font và hình ảnh thường được tải trước và tải bằng các hệ thống bên ngoài. Điều này có thể khiến việc phối hợp trở nên khó khăn trong các môi trường mới như streaming, Server Components và nhiều hơn nữa.
Chúng tôi đang xem xét việc thêm các API để tải trước và tải các tài sản bên ngoài đã được loại trùng thông qua những API React hoạt động trong mọi môi trường React.

Chúng tôi cũng đang xem xét hỗ trợ Suspense cho những API này để bạn có thể có hình ảnh, CSS và font chặn việc hiển thị cho tới khi chúng tải xong nhưng không chặn streaming và concurrent rendering. Điều này có thể giúp tránh hiện tượng [“popcorning”](https://twitter.com/sebmarkbage/status/1516852731251724293), khi giao diện bật ra và bố cục bị xê dịch.

## Static Server Rendering Optimizations {/*static-server-rendering-optimizations*/}

Static Site Generation, SSG, và Incremental Static Regeneration, ISR, là những cách tuyệt vời để đạt hiệu năng cho các trang có thể cache, nhưng chúng tôi nghĩ mình có thể bổ sung tính năng để cải thiện hiệu năng của Server Side Rendering động, đặc biệt khi phần lớn nhưng không phải toàn bộ nội dung có thể cache được. Chúng tôi đang khám phá các cách tối ưu render phía server bằng cách tận dụng biên dịch và các lượt chạy tĩnh.

## React Optimizing Compiler {/*react-compiler*/}

Chúng tôi đã cho xem [bản xem trước sớm](https://www.youtube.com/watch?v=lGEMwh32soc) của React Forget tại React Conf 2021. Đây là một compiler tự động tạo ra phần tương đương với các lời gọi `useMemo` và `useCallback` để giảm thiểu chi phí render lại, đồng thời vẫn giữ nguyên mô hình lập trình của React.

Gần đây, chúng tôi đã hoàn tất việc viết lại compiler để khiến nó đáng tin cậy và mạnh mẽ hơn. Kiến trúc mới này cho phép chúng tôi phân tích và memoize những mẫu phức tạp hơn như việc dùng [local mutation](/learn/keeping-components-pure#local-mutation-your-components-little-secret), đồng thời mở ra nhiều cơ hội tối ưu hóa ở thời điểm biên dịch vượt xa việc chỉ ngang bằng với các Hook memoization.

Chúng tôi cũng đang thực hiện một playground để khám phá nhiều khía cạnh của compiler. Dù mục tiêu của playground là làm cho việc phát triển compiler trở nên dễ hơn, chúng tôi tin rằng nó cũng sẽ giúp việc dùng thử compiler và xây dựng trực giác về những gì compiler làm trở nên đơn giản hơn. Nó hé lộ nhiều góc nhìn khác nhau về cách compiler hoạt động bên dưới, và kết xuất trực tiếp đầu ra của compiler khi bạn gõ. Playground này sẽ được phát hành cùng với compiler khi nó ra mắt.

## Offscreen {/*offscreen*/}

Ngày nay, nếu muốn ẩn và hiện một component, bạn có hai lựa chọn. Một là thêm hoặc xóa nó khỏi cây hoàn toàn. Vấn đề của cách làm này là trạng thái của UI sẽ bị mất mỗi khi bạn unmount, bao gồm cả trạng thái được lưu trong DOM như vị trí cuộn.

Lựa chọn còn lại là giữ component vẫn được mount và bật tắt sự xuất hiện của nó bằng CSS. Cách này giữ được trạng thái của UI, nhưng đánh đổi bằng chi phí hiệu năng, vì React phải tiếp tục render component bị ẩn và toàn bộ component con của nó mỗi khi nhận được cập nhật mới.

Offscreen đưa ra lựa chọn thứ ba: ẩn UI về mặt thị giác nhưng hạ độ ưu tiên của nội dung đó. Ý tưởng này tương tự về tinh thần với thuộc tính CSS `content-visibility`: khi nội dung bị ẩn, nó không cần phải luôn đồng bộ với phần còn lại của UI. React có thể hoãn công việc render lại cho tới khi phần còn lại của ứng dụng rảnh, hoặc cho tới khi nội dung lại trở nên hiển thị.

Offscreen là một năng lực cấp thấp mở khóa các tính năng cấp cao hơn. Tương tự những tính năng concurrent khác của React như `startTransition`, trong hầu hết trường hợp bạn sẽ không tương tác trực tiếp với API Offscreen, mà thông qua một framework có quan điểm rõ ràng để triển khai các mẫu như:

* **Chuyển tiếp tức thì.** Một số framework định tuyến đã tải trước dữ liệu để tăng tốc những lần điều hướng tiếp theo, chẳng hạn khi rê chuột lên một liên kết. Với Offscreen, chúng cũng sẽ có thể prerender màn hình tiếp theo ở chế độ nền.
* **Trạng thái có thể tái sử dụng.** Tương tự, khi điều hướng giữa các route hoặc tab, bạn có thể dùng Offscreen để giữ lại trạng thái của màn hình trước đó để quay lại và tiếp tục từ nơi đã dừng.
* **Kết xuất danh sách ảo hóa.** Khi hiển thị danh sách lớn, các framework danh sách ảo hóa sẽ prerender nhiều hàng hơn số hàng đang hiển thị. Bạn có thể dùng Offscreen để prerender những hàng bị ẩn với độ ưu tiên thấp hơn những mục hiện đang hiển thị trong danh sách.
* **Nội dung chạy nền.** Chúng tôi cũng đang khám phá một tính năng liên quan để hạ độ ưu tiên nội dung chạy nền mà không cần ẩn nó đi, chẳng hạn khi hiển thị một lớp phủ modal.

## Transition Tracing {/*transition-tracing*/}

Hiện tại, React có hai công cụ profiling. [Profiler gốc](https://legacy.reactjs.org/blog/2018/09/10/introducing-the-react-profiler.html) hiển thị cái nhìn tổng quan về toàn bộ các commit trong một phiên profiling. Với mỗi commit, nó cũng hiển thị tất cả component đã render và lượng thời gian mà chúng mất để render. Chúng tôi cũng có một phiên bản beta của [Timeline Profiler](https://github.com/reactwg/react-18/discussions/76) được giới thiệu trong React 18, cho thấy khi nào component lên lịch cập nhật và khi nào React xử lý những cập nhật đó. Cả hai profiler này đều giúp nhà phát triển xác định các vấn đề hiệu năng trong code.

Chúng tôi nhận ra rằng việc biết về từng commit chậm hoặc từng component chậm khi bị tách khỏi ngữ cảnh không thực sự hữu ích với nhà phát triển. Điều hữu ích hơn là biết điều gì thực sự gây ra các commit chậm đó. Nhà phát triển cũng muốn có thể theo dõi các tương tác cụ thể, ví dụ một lần nhấp nút, một lần tải ban đầu hay một lần điều hướng trang, để theo dõi sự suy giảm hiệu năng và hiểu vì sao một tương tác bị chậm cũng như cách sửa nó.

Trước đây chúng tôi đã thử giải quyết vấn đề này bằng cách tạo ra [Interaction Tracing API](https://gist.github.com/bvaughn/8de925562903afd2e7a12554adcdda16), nhưng nó có một số sai sót thiết kế nền tảng làm giảm độ chính xác của việc theo dõi lý do một tương tác bị chậm, và đôi khi còn khiến tương tác không bao giờ kết thúc. Cuối cùng chúng tôi đã [loại bỏ API này](https://github.com/facebook/react/pull/20037) vì các vấn đề đó.

Chúng tôi đang thực hiện một phiên bản mới của Interaction Tracing API, tạm gọi là Transition Tracing vì nó được khởi động thông qua `startTransition`, để giải quyết những vấn đề này.

## New React Docs {/*new-react-docs*/}

Năm ngoái, chúng tôi đã công bố phiên bản beta của website tài liệu React mới, sau này được phát hành thành react.dev. Các tài liệu học tập mới dạy Hook trước và có sơ đồ, minh họa mới, cùng rất nhiều ví dụ và thử thách tương tác. Chúng tôi đã tạm dừng công việc đó để tập trung vào bản phát hành React 18, nhưng giờ khi React 18 đã ra mắt, chúng tôi đang tích cực làm việc để hoàn thiện và phát hành bộ tài liệu mới.

Hiện tại chúng tôi đang viết một mục chi tiết về effect, vì chúng tôi nghe rằng đây là một trong những chủ đề khó hơn đối với cả người dùng React mới lẫn có kinh nghiệm. [Đồng bộ với Effects](/learn/synchronizing-with-effects) là trang đầu tiên đã được phát hành trong loạt bài này, và sẽ còn nhiều trang nữa trong những tuần tiếp theo. Khi lần đầu bắt tay vào viết một mục chi tiết về effect, chúng tôi nhận ra rằng nhiều mẫu effect phổ biến có thể được đơn giản hóa bằng cách thêm một primitive mới vào React. Chúng tôi đã chia sẻ một số suy nghĩ ban đầu về điều đó trong [RFC useEvent](https://github.com/reactjs/rfcs/pull/220). Nó hiện vẫn đang ở giai đoạn nghiên cứu sớm, và chúng tôi vẫn tiếp tục lặp lại ý tưởng này. Chúng tôi rất trân trọng những bình luận của cộng đồng về RFC cho tới nay, cũng như [phản hồi](https://github.com/reactjs/react.dev/issues/3308) và các đóng góp cho công cuộc viết lại tài liệu đang diễn ra. Chúng tôi đặc biệt muốn cảm ơn [Harish Kumar](https://github.com/harish-sethuraman) vì đã gửi lên và review rất nhiều cải tiến cho phần triển khai website mới.

*Cảm ơn [Sophie Alpert](https://twitter.com/sophiebits) đã review bài blog này!*
