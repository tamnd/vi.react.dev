---
title: Cảnh báo về Prop đặc biệt
---

Hầu hết các prop trên một phần tử JSX sẽ được truyền tiếp vào component. Tuy nhiên, có hai prop đặc biệt (`ref` và `key`) được React sử dụng, nên sẽ không được chuyển tiếp vào component.

Ví dụ, bạn không thể đọc `props.key` từ bên trong component. Nếu cần truy cập cùng giá trị đó trong component con, bạn nên truyền nó bằng một prop khác, chẳng hạn `<ListItemWrapper key={result.id} id={result.id} />` rồi đọc `props.id`. Dù điều này có vẻ dư thừa, việc tách logic của ứng dụng khỏi các gợi ý dành cho React là rất quan trọng.
