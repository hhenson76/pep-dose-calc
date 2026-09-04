# Reconstitution and dose calculator

A U-100 syringe unit calculator. Pick a peptide, a vial strength, a volume of
bacteriostatic water and a dose level, and it returns the mark to draw to.

Static site. No build step, no dependencies, no server code, no analytics.
`index.html` is entirely self-contained and also works opened directly from
a folder or USB stick, without the rest of these files.

## Files

| File | Purpose |
|---|---|
| `index.html` | The whole application |
| `manifest.webmanifest` | Lets it install to a phone home screen |
| `sw.js` | Service worker, makes it work offline after the first load |
| `icon-*.png`, `apple-touch-icon.png`, `favicon-32.png` | App icons |
| `robots.txt` | Asks search engines not to index the site |

Saved vials and logged doses live in the browser's local storage on each device.
Nothing is uploaded and there is no account. The app's backup panel exports that
data as text so it can be moved or kept. Local storage is unavailable when the
page is opened straight off the file system in some browsers, which is another
reason to serve it from a URL.

## Deploying to GitHub Pages

```
git init
git add .
git commit -m "Reconstitution calculator"
git branch -M main
git remote add origin https://github.com/USERNAME/REPO.git
git push -u origin main
```

Then Settings, then Pages, then set Source to `main` and folder to `/ (root)`.
The site appears at `https://USERNAME.github.io/REPO/` after a minute or two.

On a free GitHub account, Pages only publishes from a **public** repository, so
the code and the site are both visible to anyone. Pages from a private
repository needs GitHub Pro or above, and even then the published site is still
public unless the account is Enterprise Cloud.

`robots.txt` and the `noindex` tag in `index.html` keep it out of search results,
but they do not make it private. Anyone with the URL can open it.

## Keeping people out

If the link should not be open to the world, host the same files somewhere with
access control in front:

- **Cloudflare Pages** connects to a private repository on the free tier, and
  Cloudflare Access can require an emailed one-time code before the page loads.
- **Netlify** also deploys from private repositories on the free tier, though
  password protection is a paid feature.

## Updating

Edit `index.html`, bump the `CACHE` constant in `sw.js` to a new value, then
commit and push. Installed copies pick up the new build the next time they are
opened with a connection. Without the bump, an installed copy can keep serving
the old cached version.

## What the numbers are

Dose tiers come from one private reference sheet dated August 2026. Some are
FDA-label or published-trial amounts and some are one individual's own recorded
values; the badge under the peptide name says which. They are not
recommendations. The reconstitution volumes are concentration math, not
manufacturer instructions.
