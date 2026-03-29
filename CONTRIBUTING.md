# Đóng góp

Cảm ơn bạn đã quan tâm đến việc đóng góp cho tài liệu React.

## Quy tắc ứng xử

Facebook đã áp dụng một bộ Quy tắc ứng xử mà mọi người tham gia dự án được kỳ vọng sẽ tuân theo. Hãy [đọc toàn văn](https://code.facebook.com/codeofconduct) để hiểu hành vi nào được chấp nhận và hành vi nào không được chấp nhận.

## Mẹo viết tài liệu kỹ thuật

Đây là một [bài tổng kết hữu ích](https://medium.com/@kvosswinkel/coding-like-a-journalist-ee52360a16bc) về những điều nên lưu ý khi viết tài liệu kỹ thuật.

## Hướng dẫn cho phần văn bản

**Mỗi phần được viết với phong cách khác nhau một cách có chủ đích.**

Tài liệu được chia thành nhiều phần để phục vụ các kiểu học tập và nhu cầu sử dụng khác nhau. Khi chỉnh sửa một bài viết, hãy cố gắng giữ giọng điệu và phong cách của phần văn bản xung quanh. Khi tạo bài mới, hãy cố gắng khớp với giọng điệu của các bài khác trong cùng phần. Dưới đây là lý do cho từng phần.

**[Learn React](https://react.dev/learn)** được thiết kế để giới thiệu các khái niệm nền tảng theo từng bước. Mỗi bài trong Learn React đều dựa trên kiến thức của các bài trước đó, vì vậy đừng tạo ra các "phụ thuộc vòng tròn" giữa chúng. Điều quan trọng là người đọc có thể bắt đầu từ bài đầu tiên và đi đến bài cuối cùng mà không phải "đọc trước" để tìm định nghĩa. Điều này giải thích cho một số lựa chọn về thứ tự (ví dụ: state được giải thích trước event, hoặc "Thinking in React" không dùng ref). Learn React cũng đóng vai trò như một sổ tay tra cứu cho các khái niệm của React, nên cần đặc biệt chặt chẽ trong cách định nghĩa và mô tả quan hệ giữa chúng.

**[API Reference](https://react.dev/reference/react)** được tổ chức theo API thay vì theo khái niệm. Phần này cần đầy đủ. Mọi trường hợp góc cạnh hoặc khuyến nghị bị lược bỏ trong Learn React để giữ ngắn gọn nên được nêu ở tài liệu tham chiếu của API tương ứng.

**Hãy tự làm theo chính hướng dẫn của mình.**

Khi viết hướng dẫn từng bước, chẳng hạn cách cài đặt một công cụ, hãy cố quên đi những gì bạn đã biết và thực sự làm theo các bước mình vừa viết, từng bước một. Bạn thường sẽ phát hiện ra có kiến thức ngầm mà mình quên nhắc đến, hoặc có bước còn thiếu hay sai thứ tự. Nếu có thể, hãy nhờ người khác làm theo hướng dẫn đó và quan sát họ vướng ở đâu. Thường thì đó lại là những chỗ rất đơn giản mà bạn không ngờ tới.

## Hướng dẫn cho ví dụ mã

### Cú pháp

#### Ưu tiên JSX hơn `createElement`.

Bỏ qua quy tắc này nếu bạn đang giải thích riêng về `createElement`.

#### Dùng `const` khi có thể, nếu không thì dùng `let`. Không dùng `var`.

Bỏ qua quy tắc này nếu bạn đang viết riêng về ES5.

#### Đừng dùng tính năng ES6 nếu phiên bản ES5 tương đương không có nhược điểm gì.

Hãy nhớ rằng ES6 vẫn còn khá mới với nhiều người. Dù tài liệu có dùng nhiều tính năng như `const` / `let`, class, hay arrow function, bạn vẫn nên cân nhắc dùng mã ES5 nếu nó rõ ràng và dễ đọc không kém.

Đặc biệt, với các hàm cấp cao nhất, hãy ưu tiên khai báo `function` có tên thay vì `const myFunction = () => ...`. Tuy vậy, bạn vẫn nên dùng arrow function khi nó thực sự cải thiện mã, chẳng hạn để giữ ngữ cảnh `this` bên trong một component. Hãy cân nhắc cả hai mặt trước khi quyết định dùng một tính năng mới.

#### Đừng dùng những tính năng chưa được chuẩn hóa.

Ví dụ, **đừng** viết thế này:

```js
class MyComponent extends React.Component {
  state = {value: ''};
  handleChange = (e) => {
    this.setState({value: e.target.value});
  };
}
```

Thay vào đó, **hãy** viết như sau:

```js
class MyComponent extends React.Component {
  constructor(props) {
    super(props);
    this.handleChange = this.handleChange.bind(this);
    this.state = {value: ''};
  }
  handleChange(e) {
    this.setState({value: e.target.value});
  }
}
```

Bỏ qua quy tắc này nếu bạn đang mô tả riêng một proposal thử nghiệm. Hãy chắc chắn rằng bạn đã nêu rõ tính chất thử nghiệm của nó trong cả đoạn mã lẫn phần văn bản xung quanh.

### Phong cách mã

- Dùng dấu chấm phẩy.
- Không chèn khoảng trắng giữa tên hàm và dấu ngoặc (`method() {}` chứ không phải `method () {}`).
- Nếu phân vân, hãy dùng phong cách mặc định của [Prettier](https://prettier.io/playground/).
- Luôn viết hoa tên các khái niệm React như Hooks, Effects, và Transitions.

### Tô sáng mã

Dùng `js` làm ngôn ngữ highlight trong các khối mã Markdown:

````
```js
// code
```
````

Đôi khi bạn sẽ thấy các khối mã có kèm số.
Chúng cho website biết cần tô sáng dòng nào.

Bạn có thể tô sáng một dòng:

````
```js {2}
function hello() {
  // this line will get highlighted
}
```
````

Một dải dòng:

````
```js {2-4}
function hello() {
  // these lines
  // will get
  // highlighted
}
```
````

Hoặc nhiều dải dòng:

````
```js {2-4,6}
function hello() {
  // these lines
  // will get
  // highlighted
  console.log('hello');
  // also this one
  console.log('there');
}
```
````

Hãy lưu ý rằng nếu bạn di chuyển mã trong một ví dụ có highlight, bạn cũng cần cập nhật lại phần highlight.

Đừng ngại dùng highlight thường xuyên. Nó rất hữu ích khi bạn cần hướng sự chú ý của người đọc vào một chi tiết cụ thể dễ bị bỏ sót.
