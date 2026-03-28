# Quarto Portfolio (GitHub Pages)

If your site shows a GitHub Pages error like **"refresh repository"**, it usually means Pages is not configured to deploy built HTML yet.

## Fix (one-time)

1. Push this repository to GitHub.
2. Go to **Settings → Pages**.
3. Under **Build and deployment**, set **Source = GitHub Actions**.
4. Go to the **Actions** tab and verify the workflow **"Publish Quarto site to GitHub Pages"** runs successfully.
5. Open your site URL again after deployment finishes.

This repo includes `.github/workflows/quarto-publish.yml` to render Quarto and deploy the built site automatically.
# Guidelines.md

This guide explains how to update and publish your Quarto portfolio website in this repository.

---

## 1) Repository structure (what each file does)

- `_quarto.yml` → Site-wide configuration (navigation, theme, output folder `docs`).
- `index.qmd` → Home page (profile card + Updates section).
- `cv.qmd` → CV page that embeds `files/cv.pdf`.
- `projects.qmd` → Projects page.
- `public-goods.qmd` → Public Goods page (datasets, code, tools).
- `blogs.qmd` → Blog listing page that auto-discovers posts from `posts/`.
- `posts/*.qmd` → Individual blog post files.
- `images/` → Site images (profile picture and other local images).
- `files/` → Downloadable files (e.g., CV PDF).
- `.github/workflows/quarto-publish.yml` → GitHub Actions auto-deploy to Pages.

---

## 2) Before you edit (one-time checks)

1. On GitHub: **Settings → Pages → Source = GitHub Actions**.
2. Ensure default branch is `main` (or `master`, both are supported by workflow).
3. Ensure Actions are enabled for the repository.

---

## 3) How to update your profile on homepage

Edit `index.qmd` front matter:

- Name and intro text below `## Your Name`.
- Profile picture path in `about.image`.
- Social links in `about.links`.

### Change profile picture

- Replace file `images/profile.jpg`, OR
- Add new file (e.g., `images/me.png`) and change:

```yaml
about:
  image: images/me.png
  image-shape: round
  image-width: 14em
```

### Change social icons (example: Telegram + Instagram)

```yaml
- icon: telegram
  text: Telegram
  href: "https://t.me/your_username"
- icon: instagram
  text: Instagram
  href: "https://instagram.com/your_username"
```

> Tip: Quarto uses Bootstrap icon names in `icon:`.

---

## 4) How to maintain the Updates section

In `index.qmd`, edit the list under `### Updates`.

Recommended style:

```markdown
- **Apr 2026** • Presented paper at XYZ conference.
- **Mar 2026** • Released new replication package.
```

Best practices:
- Keep newest first.
- Keep 3–8 recent highlights.
- Remove older items periodically.

---

## 5) How to add/edit Projects

Edit `projects.qmd`.

Recommended structure for each project:

```markdown
## Project Title

**Summary:** 1–2 lines about the problem and contribution.

**Methods:** Causal inference / ML / econometrics / NLP / etc.

**Tech:** Python, R, Stata, SQL, Quarto.

**Links:** [Paper](https://...), [Code](https://github.com/...)
```

Optional: use subsections by theme:
- Academic Research
- Industry Projects
- Policy/Impact Projects

---

## 6) How to add/edit Public Goods

Edit `public-goods.qmd`.

Use this template:

```markdown
## Resource Name

**Type:** Dataset / Package / Dashboard / Tutorial

**What it provides:** 1–3 lines.

**Access:** [GitHub](https://...), [Data](https://...), [Docs](https://...)

**License:** MIT / GPL-3 / CC-BY 4.0
```

Good examples of public goods:
- Open datasets with metadata.
- Reproducible code repositories.
- Public policy dashboards.
- Teaching notebooks/tutorials.

---

## 7) How to post a new blog

1. Create a new file in `posts/`.
2. Use naming pattern: `YYYY-MM-DD-title.qmd`.

Example file: `posts/2026-04-01-my-new-post.qmd`

```markdown
---
title: "My New Post"
date: 2026-04-01
description: "One-line summary."
categories: [research, python]
---

Write in Markdown.

Inline math: $\beta_1$

Block math:
$$
Y_i = \alpha + \beta X_i + \varepsilon_i
$$

```python
print("hello")
```

```stata
sysuse auto, clear
reg price mpg weight
```
```

You do **not** need to edit `blogs.qmd`; it auto-lists posts from `posts/`.

---

## 8) Add images inside blog posts

### Local image (recommended)

1. Save image in `images/` or `posts/<post-folder>/`.
2. Reference in markdown:

```markdown
![Caption](images/my-figure.png)
```

If path is wrong, image will not appear after deploy.

### Control image size/alignment

```markdown
![Caption](images/my-figure.png){width=70% fig-align="center"}
```

---

## 9) Add videos in blog posts or pages

### YouTube embed (HTML iframe)

```html
<iframe width="100%" height="420"
  src="https://www.youtube.com/embed/VIDEO_ID"
  title="YouTube video" frameborder="0"
  allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture"
  allowfullscreen>
</iframe>
```

### Local video file

Put file in `files/` or `videos/` and embed:

```html
<video controls width="100%">
  <source src="files/demo.mp4" type="video/mp4">
  Your browser does not support the video tag.
</video>
```

---

## 10) Add PDFs, slides, or downloadable files

1. Put file in `files/`.
2. Link from any page:

```markdown
[Download slides](files/slides.pdf)
```

For CV page, keep `files/cv.pdf` updated.

---

## 11) Local preview and build

If Quarto is installed locally:

```bash
quarto preview
```

```bash
quarto render
```

`quarto render` writes output to `docs/` as configured.

---

## 12) Publish workflow (GitHub Pages)

After editing:

```bash
git add .
git commit -m "Update portfolio content"
git push origin main
```

Then:
1. Open GitHub **Actions** tab.
2. Wait for **Publish Quarto site to GitHub Pages** to pass.
3. Refresh your site URL.

---

## 13) Troubleshooting

### A) Site shows "refresh repository" / error page
- Ensure **Settings → Pages → Source = GitHub Actions**.
- Confirm workflow completed successfully.

### B) Changes not visible
- Hard refresh browser cache (Ctrl/Cmd + Shift + R).
- Wait 1–3 minutes after successful deploy.

### C) Image not showing
- Verify exact file path and case sensitivity (`.png` vs `.PNG`).
- Confirm file was committed and pushed.

### D) Blog post not listed
- Ensure file is in `posts/`.
- Ensure front matter has valid `title` and `date`.
- Ensure `.qmd` extension.

### E) Broken YAML/front matter
- Use spaces (no tabs).
- Keep `---` start/end delimiters.

---

## 14) Content quality checklist (recommended)

Before pushing:
- [ ] Name, bio, and contact links are updated.
- [ ] Updates section reflects latest 3–8 items.
- [ ] Projects/Public Goods include clear links and methods.
- [ ] New posts have title, date, description, categories.
- [ ] Images/videos render in local preview.
- [ ] No placeholder links left.

---

## 15) Suggested monthly workflow

1. Add one new update item.
2. Add/refresh one project or public good entry.
3. Publish one blog post or brief technical note.
4. Verify deployment on GitHub Pages.

---

If you want, you can later split this file into:
- `CONTRIBUTING.md` (technical workflow)
- `CONTENT_GUIDE.md` (writing/content templates)
for cleaner maintenance.

