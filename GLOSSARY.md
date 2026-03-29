# Vietnamese Translation Glossary

Use this file to keep terminology stable across `learn`, `reference`, `blog`, sidebars, and UI chrome.

## Rules

- Prefer one canonical Vietnamese translation per concept.
- Keep React API names, package names, JSX, HTML, CSS, and code identifiers in English.
- Record a decision here before translating the same term in many files.
- If a term should stay in English, mark it explicitly.
- Add notes when a term changes by context, for example noun vs verb usage.

## Status Legend

- `proposed`: candidate term, not yet widely used
- `approved`: preferred term for ongoing translation
- `avoid`: do not use except when quoting upstream

## Core Terms

| English | Vietnamese | Status | Notes |
| --- | --- | --- | --- |
| React | React | approved | Keep brand name in English. |
| component | thành phần | approved | Use `component` only when directly quoting API names or code. |
| Hook | Hook | approved | Keep the React concept name in English. |
| props | props | approved | Keep lowercase code form in prose. |
| state | state | approved | May gloss once as `trạng thái` in beginner prose if needed. |
| context | context | approved | Use `ngữ cảnh` only in generic prose, not for the React API term. |
| ref | ref | approved | Keep the short API term in English. |
| effect | Effect | approved | Keep `Effect` for the React concept; avoid generic `hiệu ứng`. |
| side effect | tác dụng phụ | approved | Use for the programming concept outside the specific React `Effect` term. |
| event handler | trình xử lý sự kiện | approved | |
| render | kết xuất | approved | Use as verb or noun depending on sentence structure. |
| rendering | kết xuất | approved | Prefer natural phrasing over literal repetition. |
| commit | commit | approved | React rendering phase term, not Git commit message context. |
| reconciliation | đối soát cây giao diện | proposed | Keep under review until used in translated docs. |
| hydration | hydration | approved | Keep English technical term for now. |
| server rendering | kết xuất phía máy chủ | approved | |
| client | client | approved | Keep English technical term in docs prose. |
| server | server | approved | Keep English technical term in docs prose. |
| tree | cây | approved | |
| node | nút | approved | |
| compiler | trình biên dịch | approved | Generic term; product name stays English. |
| React Compiler | React Compiler | approved | Keep product name in English. |
| Server Components | Server Components | approved | Keep product name in English. |
| Server Functions | Server Functions | approved | Keep product name in English. |
| escape hatch | lối thoát | approved | Use technical prose carefully to keep it readable. |
| pure | thuần | approved | Prefer short form in programming contexts. |
| impure | không thuần | approved | |
| memoization | ghi nhớ kết quả | approved | Prefer explanatory wording in prose when useful. |
| batching | gộp lô cập nhật | approved | |
| concurrency | đồng thời | approved | |
| transition | chuyển tiếp | approved | Keep API names like `startTransition` unchanged. |
| suspense | Suspense | approved | Keep product/API name in English. |

## Style Decisions

| Topic | Decision | Status | Notes |
| --- | --- | --- | --- |
| Tone | Direct, technical, and plain-language | approved | Avoid marketing tone or overly literary wording. |
| Person | Use `bạn` for user-facing guidance | approved | Keep imperative steps natural and concise. |
| Imperative instructions | Verb-first, short sentences | approved | Prefer clarity over literal translation. |
| Section headers | Natural Vietnamese headings, not English title case | approved | |
| Sidebar labels | Shorter than article titles when needed | approved | Optimize for scanability in nav. |

## Terms To Avoid

| Avoid | Use Instead | Reason |
| --- | --- | --- |
| hiển thị | kết xuất | `render` in React is broader than visual display. |
| hiệu ứng | Effect | Avoid confusion with animation or visual effects. |
| móc | Hook | Literal translation reads unnaturally in developer docs. |
| đạo cụ | props | Literal translation is misleading in this context. |
| hydrat hóa | hydration | Uncommon and awkward in Vietnamese frontend usage. |

## Open Questions

- Should `Hook` stay in English everywhere?
- Which product names should always remain in English?
- Should `reconciliation` keep a Vietnamese term, or stay in English until we hit real usage friction?
