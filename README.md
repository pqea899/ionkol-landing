# Ionkol landing site

Plain static pages: HTML, CSS and JavaScript in each file, plus photos and video. There's no build step, framework or server code. Host the `site/` folder as it is.

- **Design reference (Figma):** https://www.figma.com/design/OT16B5pzLeLPlsF1HxmLvS
- **What to connect:** [HANDOFF.md](HANDOFF.md)

## Run it locally

```
cd site
python3 -m http.server 8080
# open http://localhost:8080
```

## What's in `site/`

| File | Page |
|---|---|
| `index.html` | Home |
| `creators.html` | For creators: see jobs, get your report |
| `jobs.html`, `job.html` | Jobs list and one job post |
| `contact.html` | Contact and Book a demo |
| `signup.html`, `signup-business.html`, `signup-creator.html`, `login.html` | Sign up (choose business or creator, then one page each) and log in |
| `terms.html`, `privacy.html` | Legal pages (draft, awaiting legal review) |
| `404.html` | Not found |
| `*-ko.html`, `*-ms.html`, `*-zh-hans.html`, `*-zh-hant.html` | Korean, Malay, Simplified and Traditional Chinese versions of home, jobs, contact, sign up, log in and 404 |
| `img/` | Photos (WebP) |
| `og.jpg`, `favicon.svg` | Share image and browser icon (stand-ins until the final logo) |
| `vid/` | Hero video: `hero.mp4` (desktop), `hero-m.mp4` (phone) and `hero-poster.jpg` |

## Editing

Edit the HTML files directly. Each page is self-contained. The header, footer and colours repeat in every file, so if you change one, search all files for the same block.
