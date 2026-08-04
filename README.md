# Wenzhuo Xu's Personal Website

Source for [wenzhuoxu.com](https://wenzhuoxu.com). Jekyll + the
[Minimal Mistakes](https://github.com/mmistakes/minimal-mistakes) theme (pulled
in as a `remote_theme`, so no theme files live in this repo), built and deployed
to GitHub Pages by `.github/workflows/jekyll.yml` on every push to `main`.

## Local development

```bash
bundle install
bundle exec jekyll serve
```

Then open `http://localhost:4000`.

## Where things live

| What | File |
|---|---|
| Homepage: bio, news, selected work, education | `index.markdown` |
| Project write-ups | `_pages/research.md` |
| Publications page (structure only) | `_pages/publications.md` |
| **Every publication, talk-linked paper and report** | `_data/publications.yml` |
| CV page: experience, teaching, awards, service, skills | `_pages/cv.md` |
| Nav bar | `_data/navigation.yml` |
| Site title, description, author card, defaults | `_config.yml` |
| Custom CSS | `assets/css/main.scss` |
| Footer "last updated" stamp | `_includes/footer/custom.html` |
| Profile photo | `assets/images/self_image.jpg` (~500×500) |

## Adding a publication

Add one entry to `_data/publications.yml` in the right reverse-chronological
slot. Nothing else needs editing — the publications page and the homepage
"Selected work" section both render from that file via
`_includes/pub-list.html`.

Set `featured: true` and a `rank` to also surface an entry in Selected work on
the homepage. The `id` field becomes the anchor, so `/publications/#teecnet`
works and `_pages/research.md` can link straight to an entry.

## Adding the CV PDF

Drop a PDF at `assets/Wenzhuo_Xu_CV.pdf`. The download link on `/cv/` appears
automatically, dated from the file's own timestamp. **Strip the phone number
from the CV header first** — that page is public and indexed.

## Gotchas

- `assets/css/main.scss` **shadows** the theme's own stylesheet. The two
  `@import` lines at the bottom of its header block are what pull the theme in;
  removing either one blanks the site. Sass variable overrides must sit *above*
  those imports or they are inert.
- The Sass engine is Ruby Sass 3.7.4 (pinned by `github-pages` 228). No `@use`,
  no `@forward`, no `math.div`.
- There is no `_posts/` directory and no blog. `read_time`, `share` and
  `related` are disabled site-wide in `_config.yml`.
- `_pages/experience-redirect.html` and `_pages/awards-redirect.html` keep the
  old `/experience/` and `/awards/` URLs alive; both pages were merged into
  `/cv/`.
