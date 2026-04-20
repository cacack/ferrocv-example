# ferrocv-example

A starter template for rendering your own resume with
[`ferrocv`](https://github.com/cacack/ferrocv) — the JSON Resume →
PDF/HTML/plain-text renderer powered by Typst.

## What this is

A minimal, forkable repo that takes a single `resume.json` file and
renders it to PDF, HTML, and plain text on every push via GitHub
Actions, then publishes the results as a rolling `latest` GitHub
Release.

- **Input:** `resume.json` at the repo root ([JSON Resume
  v1.0.0](https://jsonresume.org/schema/)).
- **Output:** `resume.pdf`, `resume.html`, and `resume.txt` attached
  to a `latest` release that is overwritten on every push to `main`.
  Keep the repo private and the release (and its assets) stay private
  too.
- **Runtime:** a pinned `ferrocv` binary downloaded from the upstream
  GitHub Release. No Rust toolchain, no Node, no TeX.

The sample `resume.json` describes a fully fictional person. Replace it
with your own.

## Getting started

1. Click **"Use this template" → "Create a new repository"** at the top
   of [this repo on
   GitHub](https://github.com/cacack/ferrocv-example). Keep it private
   if you don't want your resume publicly browsable.
2. Edit `resume.json` with your own content. The schema reference lives
   at <https://jsonresume.org/schema/>.
3. Commit and push to `main`. The `build` workflow validates your
   resume, renders it, and updates the `latest` release.
4. Grab your rendered PDF from the repo's **Releases → latest** page.
   The download URL is stable; on a private repo you'll need to be
   signed in to GitHub to fetch it.

### Optional: publish to GitHub Pages

Pages is **off by default**. Turning it on means your resume is served
as a website — and on Free/Pro/Team plans, Pages from a private repo
is still published to a **public** URL. Only GitHub Enterprise Cloud
supports private-access Pages.

If you still want it, run the workflow manually:
**Actions → build → Run workflow**, set
**Also deploy to GitHub Pages** to `true`. Site will appear at
`https://<your-username>.github.io/<your-repo>/` after you set
**Settings → Pages → Source** to **GitHub Actions**.

## Local preview

Install `ferrocv` (see the
[releases](https://github.com/cacack/ferrocv/releases) or
`cargo install ferrocv`), then:

```sh
ferrocv validate resume.json
ferrocv render resume.json --theme typst-jsonresume-cv --output dist/resume.pdf
ferrocv render resume.json --format html --output dist/resume.html
ferrocv render resume.json --format text --output dist/resume.txt
```

Run `ferrocv themes list` to see the themes shipped with your
installed version.

## Adding more themes or formats

The seed workflow renders a PDF with `typst-jsonresume-cv`, plus HTML
and plain text via the default `text-minimal` theme. Other PDF themes
(`modern-cv`, `fantastic-cv`) ship with `ferrocv` v0.4.0 — swap the
`--theme` value or add extra render steps. Output filenames should
follow the `resume.<format>` convention (`resume.pdf`, `resume.html`,
`resume.txt`) so they all land cleanly on the `latest` release.

## Bumping `ferrocv`

`ferrocv` is pinned in `.github/workflows/build.yml` via the
`FERROCV_VERSION` env var. Update it to a newer tag from the
[ferrocv releases
page](https://github.com/cacack/ferrocv/releases), push, and the
workflow will pick it up.

## License

This template is dedicated to the public domain under
[CC0 1.0 Universal](./LICENSE). Your own `resume.json` content is
yours — this dedication applies only to the template scaffolding.
