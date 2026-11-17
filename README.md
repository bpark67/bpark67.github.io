# bpark67.github.io

Personal academic website of Bumjun Park, served by GitHub Pages at <https://bpark67.github.io>.
Built with Jekyll on a customised version of the
[Agency](https://startbootstrap.com/theme/agency) Bootstrap theme.

Pushing to `main` publishes the site automatically, usually within a minute or two.

## Where things live

| To change…                              | Edit                                              |
| --------------------------------------- | ------------------------------------------------- |
| Name, title, email text, social links       | `_config.yml`                                     |
| Bio paragraphs                          | `_includes/aboutme.html`                          |
| Education timeline                      | `_data/timeline.yml`                              |
| Publications                            | `_data/publications.yml`                          |
| Presentations & posters                 | `_presentations/` (one file each)                 |
| Teaching                                | `_data/teaching.yml`                              |
| Reading page (books)                    | `_data/reading.yml`                               |
| Personal pages (navbar menu)            | a `.md` file per page + `personal_pages` in config |
| Software (hidden until enabled)         | `_data/software.yml` + `show_software` in config  |
| CV                                      | replace `img/CV.pdf`, update `cv_updated` in config |
| Colours and fonts                       | `_data/template.yml`                              |
| Styling                                 | `_includes/css/agency.css` (custom rules at the bottom) |

## Common tasks

### Update the CV
1. Replace `img/CV.pdf` with the new file (keep the same name).
2. Change `cv_updated:` in `_config.yml`.

### Add a publication
Copy the commented template at the top of `_data/publications.yml` and fill it in.
Use `status: "Preprint"` (or "Under review", "In press") for work that isn't published yet.
The list sorts itself by `year`.

### Add a talk or poster
Create a file in `_presentations/` named `YYYY-MM-DD-short-name.md`:

```yaml
---
title: "Full talk or poster title"
venue: "Joint Statistical Meetings 2026"
authors: "B. Park, E. Lila"         # optional; "B. Park" is bolded
date: 2026-08-03
category: Presentation        # or Poster
keywords: Functional Data Analysis
thumbnail: jsm-small.jpg      # in img/portfolio/, ~720px wide
image: jsm-big.jpg            # in img/portfolio/, ~1800px wide
pdf: img/portfolio/jsm-poster.pdf   # optional: poster PDF
slides: img/portfolio/jsm-slides.pdf # optional: slides PDF or link
description: >-
  One paragraph describing the work.
---
```

### Add a separate page (e.g. Reading, Travel)
1. Create `reading.md` in the repository root:
   ```markdown
   ---
   layout: page
   title: Reading
   subtitle: Books I've enjoyed recently   # optional
   permalink: /reading/
   ---

   Write the page in Markdown here.
   ```
2. List it in `_config.yml` under `personal_pages` (title + url) so it
   appears in the navbar's "Personal" menu.

### Image sizes
Keep images small so the site loads fast on phones:
save photos and figures as **JPEG, at most ~1800px wide** (thumbnails ~720px).
A phone photo straight from the camera is often 5–30 MB; resize it before adding it.

## Previewing locally (optional)

Requires Ruby. From the repository folder:

```bash
bundle install
```

```bash
bundle exec jekyll serve
```

Then open <http://localhost:4000>.
