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

## Rules

- [x] Define Vietnamese terminology conventions before large-scale translation.
- [ ] Keep code, identifiers, API names, package names, and version numbers in English.
- [ ] Translate prose, headings, captions, alt text, labels, navigation text, and metadata.
- [ ] Preserve frontmatter keys, anchors, MDX components, JSX snippets, import paths, and code fences.
- [ ] Record terminology decisions in [`GLOSSARY.md`](/Users/apple/github/tamnd/vi.react.dev/GLOSSARY.md).
- [ ] Translate from current upstream first. Use `zh-hans.react.dev` only as a completeness reference.

## Repo Setup

- [x] Initialize local Git history for this fork.
- [x] Add `upstream` remote pointing to `https://github.com/reactjs/react.dev`.
- [x] Add `origin` remote pointing to `https://github.com/tamnd/vi.react.dev`.
- [ ] Add contributor instructions for Vietnamese translation workflow.
- [x] Decide the first translation milestone and mark it in this file.

## Tracking Files

- [x] Create [`TRANSLATE.md`](/Users/apple/github/tamnd/vi.react.dev/TRANSLATE.md).
- [x] Create [`GLOSSARY.md`](/Users/apple/github/tamnd/vi.react.dev/GLOSSARY.md).
- [ ] Keep this checklist updated as upstream adds, removes, or renames pages.
- [ ] Mark translated files only after content review and a local render check.

## Site Chrome And Project Files

- [x] Update [`src/siteConfig.js`](/Users/apple/github/tamnd/vi.react.dev/src/siteConfig.js) to use `languageCode: 'vi'`.
- [x] Translate [`src/sidebarHome.json`](/Users/apple/github/tamnd/vi.react.dev/src/sidebarHome.json).
- [x] Translate [`src/sidebarLearn.json`](/Users/apple/github/tamnd/vi.react.dev/src/sidebarLearn.json).
- [x] Translate [`src/sidebarReference.json`](/Users/apple/github/tamnd/vi.react.dev/src/sidebarReference.json).
- [x] Translate [`src/sidebarCommunity.json`](/Users/apple/github/tamnd/vi.react.dev/src/sidebarCommunity.json).
- [x] Translate [`src/sidebarBlog.json`](/Users/apple/github/tamnd/vi.react.dev/src/sidebarBlog.json).
- [ ] Translate shared UI strings in layout, nav, footer, feedback, search, and MDX helper components.
- [ ] Add or port a Vietnamese feedback widget equivalent to `zh-hans`'s `Feedback.tsx`.
- [ ] Translate project-facing docs as needed:
  - [x] [`README.md`](/Users/apple/github/tamnd/vi.react.dev/README.md)
  - [x] [`CONTRIBUTING.md`](/Users/apple/github/tamnd/vi.react.dev/CONTRIBUTING.md)
  - [x] [`CODE_OF_CONDUCT.md`](/Users/apple/github/tamnd/vi.react.dev/CODE_OF_CONDUCT.md)

## First Milestone: 30 Prioritized Pages

Prioritize smaller docs and UI-adjacent pages first, then move into foundational Learn and Reference entry pages.

- [x] `src/content/errors/377.md`
- [x] `src/content/errors/generic.md`
- [x] `src/content/errors/index.md`
- [x] `src/content/community/team.md`
- [x] `src/content/community/meetups.md`
- [x] `src/content/community/versioning-policy.md`
- [x] `src/content/community/videos.md`
- [x] `src/content/versions.md`
- [ ] `src/content/blog/index.md`
- [ ] `src/content/learn/index.md`
- [ ] `src/content/learn/setup.md`
- [ ] `src/content/learn/installation.md`
- [ ] `src/content/learn/describing-the-ui.md`
- [ ] `src/content/learn/your-first-component.md`
- [ ] `src/content/learn/importing-and-exporting-components.md`
- [ ] `src/content/learn/writing-markup-with-jsx.md`
- [ ] `src/content/learn/javascript-in-jsx-with-curly-braces.md`
- [ ] `src/content/learn/passing-props-to-a-component.md`
- [ ] `src/content/learn/conditional-rendering.md`
- [ ] `src/content/learn/rendering-lists.md`
- [ ] `src/content/learn/keeping-components-pure.md`
- [ ] `src/content/learn/responding-to-events.md`
- [ ] `src/content/learn/state-a-components-memory.md`
- [ ] `src/content/learn/adding-interactivity.md`
- [ ] `src/content/learn/managing-state.md`
- [ ] `src/content/reference/react/index.md`
- [ ] `src/content/reference/react/apis.md`
- [ ] `src/content/reference/react/components.md`
- [ ] `src/content/reference/react/hooks.md`
- [ ] `src/content/reference/react-dom/index.md`

## Current Working Set: Next 20 Pages

Work through these in order. Keep one reviewed page per commit and update this checklist after each completed page.

- [x] `src/content/community/versioning-policy.md`
- [x] `src/content/versions.md`
- [ ] `src/content/blog/index.md`
- [ ] `src/content/learn/index.md`
- [ ] `src/content/learn/setup.md`
- [ ] `src/content/learn/installation.md`
- [ ] `src/content/learn/describing-the-ui.md`
- [ ] `src/content/learn/your-first-component.md`
- [ ] `src/content/learn/importing-and-exporting-components.md`
- [ ] `src/content/learn/writing-markup-with-jsx.md`
- [ ] `src/content/learn/javascript-in-jsx-with-curly-braces.md`
- [ ] `src/content/learn/passing-props-to-a-component.md`
- [ ] `src/content/learn/conditional-rendering.md`
- [ ] `src/content/learn/rendering-lists.md`
- [ ] `src/content/learn/keeping-components-pure.md`
- [ ] `src/content/learn/responding-to-events.md`
- [ ] `src/content/learn/state-a-components-memory.md`
- [ ] `src/content/learn/adding-interactivity.md`
- [ ] `src/content/learn/managing-state.md`
- [ ] `src/content/reference/react/index.md`

## `src/content` Translation Checklist

### Root Pages (`2`)

- [x] `src/content/index.md`
- [x] `src/content/versions.md`

### Blog (`24`)

- [ ] `src/content/blog/2020/12/21/data-fetching-with-react-server-components.md`
- [ ] `src/content/blog/2021/06/08/the-plan-for-react-18.md`
- [ ] `src/content/blog/2021/12/17/react-conf-2021-recap.md`
- [ ] `src/content/blog/2022/03/08/react-18-upgrade-guide.md`
- [ ] `src/content/blog/2022/03/29/react-v18.md`
- [ ] `src/content/blog/2022/06/15/react-labs-what-we-have-been-working-on-june-2022.md`
- [ ] `src/content/blog/2023/03/16/introducing-react-dev.md`
- [ ] `src/content/blog/2023/03/22/react-labs-what-we-have-been-working-on-march-2023.md`
- [ ] `src/content/blog/2023/05/03/react-canaries.md`
- [ ] `src/content/blog/2024/02/15/react-labs-what-we-have-been-working-on-february-2024.md`
- [ ] `src/content/blog/2024/04/25/react-19-upgrade-guide.md`
- [ ] `src/content/blog/2024/05/22/react-conf-2024-recap.md`
- [ ] `src/content/blog/2024/10/21/react-compiler-beta-release.md`
- [ ] `src/content/blog/2024/12/05/react-19.md`
- [ ] `src/content/blog/2025/02/14/sunsetting-create-react-app.md`
- [ ] `src/content/blog/2025/04/23/react-labs-view-transitions-activity-and-more.md`
- [ ] `src/content/blog/2025/10/01/react-19-2.md`
- [ ] `src/content/blog/2025/10/07/introducing-the-react-foundation.md`
- [ ] `src/content/blog/2025/10/07/react-compiler-1.md`
- [ ] `src/content/blog/2025/10/16/react-conf-2025-recap.md`
- [ ] `src/content/blog/2025/12/03/critical-security-vulnerability-in-react-server-components.md`
- [ ] `src/content/blog/2025/12/11/denial-of-service-and-source-code-exposure-in-react-server-components.md`
- [ ] `src/content/blog/2026/02/24/the-react-foundation.md`
- [ ] `src/content/blog/index.md`

### Community (`9`)

- [x] `src/content/community/acknowledgements.md`
- [ ] `src/content/community/conferences.md`
- [x] `src/content/community/docs-contributors.md`
- [x] `src/content/community/index.md`
- [x] `src/content/community/meetups.md`
- [x] `src/content/community/team.md`
- [x] `src/content/community/translations.md`
- [x] `src/content/community/versioning-policy.md`
- [x] `src/content/community/videos.md`

### Errors (`3`)

- [x] `src/content/errors/377.md`
- [x] `src/content/errors/generic.md`
- [x] `src/content/errors/index.md`

### Learn (`52`)

- [ ] `src/content/learn/add-react-to-an-existing-project.md`
- [ ] `src/content/learn/adding-interactivity.md`
- [ ] `src/content/learn/build-a-react-app-from-scratch.md`
- [ ] `src/content/learn/choosing-the-state-structure.md`
- [ ] `src/content/learn/conditional-rendering.md`
- [ ] `src/content/learn/creating-a-react-app.md`
- [ ] `src/content/learn/describing-the-ui.md`
- [ ] `src/content/learn/editor-setup.md`
- [ ] `src/content/learn/escape-hatches.md`
- [ ] `src/content/learn/extracting-state-logic-into-a-reducer.md`
- [ ] `src/content/learn/importing-and-exporting-components.md`
- [ ] `src/content/learn/index.md`
- [ ] `src/content/learn/installation.md`
- [ ] `src/content/learn/javascript-in-jsx-with-curly-braces.md`
- [ ] `src/content/learn/keeping-components-pure.md`
- [ ] `src/content/learn/lifecycle-of-reactive-effects.md`
- [ ] `src/content/learn/managing-state.md`
- [ ] `src/content/learn/manipulating-the-dom-with-refs.md`
- [ ] `src/content/learn/passing-data-deeply-with-context.md`
- [ ] `src/content/learn/passing-props-to-a-component.md`
- [ ] `src/content/learn/preserving-and-resetting-state.md`
- [ ] `src/content/learn/queueing-a-series-of-state-updates.md`
- [ ] `src/content/learn/react-compiler/debugging.md`
- [ ] `src/content/learn/react-compiler/incremental-adoption.md`
- [ ] `src/content/learn/react-compiler/index.md`
- [ ] `src/content/learn/react-compiler/installation.md`
- [ ] `src/content/learn/react-compiler/introduction.md`
- [ ] `src/content/learn/react-developer-tools.md`
- [ ] `src/content/learn/reacting-to-input-with-state.md`
- [ ] `src/content/learn/referencing-values-with-refs.md`
- [ ] `src/content/learn/removing-effect-dependencies.md`
- [ ] `src/content/learn/render-and-commit.md`
- [ ] `src/content/learn/rendering-lists.md`
- [ ] `src/content/learn/responding-to-events.md`
- [ ] `src/content/learn/reusing-logic-with-custom-hooks.md`
- [ ] `src/content/learn/rsc-sandbox-test.md`
- [ ] `src/content/learn/scaling-up-with-reducer-and-context.md`
- [ ] `src/content/learn/separating-events-from-effects.md`
- [ ] `src/content/learn/setup.md`
- [ ] `src/content/learn/sharing-state-between-components.md`
- [ ] `src/content/learn/state-a-components-memory.md`
- [ ] `src/content/learn/state-as-a-snapshot.md`
- [ ] `src/content/learn/synchronizing-with-effects.md`
- [ ] `src/content/learn/thinking-in-react.md`
- [ ] `src/content/learn/tutorial-tic-tac-toe.md`
- [ ] `src/content/learn/typescript.md`
- [ ] `src/content/learn/understanding-your-ui-as-a-tree.md`
- [ ] `src/content/learn/updating-arrays-in-state.md`
- [ ] `src/content/learn/updating-objects-in-state.md`
- [ ] `src/content/learn/writing-markup-with-jsx.md`
- [ ] `src/content/learn/you-might-not-need-an-effect.md`
- [ ] `src/content/learn/your-first-component.md`

### Reference (`126`)

- [ ] `src/content/reference/dev-tools/react-performance-tracks.md`
- [ ] `src/content/reference/eslint-plugin-react-hooks/index.md`
- [ ] `src/content/reference/eslint-plugin-react-hooks/lints/component-hook-factories.md`
- [ ] `src/content/reference/eslint-plugin-react-hooks/lints/config.md`
- [ ] `src/content/reference/eslint-plugin-react-hooks/lints/error-boundaries.md`
- [ ] `src/content/reference/eslint-plugin-react-hooks/lints/exhaustive-deps.md`
- [ ] `src/content/reference/eslint-plugin-react-hooks/lints/gating.md`
- [ ] `src/content/reference/eslint-plugin-react-hooks/lints/globals.md`
- [ ] `src/content/reference/eslint-plugin-react-hooks/lints/immutability.md`
- [ ] `src/content/reference/eslint-plugin-react-hooks/lints/incompatible-library.md`
- [ ] `src/content/reference/eslint-plugin-react-hooks/lints/preserve-manual-memoization.md`
- [ ] `src/content/reference/eslint-plugin-react-hooks/lints/purity.md`
- [ ] `src/content/reference/eslint-plugin-react-hooks/lints/refs.md`
- [ ] `src/content/reference/eslint-plugin-react-hooks/lints/rules-of-hooks.md`
- [ ] `src/content/reference/eslint-plugin-react-hooks/lints/set-state-in-effect.md`
- [ ] `src/content/reference/eslint-plugin-react-hooks/lints/set-state-in-render.md`
- [ ] `src/content/reference/eslint-plugin-react-hooks/lints/static-components.md`
- [ ] `src/content/reference/eslint-plugin-react-hooks/lints/unsupported-syntax.md`
- [ ] `src/content/reference/eslint-plugin-react-hooks/lints/use-memo.md`
- [ ] `src/content/reference/react-compiler/compilationMode.md`
- [ ] `src/content/reference/react-compiler/compiling-libraries.md`
- [ ] `src/content/reference/react-compiler/configuration.md`
- [ ] `src/content/reference/react-compiler/directives.md`
- [ ] `src/content/reference/react-compiler/directives/use-memo.md`
- [ ] `src/content/reference/react-compiler/directives/use-no-memo.md`
- [ ] `src/content/reference/react-compiler/gating.md`
- [ ] `src/content/reference/react-compiler/logger.md`
- [ ] `src/content/reference/react-compiler/panicThreshold.md`
- [ ] `src/content/reference/react-compiler/target.md`
- [ ] `src/content/reference/react-dom/client/createRoot.md`
- [ ] `src/content/reference/react-dom/client/hydrateRoot.md`
- [x] `src/content/reference/react-dom/client/index.md`
- [ ] `src/content/reference/react-dom/components/common.md`
- [ ] `src/content/reference/react-dom/components/form.md`
- [ ] `src/content/reference/react-dom/components/index.md`
- [ ] `src/content/reference/react-dom/components/input.md`
- [ ] `src/content/reference/react-dom/components/link.md`
- [ ] `src/content/reference/react-dom/components/meta.md`
- [ ] `src/content/reference/react-dom/components/option.md`
- [ ] `src/content/reference/react-dom/components/progress.md`
- [ ] `src/content/reference/react-dom/components/script.md`
- [ ] `src/content/reference/react-dom/components/select.md`
- [ ] `src/content/reference/react-dom/components/style.md`
- [ ] `src/content/reference/react-dom/components/textarea.md`
- [ ] `src/content/reference/react-dom/components/title.md`
- [ ] `src/content/reference/react-dom/createPortal.md`
- [ ] `src/content/reference/react-dom/flushSync.md`
- [ ] `src/content/reference/react-dom/hooks/index.md`
- [ ] `src/content/reference/react-dom/hooks/useFormStatus.md`
- [ ] `src/content/reference/react-dom/index.md`
- [ ] `src/content/reference/react-dom/preconnect.md`
- [ ] `src/content/reference/react-dom/prefetchDNS.md`
- [ ] `src/content/reference/react-dom/preinit.md`
- [ ] `src/content/reference/react-dom/preinitModule.md`
- [ ] `src/content/reference/react-dom/preload.md`
- [ ] `src/content/reference/react-dom/preloadModule.md`
- [ ] `src/content/reference/react-dom/server/index.md`
- [ ] `src/content/reference/react-dom/server/renderToPipeableStream.md`
- [ ] `src/content/reference/react-dom/server/renderToReadableStream.md`
- [ ] `src/content/reference/react-dom/server/renderToStaticMarkup.md`
- [ ] `src/content/reference/react-dom/server/renderToString.md`
- [ ] `src/content/reference/react-dom/server/resume.md`
- [ ] `src/content/reference/react-dom/server/resumeToPipeableStream.md`
- [ ] `src/content/reference/react-dom/static/index.md`
- [ ] `src/content/reference/react-dom/static/prerender.md`
- [ ] `src/content/reference/react-dom/static/prerenderToNodeStream.md`
- [ ] `src/content/reference/react-dom/static/resumeAndPrerender.md`
- [ ] `src/content/reference/react-dom/static/resumeAndPrerenderToNodeStream.md`
- [ ] `src/content/reference/react/Activity.md`
- [ ] `src/content/reference/react/Children.md`
- [ ] `src/content/reference/react/Component.md`
- [ ] `src/content/reference/react/Fragment.md`
- [ ] `src/content/reference/react/Profiler.md`
- [ ] `src/content/reference/react/PureComponent.md`
- [ ] `src/content/reference/react/StrictMode.md`
- [ ] `src/content/reference/react/Suspense.md`
- [ ] `src/content/reference/react/ViewTransition.md`
- [ ] `src/content/reference/react/act.md`
- [ ] `src/content/reference/react/addTransitionType.md`
- [ ] `src/content/reference/react/apis.md`
- [ ] `src/content/reference/react/cache.md`
- [ ] `src/content/reference/react/cacheSignal.md`
- [ ] `src/content/reference/react/captureOwnerStack.md`
- [ ] `src/content/reference/react/cloneElement.md`
- [ ] `src/content/reference/react/components.md`
- [ ] `src/content/reference/react/createContext.md`
- [ ] `src/content/reference/react/createElement.md`
- [ ] `src/content/reference/react/createRef.md`
- [ ] `src/content/reference/react/experimental_taintObjectReference.md`
- [ ] `src/content/reference/react/experimental_taintUniqueValue.md`
- [ ] `src/content/reference/react/forwardRef.md`
- [ ] `src/content/reference/react/hooks.md`
- [ ] `src/content/reference/react/index.md`
- [ ] `src/content/reference/react/isValidElement.md`
- [ ] `src/content/reference/react/lazy.md`
- [ ] `src/content/reference/react/legacy.md`
- [ ] `src/content/reference/react/memo.md`
- [ ] `src/content/reference/react/startTransition.md`
- [ ] `src/content/reference/react/use.md`
- [ ] `src/content/reference/react/useActionState.md`
- [ ] `src/content/reference/react/useCallback.md`
- [ ] `src/content/reference/react/useContext.md`
- [ ] `src/content/reference/react/useDebugValue.md`
- [ ] `src/content/reference/react/useDeferredValue.md`
- [ ] `src/content/reference/react/useEffect.md`
- [ ] `src/content/reference/react/useEffectEvent.md`
- [ ] `src/content/reference/react/useId.md`
- [ ] `src/content/reference/react/useImperativeHandle.md`
- [ ] `src/content/reference/react/useInsertionEffect.md`
- [ ] `src/content/reference/react/useLayoutEffect.md`
- [ ] `src/content/reference/react/useMemo.md`
- [ ] `src/content/reference/react/useOptimistic.md`
- [ ] `src/content/reference/react/useReducer.md`
- [ ] `src/content/reference/react/useRef.md`
- [ ] `src/content/reference/react/useState.md`
- [ ] `src/content/reference/react/useSyncExternalStore.md`
- [ ] `src/content/reference/react/useTransition.md`
- [ ] `src/content/reference/rsc/directives.md`
- [ ] `src/content/reference/rsc/server-components.md`
- [ ] `src/content/reference/rsc/server-functions.md`
- [ ] `src/content/reference/rsc/use-client.md`
- [ ] `src/content/reference/rsc/use-server.md`
- [ ] `src/content/reference/rules/components-and-hooks-must-be-pure.md`
- [ ] `src/content/reference/rules/index.md`
- [ ] `src/content/reference/rules/react-calls-components-and-hooks.md`
- [ ] `src/content/reference/rules/rules-of-hooks.md`

### Warnings (`6`)

- [x] `src/content/warnings/invalid-aria-prop.md`
- [ ] `src/content/warnings/invalid-hook-call-warning.md`
- [ ] `src/content/warnings/react-dom-test-utils.md`
- [x] `src/content/warnings/react-test-renderer.md`
- [x] `src/content/warnings/special-props.md`
- [ ] `src/content/warnings/unknown-prop.md`

## Non-Markdown Text Assets

- [ ] Review [`public/html/single-file-example.html`](/Users/apple/github/tamnd/vi.react.dev/public/html/single-file-example.html) for visible English text.
- [ ] Audit SVGs under `public/images/docs/illustrations` for embedded text that should be localized.
- [ ] Audit screenshots, diagrams, and tutorial images for English labels that may need Vietnamese variants.
- [ ] Review metadata images and social previews only if they contain visible English copy.

## Translation Infrastructure

- [ ] Review [`src/content/community/translations.md`](/Users/apple/github/tamnd/vi.react.dev/src/content/community/translations.md) and adapt it for the Vietnamese project.
- [ ] Review [`src/utils/finishedTranslations.ts`](/Users/apple/github/tamnd/vi.react.dev/src/utils/finishedTranslations.ts). Add `vi` only after enough core content is complete and after upstream alignment.
- [ ] Check for search, SEO, page-title, and feedback strings in layout and MDX helper components.
- [ ] Check sandpack UI and embedded interactive examples for English-only UI copy.

## QA

- [ ] Run `yarn`.
- [ ] Run `yarn dev` and review Vietnamese pages on desktop and mobile.
- [ ] Run `yarn check-all`.
- [ ] Verify links, headings, TOC entries, and sidebars after translation.
- [ ] Verify MDX examples still compile.
- [ ] Verify code snippets were not translated.
- [ ] Verify terminology consistency against [`GLOSSARY.md`](/Users/apple/github/tamnd/vi.react.dev/GLOSSARY.md).

## Ongoing Sync

- [ ] Rebase or merge from `reactjs/react.dev` regularly.
- [ ] Add checklist items for every new upstream page before translating it.
- [ ] Track parity against both upstream and `zh-hans.react.dev`.
