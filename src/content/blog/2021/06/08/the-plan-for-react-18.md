---
title: "Kế hoạch cho React 18"
author: Andrew Clark, Brian Vaughn, Christine Abernathy, Dan Abramov, Rachel Nabors, Rick Hanlon, Sebastian Markbage, and Seth Webster
date: 2021/06/08
description: Đội ngũ React rất hào hứng được chia sẻ một vài cập nhật. Chúng tôi đã bắt đầu thực hiện bản phát hành React 18, phiên bản lớn tiếp theo của React. Chúng tôi đã tạo một Working Group để chuẩn bị cho cộng đồng áp dụng dần các tính năng mới trong React 18. Chúng tôi đã phát hành React 18 Alpha để các tác giả thư viện có thể dùng thử và gửi phản hồi...
---

Ngày 8 tháng 6 năm 2021 bởi [Andrew Clark](https://twitter.com/acdlite), [Brian Vaughn](https://github.com/bvaughn), [Christine Abernathy](https://twitter.com/abernathyca), [Dan Abramov](https://bsky.app/profile/danabra.mov), [Rachel Nabors](https://twitter.com/rachelnabors), [Rick Hanlon](https://twitter.com/rickhanlonii), [Sebastian Markbåge](https://twitter.com/sebmarkbage), và [Seth Webster](https://twitter.com/sethwebster)

---

<Intro>

Đội ngũ React rất hào hứng được chia sẻ một vài cập nhật:

1. Chúng tôi đã bắt đầu thực hiện bản phát hành React 18, phiên bản lớn tiếp theo của React.
2. Chúng tôi đã tạo một Working Group để chuẩn bị cho cộng đồng áp dụng dần các tính năng mới trong React 18.
3. Chúng tôi đã phát hành React 18 Alpha để các tác giả thư viện có thể dùng thử và gửi phản hồi.

Những cập nhật này chủ yếu hướng tới những người duy trì thư viện bên thứ ba. Nếu bạn đang học, giảng dạy hoặc dùng React để xây dựng ứng dụng hướng tới người dùng cuối, bạn có thể yên tâm bỏ qua bài viết này. Tuy vậy, nếu tò mò, bạn vẫn có thể theo dõi các cuộc thảo luận trong React 18 Working Group!

---

</Intro>

## Điều gì sẽ có trong React 18 {/*whats-coming-in-react-18*/}

Khi được phát hành, React 18 sẽ bao gồm những cải tiến sẵn có ngay từ đầu như [automatic batching](https://github.com/reactwg/react-18/discussions/21), các API mới như [`startTransition`](https://github.com/reactwg/react-18/discussions/41), và một [server renderer dạng stream mới](https://github.com/reactwg/react-18/discussions/37) có hỗ trợ dựng sẵn cho `React.lazy`.

Những tính năng này có được là nhờ một cơ chế opt-in mới mà chúng tôi thêm vào React 18. Nó được gọi là “concurrent rendering” và cho phép React chuẩn bị nhiều phiên bản UI cùng một lúc. Thay đổi này phần lớn diễn ra phía sau hậu trường, nhưng nó mở ra những khả năng mới để cải thiện cả hiệu năng thực tế lẫn hiệu năng cảm nhận của ứng dụng.

Nếu bạn đã theo dõi nghiên cứu của chúng tôi về tương lai của React, điều mà chúng tôi không kỳ vọng ở bạn, có thể bạn từng nghe tới thứ gọi là “concurrent mode” hoặc rằng nó có thể làm hỏng ứng dụng của bạn. Đáp lại phản hồi đó từ cộng đồng, chúng tôi đã thiết kế lại chiến lược nâng cấp để hỗ trợ việc áp dụng dần dần. Thay vì một “mode” kiểu tất tay hoặc không gì cả, concurrent rendering sẽ chỉ được bật cho những cập nhật được kích hoạt bởi một trong các tính năng mới. Trong thực tế, điều đó có nghĩa là **bạn sẽ có thể áp dụng React 18 mà không cần viết lại ứng dụng và thử các tính năng mới theo tốc độ riêng của mình.**

## Chiến lược áp dụng dần dần {/*a-gradual-adoption-strategy*/}

Vì concurrency trong React 18 là opt-in, sẽ không có breaking change đáng kể nào về hành vi của component ngay từ đầu. **Bạn có thể nâng cấp lên React 18 với rất ít hoặc không cần thay đổi code ứng dụng, với mức công sức tương đương một bản phát hành lớn thông thường của React**. Dựa trên kinh nghiệm của chúng tôi khi chuyển đổi một số ứng dụng sang React 18, chúng tôi kỳ vọng nhiều người dùng sẽ có thể nâng cấp chỉ trong một buổi chiều.

Chúng tôi đã triển khai thành công các tính năng concurrent cho hàng chục nghìn component tại Facebook, và theo kinh nghiệm của chúng tôi, phần lớn component React “cứ thế mà chạy” mà không cần thay đổi thêm. Chúng tôi cam kết bảo đảm đây sẽ là một bản nâng cấp mượt mà cho toàn bộ cộng đồng, vì vậy hôm nay chúng tôi công bố React 18 Working Group.

## Làm việc cùng cộng đồng {/*working-with-the-community*/}

Chúng tôi đang thử điều gì đó mới cho bản phát hành này: Chúng tôi đã mời một nhóm chuyên gia, nhà phát triển, tác giả thư viện và nhà giáo dục từ khắp cộng đồng React tham gia [React 18 Working Group](https://github.com/reactwg/react-18) để đưa ra phản hồi, đặt câu hỏi và cùng cộng tác cho bản phát hành. Chúng tôi không thể mời tất cả những người mình muốn vào nhóm nhỏ ban đầu này, nhưng nếu thử nghiệm này thành công, chúng tôi hy vọng sẽ có thêm nhiều cơ hội hơn trong tương lai!

**Mục tiêu của React 18 Working Group là chuẩn bị cho hệ sinh thái sẵn sàng áp dụng React 18 một cách mượt mà và dần dần trong các ứng dụng và thư viện hiện có.** Working Group được đặt trên [GitHub Discussions](https://github.com/reactwg/react-18/discussions) và mọi người đều có thể đọc công khai. Thành viên của nhóm có thể để lại phản hồi, đặt câu hỏi và chia sẻ ý tưởng. Đội ngũ nòng cốt cũng sẽ dùng repository thảo luận này để chia sẻ các phát hiện nghiên cứu của mình. Khi bản phát hành ổn định đến gần hơn, mọi thông tin quan trọng cũng sẽ được đăng trên blog này.

Để biết thêm thông tin về việc nâng cấp lên React 18 hoặc các tài nguyên bổ sung về bản phát hành, hãy xem [bài viết thông báo React 18](https://github.com/reactwg/react-18/discussions/4).

## Truy cập React 18 Working Group {/*accessing-the-react-18-working-group*/}

Mọi người đều có thể đọc các cuộc thảo luận trong [repo React 18 Working Group](https://github.com/reactwg/react-18).

Vì chúng tôi dự kiến sẽ có làn sóng quan tâm ban đầu dành cho Working Group, chỉ các thành viên được mời mới được phép tạo hoặc bình luận trong các chủ đề. Tuy nhiên, các chủ đề đều hiển thị công khai hoàn toàn, nên mọi người đều có quyền truy cập cùng một thông tin. Chúng tôi tin rằng đây là một sự cân bằng hợp lý giữa việc tạo ra môi trường làm việc hiệu quả cho thành viên nhóm và việc duy trì tính minh bạch với cộng đồng rộng hơn.

Như thường lệ, bạn có thể gửi báo cáo lỗi, câu hỏi và phản hồi chung qua [issue tracker](https://github.com/facebook/react/issues) của chúng tôi.

## Cách thử React 18 Alpha ngay hôm nay {/*how-to-try-react-18-alpha-today*/}

Các bản alpha mới được [phát hành đều đặn lên npm với thẻ `@alpha`](https://github.com/reactwg/react-18/discussions/9). Những bản phát hành này được build từ commit mới nhất trong repo chính của chúng tôi. Khi một tính năng hoặc bản sửa lỗi được merge, nó sẽ xuất hiện trong một bản alpha vào ngày làm việc kế tiếp.

Giữa các bản alpha có thể có thay đổi đáng kể về hành vi hoặc API. Hãy nhớ rằng **các bản alpha không được khuyến nghị cho ứng dụng production hướng tới người dùng cuối**.

## Lộ trình phát hành React 18 dự kiến {/*projected-react-18-release-timeline*/}

Chúng tôi chưa có ngày phát hành cụ thể, nhưng kỳ vọng sẽ mất vài tháng phản hồi và lặp lại trước khi React 18 sẵn sàng cho phần lớn ứng dụng production.

* Library Alpha: Có từ hôm nay
* Public Beta: Ít nhất vài tháng
* Release Candidate (RC): Ít nhất vài tuần sau Beta
* General Availability: Ít nhất vài tuần sau RC

Bạn có thể xem thêm chi tiết về lộ trình phát hành dự kiến trong [Working Group](https://github.com/reactwg/react-18/discussions/9). Chúng tôi sẽ đăng cập nhật trên blog này khi đến gần thời điểm phát hành công khai hơn.
