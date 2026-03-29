---
title: unsupported-syntax
---

<Intro>

Kiểm tra để ngăn cú pháp mà React Compiler không hỗ trợ. Nếu cần, bạn vẫn có thể dùng cú pháp này bên ngoài React, ví dụ trong một hàm tiện ích độc lập.

</Intro>

## Chi tiết luật {/*rule-details*/}

React Compiler cần phân tích tĩnh code của bạn để áp dụng tối ưu hóa. Những tính năng như `eval` và `with` khiến compiler không thể hiểu tĩnh code đang làm gì ở thời điểm biên dịch, nên compiler không thể tối ưu các thành phần dùng chúng.

### Không hợp lệ {/*invalid*/}

Ví dụ về mã không đúng cho luật này:

```js
// ❌ Using eval in component
function Component({ code }) {
  const result = eval(code); // Can't be analyzed
  return <div>{result}</div>;
}

// ❌ Using with statement
function Component() {
  with (Math) { // Changes scope dynamically
    return <div>{sin(PI / 2)}</div>;
  }
}

// ❌ Dynamic property access with eval
function Component({propName}) {
  const value = eval(`props.${propName}`);
  return <div>{value}</div>;
}
```

### Hợp lệ {/*valid*/}

Ví dụ về mã đúng cho luật này:

```js
// ✅ Use normal property access
function Component({propName, props}) {
  const value = props[propName]; // Analyzable
  return <div>{value}</div>;
}

// ✅ Use standard Math methods
function Component() {
  return <div>{Math.sin(Math.PI / 2)}</div>;
}
```

## Khắc phục sự cố {/*troubleshooting*/}

### Tôi cần đánh giá code động {/*evaluate-dynamic-code*/}

Bạn có thể cần đánh giá code do người dùng cung cấp:

```js {expectedErrors: {'react-compiler': [3]}}
// ❌ Wrong: eval in component
function Calculator({expression}) {
  const result = eval(expression); // Unsafe and unoptimizable
  return <div>Result: {result}</div>;
}
```

Hãy dùng một trình phân tích biểu thức an toàn thay thế:

```js
// ✅ Better: Use a safe parser
import {evaluate} from 'mathjs'; // or similar library

function Calculator({expression}) {
  const [result, setResult] = useState(null);

  const calculate = () => {
    try {
      // Safe mathematical expression evaluation
      setResult(evaluate(expression));
    } catch (error) {
      setResult('Invalid expression');
    }
  };

  return (
    <div>
      <button onClick={calculate}>Calculate</button>
      {result && <div>Result: {result}</div>}
    </div>
  );
}
```

<Note>

Đừng bao giờ dùng `eval` với đầu vào từ người dùng, vì đó là một rủi ro bảo mật. Hãy dùng các thư viện phân tích chuyên dụng cho từng trường hợp như biểu thức toán học, phân tích JSON hoặc đánh giá template.

</Note>
