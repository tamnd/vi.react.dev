---
title: Cảnh báo ngừng dùng `react-test-renderer`
---

## Cảnh báo `ReactTestRenderer.create()` {/*reacttestrenderercreate-warning*/}

`react-test-renderer` đã bị ngừng khuyến nghị sử dụng. Cảnh báo sẽ xuất hiện mỗi khi gọi `ReactTestRenderer.create()` hoặc `ReactShallowRender.render()`. Gói `react-test-renderer` vẫn sẽ có trên NPM nhưng sẽ không còn được bảo trì và có thể bị lỗi khi React có tính năng mới hoặc thay đổi nội bộ.

Nhóm React khuyến nghị bạn chuyển bài kiểm thử sang [@testing-library/react](https://testing-library.com/docs/react-testing-library/intro/) hoặc [@testing-library/react-native](https://callstack.github.io/react-native-testing-library/docs/start/intro) để có trải nghiệm kiểm thử hiện đại và được hỗ trợ tốt hơn.


## Cảnh báo `new ShallowRenderer()` {/*new-shallowrenderer-warning*/}

Gói `react-test-renderer` không còn export shallow renderer tại `react-test-renderer/shallow` nữa. Đây vốn chỉ là cách đóng gói lại của một gói riêng đã được tách ra trước đó: `react-shallow-renderer`. Vì vậy, bạn vẫn có thể tiếp tục dùng shallow renderer theo cùng cách bằng cách cài trực tiếp gói này. Xem tại [GitHub](https://github.com/enzymejs/react-shallow-renderer) / [NPM](https://www.npmjs.com/package/react-shallow-renderer).
