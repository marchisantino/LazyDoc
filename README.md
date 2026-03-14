# LazyDoc SERVER

LazyDoc is a lightweight documentation reader, editor and search engine, accessible by anyone on your network, served as a minimal web app (a single HTML file + a Node.js server). Here is what it does :

- **Reading** : Rendered Markdown, plain text, HTML (sandboxed iframe), PDF (browser native viewer)
- **Full-text search**: Fuzzy search across file names and contents (Fuse.js), accent-insensitive
- **Edit & save**: Built-in code editor for `.md`, `.txt`, `.html` with Ctrl+S
- **File management**: Create, drag-and-drop import, delete (with confirmation)
- **Light / dark theme**: Persisted in localStorage
- **Zero database**: Everything runs on the filesystem

## Installation

### 0. Docker prerequisites

**If you host the app in a Docker container, which I recommend because it is so lightweight, I advise creating a network and a container like this :**

Creating the network (change the addresses to fit your network and IP ranges):
```bash
docker network create -d macvlan \
  --subnet=192.168.1.0/24 \
  --gateway=192.168.1.1 \
  --ip-range=192.168.1.240/28 \
  -o parent=eth0 your_docker_network
```

Creating the container:
```bash
docker run -it --network your_docker_network --name LazyDoc -p 3000:3000 debian:latest
```

### 1. Installing dependencies

**Inside the container, or whatever machine you host the app on, as long as it's Debian (it works on everything but I'm lazy so Debian will do):**

```bash
apt update && apt install -y nodejs npm unzip curl
```

### 2. Import the project files

From a **separate terminal** on the host machine, if on docker:

```bash
docker cp "LazyDoc SERVER.zip" lazydoc:/tmp/
```

Otherwise just transfer the `LazyDoc SERVER.zip` archive like you want

### 3. Extract and install

In the terminal:

```bash
cd /opt
```

```bash
unzip /tmp/LazyDoc SERVER.zip
```

```bash
cd lazydoc-server
```

```bash
npm install
```

> You can edit the `config.json` file if you want to change the documents location or the port.

### 6. Start

```bash
node server.js
```

After this, if you get no error, the app should be available at **`http://<your-server-ip>:3000`** from any browser on the network.

## Known limitations

- **`.docx`, `.odt`, `.xlsx`, `.pptx`** — Common formats like the Office ones are not read or displayed. Supporting them would require me to work, which I won't.
- **Standalone images** (`.png`, `.jpg`…) — Not listed in the file explorer. They can be referenced inside Markdown files but not viewed directly.

- PDF viewing relies on the **browser's native viewer** via an `<iframe>`. Some browsers (especially on mobile) may render it differently or trigger a download instead.
- **No PDF editing** — PDFs cannot be modified from the interface. A library like `pdf-lib` would be needed server-side.
- **No PDF content indexing** — Full-text search does not look inside PDF files; only the filename is indexed.

- **No authentication** — Anyone on the network who can reach the port has full read/write/delete access. Do not expose to the internet without putting an authenticating reverse proxy in front (Nginx + basic auth, Authelia, etc.).
- Path traversal protection is implemented server-side, but the app has not been audited for public-facing production use. It's not even HTTPS. Heh lazy.

- **No subfolders** — The file explorer only lists files at the root of the configured folder, not nested directories.

- **No diff / history** — No versioning. Saving overwrites the file directly. For version control, point `docsDir` to a Git repository and commit manually.
