# Seminar site

A small Jekyll site for an academic seminar. Talks live in one YAML file; the
site sorts them and displays the schedule, and renders TeX with MathJax. No
plugins, no theme gem, no JavaScript beyond
MathJax itself.

```
_config.yml               site title, room, meeting time, organizers, baseurl
_data/talks.yml           scheduled talks               ← the file you edit weekly
_data/mathjax_macros.yml  optional \RR, \Spec, ... shorthand
index.html                upcoming schedule, next talk highlighted
information.md            practical details and how to propose a talk
_includes/talk.html       markup for a single talk
_includes/mathjax.html    MathJax 3 configuration
_layouts/                 default and page layouts
assets/css/style.css      all styling, themed with CSS custom properties
.github/workflows/pages.yml   build and deploy to GitHub Pages
```

## Setting it up

1. Create a repository named after the seminar — say `seminar` — under the same
   account as your `USERNAME.github.io` page, and push these files to `main`.

2. In `_config.yml`, set:

   ```yaml
   url: "https://USERNAME.github.io"   # no trailing slash
   baseurl: "/seminar"                 # the repository name, leading slash
   ```

   The site will be served at `https://USERNAME.github.io/seminar/`. Every
   internal link goes through Jekyll's `relative_url` filter, so this one line
   is all that controls it. (For a bare `USERNAME.github.io` repository, set
   `baseurl: ""` instead.)

3. In the repository, go to **Settings → Pages** and set **Source** to
   **GitHub Actions**. The workflow in `.github/workflows/pages.yml` does the
   rest on every push to `main`.

The workflow also rebuilds once a day at 07:00 UTC. That matters: the site works
out which talks are upcoming at *build* time, so without the nightly run a
finished talk would sit at the top of the schedule until the next push.

## Adding a talk

Append an entry to `_data/talks.yml`. Order does not matter — the site sorts.

```yaml
- date: 2026-10-07          # required, ISO, unquoted
  speaker: "Ada Lovelace"   # required
  title: 'Bitangents to a smooth plane quartic over $\QQ$'   # required
  affiliation: "Analytical Institute"
  url: "https://example.edu/~lovelace"
  time: "3:00–4:00 pm"      # only if it differs from the usual slot
  room: "Room 622 (note the room change)"
  abstract: >
    Folded block. Blank lines become paragraph breaks; everything else
    is joined into one paragraph, so you can wrap however you like.
  note: "Joint with the number theory seminar."
  cancelled: true           # keeps the entry, strikes it through
  links:
    slides: "https://..."   # any keys you like; underscores become spaces
    video:  "https://..."
    arxiv:  "https://..."
```

**Quote TeX with single quotes.** YAML processes `\` escapes inside double
quotes but not single ones, so `'$\mathbb{Z}$'` arrives intact while
`"$\mathbb{Z}$"` would need `\\mathbb`. This is the one thing that trips people
up when they add a talk in a hurry.

## Math

MathJax 3 is configured in `_includes/mathjax.html` for `$...$`, `$$...$$`,
`\(...\)` and `\[...\]`, with AMS equation numbering on.

Abstracts are passed through untouched apart from turning paragraph breaks into
line breaks — they are deliberately *not* run through the Markdown converter, so
underscores and backslashes in `$H^1_{\text{ét}}$` survive. The tradeoff is that
you cannot use Markdown inside an abstract; if you want that, add `| markdownify`
in `_includes/talk.html` and expect to escape underscores by hand.

On Markdown pages (`information.md` and anything you add), `kramdown` is set to
`math_engine: null` so it leaves the delimiters alone for MathJax. Display math
there needs a blank line above and below it, or kramdown will treat it as inline.

Shorthand goes in `_data/mathjax_macros.yml`:

```yaml
RR: '\mathbb{R}'
sh: ['\mathcal{#1}', 1]   # with arguments
```

## Working on it locally

```sh
bundle install
bundle exec jekyll serve --livereload
```

Then open <http://localhost:4000/seminar/> — the `baseurl` applies locally too.

## Making it yours

The palette is eight custom properties at the top of `assets/css/style.css`,
with a dark-mode block right below; changing `--accent` changes the next-talk
panel, the current nav item, and link hovers together. Typefaces are system
stacks (a Charter/Palatino-style serif for titles and abstracts, the system sans
for dates and metadata), so there are no webfont requests to wait on.
