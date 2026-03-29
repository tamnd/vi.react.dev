---
title: eslint-plugin-react-hooks
version: rc
---

<Intro>

`eslint-plugin-react-hooks` cung cấp các quy tắc ESLint để áp dụng [Các quy tắc của React](/reference/rules).

</Intro>

Plugin này giúp bạn phát hiện các vi phạm quy tắc của React ngay tại thời điểm build, bảo đảm component và Hook của bạn tuân theo các quy tắc của React để đạt được tính đúng đắn và hiệu năng. Các lint bao phủ cả những mẫu React nền tảng (`exhaustive-deps` và `rules-of-hooks`) lẫn những vấn đề do React Compiler gắn cờ. Các chẩn đoán từ React Compiler sẽ tự động được hiển thị qua plugin ESLint này, và có thể dùng ngay cả khi ứng dụng của bạn chưa áp dụng compiler.

<Note>
Khi compiler báo một chẩn đoán, điều đó có nghĩa là compiler đã có thể phát hiện tĩnh một mẫu không được hỗ trợ hoặc vi phạm Các quy tắc của React. Khi phát hiện điều đó, nó sẽ **tự động** bỏ qua những component và Hook đó, đồng thời vẫn tiếp tục biên dịch phần còn lại của ứng dụng. Điều này bảo đảm độ phủ tối ưu cho các tối ưu hóa an toàn mà không làm hỏng ứng dụng của bạn.

Điều này có nghĩa là với linting, bạn không cần sửa ngay mọi vi phạm. Hãy xử lý chúng theo tốc độ phù hợp để dần tăng số lượng component được tối ưu hóa.
</Note>

## Quy tắc được khuyến nghị {/*recommended*/}

Những quy tắc này được bao gồm trong preset `recommended` của `eslint-plugin-react-hooks`:

* [`exhaustive-deps`](/reference/eslint-plugin-react-hooks/lints/exhaustive-deps) - Kiểm tra rằng mảng dependency của React Hook chứa đầy đủ các dependency cần thiết
* [`rules-of-hooks`](/reference/eslint-plugin-react-hooks/lints/rules-of-hooks) - Kiểm tra rằng component và Hook tuân theo Rules of Hooks
* [`component-hook-factories`](/reference/eslint-plugin-react-hooks/lints/component-hook-factories) - Kiểm tra các hàm bậc cao định nghĩa component hoặc Hook lồng nhau
* [`config`](/reference/eslint-plugin-react-hooks/lints/config) - Kiểm tra các tùy chọn cấu hình của compiler
* [`error-boundaries`](/reference/eslint-plugin-react-hooks/lints/error-boundaries) - Kiểm tra việc dùng Error Boundaries thay cho try/catch với lỗi của component con
* [`gating`](/reference/eslint-plugin-react-hooks/lints/gating) - Kiểm tra cấu hình của chế độ gating
* [`globals`](/reference/eslint-plugin-react-hooks/lints/globals) - Kiểm tra việc gán/thay đổi biến toàn cục trong lúc render
* [`immutability`](/reference/eslint-plugin-react-hooks/lints/immutability) - Kiểm tra việc thay đổi props, state và các giá trị bất biến khác
* [`incompatible-library`](/reference/eslint-plugin-react-hooks/lints/incompatible-library) - Kiểm tra việc dùng các thư viện không tương thích với memoization
* [`preserve-manual-memoization`](/reference/eslint-plugin-react-hooks/lints/preserve-manual-memoization) - Kiểm tra rằng compiler vẫn giữ nguyên phần memoization thủ công hiện có
* [`purity`](/reference/eslint-plugin-react-hooks/lints/purity) - Kiểm tra rằng component/Hook là thuần bằng cách dò các hàm đã biết là không thuần
* [`refs`](/reference/eslint-plugin-react-hooks/lints/refs) - Kiểm tra cách dùng ref đúng đắn, không đọc/ghi trong lúc render
* [`set-state-in-effect`](/reference/eslint-plugin-react-hooks/lints/set-state-in-effect) - Kiểm tra việc gọi `setState` đồng bộ bên trong một Effect
* [`set-state-in-render`](/reference/eslint-plugin-react-hooks/lints/set-state-in-render) - Kiểm tra việc đặt state trong lúc render
* [`static-components`](/reference/eslint-plugin-react-hooks/lints/static-components) - Kiểm tra rằng component là tĩnh, không bị tạo lại ở mỗi lần render
* [`unsupported-syntax`](/reference/eslint-plugin-react-hooks/lints/unsupported-syntax) - Kiểm tra cú pháp mà React Compiler không hỗ trợ
* [`use-memo`](/reference/eslint-plugin-react-hooks/lints/use-memo) - Kiểm tra cách dùng Hook `useMemo` khi không có giá trị trả về
