# LazyDoc LOCAL

LazyDoc Local is the single-file, no-server version of LazyDoc. Drop the `.html` file anywhere, open it in your browser, point it at a folder on your PC, and you're **done**. No Node.js, no install, no network, no docker, NOTHING.

- **Reading** : Rendered Markdown, plain text, HTML (sandboxed iframe), PDF (browser native viewer)
- **Full-text search**: Fuzzy search across file names and contents (Fuse.js), accent-insensitive
- **Edit & save**: Built-in code editor for `.md`, `.txt`, `.html` with Ctrl+S, writes directly to disk
- **Light / dark theme**: Persisted in localStorage
- **Zero install**: One `.html` file, that's it

## Installation

I just said there wasn't. Download `LazyDoc LOCAL.html`, open it in Chrome or Edge, done.

> Firefox is not supported — it does not implement the File System Access API that LazyDoc relies on to read and write files on your disk. Chromium wins.

## Usage

### 1. Pick a folder

On first launch, click **"Choose a folder"** and select the directory containing your docs. The browser will ask for read/write permission — accept it.

LazyDoc will remember the folder between sessions. On the next launch, a **"Allow access to saved folder"** button will appear instead — click it to re-grant permission (this is a browser security requirement, it can't be bypassed).

### 2. Browse and read

Files are listed in the left sidebar. Supported formats: `.md`, `.txt`, `.pdf`, `.html`.

Click any file to open it. Markdown is rendered, plain text is displayed as-is, HTML runs in a sandboxed iframe, PDFs open with the browser's native viewer.

### 3. Search

Type in the search bar at the top of the sidebar. Search is fuzzy and looks through both file names and file contents (except PDFs).

### 4. Edit and save

Click **"Edit"** in the top toolbar to switch to the code editor. Make your changes, then either hit **Ctrl+S** or click **"Save"** — the file is written directly to disk.

Click **"Read mode"** to go back to the rendered view.

## Known limitations

- **Firefox not supported** — The File System Access API is Chrome/Edge only.
- **Permission prompt on every session** — Browsers require the user to re-grant folder access on each new session. This is a browser security constraint, not something LazyDoc can work around.
- **`.docx`, `.odt`, `.xlsx`, `.pptx`** — Office formats are not supported. I won't fix this.
- **Standalone images** (`.png`, `.jpg`…) — Not listed in the file explorer. They can be referenced inside Markdown files but not viewed directly.
- **No PDF editing** — PDFs can be viewed but not modified from the interface.
- **No PDF content indexing** — Full-text search does not look inside PDF files, only the filename is indexed.
- **No subfolders** — Only files at the root of the selected folder are listed.
- **No diff / history** — Saving overwrites the file directly. No versioning.
- **Single user, local only** — If you want to share your docs with others on the network, use [LazyDoc Server](../README.md) instead.
