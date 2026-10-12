# How To Edit This Website

This guide is written for a non-technical maintainer. Every routine update is a matter of editing one small text file — no programming needed. If you edit files directly on GitHub (the pencil icon on any file page), the website rebuilds and republishes itself automatically in a few minutes.

Anything marked **PROXY** in the files is placeholder text that still needs to be replaced with real information.

## The Five-Minute Map

| I want to change…                  | Edit this file                                    |
| ---------------------------------- | ------------------------------------------------- |
| My photo                           | Replace `assets/img/prof_pic.jpg` (keep the name) |
| My biography on the home page      | `_pages/about.md`                                 |
| The news items on the home page    | Files in the `_news/` folder                      |
| The research overview / highlights | `_pages/research.md` and files in `_projects/`    |
| The top three papers               | `_bibliography/papers.bib` (see below)            |
| My CV                              | `_data/cv.yml`                                    |
| My email and social links          | `_data/socials.yml`                               |
| The contact page                   | `_pages/contact.md`                               |
| A new blog post                    | Add a file to `_posts/` (see below)               |

## Writing A Blog Post

1. Go to the `_posts/` folder and open an existing post — for example `2026-06-20-what-is-the-gravitational-wave-background.md`. It shows everything: how to add pictures and how to write equations.
2. Copy that file and rename the copy following the pattern `YYYY-MM-DD-a-short-title.md`. The date in the file name is the publication date.
3. Edit the text. Useful ingredients:
   - **Plain text** is just typed as-is. `**bold**` and `*italics*` work as shown.
   - **Equations** are written in LaTeX between double dollar signs: `$$ E = mc^2 $$`. Put them on their own line for a displayed equation, or inside a sentence for inline math.
   - **Images**: upload the picture to `assets/img/`, then copy the one-line `figure.liquid` snippet from the example post and change the file name.
4. Save (or "Commit changes" on GitHub). Done — the post appears on the blog automatically.

## Updating Publications

The **All Papers** list on the publications page updates itself: it reads directly from your INSPIRE-HEP profile every time someone opens the page. You never need to touch it.

The **Top Three Papers** section is curated by hand in `_bibliography/papers.bib`. Each paper is a block of lines between `@article{...}` and `}`. The three papers shown are the ones containing the line `selected = {true}`. To change the top three, move that line from one block to another. To add a brand-new paper, copy its BibTeX entry from INSPIRE-HEP ("cite" button → BibTeX) and paste it at the top of the file.

## Adding A News Item

Copy a file inside `_news/`, rename it (the name just needs to be unique), update the `date:` line, and replace the sentence at the bottom. News items appear automatically on the home page and on the news page.

## Changing A Research Highlight

Each card on the research page is one file in `_projects/`. The lines at the top of the file control the card:

- `title:` — the card title
- `description:` — the one-line subtitle
- `img:` — the card image (upload yours to `assets/img/` and change the path)
- `importance:` — the card order (1 comes first)

The text below the top section is the dedicated page the card links to.

## The Cat

Clicking the small cat button under your photo on the home page swaps the site into "cat mode" (a cat picture and a spoof biography). The cat text lives in `_pages/about.md` in the block marked `bio-cat`; the picture is `assets/img/ginzona.jpg`. Delete the button from `_pages/about.md` if you ever tire of it.

## Things Marked PROXY (Still To Fill In)

- Real email address (`_data/socials.yml`, `_pages/contact.md`, `_data/cv.yml`)
- Real CV PDF (`assets/pdf/`, then update `cv_pdf:` in `_data/socials.yml`)
- Real office address (`_pages/about.md`, `_pages/contact.md`)
- Real photo (`assets/img/prof_pic.jpg`)
- Research highlight images (`_projects/*.md`, the `img:` lines)
- The biography and research texts (written from public information — review them)
- The website address (`url:` in `_config.yml`)
- Google Scholar ID and GitHub username (`_data/socials.yml`, currently commented out)

## If Something Looks Broken

Nothing you do in the folders above can permanently break the site: every change is saved in the site history on GitHub, and any file can be restored from there ("History" button on the file page). For bigger questions, the template's own documentation lives in the `docs/` folder — start with `docs/QUICKSTART.md`.
