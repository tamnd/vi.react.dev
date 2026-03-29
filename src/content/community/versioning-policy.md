---
title: Chính sách tạo phiên bản
---

<Intro>

Mọi bản dựng ổn định của React đều trải qua mức độ kiểm thử cao và tuân theo quy ước tạo phiên bản ngữ nghĩa (semantic versioning, hay semver). React cũng cung cấp các kênh phát hành không ổn định để khuyến khích nhận phản hồi sớm cho các tính năng thử nghiệm. Trang này mô tả những gì bạn có thể kỳ vọng từ các bản phát hành của React.

</Intro>

Chính sách tạo phiên bản này mô tả cách chúng tôi dùng số phiên bản cho các package như `react` và `react-dom`. Để xem danh sách các bản phát hành trước đây, hãy xem trang [Versions](/versions).

## Các bản phát hành ổn định {/*stable-releases*/}

Các bản phát hành React ổn định, còn được gọi là kênh phát hành "Latest", tuân theo các nguyên tắc của [semantic versioning (semver)](https://semver.org/).

Điều đó có nghĩa là với số phiên bản **x.y.z**:

* Khi phát hành **bản sửa lỗi nghiêm trọng**, chúng tôi tạo một **bản phát hành patch** bằng cách đổi số **z** (ví dụ: 15.6.2 thành 15.6.3).
* Khi phát hành **tính năng mới** hoặc **bản sửa lỗi không nghiêm trọng**, chúng tôi tạo một **bản phát hành minor** bằng cách đổi số **y** (ví dụ: 15.6.2 thành 15.7.0).
* Khi phát hành **thay đổi gây lỗi tương thích**, chúng tôi tạo một **bản phát hành major** bằng cách đổi số **x** (ví dụ: 15.6.2 thành 16.0.0).

Bản phát hành major cũng có thể chứa tính năng mới, và mọi bản phát hành đều có thể bao gồm sửa lỗi.

Bản phát hành minor là loại phát hành phổ biến nhất.

Chúng tôi biết người dùng vẫn tiếp tục dùng các phiên bản React cũ trong môi trường production. Nếu phát hiện một lỗ hổng bảo mật trong React, chúng tôi sẽ phát hành bản vá được backport cho mọi phiên bản major bị ảnh hưởng bởi lỗ hổng đó.

### Thay đổi gây lỗi tương thích {/*breaking-changes*/}

Các thay đổi gây lỗi tương thích gây bất tiện cho tất cả mọi người, nên chúng tôi cố gắng giảm thiểu số lượng bản phát hành major. Ví dụ, React 15 được phát hành vào tháng 4 năm 2016, React 16 vào tháng 9 năm 2017, và React 17 vào tháng 10 năm 2020.

Thay vào đó, chúng tôi phát hành tính năng mới trong các phiên bản minor. Điều này có nghĩa là các bản phát hành minor thường thú vị và đáng chú ý hơn bản major, dù tên gọi của chúng có vẻ khiêm tốn.

### Cam kết về tính ổn định {/*commitment-to-stability*/}

Khi React thay đổi theo thời gian, chúng tôi cố gắng giảm thiểu công sức cần bỏ ra để tận dụng các tính năng mới. Khi có thể, chúng tôi sẽ giữ cho API cũ vẫn hoạt động, ngay cả khi điều đó có nghĩa là phải chuyển nó sang một package riêng. Ví dụ, [mixins đã bị khuyến cáo không nên dùng trong nhiều năm](https://legacy.reactjs.org/blog/2016/07/13/mixins-considered-harmful.html) nhưng đến nay chúng vẫn được hỗ trợ [thông qua create-react-class](https://legacy.reactjs.org/docs/react-without-es6.html#mixins), và nhiều codebase vẫn tiếp tục dùng chúng trong mã legacy ổn định.

Hơn một triệu nhà phát triển dùng React, và cùng nhau duy trì hàng triệu component. Chỉ riêng codebase của Facebook đã có hơn 50.000 component React. Điều đó có nghĩa là chúng tôi cần khiến việc nâng cấp lên phiên bản React mới dễ nhất có thể. Nếu thực hiện thay đổi lớn mà không có lộ trình migrate, mọi người sẽ bị mắc kẹt ở các phiên bản cũ. Chúng tôi kiểm thử các lộ trình nâng cấp này ngay trong Facebook. Nếu đội ngũ chưa tới 10 người của chúng tôi có thể tự cập nhật hơn 50.000 component, chúng tôi hy vọng việc nâng cấp sẽ khả thi với bất kỳ ai dùng React. Trong nhiều trường hợp, chúng tôi viết [các script tự động](https://github.com/reactjs/react-codemod) để nâng cấp cú pháp component, rồi đưa chúng vào bản phát hành mã nguồn mở để mọi người có thể sử dụng.

### Nâng cấp dần thông qua cảnh báo {/*gradual-upgrades-via-warnings*/}

Bản dựng development của React bao gồm nhiều cảnh báo hữu ích. Khi có thể, chúng tôi thêm cảnh báo để chuẩn bị cho các thay đổi gây lỗi tương thích trong tương lai. Nhờ vậy, nếu ứng dụng của bạn không có cảnh báo nào trên bản phát hành mới nhất, nó sẽ tương thích với bản phát hành major tiếp theo. Điều này cho phép bạn nâng cấp ứng dụng của mình từng component một.

Cảnh báo trong bản dựng development sẽ không ảnh hưởng đến hành vi runtime của ứng dụng. Vì vậy, bạn có thể yên tâm rằng ứng dụng sẽ hoạt động giống nhau giữa bản dựng development và production. Khác biệt duy nhất là bản dựng production sẽ không ghi log các cảnh báo và hoạt động hiệu quả hơn. (Nếu bạn từng thấy khác đi, vui lòng tạo issue.)

### Điều gì được xem là thay đổi gây lỗi tương thích? {/*what-counts-as-a-breaking-change*/}

Nhìn chung, chúng tôi *không* tăng số phiên bản major đối với các thay đổi sau:

* **Cảnh báo trong development.** Vì chúng không ảnh hưởng đến hành vi ở production, chúng tôi có thể thêm cảnh báo mới hoặc sửa cảnh báo hiện có giữa các phiên bản major. Trên thực tế, đây là cách cho phép chúng tôi cảnh báo đáng tin cậy về các thay đổi gây lỗi tương thích sắp tới.
* **Các API bắt đầu bằng `unstable_`.** Đây là các tính năng thử nghiệm mà chúng tôi chưa đủ tự tin vào API của chúng. Việc phát hành chúng với tiền tố `unstable_` giúp chúng tôi lặp nhanh hơn và sớm đạt được một API ổn định hơn.
* **Các phiên bản Alpha và Canary của React.** Chúng tôi cung cấp phiên bản alpha của React như một cách để kiểm thử sớm các tính năng mới, nhưng cần có sự linh hoạt để thay đổi dựa trên những gì học được trong giai đoạn alpha. Nếu bạn dùng các phiên bản này, hãy lưu ý rằng API có thể thay đổi trước khi bản ổn định được phát hành.
* **Các API không được tài liệu hóa và cấu trúc dữ liệu nội bộ.** Nếu bạn truy cập vào các tên thuộc tính nội bộ như `__SECRET_INTERNALS_DO_NOT_USE_OR_YOU_WILL_BE_FIRED` hoặc `__reactInternalInstance$uk43rzhitjg`, sẽ không có bất kỳ bảo đảm nào. Bạn phải tự chịu trách nhiệm.

Chính sách này được thiết kế theo hướng thực dụng. Chắc chắn là chúng tôi không muốn gây đau đầu cho bạn. Nếu tăng phiên bản major cho tất cả các thay đổi này, cuối cùng chúng tôi sẽ phải phát hành nhiều bản major hơn và khiến cộng đồng chịu thêm gánh nặng về phiên bản. Điều đó cũng có nghĩa là chúng tôi không thể cải thiện React nhanh như mong muốn.

Dù vậy, nếu chúng tôi cho rằng một thay đổi trong danh sách này sẽ gây ra vấn đề trên diện rộng cho cộng đồng, chúng tôi vẫn sẽ cố gắng hết sức để cung cấp lộ trình migrate dần dần.

### Nếu một bản phát hành minor không có tính năng mới, tại sao nó không phải là patch? {/*if-a-minor-release-includes-no-new-features-why-isnt-it-a-patch*/}

Có thể một bản phát hành minor sẽ không bao gồm tính năng mới. [Điều này được semver cho phép](https://semver.org/#spec-item-7), trong đó nêu rằng **"[một phiên bản minor] CÓ THỂ được tăng lên nếu có chức năng mới đáng kể hoặc các cải tiến được đưa vào trong mã nội bộ. Nó CÓ THỂ bao gồm các thay đổi ở cấp độ patch."**

Tuy nhiên, điều này cũng đặt ra câu hỏi: tại sao những bản phát hành như vậy lại không được đánh số như patch?

Câu trả lời là mọi thay đổi đối với React, hoặc bất kỳ phần mềm nào khác, đều mang theo một mức rủi ro nào đó có thể gây lỗi theo những cách khó lường. Hãy tưởng tượng một tình huống mà một bản phát hành patch sửa một lỗi nhưng vô tình lại gây ra một lỗi khác. Điều này không chỉ làm gián đoạn công việc của nhà phát triển mà còn làm giảm niềm tin của họ vào các bản phát hành patch trong tương lai. Điều đó càng đáng tiếc hơn nếu bản sửa ban đầu dành cho một lỗi hiếm khi xảy ra trong thực tế.

Chúng tôi có thành tích khá tốt trong việc giữ cho các bản phát hành React không có lỗi, nhưng các bản phát hành patch còn có yêu cầu cao hơn nữa về độ tin cậy vì hầu hết nhà phát triển đều cho rằng họ có thể áp dụng chúng mà không gặp hậu quả bất lợi.

Vì những lý do đó, chúng tôi chỉ dành bản phát hành patch cho các lỗi nghiêm trọng nhất và các lỗ hổng bảo mật.

Nếu một bản phát hành chứa các thay đổi không thiết yếu, chẳng hạn như refactor nội bộ, thay đổi chi tiết triển khai, cải thiện hiệu năng hoặc sửa lỗi nhỏ, chúng tôi sẽ tăng phiên bản minor ngay cả khi không có tính năng mới.

## Tất cả các kênh phát hành {/*all-release-channels*/}

React dựa vào một cộng đồng mã nguồn mở năng động để gửi báo cáo lỗi, mở pull request và [gửi RFC](https://github.com/reactjs/rfcs). Để khuyến khích phản hồi, đôi khi chúng tôi chia sẻ các bản dựng React đặc biệt có chứa những tính năng chưa được phát hành.

<Note>

Phần này sẽ liên quan nhất với các nhà phát triển làm việc trên framework, thư viện hoặc công cụ dành cho lập trình viên. Những người chủ yếu dùng React để xây dựng ứng dụng hướng tới người dùng cuối thường không cần phải bận tâm đến các kênh phát hành trước của chúng tôi.

</Note>

Mỗi kênh phát hành của React được thiết kế cho một trường hợp sử dụng riêng:

- [**Latest**](#latest-channel) dành cho các bản phát hành React ổn định theo semver. Đây là thứ bạn nhận được khi cài React từ npm. Đây cũng là kênh bạn đang dùng hôm nay. **Các ứng dụng hướng tới người dùng cuối sử dụng React trực tiếp sẽ dùng kênh này.**
- [**Canary**](#canary-channel) theo dõi nhánh chính của kho mã nguồn React. Hãy xem chúng như các bản ứng viên phát hành cho bản semver tiếp theo. **[Framework hoặc các thiết lập được quản lý khác có thể chọn dùng kênh này với một phiên bản React đã được pin.](/blog/2023/05/03/react-canaries) Bạn cũng có thể dùng Canary để kiểm thử tích hợp giữa React và các dự án bên thứ ba.**
- [**Experimental**](#experimental-channel) bao gồm các API và tính năng thử nghiệm chưa có trong các bản phát hành ổn định. Chúng cũng theo dõi nhánh chính, nhưng có thêm các feature flag được bật. Hãy dùng kênh này để thử các tính năng sắp tới trước khi chúng được phát hành.

Mọi bản phát hành đều được đưa lên npm, nhưng chỉ Latest sử dụng semantic versioning. Các bản phát hành trước, tức là Canary và Experimental, có phiên bản được sinh ra từ mã hash của nội dung và ngày commit, ví dụ `18.3.0-canary-388686f29-20230503` cho Canary và `0.0.0-experimental-388686f29-20230503` cho Experimental.

**Cả Latest và Canary đều được hỗ trợ chính thức cho các ứng dụng hướng tới người dùng cuối, nhưng với kỳ vọng khác nhau**:

* Bản phát hành Latest tuân theo mô hình semver truyền thống.
* Bản phát hành Canary [phải được pin](/blog/2023/05/03/react-canaries) và có thể bao gồm thay đổi gây lỗi tương thích. Chúng tồn tại cho các thiết lập được quản lý, chẳng hạn như framework, muốn phát hành dần các tính năng mới và bản sửa lỗi của React theo lịch phát hành riêng của họ.

Các bản phát hành Experimental chỉ được cung cấp cho mục đích kiểm thử, và chúng tôi không đưa ra bất kỳ bảo đảm nào rằng hành vi sẽ không thay đổi giữa các lần phát hành. Chúng không tuân theo giao thức semver mà chúng tôi dùng cho Latest.

Bằng cách phát hành các bản prerelease lên cùng registry với các bản phát hành ổn định, chúng tôi có thể tận dụng nhiều công cụ hỗ trợ quy trình npm như [unpkg](https://unpkg.com) và [CodeSandbox](https://codesandbox.io).

### Kênh Latest {/*latest-channel*/}

Latest là kênh dùng cho các bản phát hành React ổn định. Nó tương ứng với tag `latest` trên npm. Đây là kênh được khuyến nghị cho mọi ứng dụng React được phát hành cho người dùng thực.

**Nếu bạn không chắc mình nên dùng kênh nào, hãy dùng Latest.** Nếu bạn đang dùng React trực tiếp, đây chính là kênh bạn đang sử dụng. Bạn có thể kỳ vọng các bản cập nhật của Latest sẽ cực kỳ ổn định. Các phiên bản tuân theo quy ước semantic versioning như [đã mô tả ở trên](#stable-releases).

### Kênh Canary {/*canary-channel*/}

Kênh Canary là một kênh prerelease theo dõi nhánh chính của kho lưu trữ React. Chúng tôi dùng các bản prerelease trong kênh Canary như những bản ứng viên phát hành cho kênh Latest. Bạn có thể xem Canary là một tập mở rộng của Latest được cập nhật thường xuyên hơn.

Mức độ thay đổi giữa bản phát hành Canary mới nhất và bản Latest mới nhất xấp xỉ với mức thay đổi giữa hai bản phát hành minor theo semver. Tuy nhiên, **kênh Canary không tuân theo semantic versioning.** Bạn nên kỳ vọng thỉnh thoảng sẽ có thay đổi gây lỗi tương thích giữa các bản phát hành liên tiếp trong kênh Canary.

**Không dùng trực tiếp các bản prerelease trong ứng dụng hướng tới người dùng cuối, trừ khi bạn đang làm theo [quy trình Canary](/blog/2023/05/03/react-canaries).**

Các bản phát hành trong Canary được xuất bản với tag `canary` trên npm. Phiên bản được tạo từ mã hash của nội dung bản dựng và ngày commit, ví dụ `18.3.0-canary-388686f29-20230503`.

#### Dùng kênh canary cho kiểm thử tích hợp {/*using-the-canary-channel-for-integration-testing*/}

Kênh Canary cũng hỗ trợ kiểm thử tích hợp giữa React và các dự án khác.

Mọi thay đổi của React đều trải qua quá trình kiểm thử nội bộ sâu rộng trước khi được phát hành công khai. Tuy nhiên, có vô số môi trường và cấu hình được dùng trong hệ sinh thái React, và chúng tôi không thể kiểm thử trên từng trường hợp một.

Nếu bạn là tác giả của một framework React bên thứ ba, thư viện, công cụ cho lập trình viên hoặc một dự án hạ tầng tương tự, bạn có thể giúp chúng tôi giữ React ổn định cho người dùng của bạn và cho toàn bộ cộng đồng React bằng cách định kỳ chạy bộ kiểm thử của mình với các thay đổi mới nhất. Nếu bạn quan tâm, hãy làm theo các bước sau:

- Thiết lập một cron job bằng nền tảng continuous integration bạn ưa thích. Cả [CircleCI](https://circleci.com/docs/2.0/triggers/#scheduled-builds) và [Travis CI](https://docs.travis-ci.com/user/cron-jobs/) đều hỗ trợ cron job.
- Trong cron job đó, cập nhật các package React của bạn lên bản React mới nhất trong kênh Canary bằng cách dùng tag `canary` trên npm. Nếu dùng npm cli:

  ```console
  npm update react@canary react-dom@canary
  ```

  Hoặc nếu dùng yarn:

  ```console
  yarn upgrade react@canary react-dom@canary
  ```
- Chạy bộ kiểm thử của bạn với các package đã được cập nhật.
- Nếu mọi thứ đều pass, rất tốt. Bạn có thể kỳ vọng dự án của mình sẽ hoạt động với bản phát hành minor React tiếp theo.
- Nếu có điều gì đó hỏng một cách bất ngờ, vui lòng cho chúng tôi biết bằng cách [tạo issue](https://github.com/facebook/react/issues).

Một dự án dùng quy trình này là Next.js. Bạn có thể tham khảo [cấu hình CircleCI của họ](https://github.com/zeit/next.js/blob/c0a1c0f93966fe33edd93fb53e5fafb0dcd80a9e/.circleci/config.yml) làm ví dụ.

### Kênh Experimental {/*experimental-channel*/}

Giống Canary, kênh Experimental là một kênh prerelease theo dõi nhánh chính của kho React. Khác với Canary, các bản phát hành Experimental bao gồm thêm những tính năng và API chưa sẵn sàng để phát hành rộng rãi.

Thông thường, một bản cập nhật cho Canary sẽ đi kèm với một bản cập nhật tương ứng cho Experimental. Chúng dựa trên cùng một phiên bản mã nguồn, nhưng được dựng với bộ feature flag khác nhau.

Bản phát hành Experimental có thể khác biệt đáng kể so với Canary và Latest. **Không dùng các bản phát hành Experimental trong ứng dụng hướng tới người dùng cuối.** Bạn nên kỳ vọng sẽ có những thay đổi gây lỗi tương thích thường xuyên giữa các lần phát hành trong kênh Experimental.

Các bản phát hành Experimental được xuất bản với tag `experimental` trên npm. Phiên bản được tạo từ mã hash của nội dung bản dựng và ngày commit, ví dụ `0.0.0-experimental-68053d940-20210623`.

#### Điều gì được đưa vào một bản phát hành experimental? {/*what-goes-into-an-experimental-release*/}

Các tính năng experimental là những tính năng chưa sẵn sàng để phát hành rộng rãi và có thể thay đổi mạnh trước khi được hoàn thiện. Một số thử nghiệm có thể sẽ không bao giờ được hoàn thiện. Lý do chúng tôi có các thử nghiệm là để kiểm chứng tính khả thi của những thay đổi được đề xuất.

Ví dụ, nếu kênh Experimental đã tồn tại vào thời điểm chúng tôi công bố Hooks, chúng tôi đã có thể phát hành Hooks lên kênh Experimental trước hàng tuần so với lúc chúng có mặt trên Latest.

Bạn có thể thấy việc chạy kiểm thử tích hợp với Experimental là hữu ích. Điều này tùy thuộc vào bạn. Tuy nhiên, hãy lưu ý rằng Experimental còn kém ổn định hơn cả Canary. **Chúng tôi không bảo đảm bất kỳ mức độ ổn định nào giữa các bản phát hành Experimental.**

#### Làm sao để tìm hiểu thêm về các tính năng experimental? {/*how-can-i-learn-more-about-experimental-features*/}

Các tính năng experimental có thể có hoặc không có tài liệu. Thông thường, các thử nghiệm sẽ không được tài liệu hóa cho tới khi chúng gần sẵn sàng phát hành trên Canary hoặc Latest.

Nếu một tính năng chưa được tài liệu hóa, nó có thể đi kèm với một [RFC](https://github.com/reactjs/rfcs).

Chúng tôi sẽ đăng lên [blog React](/blog) khi sẵn sàng công bố các thử nghiệm mới, nhưng điều đó không có nghĩa là mọi thử nghiệm đều sẽ được công khai rộng rãi.

Bạn luôn có thể tham khảo [lịch sử](https://github.com/facebook/react/commits/main) của kho GitHub công khai của chúng tôi để xem danh sách đầy đủ các thay đổi.
