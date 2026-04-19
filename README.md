# ferrocv-example

A starter template for rendering your own resume with
[`ferrocv`](https://github.com/cacack/ferrocv) — the JSON Resume → PDF
(soon HTML/text) renderer powered by Typst.

## What this is

A minimal, forkable repo that takes a single `resume.json` file and
renders it to PDF on every push via GitHub Actions, then publishes the
output to GitHub Pages.

- **Input:** `resume.json` at the repo root ([JSON Resume
  v1.0.0](https://jsonresume.org/schema/)).
- **Output:** two PDFs, one per bundled `ferrocv` theme, published to
  GitHub Pages on every push to `main`.
- **Runtime:** a pinned `ferrocv` binary downloaded from the upstream
  GitHub Release. No Rust toolchain, no Node, no TeX.

The sample `resume.json` describes a fully fictional person. Replace it
with your own.

## Getting started

1. Click **"Use this template" → "Create a new repository"** at the top
   of [this repo on
   GitHub](https://github.com/cacack/ferrocv-example).
2. In your new repo, go to **Settings → Pages** and set **Source** to
   **GitHub Actions**.
3. Edit `resume.json` with your own content. The schema reference lives
   at <https://jsonresume.org/schema/>.
4. Commit and push to `main`. The `build` workflow renders your resume
   and deploys the result to GitHub Pages.
5. Your rendered resume lives at
   `https://<your-username>.github.io/<your-repo>/`.

## Local preview

Install `ferrocv` (see the
[releases](https://github.com/cacack/ferrocv/releases) or
`cargo install ferrocv`), then:

```sh
ferrocv validate resume.json
ferrocv render resume.json --theme typst-jsonresume-cv --output dist/resume.pdf
```

Available themes today: `typst-jsonresume-cv`, `fantastic-cv`. Run
`ferrocv render --help` for the full list on your installed version.

## Picking a theme

The workflow renders both bundled themes so you can compare. Once
you've picked one, edit `.github/workflows/build.yml` and remove the
render step for the other theme (and remove it from `index.html`).

## Bumping `ferrocv`

`ferrocv` is pinned in `.github/workflows/build.yml` via the
`FERROCV_VERSION` env var. Update it to a newer tag from the
[ferrocv releases
page](https://github.com/cacack/ferrocv/releases), push, and the
workflow will pick it up.

## HTML and plain text output

Planned in `ferrocv` but not yet shipped (tracked as
[ferrocv#14](https://github.com/cacack/ferrocv/issues/14)). When those
land, this template will grow the matching render steps.

## License

This template is dual-licensed under either of
[Apache-2.0](./LICENSE-APACHE) or [MIT](./LICENSE-MIT), matching the
upstream `ferrocv` project. Your own `resume.json` content is yours —
this license applies only to the template scaffolding.
