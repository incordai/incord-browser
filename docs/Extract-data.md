`--dump` formats the page output without writing JavaScript.

```bash
incord-browser fetch https://example.com --dump html
incord-browser fetch https://example.com --dump text
incord-browser fetch https://example.com --dump markdown
incord-browser fetch https://example.com --dump links
incord-browser fetch https://example.com --dump assets
incord-browser fetch https://example.com --dump original
incord-browser fetch https://example.com --dump cookies
```

## `html`

Rendered HTML after JavaScript runs. Default.

```bash
incord-browser fetch https://news.ycombinator.com --dump html > hn.html
```

## `text`

Plain text. No markup.

```bash
incord-browser fetch https://en.wikipedia.org/wiki/Rust_(programming_language) --dump text
```

## `markdown`

Markdown conversion: headings, lists, links, code blocks, images.

```bash
incord-browser fetch https://docs.example.com/page --dump markdown > page.md
```

## `links`

Every `<a href>` on the page, one per line.

```bash
incord-browser fetch https://example.com --dump links
```

## `assets`

Every external resource (stylesheets, scripts, images, fonts, iframes), plus the URLs the page requested through `fetch()`/XHR, one JSON object per line.

```bash
incord-browser fetch https://example.com --dump assets
```

## `original`

The raw HTML the server sent, before JavaScript ran.

```bash
incord-browser fetch https://my-spa.example --dump original > before.html
incord-browser fetch https://my-spa.example --dump html     > after.html
diff before.html after.html
```

## `cookies`

Every cookie in the jar as a JSON array, including HttpOnly cookies that `document.cookie` cannot see. Useful for capturing session tokens set by anti-bot challenges.

```bash
incord-browser fetch https://example.com --dump cookies
```

## With `--wait-until`

`--dump` runs after the wait condition:

```bash
incord-browser fetch https://my-spa.example --wait-until load --dump markdown
```

## Pipe and redirect

```bash
incord-browser fetch https://example.com --dump markdown > example.md
incord-browser fetch https://example.com --dump text --quiet | wc -w
```
