# Maintaining the blocks

Keep the collection small and useful for interfaces, pages, and blogs. Group variants within the 14 component families. Shipped code is vanilla HTML and CSS. Do not add JavaScript, TypeScript, framework directives, inline event handlers, remote dependencies, or a build requirement.

## Source and documentation

1. Edit the canonical fragment in `components/`.
2. Update its live preview in `docs/index.html` without altering the fragment.
3. Update the corresponding readonly textarea with the HTML-escaped fragment. The decoded value must exactly equal the canonical file, including its final newline.
4. Update that block’s native download link with the UTF-8, percent-encoded fragment after the `data:text/plain;charset=utf-8,` prefix. Its `download` filename must match the canonical filename. Decode the URL and compare it to the canonical file.
5. Change `docs/styles.css` only for the documentation shell. Never rely on it to make a component work.

These are checked-in static documents. The duplicated preview/source/download representations keep the docs portable without a script or build step; they must stay synchronized.

## Fragment review

- Exactly one meaningful root, with no document-level wrappers.
- The root accepts flow content; its `style` is first. All style rules are within an implicit `@scope`, with no imports or global at-rule names.
- No scripts, event attributes, external assets, Vue syntax, IDs, or named disclosure groups.
- No literal backticks, interpolation openers, or backslashes in the source. HTML character references can represent those characters in visible text.
- Links have useful accessible names; heading levels, labels, list semantics, table captions, and header scopes match the content.
- Focus outlines remain visible. Disclosure summary is the first child of each `details`.
- Buttons declare their native type. Wrapping labels name form inputs; samples omit field names so consumers choose their form integration.
- Checkbox and switch state comes from native inputs. A visual switch must preserve the control's keyboard behavior and forced-colors fallback.
- Layout respects narrow host containers and long content. Only tables and carousels should require local horizontal scrolling.
- Carousel tracks are named, focusable, and natively scrollable; slides stay available to assistive technology. Keep position labels accurate and leave the scrollbar available.
- Default colors and any documentation theme overrides maintain readable contrast.
- Repeated fragments do not change each other or unrelated neighboring elements.

## Browser acceptance checklist

Before releasing, check current Chromium, Firefox, and Safari versions with `@scope` support. Record the actual browser/OS versions and the results in the PR. A source review is not a browser pass.

| Area | Check | Expected result |
| --- | --- | --- |
| Standalone | Paste each canonical fragment into an otherwise unstyled HTML page | Its layout and styles work without documentation CSS |
| Repeated instances | Paste each fragment twice beside unrelated headings and paragraphs | No ID collisions, shared disclosure state, or outward style changes |
| Vue insertion | Bind the full trusted string to `v-html` on a `div`; replace it with another fragment | New content and its embedded styles render; no Vue directives are required |
| Narrow layout | Use 320px and 375px viewports, and a narrow column inside a wide viewport | Text and actions remain readable; no document-level horizontal overflow |
| Zoom and long text | Use 200% zoom, 400% reflow, and long titles/URLs | Content is reachable without clipping; table/carousel overflow stays local |
| FAQ | Tab to each summary; press Enter and Space; repeat in the second instance | Each disclosure opens and closes independently |
| Buttons | Test all variants with pointer/keyboard, including inside a host form | Enabled controls show focus/active states; disabled stays inert; samples do not submit the form |
| Text field | Click the label, type an email, and test inside a real form after adding a name | The correct input receives focus; native editing and email validation remain available |
| Checkbox and switch | Click each label and press Space on the focused control; repeat in another instance | Only that native input toggles; disabled stays inert; no setting is persisted automatically |
| Carousel | Swipe, drag the native scrollbar, focus the track and use arrows, then Tab across all slide links | Every slide is reachable; only the track scrolls horizontally; no content is hidden from assistive technology |
| Focus | Reach every enabled link, button, summary, input, source field, and scroll region by keyboard | Logical order and visible focus |
| Source | Open Get HTML; focus the field; use select-all and copy | The entire canonical fragment is selected and copied by the browser |
| Download | Download every fragment and compare its UTF-8 bytes with `components/` | Exact equality, including final newline |
| Theme | Toggle Dark theme and inspect text, buttons, badges, input states, CTA, and focus | Text/controls remain readable; source and download content stay unchanged |
| Accessibility | Inspect accessibility names/roles and use a screen reader for native controls, the carousel, FAQ, and table | Names, checked/disabled/disclosure states, slide positions, and table relationships are conveyed |
| Reduced motion / forced colors | Enable each OS/browser preference | All information and controls remain available |
| Printing | Print preview in both light and dark themes | Readable dark text; all carousel slides visible; no navigation or source panels |
| Offline / scripts disabled | Open the checked-in docs with scripts disabled and no internet | Local CSS, previews, native controls, carousel, source fields, and downloads remain usable |

## Release status

All 14 components have passed static structure, native-control markup, reference, byte-consistency, and palette contrast checks. Browser execution was blocked by the implementation environment, so the browser checklist above remains pending. Do not mark these rows as passed without running them.
