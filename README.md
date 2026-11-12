# Block UI

A compact library of 14 self-contained HTML and CSS components for interfaces, pages, and blogs. Copy a fragment, keep its embedded styles, and edit the content. No installation, JavaScript, TypeScript, framework, CDN, font download, or build step.

The visual language takes inspiration from [daisyUI](https://daisyui.com/components/): clear typography, soft surfaces, rounded corners, and a focused accent color. The implementation is original vanilla HTML/CSS and does not depend on daisyUI or Tailwind.

## Start here

1. Open [docs/index.html](docs/index.html) in a current browser.
2. Open a block’s **Get HTML** disclosure. Select the source and use your normal copy command, or choose **Download .html**.
3. Paste the complete fragment, including its first-child `style` element, into a flow-content container in your page.
4. Replace the example text and destinations, choose heading levels that fit your document, and check the result in your host page.

The documentation also works when served by any static file server. Its HTML and CSS are checked in; there is nothing to compile.

**Clipboard limitation:** HTML and CSS cannot write to the system clipboard. Get HTML exposes the source; it does not pretend to copy it. A true one-click clipboard action would require JavaScript through the [Clipboard API](https://developer.mozilla.org/en-US/docs/Web/API/Clipboard/writeText). Both the blocks and this documentation stay script-free.

## The collection

| Component family | Source | Purpose |
| --- | --- | --- |
| Button | [button.html](components/button.html) | Primary, outline, ghost, and disabled native button styles |
| Avatar | [avatar.html](components/avatar.html) | Initials avatars in three sizes, with accessible names |
| Badge | [badge.html](components/badge.html) | Neutral, primary, and success labels |
| Text field | [text-field.html](components/text-field.html) | A labeled native email input with helper text |
| Checkbox and switch | [selection-control.html](components/selection-control.html) | Native checkbox, switch, and disabled states |
| Carousel | [carousel.html](components/carousel.html) | A finite row of cards with native scrolling and CSS scroll snap |
| FAQ | [accordion.html](components/accordion.html) | Independent native `details` disclosures |
| Article card | [article-card.html](components/article-card.html) | A story title, short introduction, reading time, and link |
| Callout | [callout.html](components/callout.html) | A contextual tip or note |
| Quote | [quote.html](components/quote.html) | A semantic quotation with attribution |
| Comparison table | [table.html](components/table.html) | Captioned data with row/column headers and local horizontal scrolling |
| Author card | [author-card.html](components/author-card.html) | A compact author introduction |
| Steps | [steps.html](components/steps.html) | An ordered process |
| Call to action | [cta.html](components/cta.html) | A heading, supporting text, and navigation link |

`components/` is the canonical source. `docs/` contains the separate static documentation site, live previews, selectable source, and self-contained download links. Sample people and quotations are fictional; `example.com` destinations are placeholders to replace.

Variants stay in the same family. To use one button, avatar, or badge variant, keep the root and its stylesheet and remove the examples you do not need.

### Native controls

Buttons are style specimens with explicit `type="button"`, so pasting them into a form does not submit it accidentally. Choose the correct native button type for the host form's action, such as `submit` or `reset`; the sample does not define an application action. Links in the content blocks use native navigation.

The email field, checkbox, and switch use wrapping labels, so copies do not require unique IDs. Form inputs omit `name` attributes: add the names your enclosing form expects when collecting values. The switch derives its state from the native checkbox's `checked` state. These local input states do not save settings or send data on their own. When editing the email hint, update both the visible helper text and `aria-description`.

The carousel is a finite, manually scrolled row with a named, keyboard-focusable track and labeled slides. Swipe, use the native scrollbar, focus the track and use arrow keys, or Tab through the slide links. It uses [CSS scroll snap](https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Properties/scroll-snap-type), keeps all slide content available, and has no autoplay. It has no scripted previous/next controls or active-slide announcements. When adding or removing slides, update their position labels. Print styling lays all slides out in a vertical flow.

## Fragment contract

Every component is one semantic HTML root with its entire stylesheet inside it:

```html
<article>
  <style>
    @scope {
      :scope { padding: 1.5rem; }
      :scope > h2 { margin-block-start: 0; }
    }
  </style>
  <h2>Your heading</h2>
  <p>Your content.</p>
</article>
```

- No `doctype`, `html`, `head`, or `body` wrappers in component files.
- No external stylesheet, asset, script, Vue binding, event handler, or generated ID.
- The `style` element stays first inside a root that accepts flow content. All its style rules stay inside an implicit `@scope`.
- Direct-child selectors keep the styles focused on the supplied structure. Editing the nesting may require updating the corresponding selectors.
- There are no literal backticks, `${` sequences, or backslashes in canonical fragments. The complete source can be pasted inside an ordinary backtick-delimited string without escaping. Recheck this property after editing text, CSS, or URLs; in visible HTML text, use character references such as `&#96;`, `&#36;{`, and `&#92;` when needed.
- Repeated blocks have no IDs to collide. FAQ items intentionally have no `name`, so separate instances never form one document-wide exclusive group.

The current [HTML Living Standard](https://html.spec.whatwg.org/dev/semantics.html#the-style-element) permits a first-child `style` in flow content with implicit scoped rules. Older HTML validators may still flag this newer pattern. Do not replace it with the obsolete `scoped` attribute.

## Vue 3 `v-html`

Use an existing **trusted string** containing the complete fragment:

```html
<div v-html="content"></div>
```

Use a host that accepts flow content, such as `div`; do not inject these block roots into a `p`, `span`, or table row. The fragment supplies its own styles, so it does not rely on Vue SFC scoped styles or template compilation. Do not paste its `style` element directly into a Vue SFC template and expect the same behavior: this contract is specifically for raw HTML insertion.

Vue inserts `v-html` through `innerHTML` and does not compile directives within it. It does not sanitize untrusted HTML. Keep user-generated content out of this insertion path unless your application has an appropriate sanitization policy; some sanitizers and blog editors remove styles entirely. See [Vue’s v-html documentation](https://vuejs.org/api/built-in-directives.html#v-html).

## Customizing

Edit a block’s CSS, or set its optional custom properties on a parent:

```html
<div style="--bui-primary: #146c51; --bui-tint: #eaf6ef;">
  <!-- Paste a complete block here. -->
</div>
```

| Property | Default | Used for |
| --- | --- | --- |
| `--bui-surface` | `#fff` | Card background |
| `--bui-text` | `#202437` | Main text |
| `--bui-muted` | `#585c70` | Secondary text |
| `--bui-primary` | `#5943d6` | Links, accents, CTA background |
| `--bui-primary-text` | `#fff` | Text on the CTA |
| `--bui-tint` | `#f1edff` | Soft accent surface |
| `--bui-border` | `#e4e2eb` | Dividers and borders |

Each property has a local fallback. Copying a fragment alone produces the light default; the documentation's dark theme is a demonstration of inherited overrides and is not included in downloaded fragments. Change foreground/background pairs together and recheck contrast.

`@scope` contains the block’s selectors; it is not Shadow DOM encapsulation. Host rules, inheritance, or `!important` declarations can still affect it. Test in the actual host stylesheet and container. The documentation keeps its own styles in cascade layers to avoid overriding component styles.

## Browser and hosting requirements

Use a modern browser that supports [CSS `@scope`](https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/At-rules/@scope). Without it, the content and native FAQ behavior remain available, but the block’s scoped styling is not applied. The documentation theme switch additionally uses `:has()` and retains its setting only for the current page view.

Fluid spacing, logical properties, wrapping flex layouts, and local table/carousel overflow are used without viewport-specific scripts. There are no animations. Native buttons, labeled inputs, links, focusable summaries/scroll tracks, visible focus outlines, ordered lists, captions, and header scopes provide the accessibility foundation; adjust labels and heading levels to your content.

Your site’s Content Security Policy must permit each embedded stylesheet. A strict policy can use matching style hashes or server-provided nonces on the `style` elements. Do not weaken an existing policy merely to paste a block. The documentation has a restrictive policy that blocks scripts and network resources other than its local stylesheet, while allowing its embedded component styles.

To publish **only the documentation**, serve the contents of `docs/` with any static host. Its downloads are native `data:text/plain` links containing complete HTML fragments, so the deployed site does not need access to the repository’s `components/` folder. For GitHub Pages, choose the `main` branch and `/docs` folder after merging this change. No workflow, package installation, or build command is needed. Publishing is a separate repository setting; this PR does not enable Pages.

## Verification

Static checks cover fragment structure, the no-script contract, template-string safety, source/preview/download consistency, reference IDs, and the supplied color palettes. See [CONTRIBUTING.md](CONTRIBUTING.md) for the acceptance checklist.

Live rendering, keyboard behavior, mobile reflow, download behavior, and actual Vue insertion still require browser sign-off before a production release. The implementation environment blocked browser execution; static checks do not substitute for those checks. No cross-browser certification or completed Vue runtime test is claimed.

## License

[MIT](LICENSE), including the component HTML and CSS. Keep the license notice when redistributing substantial portions.
