# Quality and release checks

## Scope

This repository ships static HTML and CSS. It does not include JavaScript, TypeScript, a package manager, a framework, build tooling, tracking, or external runtime assets. Operational CI configuration is kept separate from the shipped site.

One-click clipboard copying is intentionally unavailable under the no-JavaScript constraint. **Get HTML** reveals a readonly source field; manual selection/copying and HTML downloads are the supported flows.

## Verification record — 2026-11-12

The following checks completed on the proposed source:

| Check | Result |
| --- | --- |
| All 27 HTML files, including fragment copies | Balanced explicit markup; unique IDs; valid label references and textarea wrapping |
| Eight canonical fragments | One root each; first-child embedded style; implicit scope; no fragment IDs or named disclosure groups |
| Preview, decoded source field, download, and example article | Exact source parity for all eight components |
| Documentation navigation, assets, and local anchors | All local targets resolve; repository and example.com links are intentional external destinations |
| Script and dependency audit | No JS/TS files, script elements, event-handler attributes, script URLs, CSS imports, or URL-based assets |
| Static CI source-contract commands | Passed locally |
| Staged patch whitespace | Passed |
| Documentation stylesheet, Nu validator 26.11.9 | Passed with no diagnostics |
| Eleven full documentation pages and eight wrapped fragment fixtures, Nu validator 26.11.9 | No HTML markup diagnostics; 12 CSS diagnostics for unsupported validator features, detailed below |
| Representative default text/background pairs | Static contrast calculations exceed 4.5:1; this is not a full accessibility audit |

Nu 26.11.9's embedded CSS checker does not recognize `container-type` or `@container`. Its HTML run returned six instances of each diagnostic across article-card and author-card previews, example composition, and temporary full-document fixtures. These are intentional standard CSS enhancements, not removed to satisfy an outdated CSS checker. No other errors or warnings remained. The unfiltered validator result is therefore **not** described as a clean pass.

The browser fallback for these two components is a single-column layout. The validator was obtained from the [official Nu release](https://github.com/validator/validator/releases/tag/latest); its JAR SHA-256 was checked against the release asset digest before use. Temporary audit tools and validation fixtures are not shipped as application dependencies.

CI checks canonical/download parity, license parity, required documentation pages, prohibited script files/markup, imported style or URL assets, and patch whitespace. Full source-field and rendered-preview parity was separately checked locally; the small shell-only CI is not a complete HTML/CSS validator or browser test suite.

## Browser verification limitation

The local Chromium process could not launch because this execution environment denied socket creation. The available cloud browser also rejects local `file:` URLs under its security policy. These restrictions were not bypassed. No visual, interactive, cross-browser, screen-reader, or actual-download success is claimed from those attempts.

## Release checks in a supported browser environment

- Open every documentation page over HTTP or HTTPS, at both the host root and a repository subpath.
- Check 320px, 390px, 768px, and 1440px viewports. Only source fields and table regions should scroll horizontally.
- Open all eight canonical fragments in an ordinary HTML page without `site.css`. Paste duplicate instances and nest components to check selector boundaries and inherited custom properties.
- Disable JavaScript. Use the documentation navigation, theme checkbox, source disclosures, accordion summaries, and links with the keyboard.
- Confirm that Enter and Space operate native summaries, focus remains visible, and table scrolling works when its region has focus.
- Open **Get HTML**, copy using the platform's keyboard shortcut or touch selection menu, and compare the pasted source with the canonical file. Test all eight download links and compare their saved bytes.
- Toggle the documentation theme. Component previews should retain their independent light palette. Navigate to a new page and confirm the control does not claim persistence.
- Check increased text size and 200%/400% zoom, reduced-motion preferences, forced colors, and a screen reader.
- Check current Chromium, Firefox, and Safari on desktop, plus Safari on iOS and Chrome on Android, according to your support policy.
- Test the actual publishing editor and site's Content Security Policy. Confirm that neither removes or blocks the embedded styles.
- Replace sample text, example URLs, and fictional identities before using a snippet as real site content.
- Review current HTML/CSS validator diagnostics. Older validators may reject the recently standardized implicit scoped body-style pattern; do not silently ignore unrelated errors.

Passing static checks is useful evidence, but does not replace these rendered and interaction checks. Record browser versions, dates, and observed results before declaring a production release.
