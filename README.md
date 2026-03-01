# YuZhong Chen — Personal Website

Personal website built with [MkDocs](https://www.mkdocs.org/) and [Material for MkDocs](https://squidfunk.github.io/mkdocs-material/), deployed to [GitHub Pages](https://yuzhong-chen.github.io).

## Local setup (Docker)

The project uses a [Dev Container](https://containers.dev/) (see `.devcontainer/` and `docker/`). Open the repo in a dev-container–capable editor (e.g. VS Code with Dev Containers) and use the container as your environment. MkDocs and the Material theme are already installed there.

Inside the container:

- **Serve the site locally:** `mkdocs serve` → http://127.0.0.1:8000
- **Build only:** `mkdocs build` → output in `site/`

No venv or `pip install` needed when using Docker.

## Deployment to GitHub Pages

- **Automatic:** Pushing to the `main` branch runs the workflow in `.github/workflows/deploy.yml`, which builds the site, and deploys to GitHub Pages.
- **First-time setup — required for the site to appear:**
  1. On GitHub, open your repo → **Settings** → **Pages** (sidebar).
  2. Under **Build and deployment**, set **Source** to **GitHub Actions**.
  3. Push a commit to `main` (or run the workflow from the **Actions** tab). After the workflow completes, the site will be at https://yuzhong-chen.github.io (may take 1–2 minutes).

If the site doesn't look right, check the **Actions** tab for a successful run of "Deploy site to GitHub Pages" and that both the **build** and **deploy** jobs succeeded.

## Project structure

- `mkdocs.yml` — MkDocs configuration (site name, theme, nav, plugins).
- `docs/` — Source Markdown files (edit these to change site content).
- `docker/` — Dockerfile and compose for the dev container; installs MkDocs + Material (see `requirements.txt` for CI / optional local use without Docker).

## Adding content

- Add or edit `.md` files under `docs/`.
- Update the `nav` section in `mkdocs.yml` to include new pages in the navigation.
