# KARAKU

**Stream the Synthetic Imagination.** KARAKU is a streaming-style website for AI dramas, anime, movies and a manhua reading library, all in one self-contained `index.html`. No build step, no framework, no backend.

Made by [Accxs Creations](https://bryangablao.github.io/Accxs-Creations).

> **GitHub short description** (paste into the repo's *About* box):
> A single-file streaming-style site for AI dramas, anime, movies and manhua, with dark/light themes and no build step.

---

## Sections

| Section | Link | What it is |
|---|---|---|
| **KARAKU \| CINEMA** | `index.html` | AI Drama, Anime and Movies: featured hero, rails, search, details modal, season/episode lists and a full-screen player |
| **KARAKU \| MANHUA** | `index.html#/manhua` | Manhua library: portrait covers, genre filters, Completed and New & Popular views, chapter lists |
| **Terms of Service** | `index.html#/terms` | Legal page |
| **Privacy Policy** | `index.html#/privacy` | Legal page |

The legal pages' Back button returns to the page you came from (Cinema or Manhua).

## Features

- One file, zero dependencies. Only Google Fonts are loaded from the web.
- Dark and light theme, saved in the browser and shared by every section.
- Live search, genre filters and auto-rotating featured hero.
- Details modal first, then a full-screen player. Embeds can be YouTube, Facebook, TikTok or Google Drive.
- Fully responsive, with a mobile menu.
- Matching Cinema and Manhua headers and footers, with a live Philippine Standard Time (UTC+8) clock.
- Manhua and legal pages run in isolated shadow roots, so their styles and scripts never clash with the main site.

## Project structure

```
index.html            the whole site (Cinema + Manhua + Terms + Privacy)
image/
  letter-k.png        logo / favicon
  aidrama/            AI drama posters
  anime/              anime posters
  movies/             movie posters
  manhua/             manhua covers (portrait, 2:3 works best)
```

Poster paths are set per title in the catalogs. If an image is missing, a colored fallback cover with the title is shown.

## Run locally

Open `index.html` in a browser. To test hash links and embeds the way they behave online, serve the folder instead:

```bash
python3 -m http.server 8000
# then visit http://localhost:8000
```

## Deploy to GitHub Pages

1. Push `index.html` and the `image/` folder to your repository.
2. Go to **Settings, Pages**.
3. Choose **Deploy from a branch**, select `main` and `/ (root)`, then save.
4. Your site will be live at `https://<username>.github.io/<repo>/`.

Legal pages are reachable at `/#/terms` and `/#/privacy`. Use those URLs wherever a service asks for a Terms or Privacy Policy link.

## Adding content

Everything is data in the `<script>` blocks of `index.html`.

### Add a Cinema title

Find `const catalog = [` (the first one) and copy an existing block:

```js
{
  id:"d9",                       // unique id
  title:"My Title",
  cat:"drama",                   // "drama" | "anime" | "movie"
  genres:["Romance","Drama"],
  duration:"15 minutes per episode",
  hue:330,                       // color of the fallback cover (0-360)
  flags:"n",                     // "n" = New, "t" = Trending
  releaseMonth:10, releaseYear:2026,
  summary:"...",
  poster:"image/aidrama/my-title.jpg",
  seasons:[{ season:1, episodes:[ /* episode objects with a source */ ] }]
}
```

To feature a title in the home hero, add its id to `FEATURED_IDS`.

### Add a manhua

Find the second `const catalog = [` (the one under **HOW TO ADD A MANHUA**) and copy a block:

```js
{
  id:"mh13", title:"My Manhua",
  genres:["Action","Fantasy"],
  status:"Ongoing",              // or "Completed"
  chapters:12,
  chapterUrl:"https://example.com/my-manhua/chapter-{n}",   // {n} = chapter number; "" = Coming Soon
  hue:200, flags:"nt",           // "n" = New, "t" = Trending
  releaseMonth:10, releaseYear:2026,
  poster:"image/manhua/my-manhua.jpg",
  summary:"..."
}
```

New titles stay in **New** for their release month and the month after.

## Notes

- Videos and chapters are hosted by third-party providers and remain subject to their own terms. KARAKU only links or embeds them.
- The Terms and Privacy pages are practical website templates, not legal advice. Review them before launch, and update the Contact sections once you have a support email.
- Theme and recently viewed items are stored in the browser's local storage. If storage is blocked, the site still works and simply doesn't remember them.

## License

© 2026 Accxs Creations. All rights reserved. Add a license file here if you want to open-source the code.
