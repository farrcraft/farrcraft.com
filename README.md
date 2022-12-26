# farrcraft.com

This is the source for the farrcraft.com website.  It is built using the static site generator [Hugo](https://gohugo.io/).
The theme is based on [Profile](https://github.com/gurusabarish/hugo-profile.git) with mostly minor tweaks.
The photo galleries use the [Bootstrap 5 Lightbox](https://github.com/trvswgnr/bs5-lightbox) import
and the [Gallery Deluxe](https://github.com/bep/gallerydeluxe) layout.


All other content (c) Joshua Farr.

## Deployment

The site has outgrown the size limits of GitHub Pages.
This version publishes the files to an S3 bucket instead.

### Github Pages

The previous site deployment was hosted on GitHub Pages. There is a CD pipeline using GitHub Actions that automatically updates
the `gh-pages` branch with the generated static site whenever changes to the main branch are pushed.
