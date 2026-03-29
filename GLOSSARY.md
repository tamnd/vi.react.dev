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
| component |  | proposed | |
| Hook |  | proposed | Decide whether to keep `Hook` or translate. |
| props |  | proposed | Usually keep lowercase code form in prose if needed. |
| state |  | proposed | |
| context |  | proposed | |
| ref |  | proposed | |
| effect |  | proposed | |
| side effect |  | proposed | |
| event handler |  | proposed | |
| render |  | proposed | Decide verb and noun forms. |
| rendering |  | proposed | |
| commit |  | proposed | React rendering phase term, not Git term. |
| reconciliation |  | proposed | |
| hydration |  | proposed | |
| server rendering |  | proposed | |
| client |  | proposed | |
| server |  | proposed | |
| tree |  | proposed | |
| node |  | proposed | |
| compiler |  | proposed | Decide whether to keep `compiler` in English. |
| React Compiler | React Compiler | proposed | Likely keep English product name. |
| Server Components | Server Components | proposed | Likely keep English product name. |
| Server Functions | Server Functions | proposed | |
| escape hatch |  | proposed | |
| pure |  | proposed | |
| impure |  | proposed | |
| memoization |  | proposed | |
| batching |  | proposed | |
| concurrency |  | proposed | |
| transition |  | proposed | |
| suspense | Suspense | proposed | Product/API name. |

## Style Decisions

| Topic | Decision | Status | Notes |
| --- | --- | --- | --- |
| Tone |  | proposed | Formal vs conversational Vietnamese. |
| Person |  | proposed | `bạn`, `chúng ta`, or neutral imperative. |
| Imperative instructions |  | proposed | Keep command steps concise. |
| Section headers |  | proposed | Title case is not natural in Vietnamese. |
| Sidebar labels |  | proposed | Shorter wording may be needed than in article titles. |

## Terms To Avoid

| Avoid | Use Instead | Reason |
| --- | --- | --- |
|  |  |  |

## Open Questions

- Should `Hook` stay in English everywhere?
- Should `state` stay in English in beginner docs, or use a Vietnamese term in prose?
- Should `render` be translated, transliterated, or kept in English depending on context?
- Which product names should always remain in English?
