# ggplot2 2.2.1 Dash docset

I wanted a Dash docset for the latest ggplot2. [M. Peteuil](https://github.com/Kapeli/Dash-User-Contributions/tree/master/docsets/ggplot2) got me inspired, but it had not been updated for about 2 years, so I created my own.

As M. Peteuil, I use `dashing`. The result is not perfect, but it fits my needs reasonably well.

The process could be automated, but I don't have time for this.


## Pre-requisites
Imagemagick should be installed on your system (on the Mac: `brew install imagemagick`).

Several R packages are required. Those ones are available on CRAN:

- `ggplot2`
- `hexbin`
- `Hmisc`
- `quantreg`
- `multcomp`
- `mapdata`
- `mapproj`
- `maps`
- `testthat`

so it's just a matter of

    Rscript -e "install.packages(c('ggplot2', 'hexbin', 'Hmisc', 'quantreg', 'multcomp', 'mapdata', 'mapproj', 'maps', 'testthat'))"

Those packages should be installed using [devtools](https://github.com/hadley/devtools):

- `tidyverse/tidytemplate` (should not be used for other docs than those of tidyverse)
- `hadley/pkgdown`

so you install them with

    Rscript -e "devtools::install_github('tidyverse/tidytemplate')"
    Rscript -e "devtools::install_github('hadley/pkgdown')"

Finally, install [dashing](https://github.com/technosophos/dashing) Dash documentation generator tool

    go get -u github.com/technosophos/dashing


## Building the ggplot package doc

First clone ggplot's repo

    git clone https://github.com/tidyverse/ggplot2
    cd ggplot2

in the file `_pkgdown.yml`, remove the line containing `+.gg` because for some reason it makes pkgdown unhappy.

Then build ggplot2's doc site

    Rscript -e "pkgdown::build_site()"  # will create a 'docs' folder


## Building the Dash docset using `dashing`

Finally, copy the two icons PNG files and the `dashing.json` from this repo to the `docs` folder and run

    dashing build ggplot2

This parses the docs and produces a `ggplot2.docset` folder in the `docs` folder.

You can put this docset wherever you see fit and import it into Dash.
