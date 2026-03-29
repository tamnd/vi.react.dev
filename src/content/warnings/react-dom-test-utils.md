---
title: Cảnh báo ngừng hỗ trợ react-dom/test-utils
---

## Cảnh báo ReactDOMTestUtils.act() {/*reactdomtestutilsact-warning*/}

`act` từ `react-dom/test-utils` đã bị ngừng hỗ trợ để nhường chỗ cho `act` từ `react`.

Before:

```js
import {act} from 'react-dom/test-utils';
```

After:

```js
import {act} from 'react';
```

## Các API ReactDOMTestUtils còn lại {/*rest-of-reactdomtestutils-apis*/}

Mọi API ngoại trừ `act` đều đã bị loại bỏ.

Đội ngũ React khuyến nghị chuyển bài kiểm thử của bạn sang [@testing-library/react](https://testing-library.com/docs/react-testing-library/intro/) để có trải nghiệm kiểm thử hiện đại và được hỗ trợ tốt.

### ReactDOMTestUtils.renderIntoDocument {/*reactdomtestutilsrenderintodocument*/}

`renderIntoDocument` có thể được thay bằng `render` từ `@testing-library/react`.

Before:

```js
import {renderIntoDocument} from 'react-dom/test-utils';

renderIntoDocument(<Component />);
```

After:

```js
import {render} from '@testing-library/react';

render(<Component />);
```

### ReactDOMTestUtils.Simulate {/*reactdomtestutilssimulate*/}

`Simulate` có thể được thay bằng `fireEvent` từ `@testing-library/react`.

Before:

```js
import {Simulate} from 'react-dom/test-utils';

const element = document.querySelector('button');
Simulate.click(element);
```

After:

```js
import {fireEvent} from '@testing-library/react';

const element = document.querySelector('button');
fireEvent.click(element);
```

Lưu ý rằng `fireEvent` sẽ phát một sự kiện thật trên phần tử chứ không chỉ gọi hàm xử lý sự kiện theo cách giả lập.

### Danh sách toàn bộ API đã bị loại bỏ {/*list-of-all-removed-apis-list-of-all-removed-apis*/}

- `mockComponent()`
- `isElement()`
- `isElementOfType()`
- `isDOMComponent()`
- `isCompositeComponent()`
- `isCompositeComponentWithType()`
- `findAllInRenderedTree()`
- `scryRenderedDOMComponentsWithClass()`
- `findRenderedDOMComponentWithClass()`
- `scryRenderedDOMComponentsWithTag()`
- `findRenderedDOMComponentWithTag()`
- `scryRenderedComponentsWithType()`
- `findRenderedComponentWithType()`
- `renderIntoDocument`
- `Simulate`
