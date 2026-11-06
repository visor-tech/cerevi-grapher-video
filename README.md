# Cerevi Grapher — Video Demos

Two short H.264 demos of Cerevi Grapher, shown on a single self-contained page.
No build step, no dependencies: `index.html` + two `.mp4` files.

| # | File | Title | Length | Size |
|---|------|-------|--------|------|
| 01 | `Atlas-aware Labeling.mp4` | Atlas-aware Labeling | 23 s | 19.5 MB |
| 02 | `boundary-based annotation.mp4` | Boundary-based Annotation | 38 s | 21.2 MB |

Both are 2560 × 1440 H.264 (High, Level 5.1), which every modern browser plays natively.

## Preview locally

```bash
python -m http.server 8000
# open http://localhost:8000/
```

(Opening `index.html` directly via `file://` also works.)

## Publish with GitHub Pages

1. Push this folder to `visor-tech/cerevi-grapher-video` on the `main` branch.
2. Repository → **Settings** → **Pages**.
3. **Source**: *Deploy from a branch* → **Branch**: `main`, **Folder**: `/ (root)` → **Save**.
4. Wait ~1 minute for the first build, then open
   **https://visor-tech.github.io/cerevi-grapher-video/**

The repository is public, so Pages is available on the free plan. `.nojekyll` keeps
GitHub from running the content through Jekyll.

### Alternative: deploy with GitHub Actions

If you prefer an explicit workflow (or later move the site into a `docs/` folder),
set **Source** to *GitHub Actions* and commit `.github/workflows/pages.yml`:

```yaml
name: Deploy to GitHub Pages
on:
  push:
    branches: [main]
  workflow_dispatch:
permissions:
  contents: read
  pages: write
  id-token: write
concurrency:
  group: pages
  cancel-in-progress: true
jobs:
  deploy:
    runs-on: ubuntu-latest
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}
    steps:
      - uses: actions/checkout@v4
      - uses: actions/configure-pages@v5
      - uses: actions/upload-pages-artifact@v3
        with:
          path: .
      - id: deployment
        uses: actions/deploy-pages@v4
```

## Notes

- GitHub rejects files over 100 MB; these two are 19.5 MB and 21.2 MB, so plain Git is fine.
- Pages serves the whole site up to 1 GB — well within budget.
- Keep the file names as they are (`index.html` references them URL-encoded, `%20` for the spaces).
