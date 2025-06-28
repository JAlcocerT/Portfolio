# DecapCMS + GitHub Integration Guide

This guide documents how to set up DecapCMS (Netlify CMS) as a self-hosted, Git-based content manager UI for your Hugo site, using GitHub as the backend. This enables editing Hugo content via a UI and committing changes directly to your repository—no Netlify services required.

---

## 1. Prepare Your Hugo Site
- Ensure your Hugo project is versioned on GitHub (public repo recommended for easiest setup).
- Confirm your content lives in the `content/` directory and that you have a working Hugo site.

---

## 2. Add DecapCMS Admin UI
- Place `index.html` and `config.json` in `static/admin/`.
- Example `config.json` for GitHub backend:

```json
{
  "backend": {
    "name": "github",
    "repo": "JAlcocerT/Portfolio",
    "branch": "main"
  },
  "media_folder": "static/images/uploads",
  "public_folder": "/images/uploads",
  "collections": [
    {
      "name": "test",
      "label": "Test",
      "folder": "content",
      "create": true,
      "fields": [
        { "label": "Title", "name": "title", "widget": "string" },
        { "label": "Body", "name": "body", "widget": "markdown" }
      ]
    }
  ]
}
```

---

## 3. GitHub Authentication (OAuth App)
1. Go to [GitHub Developer Settings – OAuth Apps](https://github.com/settings/developers).
2. Click "New OAuth App" and fill in:
   - Application name: (anything)
   - Homepage URL: `http://localhost:1313` (for local dev)
   - Authorization callback URL: `http://localhost:1313/admin/`
3. Register the app. Copy your **Client ID**.
4. Add `"client_id": "YOUR_CLIENT_ID"` to your `config.json` backend section.

---

## 4. Running Locally
- Start Hugo: `hugo server --bind="0.0.0.0" --baseURL="http://localhost:1313" --port=1313`
- Visit `http://localhost:1313/admin/` in your browser.
- Log in with GitHub (authorize the app). You can now edit and commit content from the UI.

---

## 5. GitHub Actions for Deployment
- Your repo contains a GitHub Actions workflow (`.github/workflows/hugo.yml`) for deploying to GitHub Pages.
- Example (with manual trigger):

```yaml
name: Deploy Hugo site to Pages

on:
  # push:
  #   branches: ["main"]
  workflow_dispatch:

permissions:
  contents: read
  pages: write
  id-token: write

concurrency:
  group: "pages"
  cancel-in-progress: true

defaults:
  run:
    shell: bash

jobs:
  # ...
```

---

## Key Points
- Hugo dev server may not serve `.yml` files; use `.json` for DecapCMS config locally.
- For public repos, GitHub OAuth is the simplest authentication method.
- No Netlify services are required—everything is self-hosted.
- GitHub Actions can be used to deploy your Hugo site to GitHub Pages after content changes.

---

_This file documents the process and configuration for using DecapCMS as a Git-based CMS for a Hugo site on GitHub._
