# RepoScrape — Bulk GitHub Repository Scraper

RepoScrape is a self-contained, browser-based tool for searching GitHub repositories and collecting matching files. It turns repository searches into downloadable archives without requiring a server or installation.

Open `index.html` to use the app. The interface guides you through an eight-step wizard:

1. **Device** — select Windows, macOS, Linux, ChromeOS, Android, iOS, or another system and receive battery/power guidance.
2. **Queries** — add one or more plain GitHub repository search strings.
3. **Token & Search** — optionally authenticate with a classic GitHub personal access token, set pages and repository limits, and choose result sorting.
4. **Files & Archives** — choose ZIP, 7z, TAR, or gzip-wrapped formats and configure archive splitting.
5. **Scrape Filters** — select file presets or custom extensions and set duplicate, asset, blank-file, folder, and file-size rules.
6. **Find Repositories** — search GitHub and select repositories to scrape.
7. **The Magic** — inspect live collection statistics and begin or stop scraping.
8. **Download** — review the collected files and download the generated archive.

## Key Features

- GitHub repository search with optional personal access token authentication
- Anonymous access support, with GitHub API rate-limit handling
- File-type presets for web, game, Python, systems, and data projects
- Custom file extensions and directory exclusions
- Duplicate detection and optional filtering of external-asset references
- Blank-file and per-repository file-count limits
- Minimum and maximum file-size limits
- Raw-file size limits and configurable archive parts
- ZIP, 7z, TAR, ZIP.GZ, 7Z.GZ, and TAR.GZ output options
- Browser-only collection and local ZIP/TAR/7z packing
- Offline demo repositories for trying the interface without network access
- Persistent browser settings using `localStorage`
- Optional Screen Wake Lock to keep scraping tabs active

## Getting Started

### Run locally

No build step or package installation is required.

```bash
git clone https://github.com/the-creative-master/RepoScrape.git
cd RepoScrape
python3 -m http.server 8000
```

Then open `http://localhost:8000`.

You can also open `index.html` directly in a browser. A local HTTP server is recommended for the best browser compatibility and archive behavior.

### Basic workflow

1. Choose the device and power situation for the scraping run.
2. Add repository search queries, such as `topic:games` or `language:python stars:>100`.
3. Configure the optional GitHub token and search limits.
4. Choose an archive format and size limits.
5. Select file types and scrape filters.
6. Search GitHub and select repositories.
7. Start scraping and inspect the live log and statistics.
8. Download the resulting archive.

## Search Examples

```text
topic:games
nice utilities
topic:tools
language:python stars:>100
topic:html5-game
portfolio
```

Narrow queries generally provide better, more targeted results than broad searches. GitHub repository search is limited to 1,000 results per query, so RepoScrape lets you add several focused queries and control pages per query.

## GitHub Authentication

A classic personal access token is optional. If supplied, it is stored only in this browser's `localStorage` and is sent only to `api.github.com`.

Anonymous searching has lower limits than authenticated searching. RepoScrape displays rate-limit status and waits automatically when a GitHub rate limit is encountered.

> Treat GitHub tokens like passwords. Never paste or commit a fine-grained or otherwise sensitive credential to source files.

## Filters

### File types

The app includes presets such as:

- **Web:** HTML, CSS, JavaScript, JSON, SVG
- **Games:** HTML, CSS, JavaScript, JSON, C, C++, H, Lua, GLSL
- **Python:** Python, IPython notebooks, text, Markdown, JSON
- **Systems:** C, C++, headers, Rust, Go, Swift
- **Data:** JSON, CSV, YAML, XML, text

You can also add custom comma-separated extensions such as:

```text
glsl, frag, lua
```

### Scrape rules

- **Duplicate files:** skip repeated file contents across repositories.
- **External asset files:** optionally drop scripts or markup that reference external assets.
- **Blank files:** skip files containing only whitespace or null characters.
- **Excluded directories:** skip folders such as `node_modules`, `.git`, `dist`, `build`, and `vendor`.
- **Minimum file size:** ignore files smaller than the configured threshold.
- **Maximum file size:** skip large binaries before downloading their contents.
- **Maximum files per repository:** prevent a large monorepository from consuming the whole run.

## Archive Formats

| Format | Description |
| --- | --- |
| ZIP | Broad OS compatibility and random file access |
| 7z | Strong compression for smaller archives |
| TAR | Fast, stream-friendly, uncompressed output |
| ZIP.GZ | Gzip-compressed finished ZIP |
| 7Z.GZ | Gzip-compressed finished 7z |
| TAR.GZ | Gzip-compressed TAR, common on Unix systems |

ZIP and TAR/7z support depends on the browser and build codec support. The app provides multiple archive options and reports the selected format in the final step.

## Privacy and Data Handling

RepoScrape does not require a backend service. It:

- stores wizard settings in browser `localStorage`;
- sends repository searches and file requests to GitHub APIs;
- keeps collected file contents in browser memory; and
- generates downloads entirely in the user's browser.

Closing or refreshing the page clears collected in-memory file data unless the browser restores saved settings. Downloaded archives remain in the browser's downloads folder.

## Browser Requirements

RepoScrape uses modern browser APIs, including:

- `fetch`, `TextEncoder`, `TextDecoder`, and `Blob`;
- `localStorage` and `URL.createObjectURL`; and
- optional `CompressionStream` support for gzip output.

Chrome, Edge, Firefox, Safari, and current Chromium-based mobile browsers should provide the core experience. The Screen Wake Lock API is optional and is shown as unavailable when unsupported.

## Stopping a Scrape

Use **Stop & download** during a run to stop further collection and move to the download step. RepoScrape preserves the files collected before the stop, subject to configured archive limits.

## Limitations

- GitHub API quotas apply to repository searches and file requests.
- GitHub searches return at most 1,000 results per query.
- Large or binary files may need to be filtered before download.
- Browser memory limits apply to very large runs.
- Background behavior varies by operating system and browser power settings.
- Keeping an Android or iOS browser tab active may require adjusting OEM battery restrictions.
- Network access is required for live searches and repository collection unless the offline demo is used.

## Repository Structure

```text
.
├── index.html       # Complete RepoScrape interface and application logic
└── README/
    └── README.md    # Project documentation
```

## License

No license has been explicitly identified for this repository. Review the repository owner’s terms before redistributing or commercializing collected data.
