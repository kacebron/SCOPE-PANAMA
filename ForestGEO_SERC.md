Locating tree species at SERC
================
Kelvin Acebron
2022-07-06

#### Uploading data

``` r
library(tidyverse)
```

    ## ── Attaching packages ─────────────────────────────────────── tidyverse 1.3.1 ──

    ## ✔ ggplot2 3.3.6     ✔ purrr   0.3.4
    ## ✔ tibble  3.1.7     ✔ dplyr   1.0.9
    ## ✔ tidyr   1.2.0     ✔ stringr 1.4.0
    ## ✔ readr   2.1.2     ✔ forcats 0.5.1

    ## ── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
    ## ✖ dplyr::filter() masks stats::filter()
    ## ✖ dplyr::lag()    masks stats::lag()

``` r
ForestGEO_SERC <- read.csv("/Users/kelvinacebron/Documents/SERC NASA ROSES grant /03 Data/FORESTGEO SERC/SERC_censuses_with_UTMs_5_apr_2022.csv")
ForestGEO_SERC$DBH_1 <- parse_number(ForestGEO_SERC$DBH_1)
```

    ## Warning: 1 parsing failure.
    ##  row col expected actual
    ## 5751  -- a number   NULL

``` r
ForestGEO_SERC$DBH_2 <- parse_number(ForestGEO_SERC$DBH_2)
```

    ## Warning: 5694 parsing failures.
    ## row col expected actual
    ##  36  -- a number   NULL
    ##  41  -- a number   NULL
    ##  68  -- a number   NULL
    ##  71  -- a number   NULL
    ##  88  -- a number   NULL
    ## ... ... ........ ......
    ## See problems(...) for more details.

``` r
ForestGEO_SERC$DBH_3 <- parse_number(ForestGEO_SERC$DBH_3)
```

    ## Warning: 15486 parsing failures.
    ## row col expected actual
    ##   1  -- a number   NULL
    ##   4  -- a number   NULL
    ##   7  -- a number   NULL
    ##  12  -- a number   NULL
    ##  15  -- a number   NULL
    ## ... ... ........ ......
    ## See problems(...) for more details.

``` r
print(str(ForestGEO_SERC))
```

    ## 'data.frame':    55572 obs. of  32 variables:
    ##  $ X.1        : int  1 2 3 4 5 6 7 8 9 10 ...
    ##  $ QuadratName: int  10101 10101 10101 10101 10101 10101 10101 10101 10101 10101 ...
    ##  $ Tag        : int  102401 102401 102401 102402 102403 102403 102404 102405 102405 102405 ...
    ##  $ StemTag    : int  102401 104569 104570 102402 102403 103208 102404 102405 102406 102407 ...
    ##  $ H          : int  10 10 10 10 10 10 10 10 10 10 ...
    ##  $ X          : int  10 10 10 10 10 10 10 10 10 10 ...
    ##  $ Y          : int  1 1 1 1 1 1 1 1 1 1 ...
    ##  $ Mnemonic   : chr  "LIBE3" "LIBE3" "LIBE3" "LIBE3" ...
    ##  $ QX         : num  0.5 0.5 0.5 0.1 1.4 1.4 2.7 4 4 4 ...
    ##  $ QY         : num  8.4 8.4 8.4 8.2 8.8 8.8 9.4 8.5 8.5 8.5 ...
    ##  $ DBH_1      : num  1.6 NA NA 1.1 1.4 NA 1.3 45.9 3.1 2.8 ...
    ##   ..- attr(*, "problems")= tibble [1 × 4] (S3: tbl_df/tbl/data.frame)
    ##   .. ..$ row     : int 5751
    ##   .. ..$ col     : int NA
    ##   .. ..$ expected: chr "a number"
    ##   .. ..$ actual  : chr "NULL"
    ##  $ DBH_2      : num  1.6 NA NA 1 1.4 1.4 1.6 47.5 3.2 2.1 ...
    ##   ..- attr(*, "problems")= tibble [5,694 × 4] (S3: tbl_df/tbl/data.frame)
    ##   .. ..$ row     : int [1:5694] 36 41 68 71 88 89 115 117 135 136 ...
    ##   .. ..$ col     : int [1:5694] NA NA NA NA NA NA NA NA NA NA ...
    ##   .. ..$ expected: chr [1:5694] "a number" "a number" "a number" "a number" ...
    ##   .. ..$ actual  : chr [1:5694] "NULL" "NULL" "NULL" "NULL" ...
    ##  $ DBH_3      : num  NA 1.1 1.1 NA 1.3 2.5 NA 51.7 3.5 2 ...
    ##   ..- attr(*, "problems")= tibble [15,486 × 4] (S3: tbl_df/tbl/data.frame)
    ##   .. ..$ row     : int [1:15486] 1 4 7 12 15 17 19 22 24 26 ...
    ##   .. ..$ col     : int [1:15486] NA NA NA NA NA NA NA NA NA NA ...
    ##   .. ..$ expected: chr [1:15486] "a number" "a number" "a number" "a number" ...
    ##   .. ..$ actual  : chr [1:15486] "NULL" "NULL" "NULL" "NULL" ...
    ##  $ Status_1   : chr  "LI" NA NA "LI" ...
    ##  $ Status_2   : chr  "LI" NA NA "DS" ...
    ##  $ Status_3   : chr  "DC" "LI" "LI" "DC" ...
    ##  $ ExactDate_1: chr  "4/14/2010" NA NA "4/14/2010" ...
    ##  $ ExactDate_2: chr  "5/14/2014" NA NA "5/14/2014" ...
    ##  $ ExactDate_3: chr  "9/27/2019" "9/27/2019" "9/27/2019" "9/27/2019" ...
    ##  $ ListOfTSM_1: chr  "LI" NA NA "LI" ...
    ##  $ ListOfTSM_2: chr  "LI" NA NA "DS" ...
    ##  $ ListOfTSM_3: chr  "DC;TC" "LI;M" "LI;SEC" "DC;TC" ...
    ##  $ FGStatus_1 : chr  "alive" NA NA "alive" ...
    ##  $ FGStatus_2 : chr  "alive" NA NA "stem dead" ...
    ##  $ FGStatus_3 : chr  "stem dead" "alive" "alive" "stem dead" ...
    ##  $ Family     : chr  "Lauraceae" "Lauraceae" "Lauraceae" "Lauraceae" ...
    ##  $ Genus      : chr  "Lindera" "Lindera" "Lindera" "Lindera" ...
    ##  $ SpeciesName: chr  "benzoin" "benzoin" "benzoin" "benzoin" ...
    ##  $ PX         : num  290 290 290 290 291 ...
    ##  $ PY         : num  108 108 108 108 109 ...
    ##  $ UTMX_TREES : num  438312 438312 438312 438311 438313 ...
    ##  $ UTMY_TREES : num  135703 135703 135703 135703 135703 ...
    ## NULL

#### List all Families

``` r
levels(factor(ForestGEO_SERC$Family))
```

    ##  [1] "Adoxaceae"            "Altingiaceae"         "Anacardiaceae"       
    ##  [4] "Annonaceae"           "Aquifoliaceae"        "Araliaceae"          
    ##  [7] "Betulaceae"           "Bignoniaceae"         "Cannabaceae"         
    ## [10] "Caprifoliaceae"       "Celastraceae"         "Cornaceae"           
    ## [13] "Cupressaceae"         "Ebenaceae"            "Elaeagnaceae"        
    ## [16] "Ericaceae"            "Fabaceae"             "Fabaceae-mimosoideae"
    ## [19] "Fagaceae"             "Juglandaceae"         "Lauraceae"           
    ## [22] "Magnoliaceae"         "Moraceae"             "Nyssaceae"           
    ## [25] "Oleaceae"             "Paulowniaceae"        "Pinaceae"            
    ## [28] "Platanaceae"          "Rosaceae"             "Rubiaceae"           
    ## [31] "Salicaceae"           "Sapindaceae"          "Simaroubaceae"       
    ## [34] "Smilacaceae"          "Ulmaceae"             "Unknown"             
    ## [37] "Vitaceae"

There are 37 different treee families

#### List all Genus

``` r
levels(factor(ForestGEO_SERC$Genus))
```

    ##  [1] "Acer"           "Ailanthus"      "Albizia"        "Amelanchier"   
    ##  [5] "Aralia"         "Asimina"        "Broussonetia"   "Campsis"       
    ##  [9] "Carpinus"       "Carya"          "Celastrus"      "Celtis"        
    ## [13] "Cephalanthus"   "Cercis"         "Cornus"         "Diospyros"     
    ## [17] "Elaeagnus"      "Euonymus"       "Fagus"          "Fraxinus"      
    ## [21] "Hedera"         "Ilex"           "Juglans"        "Juniperus"     
    ## [25] "Kalmia"         "Ligustrum"      "Lindera"        "Liquidambar"   
    ## [29] "Liriodendron"   "Lonicera"       "Morus"          "Nyssa"         
    ## [33] "Parthenocissus" "Paulownia"      "Pinus"          "Platanus"      
    ## [37] "Populus"        "Prunus"         "Pyrus"          "Quercus"       
    ## [41] "Rhododendron"   "Rosa"           "Rubus"          "Salix"         
    ## [45] "Sambucus"       "Sassafras"      "Smilax"         "Toxicodendron" 
    ## [49] "Ulmus"          "Unidentified"   "Vaccinium"      "Viburnum"      
    ## [53] "Vitis"

Theres a total of 53 different Genus

#### List all Species present in the data

``` r
levels(factor(interaction(ForestGEO_SERC$Genus,ForestGEO_SERC$SpeciesName)))
```

    ##  [1] "Viburnum.acerifolium"        "Quercus.alba"               
    ##  [3] "Sassafras.albidum"           "Ailanthus.altissima"        
    ##  [5] "Fraxinus.americana"          "Ulmus.americana"            
    ##  [7] "Euonymus.americanus"         "Cornus.amomum"              
    ##  [9] "Elaeagnus.angustifolia"      "Amelanchier.arborea"        
    ## [11] "Rhododendron.arborescens"    "Prunus.avium"               
    ## [13] "Lindera.benzoin"             "Pyrus.calleryana"           
    ## [15] "Amelanchier.canadensis"      "Cercis.canadensis"          
    ## [17] "Carpinus.caroliniana"        "Quercus.coccinea"           
    ## [19] "Carya.cordiformis"           "Vaccinium.corymbosum"       
    ## [21] "Viburnum.dentatum"           "Quercus.falcata"            
    ## [23] "Cornus.florida"              "Carya.glabra"               
    ## [25] "Populus.grandidentata"       "Fagus.grandifolia"          
    ## [27] "Hedera.helix"                "Lonicera.japonica"          
    ## [29] "Albizia.julibrissin"         "Kalmia.latifolia"           
    ## [31] "Lonicera.maackii"            "Quercus.michauxii"          
    ## [33] "Quercus.montana"             "Rosa.multiflora"            
    ## [35] "Acer.negundo"                "Juglans.nigra"              
    ## [37] "Salix.nigra"                 "Sambucus.nigra"             
    ## [39] "Celtis.occidentalis"         "Cephalanthus.occidentalis"  
    ## [41] "Platanus.occidentalis"       "Ilex.opaca"                 
    ## [43] "Celastrus.orbiculatus"       "Quercus.palustris"          
    ## [45] "Rosa.palustris"              "Broussonetia.papyrifera"    
    ## [47] "Fraxinus.pennsylvanica"      "Viburnum.prunifolium"       
    ## [49] "Parthenocissus.quinquefolia" "Campsis.radicans"           
    ## [51] "Toxicodendron.radicans"      "Smilax.rotundifolia"        
    ## [53] "Morus.rubra"                 "Quercus.rubra"              
    ## [55] "Ulmus.rubra"                 "Acer.rubrum"                
    ## [57] "Prunus.serotina"             "Carya.sp."                  
    ## [59] "Ligustrum.sp."               "Quercus.sp."                
    ## [61] "Rubus.sp."                   "Vaccinium.sp."              
    ## [63] "Vitis.sp."                   "Aralia.spinosa"             
    ## [65] "Quercus.stellata"            "Liquidambar.styraciflua"    
    ## [67] "Nyssa.sylvatica"             "Pinus.taeda"                
    ## [69] "Carya.tomentosa"             "Paulownia.tomentosa"        
    ## [71] "Asimina.triloba"             "Liriodendron.tulipifera"    
    ## [73] "Elaeagnus.umbellata"         "Unidentified.Unknown"       
    ## [75] "Unidentified.unknown 3"      "Quercus.velutina"           
    ## [77] "Ilex.verticillata"           "Diospyros.virginiana"       
    ## [79] "Juniperus.virginiana"        "Pinus.virginiana"

Theres a total of 80 different tree species, with two unidentified Genus
and unknown species

#### Now lets analyse the data

``` r
dff <- ForestGEO_SERC
sp.n <- length(unique(dff$Mnemonic))
#dff <- subset(dff, as.numeric(DBH_1) >= 80)
dbh <- as.numeric(dff$DBH_1)
plot(dff$PX, dff$PY, col = heat.colors(sp.n)[factor(dff$Mnemonic)], cex = dbh/100, pch = 19)
```

![](ForestGEO_SERC_files/figure-gfm/unnamed-chunk-5-1.png)<!-- -->

``` r
library(dplyr)
library(ggplot2)
ForestGEO_SERC %>%
  filter(DBH_1 >= 30) %>%
  ggplot(aes(x=PX, y=PY, group = Family)) + 
  geom_point(aes(color=interaction(Genus, SpeciesName), size=(DBH_1)^3)) +
  theme_bw() +
  theme(legend.position='none') +
  scale_x_continuous(breaks = seq(0, 400, by = 30)) +
  scale_y_continuous(breaks = seq(0,400, by = 30)) +
  theme(panel.grid.major.y = element_line(color = "black",
                                          size = 1,
                                          linetype = 1)) +
  theme(panel.grid.major.x = element_line(color = "black",
                                          size = 1,
                                          linetype = 1))
```

![](ForestGEO_SERC_files/figure-gfm/unnamed-chunk-6-1.png)<!-- -->

``` r
sp.table <- sort(table(dff$Mnemonic), decreasing = TRUE)
barplot((sp.table))
```

![](ForestGEO_SERC_files/figure-gfm/unnamed-chunk-7-1.png)<!-- -->

``` r
dff.large <- subset(dff, DBH_1 >= 25)
sp.table <- sort(table(dff.large$Mnemonic), decreasing = TRUE)
barplot((sp.table))
```

![](ForestGEO_SERC_files/figure-gfm/unnamed-chunk-8-1.png)<!-- -->

Note that the `echo = FALSE` parameter was added to the code chunk to
prevent printing of the R code that generated the plot.
