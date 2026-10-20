# DrSGBhat.github.io

Source for [Sandesh G. Bhat's academic website](https://DrSGBhat.github.io/), built with [Jekyll](https://jekyllrb.com/) and hosted on GitHub Pages. The theme is forked from [AcademicPages](https://github.com/academicpages/academicpages.github.io).

This README explains how to keep the site up to date.

## How publishing works

- Every change pushed to the `main` branch is published automatically. GitHub rebuilds the site in about a minute.
- Check the build under the repository's **Actions** tab ("pages build and deployment"). A green check means it's live; a red cross means the build failed and the live site still shows the previous version. Open the failed run to see the error.
- After a successful build, a page can take up to about 10 minutes to refresh because of GitHub's cache. A hard refresh in the browser helps.

## Ways to edit

- **On GitHub (simplest):** open a file on github.com, click the pencil icon, edit, and choose **Commit changes** on `main`. To add a file (a PDF, an image), open its folder and use **Add file → Upload files**.
- **On your computer:** edit the files, then commit and push with git (`git add`, `git commit -m "what changed"`, `git push`). `git_push.sh` does all three in one step, always with the same commit message.

## Where things live

| What you want to change | File |
|---|---|
| Home page (About me) | `_pages/about.md` |
| CV page and CV PDF | `_pages/cv.md` and `files/Bhat_CV.pdf` |
| Publications list | `_data/publications.yml` |
| A publication's abstract page | `_publications/<ID>.md` |
| Presentations | `_pages/presentations.md` |
| Teaching | `_pages/teaching.md` |
| Service | `_pages/service.md` |
| Contact page | `_pages/contact.md` |
| Top menu | `_data/navigation.yml` |
| Sidebar (name, title, photo, email, profile links), site description, analytics | `_config.yml` |
| Profile photo | `images/sandesh.jpg` |
| PDFs (CV, open-access papers) | `files/` |
| Browser tab icon (favicon) | `favicon.ico` and the `images/favicon-*`, `apple-touch-icon.png`, `android-chrome-*` files |

Several pages show a hand-written `updated: M/D/YYYY` line near the top. Change it whenever you edit that page.

## Common updates

### Add a publication

1. Add a block at the **top of its year** in `_data/publications.yml`. Keep the whole list newest first: the page groups entries by `year` and numbers them automatically in that order.

   ```yaml
   - title: "Paper title"
     authors: 'First Author, <i><b>Sandesh G. Bhat</b></i>, Last Author'
     journal: "Journal name"
     status: "Publish Ahead of Print, March 1, 2027"   # optional; remove once it's in an issue
     year: 2027
     doi: "10.xxxx/xxxxx"                # optional; adds the "doi:" link
     page: /publications/JOURNAL27       # optional; abstract page (step 2)
   ```

   - Wrap your own name in `<i><b>…</b></i>` and put single quotes around `authors`.
   - For conference papers, add `event: "IMECE 2027"` to show the short conference name in bold.
   - The title links to `page` if there is one, otherwise to the DOI, otherwise to `url:` (a plain link you can add instead).

2. Optionally create an abstract page, `_publications/JOURNAL27.md`, whose name matches the `page` above:

   ```markdown
   ---
   title: "Paper title"
   collection: publications
   permalink: /publications/JOURNAL27
   date: 2027-03-01
   venue: 'Journal name'
   citation: 'First Author, <i><b>Sandesh G. Bhat</b></i>, Last Author.'
   ---

   [[Publication]](https://doi.org/10.xxxx/xxxxx)

   ## Abstract
   Abstract text…
   ```

   The page shows "Published in *venue*, *year*" from `venue` and `date`.

3. Update the `updated:` date in `_pages/publications.md`.

**PDFs of papers:** only upload a paper to `files/` if the publisher allows it. Open-access articles (CC BY) are fine. For subscription articles, publishers usually allow only your accepted manuscript, and only with conditions:
- Elsevier: any time, labelled CC BY-NC-ND, with a DOI link.
- Wiley: 12 months after publication, with Wiley's "accepted version" note.
- IEEE: with IEEE's copyright notice and the DOI.

Never upload the publisher's final formatted PDF of a subscription article.

### Add a presentation, course, or service entry

- **Presentations** (`_pages/presentations.md`) are grouped under `# Extramural` / `# Intramural` and `## Oral` / `## Poster`. Copy an existing entry, put it at the top of its section, and give it the next number. Numbers in these lists are typed by hand.

  ```
  11. <b>Talk title</b><br>
  	Month, Year<br>
  	Conference or event<br>
  	City, ST.
  ```

  The lines under the title start with a **tab**, which keeps them inside the numbered item.

- **Teaching** (`_pages/teaching.md`) follows the same pattern: newest course first, with the next number.
- **Service** (`_pages/service.md`) is a bulleted list under `# Academic`, `# Organizational` and `# Community`.

### Update the CV

1. Upload the new PDF to `files/` with the **same name**, `Bhat_CV.pdf`, so the existing links keep working.
2. Update the `(updated: …)` date and any changed sections in `_pages/cv.md`.

### Change the sidebar, menu, or contact details

- **Sidebar:** the name, title, location, email and profile links are in the `author:` block of `_config.yml`. Leave a field empty to hide its icon.
- **Menu:** edit `_data/navigation.yml`. Each item is a `title` and a `url`; external links (like the RASR Lab) use the full address.
- **Contact page:** `_pages/contact.md`.

### Change the profile photo

Replace `images/sandesh.jpg`, keeping the same name. Use a square photo about **600 × 600 pixels**. Large camera originals slow the site down because the photo loads on every page.

## Search engines, link previews and analytics

- **Search results:** each main page has a `description:` line in its front matter (the block between the `---` lines). That text is what search results show. The home page uses `excerpt:`. The site-wide fallback is `description` in `_config.yml`.
- **Sitemap:** `sitemap.xml` is generated automatically, and `robots.txt` points search engines to it. To keep a page out of it, add `sitemap: false` to the page's front matter. The hidden Awards, Travel and Photography pages already have this.
- **Link previews:** when a page is shared on LinkedIn, Slack or email, the preview shows the image named by `og_image` in `_config.yml` (currently the profile photo).
- **Analytics:** Google Analytics 4 is set by `analytics: google: tracking_id` in `_config.yml`. It runs only on the live site, so local previews aren't counted.

## Preview the site on your computer (optional)

You need Ruby (3.x) and Bundler. Then, from the repository folder:

```sh
bundle install                # first time, or after the Gemfile changes
bundle exec jekyll serve      # then open http://localhost:4000
```

The preview updates as you save files. Restart it after changing `_config.yml`.

GitHub Pages ignores the `Gemfile`: it builds the live site with its own fixed set of gems. The `Gemfile` only lists Jekyll and the plugins this site uses, at the same versions GitHub Pages runs. Please don't add the umbrella `github-pages` gem back. It pulls in an old `rubyzip` with a known security flaw (CVE-2026-85396), which GitHub's Dependabot reports as a security alert.

## Things to watch out for

- **One file per page address.** If two files share the same `permalink:`, one silently replaces the other on the live site. That's how an old Service page once hid newer entries.
- **YAML formatting.** In `_config.yml`, `_data/*.yml` and front matter, indentation matters. Use spaces, never tabs. Put quotes around text that contains a colon, `#`, or HTML. A formatting mistake shows up as a failed build in the **Actions** tab.
- **Removed files are still in the history.** Deleting a file takes it off the website, but it remains in this repository's history on GitHub.
- **Mac clutter.** `.DS_Store` files are ignored by `.gitignore`, so they won't be committed.
