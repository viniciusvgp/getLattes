
<!-- README.md is generated from README.Rmd. Please edit that file -->

# getLattes

<!-- badges: start -->

[![DOI](https://zenodo.org/badge/258844181.svg)](https://zenodo.org/badge/latestdoi/258844181)
<!-- badges: end -->

The `getLattes` `R` package, written by [Roney Fraga
Souza](http://roneyfraga.com) and [Winicius
Sabino](https://stackoverflow.com/users/9278241/winicius-sabino), was
built to extract data from the [Lattes](http://lattes.cnpq.br/)
curriculum platform exported as `XML`.

![](http://roneyfraga.com/volume/getLattes_data/lattes_xml_download.gif)

The `XML` file needs to be extracted from `.zip`.

To automate the download process, please see [Captchas Negated by Python
reQuests - CNPQ](https://github.com/josefson/CNPQ).

## Installation

You can install the released version of getLattes from
[github](https://CRAN.R-project.org) with:

``` r
# install and load devtools from CRAN
install.packages("devtools")
library(devtools)

# install and load getLattes
devtools::install_github("roneyfraga/getLattes")
library(getLattes)
```

## Import XML file as R list

``` r
# the file 4984859173592703.xml is stored in datatest directory
cl <- readLattes(filexml='4984859173592703.xml', path='datatest/')

# import all Lattes XML files in datateste
cls <- readLattes(filexml='*.xml$', path='datatest/')

# import all Lattes XML files in the working directory
cls <- readLattes(filexml='*.xml$')
```

## Loaded data

To load 500 random curricula data imported as an R list.

``` r
data(xmlsLattes)
length(xmlsLattes)
```

## Import general data

``` r
# to combine list of data frames in data frame
library(dplyr)

# to import from one curriculum 
getDadosGerais(xmlsLattes[[499]])

# to import from two or more curricula
lt <- lapply(xmlsLattes, getDadosGerais)
head(bind_rows(lt))
```

## Import Published Academic Papers

``` r
# to import from one curriculum 
getArtigosPublicados(xmlsLattes[[462]]) 

# to import from two or more curricula
lt <- lapply(xmlsLattes, getArtigosPublicados)
head(bind_rows(lt))
```

## Normalize informations

See `normalizeByDoi`, `normalizeByJournal` and `normalizeByYear` to
normalize publications data (journal title, ISSN and year).
