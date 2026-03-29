---
title: Cảnh báo về prop ARIA không hợp lệ
---

Cảnh báo này sẽ xuất hiện nếu bạn cố gắng render một phần tử DOM với một prop `aria-*` không tồn tại trong [đặc tả](https://www.w3.org/TR/wai-aria-1.1/#states_and_properties) Accessible Rich Internet Application (ARIA) của Web Accessibility Initiative (WAI).

1. Nếu bạn cho rằng mình đang dùng một prop hợp lệ, hãy kiểm tra thật kỹ chính tả. `aria-labelledby` và `aria-activedescendant` thường hay bị viết sai.

2. Nếu bạn viết `aria-role`, rất có thể bạn muốn dùng `role`.

3. Nếu không, và bạn đang dùng phiên bản React DOM mới nhất đồng thời đã xác minh rằng mình đang dùng một tên thuộc tính hợp lệ có trong đặc tả ARIA, vui lòng [báo lỗi](https://github.com/facebook/react/issues/new/choose).
