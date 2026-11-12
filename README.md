# Block UI

Eight self-contained HTML and CSS components for pages, blogs, and personal sites. Copy a complete snippet, including its embedded styles, into an HTML page. No installation, build, framework, CDN, font download, or JavaScript is required.

The documentation takes visual inspiration from daisyUI's approachable component catalog. All markup and styling here are original; daisyUI and Tailwind are not dependencies.

## Browse locally

Open [`docs/index.html`](docs/index.html) in a modern browser, or serve `docs/` with any static web server. The documentation includes previews, source fields, snippet downloads, a guide, and an example article. Downloads work most consistently over HTTP or HTTPS.

**Copying is manual.** HTML and CSS cannot write to the clipboard on a button click. Open **Get HTML**, focus the readonly source field, select all, and copy using your keyboard or device menu. Alternatively, download the snippet. No control claims to have copied text automatically.

## Components

| Component | Source | Purpose |
| --- | --- | --- |
| Article card | [article-card.html](components/article-card.html) | Introduce a story or resource |
| Callout | [callout.html](components/callout.html) | Highlight a supporting note |
| Quote | [quote.html](components/quote.html) | Present a quotation with attribution |
| Accordion | [accordion.html](components/accordion.html) | Native, independent disclosures |
| Link button | [link-button.html](components/link-button.html) | A clear navigation destination |
| Badges | [badges.html](components/badges.html) | Informational labels |
| Table | [table.html](components/table.html) | A semantic, horizontally scrollable table |
| Author card | [author-card.html](components/author-card.html) | Introduce the person behind a post |

## Embedding contract

1. Paste the complete outer element into your page's body. Preserve its first `<style>` child.
2. Replace example text, fictional identities, and `https://example.com/` destinations. Adjust heading levels to fit the surrounding document.
3. Use an editor that preserves raw HTML, embedded style elements, and style attributes. Sanitized Markdown and email clients are not supported targets.
4. Check the final page with your own CSS and Content Security Policy. Inline styles must be allowed by that site's policy; do not weaken a strict policy automatically.

Essential styling lives in `style` attributes. Enhanced states and responsive layout live in implicit `@scope to ([data-bui]) { ... }` blocks. The current HTML standard permits a body `<style>` as its parent's first child when its style rules are implicitly scoped and it contains no `@import`. Older HTML validators may not yet recognize this pattern.

The scope boundary prevents the component's selectors from styling unrelated content or nested component roots. It does **not** block incoming host CSS or inherited properties. This is not Shadow DOM isolation.

The snippets have no IDs or named disclosure groups, so repeated copies do not collide. If you add IDs or exclusive accordion names, make them unique per instance.

## Customization

Set the variables used by a snippet on its outer element. Each has a local fallback, so a shared token file is unnecessary.

| Variable | Purpose | Typical default |
| --- | --- | --- |
| `--bui-text` | Main text | `#20242e` |
| `--bui-muted` | Secondary text | `#555d6d` |
| `--bui-accent` | Links and emphasis | `#5a35cc` |
| `--bui-on-accent` | Text on the link button | `#ffffff` |
| `--bui-surface` | Card background | `#ffffff` |
| `--bui-tint` | Soft accent background | `#f6f4fc` |
| `--bui-border` | Dividers and borders | `#e3e3ec` |
| `--bui-font` | Body font stack | System sans serif |

Not every component uses every variable. Decorative artwork and the green badge have their own inline colors. Change foreground/background colors together and check contrast. The documentation's dark theme affects its interface only and does not persist between page navigations.

## Repository layout

| Path | Responsibility |
| --- | --- |
| `components/` | Canonical pasteable fragments |
| `docs/index.html` | Component catalog |
| `docs/components/` | Preview and source pages |
| `docs/snippets/` | Exact copies of canonical fragments for downloads |
| `docs/assets/site.css` | Documentation interface only |
| `docs/guide.html` | Usage, compatibility, and publishing guide |
| `docs/examples/article.html` | A composition of all eight components |
| `QUALITY.md` | Verification record and release checks |

## Maintaining a component

Edit `components/<name>.html`, update the identical download in `docs/snippets/`, the preview and escaped textarea source in its documentation page, and its occurrence in the example article. Decode the source field before comparing it with the original; escape `&` and `<` when embedding source in HTML.

Keep all component selectors inside the implicit scope. Keep `<summary>` first inside `<details>`; place the component's style in an outer wrapper instead. Do not add scripts, event-handler attributes, framework classes, external assets, global resets, or hidden dependencies. Native links and disclosures should retain their keyboard behavior and focus indicators.

## Publish

The entire `docs/` directory can be deployed as a static site without a build step. Relative asset and navigation URLs support repository subpaths. The folder includes its own downloads, license, and `.nojekyll` file.

For GitHub Pages, after merging, select **Deploy from a branch**, **main**, and **/docs** in repository Pages settings. This PR does not enable hosting or deploy a site.

Review [QUALITY.md](QUALITY.md) before a production release. This implementation is prepared for review; cross-browser and assistive-technology checks must be completed for your supported environments.

## References

- [HTML style element](https://html.spec.whatwg.org/multipage/semantics.html#the-style-element)
- [CSS `@scope`](https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/At-rules/@scope)
- [Native disclosures](https://html.spec.whatwg.org/multipage/interactive-elements.html#the-details-element)
- [Clipboard API](https://www.w3.org/TR/clipboard-apis/)
- [Visual reference: daisyUI components](https://daisyui.com/components/)

## License

[MIT](LICENSE). Retain the existing copyright and license notice when redistributing substantial portions of the library.
