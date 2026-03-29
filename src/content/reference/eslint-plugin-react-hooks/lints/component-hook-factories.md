---
title: component-hook-factories
---

<Intro>

Kiểm tra để ngăn các hàm bậc cao định nghĩa thành phần hoặc Hook lồng nhau. Thành phần và Hook nên được định nghĩa ở cấp module.

</Intro>

## Chi tiết luật {/*rule-details*/}

Việc định nghĩa thành phần hoặc Hook bên trong các hàm khác sẽ tạo ra instance mới ở mỗi lần gọi. React coi mỗi instance đó là một thành phần hoàn toàn khác, phá hủy và tạo lại toàn bộ cây thành phần, làm mất toàn bộ state và gây ra vấn đề về hiệu năng.

### Không hợp lệ {/*invalid*/}

Ví dụ về mã không đúng cho luật này:

```js {expectedErrors: {'react-compiler': [14]}}
// ❌ Factory function creating components
function createComponent(defaultValue) {
  return function Component() {
    // ...
  };
}

// ❌ Component defined inside component
function Parent() {
  function Child() {
    // ...
  }

  return <Child />;
}

// ❌ Hook factory function
function createCustomHook(endpoint) {
  return function useData() {
    // ...
  };
}
```

### Hợp lệ {/*valid*/}

Ví dụ về mã đúng cho luật này:

```js
// ✅ Component defined at module level
function Component({ defaultValue }) {
  // ...
}

// ✅ Custom hook at module level
function useData(endpoint) {
  // ...
}
```

## Khắc phục sự cố {/*troubleshooting*/}

### Tôi cần hành vi thành phần động {/*dynamic-behavior*/}

Bạn có thể nghĩ rằng mình cần một factory để tạo các thành phần tùy biến:

```js
// ❌ Wrong: Factory pattern
function makeButton(color) {
  return function Button({children}) {
    return (
      <button style={{backgroundColor: color}}>
        {children}
      </button>
    );
  };
}

const RedButton = makeButton('red');
const BlueButton = makeButton('blue');
```

Hãy truyền [JSX làm children](/learn/passing-props-to-a-component#passing-jsx-as-children) thay thế:

```js
// ✅ Better: Pass JSX as children
function Button({color, children}) {
  return (
    <button style={{backgroundColor: color}}>
      {children}
    </button>
  );
}

function App() {
  return (
    <>
      <Button color="red">Red</Button>
      <Button color="blue">Blue</Button>
    </>
  );
}
```
