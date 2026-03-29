---
title: set-state-in-effect
---

<Intro>

Kiểm tra để ngăn việc gọi setState đồng bộ bên trong effect, vì điều này có thể dẫn đến các lần kết xuất lại làm giảm hiệu năng.

</Intro>

## Chi tiết luật {/*rule-details*/}

Việc đặt state ngay bên trong effect buộc React phải khởi động lại toàn bộ chu kỳ kết xuất. Khi bạn cập nhật state trong effect, React phải kết xuất lại thành phần, áp dụng thay đổi vào DOM, rồi chạy effect lần nữa. Điều này tạo ra một lượt kết xuất thừa mà lẽ ra có thể tránh được bằng cách biến đổi dữ liệu trực tiếp trong lúc kết xuất hoặc suy ra state từ props. Thay vào đó, hãy biến đổi dữ liệu ở cấp cao nhất của thành phần. Đoạn mã đó sẽ tự chạy lại khi props hoặc state thay đổi mà không kích hoạt thêm chu kỳ kết xuất.

Các lệnh gọi `setState` đồng bộ trong effect kích hoạt kết xuất lại ngay lập tức trước khi trình duyệt kịp vẽ, gây ra vấn đề hiệu năng và hiện tượng giật hình. React phải kết xuất hai lần: một lần để áp dụng cập nhật state, rồi một lần nữa sau khi effect chạy. Việc kết xuất kép này là lãng phí khi cùng kết quả đó có thể đạt được chỉ với một lần kết xuất.

Trong nhiều trường hợp, bạn thậm chí không cần effect. Hãy xem [Bạn Có thể Không Cần Effect](/learn/you-might-not-need-an-effect) để biết thêm chi tiết.

## Các vi phạm thường gặp {/*common-violations*/}

Luật này bắt một số mẫu nơi setState đồng bộ bị dùng không cần thiết:

- Đặt state loading một cách đồng bộ
- Suy ra state từ props trong effect
- Biến đổi dữ liệu trong effect thay vì trong lúc kết xuất

### Không hợp lệ {/*invalid*/}

Ví dụ về mã không đúng cho luật này:

```js
// ❌ Synchronous setState in effect
function Component({data}) {
  const [items, setItems] = useState([]);

  useEffect(() => {
    setItems(data); // Extra render, use initial state instead
  }, [data]);
}

// ❌ Setting loading state synchronously
function Component() {
  const [loading, setLoading] = useState(false);

  useEffect(() => {
    setLoading(true); // Synchronous, causes extra render
    fetchData().then(() => setLoading(false));
  }, []);
}

// ❌ Transforming data in effect
function Component({rawData}) {
  const [processed, setProcessed] = useState([]);

  useEffect(() => {
    setProcessed(rawData.map(transform)); // Should derive in render
  }, [rawData]);
}

// ❌ Deriving state from props
function Component({selectedId, items}) {
  const [selected, setSelected] = useState(null);

  useEffect(() => {
    setSelected(items.find(i => i.id === selectedId));
  }, [selectedId, items]);
}
```

### Hợp lệ {/*valid*/}

Ví dụ về mã đúng cho luật này:

```js
// ✅ setState in an effect is fine if the value comes from a ref
function Tooltip() {
  const ref = useRef(null);
  const [tooltipHeight, setTooltipHeight] = useState(0);

  useLayoutEffect(() => {
    const { height } = ref.current.getBoundingClientRect();
    setTooltipHeight(height);
  }, []);
}

// ✅ Calculate during render
function Component({selectedId, items}) {
  const selected = items.find(i => i.id === selectedId);
  return <div>{selected?.name}</div>;
}
```

**Khi một giá trị có thể được tính từ props hoặc state hiện có, đừng đặt nó vào state.** Thay vào đó, hãy tính nó trong lúc kết xuất. Cách này giúp code nhanh hơn, đơn giản hơn và ít lỗi hơn. Tìm hiểu thêm trong [Bạn Có thể Không Cần Effect](/learn/you-might-not-need-an-effect).
