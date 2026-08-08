# Wooz's Movie Picks

A single-page, curated film recommendation site. Plain HTML, CSS, and vanilla
JavaScript — no framework, no build step, no dependencies. Film data lives in a
`DATA` array inside a `<script>` tag in the HTML file itself.

Deployed via GitHub Pages from this repo. Deploy = commit and push to GitHub;
Pages serves it automatically. Environment is Windows.

## Files

- `index.html` — the live site. Must stay at the repo root so it serves at the
  root URL. Includes a collapsible "Add a Film" form (validation + a "Download
  Updated Page" button that re-serializes the DATA array into a fresh copy of
  the page).
- `wooz-movie-picks.html` — a static snapshot of the same site, without the
  add-film form. Kept in sync with `index.html` for everything else.

If a change affects both files, apply it to both unless told otherwise.

## Data conventions

Each film is a 5-element array:

```js
["1975", "Jaws", "Steven Spielberg", "Richard Dreyfuss", "tt0073195"]
//  year   title    director           starring           IMDb ID
```

Grouped into decade objects labeled `"1970's"` — four-digit decade, apostrophe,
lowercase `s`. The page CSS deliberately does NOT uppercase these labels, so the
lowercase `s` survives rendering.

**Sort order: decade → year → title.** Titles sort alphabetically with a leading
`The`, `A`, or `An` ignored (`sortTitle()` in the script). Do not extend this to
foreign-language articles — the list contains *Die Hard*, where "Die" is the
English verb, not an article.

Multiple names in one field are joined with `&`, never `/` or `and`
(e.g. `"Steve McQueen & Dustin Hoffman"`).

The header's film count and each decade's count are computed at render time from
`DATA` — never hardcode them.

## Adding films

**Always look up IMDb IDs; never write one from memory.** They are not
guessable and a wrong ID produces a link to an unrelated film. (A previous
session recalled `tt0091680` for *Manhunter*; the real ID is `tt0091474`.)

Verify the release year too — several entries in the original source list were
off by a year or filed under the wrong decade.

Where the user's source data lists a director in the actor field or vice versa,
flag it rather than silently entering it. This has happened several times
(e.g. *A Streetcar Named Desire*, *Singin' in the Rain*).

## Design

Dark "35mm film archive" theme: near-black background, amber accents, Oswald for
display type, JetBrains Mono for data. Sprocket-hole rails down the page edges,
countdown-leader mark in the header, film-reel SVG favicon embedded as a data
URI (no separate favicon file needed). Colors are CSS custom properties on
`:root` — change them there, not inline.

Layout must stay readable on both desktop and mobile; each film row is a
two-line grid (year + title, then labeled Director / Starring beneath).

## Working style

Make targeted edits. Don't reformat or regenerate the whole file for a small
change, and don't restructure the CSS unless asked.
