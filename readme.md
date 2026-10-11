# Notes to Myself on Software Development

Source for my blog at https://mfahim.github.io/. Newer writing lives in my newsletter, [Forever Draft](https://foreverdraft.substack.com).

Built with [Hugo](https://gohugo.io/) (extended, 0.167.0 or later) and the [PaperMod](https://github.com/adityatelange/hugo-PaperMod) theme, with a small style override for the Forever Draft look.

## Running locally

```sh
brew install hugo                      # extended build
git clone --recurse-submodules https://github.com/mfahim/mfahim.github.io.git
cd mfahim.github.io
hugo server                            # http://localhost:1313/
```

If you cloned without `--recurse-submodules`, run `git submodule update --init` to fetch the theme.

## Where things live

| Path | What |
|---|---|
| `content/posts/` | Posts. Slugs are set in front matter; don't change them, they are live URLs. |
| `content/about.md` | About page |
| `hugo.toml` | Site config, menu, theme params |
| `assets/css/extended/forever-draft.css` | Palette, fonts and layout overrides on top of PaperMod |
| `layouts/_partials/extend_head.html` | Google Fonts and dark-mode listener |
| `static/` | Favicons (FD mark) |
| `themes/PaperMod` | Theme, as a git submodule pinned to a commit |

To update the theme: `git submodule update --remote themes/PaperMod`, check with `hugo server`, then commit the new submodule pointer.

## Deploying

Pushing to `master` runs `.github/workflows/hugo.yml`, which builds the site and deploys it with GitHub Pages. Nothing built is committed; `public/` is ignored. To bump Hugo, change `HUGO_VERSION` in the workflow and `module.hugoVersion.min` in `hugo.toml` together.

### One-off migration (from the old two-repo setup)

The site used to be built locally and pushed to a separate `mfahim.github.io` repo. To move to this single repo:

1. On GitHub, rename the old `mfahim/mfahim.github.io` repo to `mfahim.github.io-archive`, then in its **Settings → Pages** unpublish the site. Expect a few minutes of downtime between here and step 4.
2. Rename this repo from `Blog` to `mfahim.github.io` (**Settings → General → Repository name**). GitHub redirects the old URL, but update your local remote anyway:
   `git remote set-url origin https://github.com/mfahim/mfahim.github.io.git`
3. In **Settings → Pages**, set **Source** to **GitHub Actions**.
4. `git push origin master`. Watch the run under **Actions**; the site is back when the `deploy` job goes green.
