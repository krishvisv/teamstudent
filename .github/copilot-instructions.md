This repository is a Jekyll-based GitHub Pages site used as an educational "student" starter site (site root: `/_site` when built).

Quick context
- This repo builds with Jekyll and is deployed via GitHub Pages Actions. Key config: `_config.yml` (see `github_repo` and `baseurl`).
- Local development is driven by the `Makefile`. Typical workflow: run `make` (starts Jekyll serve), `make stop`, `make clean`, `make convert`.
- Notebooks in `_notebooks/` are converted to posts in `_posts/` using `scripts/convert_notebooks.py`. The Makefile triggers conversion on changes.

What to do first (fast path)
- To preview site: run `./scripts/venv.sh && source venv/bin/activate && bundle install` then `make`.
- If you only need to convert a single notebook: run `python3 -c 'from scripts.convert_notebooks import convert_single_notebook; convert_single_notebook("_notebooks/...ipynb")'` (the Makefile runs a similar command).

Architecture & important files
- Content: `_posts/` (markdown posts) and `_notebooks/` (Jupyter notebooks). Converted notebooks produce `*_IPYNB_2_.md` files in `_posts/`.
- Layouts & includes: `_layouts/` (page templates) and `_includes/` (partials like `custom-head.html`, `notebook_*_link.html`, `game.html`). When editing markup, change the layouts here.
- Scripts: `scripts/convert_notebooks.py`, `scripts/venv.sh`, `scripts/activate_*.sh` — these implement the local dev and conversion logic. Refer to them when automating conversions or CI steps.
- Build: `Gemfile` uses `github-pages` gem. `Makefile` wraps `bundle exec jekyll serve` and log parsing; use it instead of invoking Jekyll directly to preserve conversion hooks.

Project-specific conventions
- Notebook conversion naming: converted files include `_IPYNB_2_.md` suffix. Do not edit converted files directly; edit the source notebook in `_notebooks/` and re-run conversion.
- Front matter conventions: posts and notebooks expect YAML front matter (see examples in existing files). Dates must be zero-padded (YYYY-MM-DD). Use `search_exclude: true` in front matter to hide pages from search.
- Port and repo override: `Makefile` accepts `PORT` and `REPO_NAME` environment overrides. Example: `make PORT=4610 REPO_NAME=myrepo`.

CI / deployment notes
- Deployment is GitHub Pages via Actions (standard pages workflow). Avoid changing `_config.yml` keys used by CI: `github_repo` and `baseurl` unless you know deployment target.
- The repo expects `future: true` in `_config.yml` to show future-dated posts during local dev.

Patterns for code changes
- When adding UI components, prefer editing `_includes/` and `_layouts/` then wire them into pages via Liquid includes: e.g. `{%- include post_list.html -%}`.
- JavaScript games and samples live as standalone `.html` or under `assets/` and `_includes/game.html`. Keep interactive demos self-contained.

Examples to reference
- Convert all notebooks: `make convert` (uses `scripts/convert_notebooks.py`).
- Start dev server: `make` (backgrounds server and tails logs at `/tmp/jekyll$(PORT).log`).
- Clean site: `make clean` (removes `_site` and converted markdown).

When you are editing or creating content
- Edit source (`_notebooks/*.ipynb` or `_posts/*.md`). Do not hand-edit generated `_posts/*_IPYNB_2_.md` unless you intend to keep the generated form permanently.
- If a notebook does not convert correctly, inspect `LOG_FILE` (`/tmp/jekyll$(PORT).log`) and re-run `make convert`.

If you need more info
- Read `README.md` for full onboarding steps and `scripts/` for conversion/dev automation details.
- Ask for the preferred GitHub Actions workflow if you plan to modify CI or deployment.

If anything in this file looks incorrect or missing for your workflow, tell me which area (build, conversion, layouts, CI) and I'll refine these instructions.
