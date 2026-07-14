# Applied Data Science with Python — Fall 2026 course website

Quarto website for CS 4622/5622 (University of Idaho), published via GitHub
Actions (`.github/workflows/publish.yml`) to GitHub Pages on every push to
`main`. Lectures are pre-executed Jupyter notebooks (`execute: enabled: false`
in `_quarto.yml` — builds never run notebook code; saved outputs render as-is).

## Adding a new lecture notebook (the common task)

### 1. File layout

```
Lectures/Theme_X-Theme_Name/Lecture_N-Short_Title/
├── Lecture_N-Short_Title.ipynb     (same name as folder)
└── images/                          (all figures, relative paths)
```

Spaces in names become `_`; commas are fine (e.g. `Lecture_3-Files,_Functions`).
Run the notebook fully before committing so all cell outputs are saved.

### 2. Required notebook header (first 4 markdown cells)

- **Cell 0** — title: `# Lecture N - Full Title`
- **Cell 1** — three badges. Replace `<PATH>` with the notebook's repo path,
  commas URL-encoded as `%2C`:

  ```markdown
  [![View notebook on Github](https://img.shields.io/static/v1.svg?logo=github&label=Repo&message=View%20On%20Github&color=lightgrey)](https://github.com/avakanski/Fall-2026-Applied-Data-Science-with-Python/blob/main/<PATH>.ipynb)
  [![Open In Collab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/avakanski/Fall-2026-Applied-Data-Science-with-Python/blob/main/<PATH>.ipynb)
  [![View on Website](https://img.shields.io/static/v1.svg?logo=quarto&label=Web&message=View%20on%20Website&color=blue)](https://avakanski.github.io/Fall-2026-Applied-Data-Science-with-Python/<PATH>.html)
  ```

- **Cell 2** — `<a id='top'></a>`
- **Cell 3** — table of contents: bullet list of links to the section anchors
  (see numbering below), ending with `- [References](#references)`

### 3. Headings, numbering, and anchors

- `## N.1 Section Title` — numbered second-level sections
- `### N.1.1 Subsection Title` — numbered third-level subsections
- `####` and deeper — unnumbered
- Appendices: `## Appendix: Title` (or `Appendix 1:`, `Appendix 2:` if several)
- End with `## References` (numbered list) and a final `[BACK TO TOP](#top)` cell.

Every heading that the TOC links to needs an anchor **on its own line above
the heading, followed by a blank line**, id = lowercase title, spaces → `-`:

```markdown
<a id="3.1.2-opening-a-file"></a>

### 3.1.2 Opening a file
```

**Never** use self-closing `<a id="..."/>` and never put the anchor inside the
heading text — both break in-page links on the website (browsers treat `<a/>`
as an unclosed tag, and Quarto clones heading contents into the right-hand
TOC, duplicating the id).

### 4. Register the lecture in `_quarto.yml`

Add a sidebar entry under the right theme section (`website.sidebar.contents`):

```yaml
- href: "Lectures/Theme_X-Theme_Name/Lecture_N-Short_Title/Lecture_N-Short_Title.ipynb"
  text: "Lecture N - Full Title"
```

Sidebar text can abbreviate (e.g. "OOP") to avoid wrapping in the 360px pane.
For a new theme, add a `- section: "Theme X - Name"` block. PDF-based pages
(like Lecture 1) instead use a small `.qmd` with an `<iframe>` — copy
`Lectures/Lecture_1-A_Short_History_of_AI/` as a template.

### 5. Verify and publish

- Local render (optional but recommended):
  `quarto render` — quarto lives at `%LOCALAPPDATA%\Programs\quarto\bin\quarto.cmd`
  and needs `C:\Windows\System32` on PATH in sandboxed shells.
- Check the new page in `_site/`: section ids unique, sidebar entry present.
- Commit and push to `main`; GitHub Actions rebuilds the site (~2 min).
- Browsers cache pages for 10 min — if a page looks unstyled or stale after a
  deploy, **Ctrl+F5**, don't debug.

## Site-wide conventions (don't break these)

- Theme: `cosmo` + `theme.scss` / `theme-dark.scss` (STA 210-style), Atkinson
  Hyperlegible font, teal `#D9E3E4` sidebar/footer, no top navbar (title,
  search, and GitHub tool live in the sidebar header).
- `styles.css`: bold blue top-level sidebar entries, 16px main content,
  right-TOC subsection styling, TOC expand-arrow styling.
- `toc-arrows.html` (included on every page): expand/collapse arrows in the
  right-hand TOC, and it collapses the sidebar section literally named
  "Course Information" on load — if that section is renamed, update the
  string there too.
- Retired notebooks (old Lectures 2–5 before consolidation) stay in the repo
  but are excluded from rendering via `project.render` negations in
  `_quarto.yml`. Exclude, don't delete, superseded material.
- The user sometimes edits via the GitHub web UI — run `git fetch` and check
  `origin/main` before diagnosing "missing" changes locally.
