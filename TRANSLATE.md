# Vietnamese Translation Checklist for `vi.react.dev`

This repo is a Vietnamese fork of [`reactjs/react.dev`](https://github.com/reactjs/react.dev).

This checklist is based on:

- the current source tree cloned on 2026-03-29
- the structure and completeness of [`reactjs/zh-hans.react.dev`](https://github.com/reactjs/zh-hans.react.dev)

## Baseline

- Current upstream content files under `src/content`: `222`
- `zh-hans.react.dev` content files under `src/content`: `221`
- Current upstream has two pages not present in `zh-hans`:
  - `src/content/blog/2026/02/24/the-react-foundation.md`
  - `src/content/learn/rsc-sandbox-test.md`
- `zh-hans` still has one legacy page not present in current upstream:
  - `src/content/reference/react/experimental_useEffectEvent.md`

## Translation Rules

- [ ] Set and document Vietnamese terminology conventions before large-scale translation.
- [ ] Keep code, identifiers, API names, package names, and version numbers in English.
- [ ] Translate prose, headings, captions, alt text, link labels, button labels, navigation labels, and metadata.
- [ ] Preserve MDX components, JSX snippets, code fences, frontmatter keys, anchors, and import paths.
- [ ] Decide when to keep established terms in English, for example `Hooks`, `React Compiler`, `Server Components`.
- [ ] Keep a glossary for recurring terms so wording stays consistent across `learn`, `reference`, and `blog`.

## Repo Setup

- [ ] Initialize local Git history for this fork.
- [ ] Add `upstream` remote pointing to `https://github.com/reactjs/react.dev`.
- [ ] Add `origin` remote pointing to `https://github.com/tamnd/vi.react.dev`.
- [ ] Add contributor instructions for Vietnamese translation workflow.

## Site Chrome And Project Files

- [ ] Update [`src/siteConfig.js`](/Users/apple/github/tamnd/vi.react.dev/src/siteConfig.js) to use `languageCode: 'vi'`.
- [ ] Translate sidebar labels in:
  - [ ] [`src/sidebarHome.json`](/Users/apple/github/tamnd/vi.react.dev/src/sidebarHome.json)
  - [ ] [`src/sidebarLearn.json`](/Users/apple/github/tamnd/vi.react.dev/src/sidebarLearn.json)
  - [ ] [`src/sidebarReference.json`](/Users/apple/github/tamnd/vi.react.dev/src/sidebarReference.json)
  - [ ] [`src/sidebarCommunity.json`](/Users/apple/github/tamnd/vi.react.dev/src/sidebarCommunity.json)
  - [ ] [`src/sidebarBlog.json`](/Users/apple/github/tamnd/vi.react.dev/src/sidebarBlog.json)
- [ ] Translate shared UI strings in layout and navigation components.
- [ ] Add or port a Vietnamese feedback widget equivalent to the one in `zh-hans` for [`src/components/Layout/Feedback.tsx`](/Users/apple/github/tamnd/zh-hans.react.dev/src/components/Layout/Feedback.tsx).
- [ ] Translate project-facing docs where appropriate:
  - [ ] [`README.md`](/Users/apple/github/tamnd/vi.react.dev/README.md)
  - [ ] [`CONTRIBUTING.md`](/Users/apple/github/tamnd/vi.react.dev/CONTRIBUTING.md)
  - [ ] [`CODE_OF_CONDUCT.md`](/Users/apple/github/tamnd/vi.react.dev/CODE_OF_CONDUCT.md)
  - [ ] [`TRANSLATE.md`](/Users/apple/github/tamnd/vi.react.dev/TRANSLATE.md) maintenance

## Content Translation

- [ ] Home and version pages: `2`
  - [ ] `src/content/index.md`
  - [ ] `src/content/versions.md`

- [ ] Blog: `24`
  - [ ] Blog index
  - [ ] 2020 posts: `1`
  - [ ] 2021 posts: `2`
  - [ ] 2022 posts: `3`
  - [ ] 2023 posts: `3`
  - [ ] 2024 posts: `5`
  - [ ] 2025 posts: `8`
  - [ ] 2026 posts: `1`

- [ ] Community: `9`
  - [ ] Community index
  - [ ] Conferences
  - [ ] Meetups
  - [ ] Videos
  - [ ] Team
  - [ ] Docs Contributors
  - [ ] Translations
  - [ ] Acknowledgements
  - [ ] Versioning Policy

- [ ] Errors: `3`
  - [ ] `errors/index.md`
  - [ ] `errors/generic.md`
  - [ ] `errors/377.md`

- [ ] Learn: `52`
  - [ ] Learn index: `1`
  - [ ] Installation and setup pages: `8`
  - [ ] React Compiler learn pages: `5`
  - [ ] Core learn pages: `38`
  - [ ] Current upstream-only page: `learn/rsc-sandbox-test.md`

- [ ] Reference: `126`
  - [ ] Dev Tools: `1`
  - [ ] `eslint-plugin-react-hooks`: `18`
  - [ ] `react`: `49`
  - [ ] `react-dom`: `39`
  - [ ] `react-compiler`: `10`
  - [ ] `rsc`: `5`
  - [ ] `rules`: `4`
  - [ ] Do not copy `zh-hans`'s legacy-only `reference/react/experimental_useEffectEvent.md` unless upstream restores it.

- [ ] Warnings: `6`
  - [ ] Invalid ARIA prop
  - [ ] Invalid hook call
  - [ ] `react-dom/test-utils`
  - [ ] `react-test-renderer`
  - [ ] Special props
  - [ ] Unknown prop

## Non-Markdown Text Assets

- [ ] Review [`public/html/single-file-example.html`](/Users/apple/github/tamnd/vi.react.dev/public/html/single-file-example.html) for visible English text.
- [ ] Audit SVGs under `public/images/docs/illustrations` for embedded text that should be localized.
- [ ] Audit screenshots, diagrams, and tutorial images for English labels that may need Vietnamese variants.
- [ ] Review metadata images and social previews only if they contain visible English copy.

## Translation Infrastructure

- [ ] Review [`src/content/community/translations.md`](/Users/apple/github/tamnd/vi.react.dev/src/content/community/translations.md) and adapt it for the Vietnamese project.
- [ ] Review [`src/utils/finishedTranslations.ts`](/Users/apple/github/tamnd/vi.react.dev/src/utils/finishedTranslations.ts); add `vi` only after enough core content is complete and after alignment with upstream policy.
- [ ] Check for search, SEO, and page-title strings in components such as `Seo`, `Footer`, `DocsFooter`, `Search`, and layout/nav components.
- [ ] Check for hard-coded strings in MDX helper components and sandpack UI.

## QA

- [ ] Run `yarn` to install dependencies.
- [ ] Run `yarn dev` and review pages in Vietnamese on desktop and mobile.
- [ ] Run `yarn check-all`.
- [ ] Verify links, headings, table of contents entries, and sidebar labels after translation.
- [ ] Verify MDX examples still compile.
- [ ] Verify code snippets did not get accidentally translated.
- [ ] Verify terminology consistency across the whole site.

## Ongoing Sync

- [ ] Rebase or merge from `reactjs/react.dev` regularly.
- [ ] Add checklist items for every new upstream page before translating it.
- [ ] Track translation parity against both upstream and `zh-hans.react.dev`.
- [ ] Prefer translating from current upstream, using `zh-hans` as a completeness reference rather than a source of truth.
