---
title: incompatible-library
---

<Intro>

Kiểm tra việc sử dụng các thư viện không tương thích với memoization, dù là thủ công hay tự động.

</Intro>

<Note>

Những thư viện này được thiết kế trước khi các quy tắc về memoization của React được ghi lại đầy đủ. Tại thời điểm đó, chúng đã đưa ra những lựa chọn hợp lý để giữ cho component vừa đủ phản ứng khi state của ứng dụng thay đổi. Dù các mẫu cũ này từng hoạt động, giờ chúng tôi đã biết rằng chúng không tương thích với mô hình lập trình của React. Chúng tôi sẽ tiếp tục làm việc với tác giả thư viện để chuyển các thư viện này sang các mẫu tuân theo Các quy tắc của React.

</Note>

## Chi tiết luật {/*rule-details*/}

Một số thư viện dùng các mẫu mà React không hỗ trợ. Khi linter phát hiện cách dùng các API này từ một [danh sách đã biết](https://github.com/facebook/react/blob/main/compiler/packages/babel-plugin-react-compiler/src/HIR/DefaultModuleTypeProvider.ts), nó sẽ gắn cờ theo luật này. Điều này có nghĩa là React Compiler có thể tự động bỏ qua các component sử dụng những API không tương thích đó để tránh làm hỏng ứng dụng của bạn.

```js
// Example of how memoization breaks with these libraries
function Form() {
  const { watch } = useForm();

  // ❌ This value will never update, even when 'name' field changes
  const name = useMemo(() => watch('name'), [watch]);

  return <div>Name: {name}</div>; // UI appears "frozen"
}
```

React Compiler tự động memoize các giá trị tuân theo Các quy tắc của React. Nếu một thứ bị hỏng với `useMemo` thủ công, nó cũng sẽ làm hỏng tối ưu hóa tự động của compiler. Luật này giúp xác định các mẫu có vấn đề đó.

<DeepDive>

#### Thiết kế API tuân theo Các quy tắc của React {/*designing-apis-that-follow-the-rules-of-react*/}

Một câu hỏi nên tự đặt ra khi thiết kế API hay Hook cho thư viện là: liệu lời gọi API đó có thể được memoize an toàn bằng `useMemo` không. Nếu không, cả memoization thủ công lẫn memoization của React Compiler đều sẽ làm hỏng code của người dùng.

Ví dụ, một mẫu không tương thích là "interior mutability". Đây là khi một object hoặc function giữ state ẩn của riêng nó thay đổi theo thời gian, dù tham chiếu đến nó vẫn không đổi. Hãy tưởng tượng một chiếc hộp trông vẫn y hệt ở bên ngoài nhưng bên trong lại bí mật thay đổi đồ đạc. React không thể biết có gì thay đổi vì nó chỉ kiểm tra xem bạn có đưa cho nó một chiếc hộp khác hay không, chứ không nhìn vào bên trong. Điều này phá vỡ memoization, vì React dựa vào việc object hoặc function bên ngoài phải thay đổi nếu một phần giá trị của nó đã thay đổi.

Như một quy tắc ngón tay cái, khi thiết kế API cho React, hãy nghĩ xem `useMemo` có làm nó hỏng không:

```js
function Component() {
  const { someFunction } = useLibrary();
  // it should always be safe to memoize functions like this
  const result = useMemo(() => someFunction(), [someFunction]);
}
```

Thay vào đó, hãy thiết kế API trả về state bất biến và dùng các hàm cập nhật tường minh:

```js
// ✅ Good: Return immutable state that changes reference when updated
function Component() {
  const { field, updateField } = useLibrary();
  // this is always safe to memo
  const greeting = useMemo(() => `Hello, ${field.name}!`, [field.name]);

  return (
    <div>
      <input
        value={field.name}
        onChange={(e) => updateField('name', e.target.value)}
      />
      <p>{greeting}</p>
    </div>
  );
}
```

</DeepDive>

### Không hợp lệ {/*invalid*/}

Ví dụ về mã không đúng cho luật này:

```js
// ❌ react-hook-form `watch`
function Component() {
  const {watch} = useForm();
  const value = watch('field'); // Interior mutability
  return <div>{value}</div>;
}

// ❌ TanStack Table `useReactTable`
function Component({data}) {
  const table = useReactTable({
    data,
    columns,
    getCoreRowModel: getCoreRowModel(),
  });
  // table instance uses interior mutability
  return <Table table={table} />;
}
```

<Pitfall>

#### MobX {/*mobx*/}

Các mẫu như `observer` của MobX cũng phá vỡ các giả định của memoization, nhưng linter vẫn chưa phát hiện chúng. Nếu bạn phụ thuộc vào MobX và thấy ứng dụng không chạy với React Compiler, bạn có thể cần dùng chỉ thị `"use no memo"`.

```js
// ❌ MobX `observer`
const Component = observer(() => {
  const [timer] = useState(() => new Timer());
  return <span>Seconds passed: {timer.secondsPassed}</span>;
});
```

</Pitfall>

### Hợp lệ {/*valid*/}

Ví dụ về mã đúng cho luật này:

```js
// ✅ For react-hook-form, use `useWatch`:
function Component() {
  const {register, control} = useForm();
  const watchedValue = useWatch({
    control,
    name: 'field'
  });

  return (
    <>
      <input {...register('field')} />
      <div>Current value: {watchedValue}</div>
    </>
  );
}
```

Một số thư viện khác vẫn chưa có API thay thế tương thích với mô hình memoization của React. Nếu linter không tự động bỏ qua component hoặc Hook của bạn khi gọi các API này, hãy [tạo issue](https://github.com/facebook/react/issues) để chúng tôi bổ sung nó vào linter.
