# farrcraft.com

This is the source for the farrcraft.com website.  It is built using the static site generator [Hugo](https://gohugo.io/).
The theme is based on [Profile](https://github.com/gurusabarish/hugo-profile.git) with mostly minor tweaks.
The photo gallery uses the [Bootstrap 5 Lightbox](https://github.com/trvswgnr/bs5-lightbox) import.


All other content (c) Joshua Farr.

## Deployment

The current site deployment is hosted on GitHub Pages. There is a CD pipeline using GitHub Actions that automatically updates
the `gh-pages` branch with the generated static site whenever changes to the main branch are pushed.
