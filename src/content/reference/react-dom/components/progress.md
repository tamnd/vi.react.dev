---
title: "<progress>"
---

<Intro>

[Component `<progress>` dựng sẵn của trình duyệt](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/progress) cho phép bạn kết xuất một chỉ báo tiến trình.

```js
<progress value={0.5} />
```

</Intro>

<InlineToc />

---

## Reference {/*reference*/}

### `<progress>` {/*progress*/}

Để hiển thị một chỉ báo tiến trình, hãy kết xuất component [`<progress>` dựng sẵn của trình duyệt](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/progress).

```js
<progress value={0.5} />
```

[Xem thêm ví dụ ở bên dưới.](#usage)

#### Props {/*props*/}

`<progress>` hỗ trợ toàn bộ [prop phần tử thông dụng.](/reference/react-dom/components/common#common-props)

Ngoài ra, `<progress>` còn hỗ trợ các prop sau:

* [`max`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/progress#max): Một số. Chỉ định `value` tối đa. Mặc định là `1`.
* [`value`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/progress#value): Một số trong khoảng từ `0` đến `max`, hoặc `null` cho trạng thái tiến trình không xác định. Chỉ định mức độ đã hoàn thành.

---

## Usage {/*usage*/}

### Điều khiển một chỉ báo tiến trình {/*controlling-a-progress-indicator*/}

Để hiển thị một chỉ báo tiến trình, hãy kết xuất component `<progress>`. Bạn có thể truyền một số `value` trong khoảng từ `0` đến giá trị `max` mà bạn chỉ định. Nếu bạn không truyền `max`, nó sẽ mặc định được hiểu là `1`.

Nếu thao tác không có tiến độ xác định, hãy truyền `value={null}` để đưa chỉ báo tiến trình vào trạng thái không xác định.

<Sandpack>

```js
export default function App() {
  return (
    <>
      <progress value={0} />
      <progress value={0.5} />
      <progress value={0.7} />
      <progress value={75} max={100} />
      <progress value={1} />
      <progress value={null} />
    </>
  );
}
```

```css
progress { display: block; }
```

</Sandpack>
