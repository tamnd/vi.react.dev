---
title: static-components
---

<Intro>

Kiểm tra để bảo đảm các thành phần là tĩnh, không bị tạo lại ở mỗi lần kết xuất. Những thành phần bị tạo lại động có thể làm reset state và gây ra việc kết xuất lại quá mức.

</Intro>

## Chi tiết luật {/*rule-details*/}

Các thành phần được định nghĩa bên trong thành phần khác sẽ bị tạo lại ở mỗi lần kết xuất. React xem mỗi thành phần đó như một loại thành phần hoàn toàn mới, unmount cái cũ rồi mount cái mới, làm mất toàn bộ state và các nút DOM trong quá trình đó.

### Không hợp lệ {/*invalid*/}

Ví dụ về mã không đúng cho luật này:

```js
// ❌ Component defined inside component
function Parent() {
  const ChildComponent = () => { // New component every render!
    const [count, setCount] = useState(0);
    return <button onClick={() => setCount(count + 1)}>{count}</button>;
  };

  return <ChildComponent />; // State resets every render
}

// ❌ Dynamic component creation
function Parent({type}) {
  const Component = type === 'button'
    ? () => <button>Click</button>
    : () => <div>Text</div>;

  return <Component />;
}
```

### Hợp lệ {/*valid*/}

Ví dụ về mã đúng cho luật này:

```js
// ✅ Components at module level
const ButtonComponent = () => <button>Click</button>;
const TextComponent = () => <div>Text</div>;

function Parent({type}) {
  const Component = type === 'button'
    ? ButtonComponent  // Reference existing component
    : TextComponent;

  return <Component />;
}
```

## Khắc phục sự cố {/*troubleshooting*/}

### Tôi cần kết xuất các thành phần khác nhau có điều kiện {/*conditional-components*/}

Bạn có thể định nghĩa thành phần bên trong để truy cập state cục bộ:

```js {expectedErrors: {'react-compiler': [13]}}
// ❌ Wrong: Inner component to access parent state
function Parent() {
  const [theme, setTheme] = useState('light');

  function ThemedButton() { // Recreated every render!
    return (
      <button className={theme}>
        Click me
      </button>
    );
  }

  return <ThemedButton />;
}
```

Thay vào đó hãy truyền dữ liệu qua props:

```js
// ✅ Better: Pass props to static component
function ThemedButton({theme}) {
  return (
    <button className={theme}>
      Click me
    </button>
  );
}

function Parent() {
  const [theme, setTheme] = useState('light');
  return <ThemedButton theme={theme} />;
}
```

<Note>

Nếu bạn thấy mình muốn định nghĩa thành phần bên trong thành phần khác để truy cập biến cục bộ, đó là dấu hiệu cho thấy bạn nên truyền props thay thế. Cách này giúp thành phần dễ tái sử dụng hơn và dễ kiểm thử hơn.

</Note>
