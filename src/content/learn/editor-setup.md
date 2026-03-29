---
title: Thiết lập trình soạn thảo
---

<Intro>

Một trình soạn thảo được cấu hình đúng cách có thể giúp code dễ đọc hơn và viết nhanh hơn. Nó thậm chí còn có thể giúp bạn phát hiện lỗi ngay khi đang gõ! Nếu đây là lần đầu bạn thiết lập trình soạn thảo hoặc bạn muốn tinh chỉnh trình soạn thảo hiện tại, chúng tôi có một vài khuyến nghị.

</Intro>

<YouWillLearn>

* Những trình soạn thảo phổ biến nhất là gì
* Cách tự động định dạng code của bạn

</YouWillLearn>

## Trình soạn thảo của bạn {/*your-editor*/}

[VS Code](https://code.visualstudio.com/) là một trong những trình soạn thảo phổ biến nhất hiện nay. Nó có kho tiện ích mở rộng rất lớn và tích hợp tốt với các dịch vụ phổ biến như GitHub. Phần lớn các tính năng được liệt kê bên dưới cũng có thể được thêm vào VS Code dưới dạng tiện ích mở rộng, khiến nó có khả năng tùy biến rất cao!

Những trình soạn thảo văn bản phổ biến khác trong cộng đồng React bao gồm:

* [WebStorm](https://www.jetbrains.com/webstorm/) là môi trường phát triển tích hợp được thiết kế riêng cho JavaScript.
* [Sublime Text](https://www.sublimetext.com/) có hỗ trợ JSX và TypeScript, [tô sáng cú pháp](https://stackoverflow.com/a/70960574/458193) và tự động hoàn thành được tích hợp sẵn.
* [Vim](https://www.vim.org/) là trình soạn thảo văn bản có khả năng tùy biến cao, được xây dựng để việc tạo và chỉnh sửa mọi loại văn bản trở nên rất hiệu quả. Nó được đi kèm dưới tên "vi" trong hầu hết các hệ thống UNIX và Apple OS X.

## Tính năng trình soạn thảo được khuyến nghị {/*recommended-text-editor-features*/}

Một số trình soạn thảo đã có sẵn những tính năng này, nhưng những trình khác có thể yêu cầu cài thêm tiện ích mở rộng. Hãy kiểm tra xem trình soạn thảo bạn chọn hỗ trợ những gì để chắc chắn.

### Linting {/*linting*/}

Trình lint code phát hiện vấn đề trong code của bạn ngay khi bạn viết, giúp bạn sửa chúng sớm. [ESLint](https://eslint.org/) là một trình lint mã nguồn mở phổ biến cho JavaScript.

* [Cài ESLint với cấu hình được khuyến nghị cho React](https://www.npmjs.com/package/eslint-config-react-app) (hãy chắc chắn bạn đã [cài Node!](https://nodejs.org/en/download/current/))
* [Tích hợp ESLint vào VSCode bằng tiện ích mở rộng chính thức](https://marketplace.visualstudio.com/items?itemName=dbaeumer.vscode-eslint)

**Hãy chắc chắn rằng bạn đã bật toàn bộ các quy tắc của [`eslint-plugin-react-hooks`](https://www.npmjs.com/package/eslint-plugin-react-hooks) cho dự án của mình.** Chúng rất quan trọng và phát hiện những lỗi nghiêm trọng nhất từ sớm. Preset [`eslint-config-react-app`](https://www.npmjs.com/package/eslint-config-react-app) được khuyến nghị đã bao gồm chúng.

### Định dạng {/*formatting*/}

Điều cuối cùng bạn muốn làm khi chia sẻ code với người đóng góp khác là lao vào cuộc tranh luận về [tab hay space](https://www.google.com/search?q=tabs+vs+spaces)! May mắn là [Prettier](https://prettier.io/) sẽ dọn dẹp code của bạn bằng cách định dạng lại để tuân theo các quy tắc có sẵn và có thể cấu hình. Hãy chạy Prettier, và toàn bộ tab của bạn sẽ được chuyển thành space; phần thụt lề, dấu nháy, v.v. cũng sẽ được thay đổi để phù hợp với cấu hình. Trong thiết lập lý tưởng, Prettier sẽ chạy mỗi khi bạn lưu tệp và nhanh chóng thực hiện các chỉnh sửa này giúp bạn.

Bạn có thể cài [tiện ích mở rộng Prettier cho VSCode](https://marketplace.visualstudio.com/items?itemName=esbenp.prettier-vscode) bằng các bước sau:

1. Mở VS Code
2. Dùng Quick Open bằng cách nhấn `Ctrl/Cmd+P`
3. Dán `ext install esbenp.prettier-vscode`
4. Nhấn Enter

#### Định dạng khi lưu {/*formatting-on-save*/}

Lý tưởng nhất là bạn nên định dạng code ở mỗi lần lưu. VS Code có sẵn cài đặt cho việc này!

1. Trong VS Code, nhấn `CTRL/CMD + SHIFT + P`.
2. Gõ "settings"
3. Nhấn Enter
4. Trong ô tìm kiếm, gõ "format on save"
5. Hãy chắc chắn rằng tùy chọn "format on save" đã được bật!

> Nếu preset ESLint của bạn có các quy tắc định dạng, chúng có thể xung đột với Prettier. Chúng tôi khuyến nghị tắt toàn bộ quy tắc định dạng trong preset ESLint của bạn bằng [`eslint-config-prettier`](https://github.com/prettier/eslint-config-prettier) để ESLint *chỉ* được dùng cho việc phát hiện lỗi logic. Nếu bạn muốn bắt buộc tệp phải được định dạng trước khi pull request được hợp nhất, hãy dùng [`prettier --check`](https://prettier.io/docs/en/cli.html#--check) trong quy trình tích hợp liên tục của bạn.
