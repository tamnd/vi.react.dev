---
title: Các quy tắc của Hook
---

<Intro>
Hook được định nghĩa bằng các hàm JavaScript, nhưng chúng đại diện cho một kiểu logic UI có thể tái sử dụng đặc biệt, với những giới hạn về nơi chúng có thể được gọi.
</Intro>

<InlineToc />

---

## Chỉ gọi Hook ở cấp cao nhất {/*only-call-hooks-at-the-top-level*/}

Trong React, các hàm có tên bắt đầu bằng `use` được gọi là [*Hook*](/reference/react).

**Đừng gọi Hook bên trong vòng lặp, điều kiện, hàm lồng nhau hoặc khối `try`/`catch`/`finally`.** Thay vào đó, hãy luôn dùng Hook ở cấp cao nhất của hàm React, trước mọi lệnh return sớm. Bạn chỉ có thể gọi Hook khi React đang kết xuất một function component:

* ✅ Gọi chúng ở cấp cao nhất trong thân của [function component](/learn/your-first-component).
* ✅ Gọi chúng ở cấp cao nhất trong thân của [custom Hook](/learn/reusing-logic-with-custom-hooks).

```js{2-3,8-9}
function Counter() {
  // ✅ Good: top-level in a function component
  const [count, setCount] = useState(0);
  // ...
}

function useWindowWidth() {
  // ✅ Good: top-level in a custom Hook
  const [width, setWidth] = useState(window.innerWidth);
  // ...
}
```

Việc gọi Hook, tức các hàm bắt đầu bằng `use`, trong các trường hợp khác là **không được hỗ trợ**, ví dụ:

* 🔴 Không gọi Hook trong điều kiện hoặc vòng lặp.
* 🔴 Không gọi Hook sau lệnh `return` có điều kiện.
* 🔴 Không gọi Hook trong event handler.
* 🔴 Không gọi Hook trong class component.
* 🔴 Không gọi Hook bên trong hàm được truyền vào `useMemo`, `useReducer` hoặc `useEffect`.
* 🔴 Không gọi Hook bên trong khối `try`/`catch`/`finally`.

Nếu bạn phá vỡ các quy tắc này, bạn có thể thấy lỗi sau.

```js{3-4,11-12,20-21}
function Bad({ cond }) {
  if (cond) {
    // 🔴 Bad: inside a condition (to fix, move it outside!)
    const theme = useContext(ThemeContext);
  }
  // ...
}

function Bad() {
  for (let i = 0; i < 10; i++) {
    // 🔴 Bad: inside a loop (to fix, move it outside!)
    const theme = useContext(ThemeContext);
  }
  // ...
}

function Bad({ cond }) {
  if (cond) {
    return;
  }
  // 🔴 Bad: after a conditional return (to fix, move it before the return!)
  const theme = useContext(ThemeContext);
  // ...
}

function Bad() {
  function handleClick() {
    // 🔴 Bad: inside an event handler (to fix, move it outside!)
    const theme = useContext(ThemeContext);
  }
  // ...
}

function Bad() {
  const style = useMemo(() => {
    // 🔴 Bad: inside useMemo (to fix, move it outside!)
    const theme = useContext(ThemeContext);
    return createStyle(theme);
  });
  // ...
}

class Bad extends React.Component {
  render() {
    // 🔴 Bad: inside a class component (to fix, write a function component instead of a class!)
    useEffect(() => {})
    // ...
  }
}

function Bad() {
  try {
    // 🔴 Bad: inside try/catch/finally block (to fix, move it outside!)
    const [x, setX] = useState(0);
  } catch {
    const [x, setX] = useState(1);
  }
}
```

Bạn có thể dùng plugin [`eslint-plugin-react-hooks`](https://www.npmjs.com/package/eslint-plugin-react-hooks) để bắt những lỗi này.

<Note>

[Custom Hook](/learn/reusing-logic-with-custom-hooks) *có thể* gọi các Hook khác, đó chính là mục đích của chúng. Điều này hoạt động vì custom Hook cũng chỉ được gọi khi function component đang kết xuất.

</Note>

---

## Chỉ gọi Hook từ các hàm React {/*only-call-hooks-from-react-functions*/}

Đừng gọi Hook từ các hàm JavaScript thông thường. Thay vào đó, bạn có thể:

✅ Gọi Hook từ React function component.
✅ Gọi Hook từ [custom Hook](/learn/reusing-logic-with-custom-hooks#extracting-your-own-custom-hook-from-a-component).

Làm theo quy tắc này giúp bạn bảo đảm mọi logic có state trong component đều hiển hiện rõ ràng ngay trong source code của nó.

```js {2,5}
function FriendList() {
  const [onlineStatus, setOnlineStatus] = useOnlineStatus(); // ✅
}

function setOnlineStatus() { // ❌ Not a component or custom Hook!
  const [onlineStatus, setOnlineStatus] = useOnlineStatus();
}
```
