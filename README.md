
<!-- README.md is generated from README.Rmd. Please edit that file -->
rppo
====

[![Build Status](https://travis-ci.org/biocodellc/rppo.svg?branch=master)](https://travis-ci.org/biocodellc/rppo)

The global plant phenology data portal (PPO data portal) is an aggregation of plant phenological observations from [USA-NPN](https://www.usanpn.org/usa-national-phenology-network), [NEON](https://www.neonscience.org/), and [PEP725](http://www.pep725.eu/) representing 20 million phenological observations from across North America and Europe. The PPO data portal utilizes the [Plant Phenology Ontology](https://github.com/PlantPhenoOntology/ppo/) to align phenological terms and measurements from the various databases. The rppo R package enables programmatic access to all data contained in the PPO data portal.

For more information visit the [PPO global data portal](http://plantphenology.org/) or the [ppo-data-pipeline git repository](https://github.com/biocodellc/ppo-data-pipeline).

Installation
------------

The production version of rppo can be installed with (when available on CRAN):

``` r
#install.packages("rppo")
#library(rppo)
```

You can install the development version of rppo from github with:

``` r
# install.packages("devtools")
devtools::install_github("biocodellc/rppo")
```

Example
-------

Query the plant phenology ontology and return a list of present or absent terms. Use the termIDs returned from this function to query terms in the ppo\_data function

``` r
library(rppo)
present_terms <- ppo_terms(present=T)
#> [1] "uncaught status code  404"
#> Warning in ppo_terms(present = T): Not Found (HTTP 404).
```

A simple query example. The results of the ppo\_data function are returned as a list. Hence, to retrieve the data portion of the returned results you will need to access the "data" element of the returned list.

``` r
results <- ppo_data(genus = "Quercus", fromYear = 2013, toYear = 2013, fromDay = 100, toDay = 110,termID='obo:PPO_0002313', limit=10)
#> [1] "sending request to http://api.plantphenology.org/v1/download/?q=%2Bgenus:Quercus+AND+%2BplantStructurePresenceTypes:\"obo:PPO_0002313\"+AND+%2Byear:>=2013+AND+%2Byear:<=2013+AND+%2BdayOfYear:>=100+AND+%2BdayOfYear:<=110+AND+source:USA-NPN,NEON&source=latitude,longitude,year,dayOfYear,plantStructurePresenceTypes&limit=10"
#> [1] "uncaught status code 404"
#> Warning in ppo_data(genus = "Quercus", fromYear = 2013, toYear = 2013,
#> fromDay = 100, : Not Found (HTTP 404).
df <- results$data
readme <- results$readme
citation <- results$citation

# use cat(readme) and cat(citation) to view the text output
```

Citation
--------

To cite the 'rppo' R package in publications use:

       'John Deck, Brian Stucky, Ramona Walls, Kjell Bolmgren, Ellen Denny, Robert Guralnick' (2018). rppo: An interface to the Plant Phenology Ontology and associated data store.  R package version 1.0
       https://github.com/biocodellc/rppo

Code of Conduct
---------------

View our [code of conduct](CONDUCT.md)
