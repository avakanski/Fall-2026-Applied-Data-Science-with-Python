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

### 4. Register the lecture in all three places

A lecture is listed in three files, and they drift apart if you update only
one. Change all three whenever a lecture is added, renamed, or consolidated:

1. **`_quarto.yml`** — sidebar entry under the right theme section
   (`website.sidebar.contents`):

   ```yaml
   - href: "Lectures/Theme_X-Theme_Name/Lecture_N-Short_Title/Lecture_N-Short_Title.ipynb"
     text: "Lecture N - Full Title"
   ```

   Sidebar text can abbreviate (e.g. "OOP") to avoid wrapping in the 360px
   pane. For a new theme, add a `- section: "Theme X - Name"` block.

2. **`index.qmd`** — the week's row in the Course Schedule table. Lecture
   titles start as plain `**bold**` text and become links once the notebook is
   posted.

3. **`README.md`** — the repo's landing page on GitHub, and the one that gets
   forgotten. It duplicates the header, lecture list, and grading information
   from `index.qmd`; keep those sections in sync. Its links are repo-relative
   (`.ipynb`/`.pdf`), not website `.html` links.

PDF-based pages (like Lecture 1) instead use a small `.qmd` with an
`<iframe>` — copy `Lectures/Lecture_1-A_Short_History_of_AI/` as a template.

### 5. Verify and publish

- Local render (optional but recommended):
  `quarto render` — quarto lives at `%LOCALAPPDATA%\Programs\quarto\bin\quarto.cmd`
  and needs `C:\Windows\System32` on PATH in sandboxed shells.
- Check the new page in `_site/`: section ids unique, sidebar entry present.
- Check that `index.qmd` and `README.md` both list the lecture and that the
  README's paths point at files that exist (renames silently break them).
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
- Superseded material is deleted, not kept. The old Lectures 2–5 were first
  excluded from rendering via `project.render` negations, but students
  browsing the repo saw both sets of Python lectures side by side, so the
  four folders were removed outright (recoverable from git history at
  `db24897~1`). If a lecture is retired, delete its folder and drop any render
  negation that referenced it.
- The user sometimes edits via the GitHub web UI — run `git fetch` and check
  `origin/main` before diagnosing "missing" changes locally (see Git workflow).

## Git workflow

Local-first is the default: edit here, commit, push. The web UI is the
exception — single binary drops (a revised syllabus or lecture PDF) when the
user is away from this machine. Notebooks must never be edited on the web:
`execute: enabled: false` means the site renders whatever outputs are saved in
the `.ipynb`, and only a local run produces them.

Publishing a local edit:

```bash
git pull --ff-only              # sync first, in case of web-UI edits
git add index.qmd               # or -A for everything changed
git commit -m "Short message"
git push                        # → Actions rebuilds the site (~2 min)
```

Start every local session with `git pull --ff-only`. It fast-forwards or
refuses; plain `git pull` would silently create a merge commit instead. To
inspect before pulling, `git fetch origin` (never touches files) then
`git status`, which reports one of:

| Status | Meaning | Action |
|--------|---------|--------|
| up to date | nothing new | work |
| `behind … can be fast-forwarded` | web-UI edits not local yet | `git pull --ff-only` |
| `ahead by N` | local commits not pushed | `git push` |
| `have diverged` | both sides moved | `git pull --rebase` |

Divergence comes from alternating directions — the fix is to never leave
unpushed local commits sitting while editing on the web. `git pull --rebase`
suits this repo, since local `.qmd` edits usually sit on top of web-UI PDF
uploads. If a pull is blocked by uncommitted work: `git stash`, pull,
`git stash pop`.

## Windows long paths (phantom deletions)

If `git status` shows dozens of files deleted under
`Lecture_4-OOP,_Modules,_Packages/MyRelativeImportPackage/…` that nobody
deleted, it is the Windows 260-character `MAX_PATH` limit, not a real deletion
and not a OneDrive sync problem. The deepest paths in that folder reach ~269
characters because the OneDrive prefix
(`C:\Users\…\OneDrive - University of Idaho\…\Fall-2026-Applied-Data-Science-with-Python\`)
alone consumes ~136 of them, so Git cannot create the files and reports them
missing on every status.

Fix, do not commit the deletions:

```bash
git config core.longpaths true   # already set in this clone; --global fixes it machine-wide
git restore -- Lectures
```

`core.longpaths` lives in `.git/config` and is **not** committed, so a fresh
clone on Windows hits this again. Cloning to a shorter path avoids it entirely.
