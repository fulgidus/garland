---
name: obscura
description: Install and drive Obscura headless browser for JS-rendering web scraping and AI agent web research. Use when fetching dynamic pages, scraping multiple URLs in parallel, or needing a CDP-compatible browser without Chrome. Do NOT trigger for static HTML fetches where a plain curl suffices.
---

# Obscura

## Install

```bash
# Linux x86_64
curl -LO https://github.com/h4ckf0r0day/obscura/releases/latest/download/obscura-x86_64-linux.tar.gz
tar xzf obscura-x86_64-linux.tar.gz && sudo mv obscura /usr/local/bin/

# macOS Apple Silicon
curl -LO https://github.com/h4ckf0r0day/obscura/releases/latest/download/obscura-aarch64-macos.tar.gz
tar xzf obscura-aarch64-macos.tar.gz && sudo mv obscura /usr/local/bin/

# macOS Intel
curl -LO https://github.com/h4ckf0r0day/obscura/releases/latest/download/obscura-x86_64-macos.tar.gz
tar xzf obscura-x86_64-macos.tar.gz && sudo mv obscura /usr/local/bin/
```

Verify: `obscura --version`

Single binary. No Chrome, no Node.js, no dependencies.

## Rules

1. Always run `obscura --version` after install to confirm it is in PATH.
2. Use `--dump text` by default for content extraction; use `--dump html` only when DOM structure is required.
3. Use `--wait-until networkidle0` for SPAs and pages that load data via JS after initial render.
4. Use `obscura scrape` with `--concurrency` for any batch of >2 URLs; never loop `fetch` manually.
5. Add `--stealth` when the target site is likely to fingerprint or block headless browsers.
6. Start the CDP server with `obscura serve --port 9222` before connecting Puppeteer or Playwright.
7. Always pass `--quiet` in scripted/pipeline contexts to suppress the banner.

## Quick reference

```bash
# Readable text — best default for content extraction
obscura fetch https://example.com --dump text --quiet

# Markdown (via built-in LP domain)
obscura fetch https://example.com --dump html --quiet  # then parse with LP.getMarkdown if needed

# Evaluate a JS expression
obscura fetch https://example.com --eval "document.title" --quiet

# Wait for dynamic content
obscura fetch https://spa.example.com --wait-until networkidle0 --dump text --quiet

# Parallel scrape → JSON
obscura scrape url1 url2 url3 \
  --concurrency 10 \
  --eval "document.querySelector('h1')?.textContent?.trim()" \
  --format json

# CDP server for Puppeteer / Playwright
obscura serve --port 9222 --stealth --workers 4
```

## Anti-patterns

- Do not build from source unless no release binary exists for your platform; first build is ~5 min.
- Do not pipe `--dump html` into LLM context when `--dump text` is sufficient; it wastes tokens.
- Do not assume JS has executed with the default `--wait-until load`; use `networkidle0` for dynamic pages.
- Do not use `obscura fetch` in a shell loop for bulk URLs; use `obscura scrape` instead.

## Refs

- Source: https://github.com/h4ckf0r0day/obscura
- [[wiki/beliefs/web-research]]
