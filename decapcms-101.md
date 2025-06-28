# DecapCMS 101: Integrating DecapCMS (Netlify CMS) with a Hugo Site

## Goal
Set up DecapCMS as a self-hosted, Git-based content manager UI for a Hugo site, without using Netlify services. The UI should allow editing Hugo content and committing changes to the repo.

---

## Steps Completed

### 1. Add DecapCMS Admin UI
- Created `static/admin/index.html` to load DecapCMS from CDN.
- Created `static/admin/config.yml` (later switched to `config.json` for Hugo dev server compatibility).

### 2. Hugo Static File Serving Issue
- Hugo's dev server sometimes fails to serve `.yml` files. Switched config to `static/admin/config.json`.
- Confirmed `/admin/config.json` is accessible in the browser.

### 3. Minimal DecapCMS Configuration
- Used a minimal `config.json` with a single collection pointing to the `content` directory.
- Created a test Markdown file (`content/test.md`) with valid front matter.

### 4. Script Loading Issue
- Fixed `index.html` to load DecapCMS only after the DOM is ready, preventing `document.body is null` error.

### 5. Local Backend ("local")
- Attempted to use the `local` backend for local file editing.
- Discovered that the CDN build of DecapCMS does not include the `local` backend.
- Installed and attempted to run `netlify-cms-proxy-server` (the correct package for local backend support).
- Proxy server ran, but the CDN DecapCMS still did not recognize the local backend.

### 6. Next Steps: GitHub Backend
- Decided to switch to the GitHub backend for real content editing and committing changes directly to the repository.

---

## Key Learnings
- **Hugo dev server** may not serve `.yml` files; use `.json` for config when testing locally.
- **DecapCMS CDN build** does not support the `local` backend; use GitHub/GitLab/Bitbucket backend for most workflows.
- **To use the local backend**, you must use a custom DecapCMS build (advanced) or use the official starter template.
- **For most users, the Git backend is recommended** for content editing and collaboration.

---

## Next Steps (GitHub Backend)
1. Update `config.json` to use the GitHub backend.
2. Set up GitHub authentication (OAuth or personal access token).
3. Commit and push changes via the DecapCMS UI.

---

_This file documents the process of integrating DecapCMS with a Hugo site, troubleshooting static file serving, and preparing for Git-based content management._
