# Data Donation Network website

Source for the Data Donation Network website, built with [Quarto](https://quarto.org) and hosted on GitHub Pages.

## Editing content

Every page is a Markdown file (`.qmd`). Edit it on GitHub or locally and push to `main`; a GitHub Action rebuilds and publishes the site automatically.

| Page | File |
|------|------|
| Home | `index.qmd` |
| About | `about.qmd` |
| People | `people.qmd` |
| Symposium overview | `symposium/index.qmd` |
| Early Career Network | `early-career.qmd` |
| Join & Contact | `join.qmd` |

Mailing-list links and the contact email are set once in `_variables.yml`.
Colours and fonts are set in `styles.scss`.

### Adding a symposium

Each edition is a folder, `symposium/<year>/`. The edition the network is currently working on has several pages:

- `index.qmd`: overview and key dates
- `call.qmd`: call for papers
- `programme.qmd`: programme
- `venue.qmd`: venue and travel

`_nav.qmd` holds the menu shown at the top of those pages. After the event the folder stays as it is and becomes that edition's archive, so links keep working. Older editions (2022–2026) have a single page.

When the next edition is announced:

1. Copy the folder `symposium/_template` to `symposium/<year>/`. Delete pages you don't need, and remove them from `_nav.qmd` too.
2. Fill in the front matter of `index.qmd` (`title`, `date`, `dates`, `location`, `host`, `description`). `date` is the first day and is used for sorting. `dates` is the text shown on the card, e.g. "8–9 October 2027" or "To be announced".
3. Set `status: upcoming`. It then appears on the home page and under "Next symposium" on the Previous symposia page.
4. Set the previous edition to `status: past`. It then moves to "Previous symposia".
5. Point the **Symposium menu** in `_quarto.yml` to the new folder: the year in each `href`, and the city and year in the first item. Keep the menu on the last edition until the next one is announced, even after the event has taken place.
6. Add the new host city to the map in `_symposium-map.qmd`; the comment in that file explains the coordinates. Then update the logo (see below).

### The logo changes every year

The logo is not a fixed mark. It is drawn from the symposium map: one dot per host city, joined in the order the symposia took place, ending at the upcoming city in the accent colour. Each time a new symposium is announced, the logo changes with it. This represents the every dynamic nature of the network build on collaboration.

The logo exists in two files, and both need updating:

- `images/ddn-logo.svg`: light version for the navbar.
- `images/favicon.svg`: dark version for the browser tab.

To keep it legible at small sizes, the logo shows **at most 7 cities**. It currently shows 6, Utrecht 2022 to Budapest 2027. Once the cap is reached, drop the oldest city when adding a new one. The cap only applies to the logo: the map on the home page keeps every edition. The exact cap (6 or 7) is still to be decided.

## Previewing locally

Install Quarto, then run:

```bash
quarto preview
```

## First-time deployment setup

1. Create the GitHub repository and push `main`.
2. Run `quarto publish gh-pages` once locally to create the `gh-pages` branch.
3. In the repository, go to **Settings → Pages** and set the source to the `gh-pages` branch.
4. After that, every push to `main` publishes through `.github/workflows/publish.yml`.

### Custom domain: datadonationnetwork.org

Until the domain is connected, the site is previewed at `datadonationnetwork.github.io/ddn-website`. To switch over:

1. At the domain registrar, point DNS to GitHub Pages: `A` records for `datadonationnetwork.org` to `185.199.108.153`, `185.199.109.153`, `185.199.110.153` and `185.199.111.153`, and a `CNAME` record for `www` to `datadonationnetwork.github.io`.
2. Recommended: verify the domain for the GitHub organisation (**Organisation settings → Pages → Add a domain**). This stops others from claiming it.
3. Add a file `CNAME` at the repository root containing only `datadonationnetwork.org`.
4. In `_quarto.yml`, uncomment `resources: - CNAME` and `site-url`, then push.
5. In **Settings → Pages**, check that the custom domain is set, and enable **Enforce HTTPS** once the certificate has been issued.

Don't add the `CNAME` file before DNS works: GitHub would redirect the preview address to a domain that doesn't resolve yet.
