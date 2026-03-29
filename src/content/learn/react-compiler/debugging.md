---
title: Gỡ lỗi và khắc phục sự cố
---

<Intro>
Hướng dẫn này giúp bạn xác định và sửa lỗi khi dùng React Compiler. Bạn sẽ học cách gỡ lỗi các vấn đề biên dịch và xử lý những lỗi thường gặp.
</Intro>

<YouWillLearn>

* Sự khác nhau giữa lỗi compiler và vấn đề thời gian chạy
* Những mẫu phổ biến làm hỏng quá trình biên dịch
* Quy trình gỡ lỗi từng bước

</YouWillLearn>

## Hiểu cách compiler hoạt động {/*understanding-compiler-behavior*/}

React Compiler được thiết kế để xử lý code tuân theo [Các quy tắc của React](/reference/rules). Khi gặp code có thể vi phạm các quy tắc này, nó sẽ an toàn bỏ qua tối ưu hóa thay vì mạo hiểm làm thay đổi hành vi của ứng dụng.

### Lỗi compiler và vấn đề thời gian chạy {/*compiler-errors-vs-runtime-issues*/}

**Lỗi compiler** xảy ra ở thời điểm build và ngăn code của bạn được biên dịch. Những lỗi này hiếm gặp vì compiler được thiết kế để bỏ qua code có vấn đề thay vì thất bại.

**Vấn đề thời gian chạy** xảy ra khi code đã biên dịch hoạt động khác với mong đợi. Phần lớn thời gian, nếu bạn gặp vấn đề với React Compiler thì đó là vấn đề thời gian chạy. Điều này thường xảy ra khi code của bạn vi phạm Các quy tắc của React theo những cách tinh vi mà compiler không phát hiện được, và compiler đã nhầm lẫn biên dịch một thành phần đáng lẽ nên bị bỏ qua.

Khi gỡ lỗi các vấn đề thời gian chạy, hãy tập trung tìm các vi phạm Quy tắc của React trong những thành phần bị ảnh hưởng mà luật ESLint chưa phát hiện ra. Compiler dựa vào việc code của bạn tuân theo những quy tắc này, và khi chúng bị phá vỡ theo cách mà compiler không thể phát hiện, đó là lúc vấn đề thời gian chạy xuất hiện.


## Các mẫu thường làm hỏng ứng dụng {/*common-breaking-patterns*/}

Một trong những cách chính khiến React Compiler có thể làm hỏng ứng dụng là khi code của bạn được viết để dựa vào memoization cho tính đúng đắn. Điều này nghĩa là ứng dụng phụ thuộc vào việc một số giá trị cụ thể phải được memoize thì mới hoạt động đúng. Vì compiler có thể memoize khác với cách thủ công của bạn, điều đó có thể dẫn đến hành vi bất ngờ như effect chạy quá nhiều, vòng lặp vô hạn hoặc thiếu cập nhật.

Các tình huống phổ biến gồm:

- **Effect dựa vào tính bằng nhau theo tham chiếu** - Khi effect phụ thuộc vào việc object hoặc array giữ nguyên cùng một tham chiếu qua các lần kết xuất
- **Mảng dependency cần tham chiếu ổn định** - Khi dependency không ổn định khiến effect chạy quá thường xuyên hoặc tạo vòng lặp vô hạn
- **Logic điều kiện dựa trên kiểm tra tham chiếu** - Khi code dùng phép kiểm tra bằng nhau theo tham chiếu để cache hoặc tối ưu hóa

## Quy trình gỡ lỗi {/*debugging-workflow*/}

Hãy làm theo các bước sau khi bạn gặp sự cố:

### Lỗi build của compiler {/*compiler-build-errors*/}

Nếu bạn gặp một lỗi compiler bất ngờ làm hỏng quá trình build, rất có thể đó là lỗi của compiler. Hãy báo cáo nó cho kho [facebook/react](https://github.com/facebook/react/issues) kèm theo:
- Thông báo lỗi
- Đoạn code gây ra lỗi
- Phiên bản React và compiler bạn đang dùng

### Vấn đề thời gian chạy {/*runtime-issues*/}

Đối với các vấn đề về hành vi thời gian chạy:

### 1. Tạm thời vô hiệu hóa biên dịch {/*temporarily-disable-compilation*/}

Dùng `"use no memo"` để tách biệt xem vấn đề có liên quan đến compiler hay không:

```js
function ProblematicComponent() {
  "use no memo"; // Skip compilation for this component
  // ... rest of component
}
```

Nếu vấn đề biến mất, nhiều khả năng nó liên quan đến một vi phạm Quy tắc của React.

Bạn cũng có thể thử bỏ memoization thủ công (`useMemo`, `useCallback`, `memo`) khỏi thành phần có vấn đề để kiểm tra xem ứng dụng của bạn có hoạt động đúng mà không cần bất kỳ memoization nào không. Nếu lỗi vẫn xảy ra khi toàn bộ memoization đã được loại bỏ, bạn đang có một vi phạm Quy tắc của React cần được sửa.

### 2. Sửa lỗi từng bước {/*fix-issues-step-by-step*/}

1. Xác định nguyên nhân gốc (thường là memoization vì tính đúng đắn)
2. Kiểm tra lại sau mỗi lần sửa
3. Gỡ `"use no memo"` sau khi đã sửa xong
4. Xác minh thành phần hiển thị huy hiệu ✨ trong React DevTools

## Báo lỗi compiler {/*reporting-compiler-bugs*/}

Nếu bạn tin rằng mình đã tìm thấy lỗi của compiler:

1. **Xác minh đó không phải là vi phạm Quy tắc của React** - Kiểm tra bằng ESLint
2. **Tạo ví dụ tái hiện tối thiểu** - Cô lập vấn đề trong một ví dụ nhỏ
3. **Kiểm tra khi không dùng compiler** - Xác nhận rằng vấn đề chỉ xảy ra khi có biên dịch
4. **Tạo một [issue](https://github.com/facebook/react/issues/new?template=compiler_bug_report.yml)**:
   - Phiên bản React và compiler
   - Mã tái hiện tối thiểu
   - Hành vi kỳ vọng so với thực tế
   - Mọi thông báo lỗi

## Bước tiếp theo {/*next-steps*/}

- Xem lại [Các quy tắc của React](/reference/rules) để ngăn lỗi phát sinh
- Xem [hướng dẫn áp dụng dần](/learn/react-compiler/incremental-adoption) để có chiến lược triển khai từng bước
