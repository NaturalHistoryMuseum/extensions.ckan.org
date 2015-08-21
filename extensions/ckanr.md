---
layout: extension
name: ckanr
title: R client for CKAN RESTful API
author: rOpenSci
homepage: https://github.com/ropensci/ckanr
github_user: ropensci
github_repo: ckanr
category: Extension
featured: 
permalink: /extension/ckanr/
---


ckanr
=====



[![Build Status](https://api.travis-ci.org/ropensci/ckanr.png)](https://travis-ci.org/ropensci/ckanr)
[![Build status](https://ci.appveyor.com/api/projects/status/5yqd882v4fbeggd5?svg=true)](https://ci.appveyor.com/project/sckott/ckanr)
[![codecov.io](https://codecov.io/github/ropensci/ckanr/coverage.svg?branch=master)](https://codecov.io/github/ropensci/ckanr?branch=master)

`ckanr` is an R client for the generic CKAN API - that is, plug in a base url for the CKAN instance of interest. 

## Installation


```r
install.packages("devtools")
devtools::install_github("ropensci/ckanr")
```


```r
library('ckanr')
```

Note: the default base CKAN URL is set to 
[http://data.techno-science.ca/](http://data.techno-science.ca/). 
Functions requiring write permissions in CKAN additionally require a privileged
CKAN API key. 
You can change this using `ckanr_setup()`, or change the URL using the `url` 
parameter in each function call.
To set one or both, run:
```r
ckanr_setup() # restores default CKAN url to http://data.techno-science.ca/
ckanr_setup(url="http://data.techno-science.ca/")
ckanr_setup(url="http://data.techno-science.ca/", key="my-ckan-api-key")
```


## Changes


```r
changes(limit = 2, as = "table")[, 1:4]
#>                                user_id                  timestamp
#> 1 27778230-2e90-4818-9f00-bbf778c8fa09 2015-03-30T15:06:55.500589
#> 2 27778230-2e90-4818-9f00-bbf778c8fa09 2015-01-09T23:33:14.303237
#>                              object_id
#> 1 f4406699-3e11-4856-be48-b55da98b3c14
#> 2 0a801729-aa94-4d76-a5e0-7b487303f4e5
#>                            revision_id
#> 1 12381b05-9e46-4d26-a356-7baed60e8471
#> 2 100c4915-f995-4925-956e-bcacfdd8de89
```

## List datasets


```r
package_list(as = "table")
#>  [1] "artifact-data-agriculture"                                  
#>  [2] "artifact-data-aviation"                                     
#>  [3] "artifact-data-bookbinding"                                  
#>  [4] "artifact-data-chemistry"                                    
#>  [5] "artifact-data-communications"                               
#>  [6] "artifact-data-computing-technology"                         
#>  [7] "artifact-data-domestic-technology"                          
#>  [8] "artifact-data-energy-electric"                              
#>  [9] "artifact-data-exploration-and-survey"                       
#> [10] "artifact-data-fisheries"                                    
...
```

## List tags


```r
tag_list('aviation', as = 'table')
#>   vocabulary_id                     display_name
#> 1            NA                         Aviation
#> 2            NA Canada Aviation and Space Museum
#>                                     id                             name
#> 1 cc1db2db-b08b-4888-897f-a17eade2461b                         Aviation
#> 2 8d05a650-bc7b-4b89-bcc8-c10177e60119 Canada Aviation and Space Museum
```

## Show tags

Subset for readme brevity


```r
tag_show('Aviation')$packages[[1]][1:3]	
#> $owner_org
#> [1] "fafa260d-e2bf-46cd-9c35-34c1dfa46c57"
#> 
#> $maintainer
#> [1] ""
#> 
#> $relationships_as_object
#> list()
```

## List groups


```r
group_list(as = 'table')[, 1:3]
#>                         display_name description
#> 1                     Communications            
#> 2 Domestic and Industrial Technology            
#> 3                         Everything            
#> 4                           Location            
#> 5                          Resources            
#> 6         Scientific Instrumentation            
#> 7                     Transportation            
#>                                title
#> 1                     Communications
#> 2 Domestic and Industrial Technology
#> 3                         Everything
#> 4                           Location
#> 5                          Resources
#> 6         Scientific Instrumentation
#> 7                     Transportation
```

## Show groups

Subset for readme brevity


```r
group_show('communications', as = 'table')$users
#>   openid about capacity     name                    created
#> 1     NA  <NA>    admin     marc 2014-10-24T14:44:29.885262
#> 2     NA          admin sepandar 2014-10-23T19:40:42.056418
#>                         email_hash sysadmin
#> 1 a32002c960476614370a16e9fb81f436    FALSE
#> 2 10b930a228afd1da2647d62e70b71bf8     TRUE
#>   activity_streams_email_notifications  state number_of_edits
#> 1                                FALSE active             379
#> 2                                FALSE active              44
#>   number_administered_packages display_name fullname
#> 1                           39         marc     <NA>
#> 2                            1     sepandar         
#>                                     id
#> 1 27778230-2e90-4818-9f00-bbf778c8fa09
#> 2 b50449ea-1dcc-4d52-b620-fc95bf56034b
```

## Show a package


```r
package_show('34d60b13-1fd5-430e-b0ec-c8bc7f4841cf', as = 'table')$resources[, 1:10]
#>                      resource_group_id cache_last_updated
#> 1 ea8533d9-cdc6-4e0e-97b9-894e06d50b92                 NA
#> 2 ea8533d9-cdc6-4e0e-97b9-894e06d50b92                 NA
#> 3 ea8533d9-cdc6-4e0e-97b9-894e06d50b92                 NA
#> 4 ea8533d9-cdc6-4e0e-97b9-894e06d50b92                 NA
#>           revision_timestamp webstore_last_updated
#> 1 2014-10-28T18:13:22.213530                    NA
#> 2 2014-11-04T02:59:50.567068                    NA
#> 3 2014-11-05T21:23:58.533397                    NA
#> 4 2014-11-05T21:25:16.848423                    NA
#>                                     id size  state hash
#> 1 be2b0af8-24a8-4a55-8b30-89f5459b713a   NA active     
#> 2 7d65910e-4bdc-4f06-a213-e24e36762767   NA active     
#> 3 97622ad7-1507-4f6a-8acb-14e826447389   NA active     
#> 4 7a72498a-c49c-4e84-8b10-58991de10df6   NA active     
#>                                    description format
#> 1                                  XML Dataset    XML
#> 2 Data dictionary for CSTMC artifact datasets.    XLS
#> 3       Tips for using the artifacts datasets.   .php
#> 4       Tips for using the artifacts datasets.   .php
```

## Search for packages


```r
out <- package_search(q = '*:*', rows = 2, as = "table")$results
out[, !names(out) %in% 'resources'][, 1:10]
#>                      license_title maintainer relationships_as_object
#> 1 Open Government Licence - Canada                               NULL
#> 2 Open Government Licence - Canada                               NULL
#>   private maintainer_email         revision_timestamp
#> 1   FALSE                  2014-10-28T21:18:27.068320
#> 2   FALSE                  2014-10-28T21:18:58.958555
#>                                     id           metadata_created
#> 1 f4406699-3e11-4856-be48-b55da98b3c14 2014-10-28T16:50:30.068996
#> 2 0a801729-aa94-4d76-a5e0-7b487303f4e5 2014-10-24T19:16:59.160533
#>            metadata_modified author
#> 1 2015-03-30T15:06:55.218176       
#> 2 2015-01-09T23:33:13.972898
```

## Search for resources


```r
resource_search(q = 'name:data', limit = 2, as = 'table')
#> $count
#> [1] 71
#> 
#> $results
#>                      resource_group_id cache_last_updated
#> 1 01a82e52-01bf-4a9c-9b45-c4f9b92529fa                 NA
#> 2 01a82e52-01bf-4a9c-9b45-c4f9b92529fa                 NA
#>   webstore_last_updated                                   id size  state
#> 1                    NA e179e910-27fb-44f4-a627-99822af49ffa   NA active
#> 2                    NA ba84e8b7-b388-4d2a-873a-7b107eb7f135   NA active
#>   last_modified hash                                  description format
#> 1            NA                                       XML Dataset    XML
#> 2            NA      Data dictionary for CSTMC artifact datasets.    XLS
#>   mimetype_inner url_type mimetype cache_url
#> 1             NA       NA       NA        NA
#> 2             NA       NA       NA        NA
#>                                           name                    created
#> 1 Artifact Data - Exploration and Survey (XML) 2014-10-28T15:50:35.374303
#> 2                              Data Dictionary 2014-11-03T18:01:02.094210
#>                                                                                                                                                    url
#> 1              http://source.techno-science.ca/datasets-donn%C3%A9es/artifacts-artefacts/groups-groupes/exploration-and-survey-exploration-et-leve.xml
#> 2 http://source.techno-science.ca/datasets-donn%C3%A9es/artifacts-artefacts/cstmc-artifact-data-dictionary-dictionnaire-de-donnees-artefacts-smstc.xls
#>   webstore_url position                          revision_id resource_type
#> 1           NA        0 a22e6741-3e89-4db0-a802-ba594b1c1fad            NA
#> 2           NA        1 da1f8585-521d-47ef-8ead-7832474a3421            NA
```

## Examples of different CKAN APIs

### The Natural History Museum

Website: [http://data.nhm.ac.uk/](http://data.nhm.ac.uk/)

List datasets


```r
nhmbase <- "http://data.nhm.ac.uk"
package_list(as = "table", url = nhmbase)
#>  [1] "bibliography-scleractinia"                                           
#>  [2] "bioacoustica"                                                        
#>  [3] "bothriocephalidea-phylogeny"                                         
#>  [4] "checklist-of-the-lepidoptera-of-the-british-isles-data"              
#>  [5] "chrysoperla-carnea-lectotype"                                        
#>  [6] "collection-artefacts"                                                
#>  [7] "collection-indexlots"                                                
#>  [8] "collection-specimens"                                                
#>  [9] "crowdsourcing-the-collection"                                        
#> [10] "images-for-the-evaluation-of-automatic-image-segmentation-algorithms"
...
```

Tags

_list_


```r
head(tag_list(as = "table", url = nhmbase))
#>   vocabulary_id    display_name                                   id
#> 1            NA alpha diversity 05935722-6507-4f07-ac82-83d48555d251
#> 2            NA    archival DNA b93861ac-0e31-42bd-87aa-7a7bd2af8043
#> 3            NA      arthropods f9245868-f4cb-4c85-a59d-11692db19e86
#> 4            NA       Barcoding ea0cda10-2d9e-4a80-b8b5-15d24e693ace
#> 5            NA    Bibliography 73c85f3f-49b4-416a-80fe-4eb77e99a58d
#> 6            NA    bioacoustics 11faa593-7ccb-4a6f-8a97-c88ca8939624
#>              name
#> 1 alpha diversity
#> 2    archival DNA
#> 3      arthropods
#> 4       Barcoding
#> 5    Bibliography
#> 6    bioacoustics
```

_show_


```r
tag_show('arthropods', as = 'table', url = nhmbase)
#> $vocabulary_id
#> NULL
#> 
#> $packages
#> list()
#> 
#> $display_name
#> [1] "arthropods"
#> 
#> $id
#> [1] "f9245868-f4cb-4c85-a59d-11692db19e86"
#> 
#> $name
#> [1] "arthropods"
```

Packages

_search_


```r
out <- package_search(q = '*:*', rows = 2, as = 'table', url = nhmbase)
out$results[, 1:10]
#>             license_title maintainer relationships_as_object private
#> 1 Creative Commons CCZero         NA                    NULL   FALSE
#> 2   License not specified         NA                    NULL   FALSE
#>   maintainer_email num_tags update_frequency
#> 1               NA        1           weekly
#> 2               NA        1                 
#>                                     id           metadata_created
#> 1 56e711e6-c847-4f99-915a-6894bb5c5dea 2014-12-08T16:39:22.346941
#> 2 b99a29cc-5d74-4c62-ad82-51473d403cbe 2015-04-23T08:33:47.736376
#>            metadata_modified
#> 1 2015-03-03T12:40:11.196427
#> 2 2015-04-23T08:38:48.328908
```

_show_


```r
package_show(id = "56e711e6-c847-4f99-915a-6894bb5c5dea", as = "table", url = nhmbase)
#> $domain
#> [1] "data.nhm.ac.uk"
#> 
#> $owner_org
#> [1] "7854c918-d7eb-4341-96e9-3adfb8d636a0"
#> 
#> $maintainer
#> NULL
#> 
#> $relationships_as_object
...
```

## Meta

* Please [report any issues or bugs](https://github.com/ropensci/ckanr/issues).
* License: MIT
* Get citation information for `ckanr` in R doing `citation(package = 'ckanr')`

[![ropensci](http://ropensci.org/public_images/github_footer.png)](http://ropensci.org)

