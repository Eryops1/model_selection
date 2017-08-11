# MS2_model






```r
extinct.raw <- read.csv("model_data2.csv")
extinct <- extinct.raw[,c("ma_range", "lat_range", "gcd", "svl", "mean_lat",
                 "min_lat", "abu_cat")]
extant <- read.csv("living_data2.csv")
extant <- extant[,-c(1,2)]
names(extant) <- c("species", "svl", "count", "abu_cat", "lat_range", "gcd", "mean_lat", "min_lat",
                                 "Red.List.status", "order", "family", "genus", "hab.cat.b")
```


# Data description
## Extant

```r
nrow(na.omit(extant))
```

```
## [1] 261
```

```r
summary(extant)
```

```
##                      species          svl              count        
##  Lyciasalamandra luschani:   2   Min.   :  9.699   Min.   :   1.00  
##  Salamandra algira       :   2   1st Qu.: 26.494   1st Qu.:   3.00  
##  Salamandrina terdigitata:   2   Median : 37.504   Median :  13.00  
##  Acanthixalus spinosus   :   1   Mean   : 46.469   Mean   : 110.11  
##  Acris blanchardi        :   1   3rd Qu.: 56.000   3rd Qu.:  42.25  
##  Acris crepitans         :   1   Max.   :927.994   Max.   :5037.00  
##  (Other)                 :1959   NA's   :4         NA's   :1628     
##     abu_cat       lat_range             gcd             mean_lat      
##  Min.   :1.00   Min.   : 0.00201   Min.   :    0.0   Min.   :-44.261  
##  1st Qu.:1.00   1st Qu.: 0.52441   1st Qu.:  111.3   1st Qu.:-12.451  
##  Median :3.00   Median : 3.03725   Median :  446.4   Median :  2.367  
##  Mean   :2.52   Mean   : 6.88834   Mean   : 1098.5   Mean   :  2.770  
##  3rd Qu.:3.00   3rd Qu.: 9.83493   3rd Qu.: 1415.4   3rd Qu.: 14.338  
##  Max.   :4.00   Max.   :86.89850   Max.   :20038.3   Max.   : 59.385  
##  NA's   :565    NA's   :181        NA's   :181       NA's   :181      
##     min_lat         Red.List.status     order               family   
##  Min.   :-47.8074   LC     :817     ANURA  :1664   BUFONIDAE   :192  
##  1st Qu.:-16.4686   EN     :257     CAUDATA:  85   MANTELLIDAE :170  
##  Median : -1.3746   CR     :186     NA's   : 219   HYPEROLIIDAE:160  
##  Mean   : -0.7894   VU     :182                    HYLIDAE     :141  
##  3rd Qu.: 10.9962   DD     :169                    MICROHYLIDAE: 92  
##  Max.   : 45.9292   (Other):138                    (Other)     :994  
##  NA's   :181        NA's   :219                    NA's        :219  
##                genus        hab.cat.b  
##  Hyperolius       :  91   high   : 12  
##  Eleutherodactylus:  75   highlow:880  
##  Phrynobatrachus  :  66   low    :453  
##  Atelopus         :  63   NA's   :623  
##  Boophis          :  57                
##  (Other)          :1397                
##  NA's             : 219
```



```r
extant <- na.omit(extant)
extant <- droplevels(extant)
summary(extant)
```

```
##                   species         svl             count        
##  Acris crepitans      :  1   Min.   : 12.90   Min.   :   1.00  
##  Acris gryllus        :  1   1st Qu.: 30.50   1st Qu.:   4.00  
##  Adenomera andreae    :  1   Median : 43.99   Median :  14.00  
##  Afrixalus dorsalis   :  1   Mean   : 53.25   Mean   :  93.69  
##  Afrixalus lacteus    :  1   3rd Qu.: 65.21   3rd Qu.:  42.00  
##  Agalychnis callidryas:  1   Max.   :286.99   Max.   :5037.00  
##  (Other)              :255                                     
##     abu_cat        lat_range             gcd             mean_lat      
##  Min.   :1.000   Min.   : 0.05339   Min.   :    0.0   Min.   :-35.839  
##  1st Qu.:3.000   1st Qu.: 6.44265   1st Qu.:  995.1   1st Qu.:-12.412  
##  Median :3.000   Median :13.49661   Median : 2183.4   Median :  2.069  
##  Mean   :2.835   Mean   :17.35401   Mean   : 2731.8   Mean   :  2.168  
##  3rd Qu.:3.000   3rd Qu.:24.45622   3rd Qu.: 3597.7   3rd Qu.:  9.819  
##  Max.   :4.000   Max.   :86.89850   Max.   :20038.3   Max.   : 58.814  
##                                                                        
##     min_lat        Red.List.status   order                 family   
##  Min.   :-43.703   CR:  4          ANURA:261   HYLIDAE        : 39  
##  1st Qu.:-21.051   DD:  4                      MANTELLIDAE    : 38  
##  Median : -8.568   EN:  8                      BUFONIDAE      : 25  
##  Mean   : -6.929   EX:  1                      LEPTODACTYLIDAE: 20  
##  3rd Qu.:  4.738   LC:224                      MICROHYLIDAE   : 17  
##  Max.   : 40.415   NT:  9                      HYPEROLIIDAE   : 15  
##                    VU: 11                      (Other)        :107  
##              genus       hab.cat.b  
##  Boophis        : 16   high   :  2  
##  Phrynobatrachus: 14   highlow:146  
##  Mantidactylus  : 13   low    :113  
##  Leptodactylus  : 12                
##  Hyperolius     :  9                
##  Ptychadena     :  9                
##  (Other)        :188
```

```r
hist(extant$svl)
```

![](figures/unnamed-chunk-1-1.jpeg)<!-- -->

```r
barplot(table(extant$abu_cat))
```

![](figures/unnamed-chunk-1-2.jpeg)<!-- -->

```r
hist(extant$lat_range)
```

![](figures/unnamed-chunk-1-3.jpeg)<!-- -->

```r
hist(extant$gcd)
```

![](figures/unnamed-chunk-1-4.jpeg)<!-- -->

```r
hist(extant$mean_lat)
```

![](figures/unnamed-chunk-1-5.jpeg)<!-- -->

```r
hist(extant$min_lat)
```

![](figures/unnamed-chunk-1-6.jpeg)<!-- -->

261 complete cases in the data. Body size distribution as expected (follows a negative binomial, cut off at the lower end).


```r
ggplot(extant, aes(Red.List.status))+geom_bar()#+scale_y_log10()#+scale_y_continuous(limits = c(0,200), oob = squish)
```

![](figures/unnamed-chunk-2-1.jpeg)<!-- -->



```r
ggplot(extant, aes(hab.cat.b))+geom_bar()+scale_y_log10()#limits = c(0,400), oob = squish)
```

![](figures/unnamed-chunk-3-1.jpeg)<!-- -->

Habitat distribution looks similar to extinct species. Only very few species from high energy habitats only.




## Comparability with fossil data
Data from the fossil record and from living species can differ greatly, but also share some common points. Data on geographic ranges, body size and habitat are comparable without further adjustments (?), whereas comparing data on abundance from extinct and living species would be most likely to the disadvantage of the extinct species, caused by the in general low preservation probability of terrestrial organisms. Another variable that is not comparable without further adjustments is extinction risk, wich is defined as species duration in the fossil record, but as category in the IUCN Red List. 
To bridge these differences between datasets, we chose to categorize data for abundance (mni_max and spec_max) and extinction risk (duration) for the extinct species data. 


Applying the fossil data fitted model I will predict duration for extant species, which can be compared to their current assassment categories. Therefore, only abundance categorization has to be done.
We regard EW and EX to be of the same results and therefore similar for our approach. DD species is not a category for extinction risk, therefore there is 6 categories for living species, which is in increasing order: LC, NT, VU, EN, CR, and EX.



# Modelling
## Data imputation
Data was imputed for missing cases of bodysize (svl) and abundance categories. This allows us to use all 354 
We excluded habitat category from our data prior to calculations as we have shown that it`s influence on extinction risk seems to be reversed by human activities. Imputation was performed using the mice package, using the average results of 50 imputation repetitions. Procedures and imputation validation can be found in the supplement. 

```r
extinct.imp <- extinct.raw[,c("ma_range", "lat_range", "gcd", "svl", "mean_lat",
                 "min_lat", "abu_cat")]
extinct.imp$abu_cat <- as.factor(extinct.imp$abu_cat) # set abundance as factor

imputation_rf_svl <- matrix(ncol=50, nrow=nrow(extinct.imp))
imputation_rf_abu <- matrix(ncol=50, nrow=nrow(extinct.imp))
for(i in 1:50){
  imputed <- rfImpute(extinct.imp, extinct$ma_range)
  imputation_rf_svl[,i] <- imputed$svl
  imputation_rf_abu[,i] <- imputed$abu_cat
}
```

```
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    9.088    23.99 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    9.044    23.88 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    8.719    23.02 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    9.453    24.96 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    8.972    23.69 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    8.534    22.53 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    9.015    23.80 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    9.024    23.83 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    9.017    23.81 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    9.476    25.02 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |      9.2    24.29 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    8.951    23.63 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |     8.68    22.92 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |     8.43    22.26 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    9.029    23.84 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    8.878    23.44 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    8.598    22.70 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    8.862    23.40 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    8.037    21.22 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    9.169    24.21 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    8.566    22.61 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    9.389    24.79 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    9.708    25.63 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    9.114    24.06 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    9.671    25.53 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    8.748    23.10 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    9.223    24.35 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    9.332    24.64 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    9.363    24.72 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    8.588    22.67 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |     8.56    22.60 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    9.089    24.00 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |     8.79    23.21 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    8.965    23.67 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    9.019    23.81 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    7.825    20.66 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |     9.38    24.77 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |     8.22    21.70 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    8.743    23.08 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    8.929    23.57 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    8.957    23.65 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    9.461    24.98 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    8.533    22.53 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    8.648    22.83 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    8.901    23.50 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    8.925    23.56 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    9.286    24.52 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    9.269    24.47 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |     8.61    22.73 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    8.512    22.47 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    9.305    24.57 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    8.316    21.96 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    8.911    23.53 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    7.979    21.07 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    8.373    22.11 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    9.023    23.82 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    8.574    22.64 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    8.969    23.68 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    8.654    22.85 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    9.272    24.48 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    8.056    21.27 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    9.384    24.77 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    9.079    23.97 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    8.307    21.93 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    9.252    24.43 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    8.417    22.22 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    8.452    22.32 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    9.752    25.75 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    8.105    21.40 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    8.856    23.38 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    8.908    23.52 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |      8.8    23.23 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    9.016    23.81 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    8.091    21.36 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    9.226    24.36 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    8.712    23.00 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    9.541    25.19 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    8.691    22.95 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    9.726    25.68 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    8.708    22.99 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    9.124    24.09 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    8.286    21.88 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    8.774    23.17 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    9.194    24.27 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    9.102    24.03 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    8.462    22.34 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    8.495    22.43 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    9.151    24.16 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |     8.88    23.45 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    8.744    23.08 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    9.343    24.67 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    8.756    23.12 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    10.18    26.89 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    9.015    23.80 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    9.232    24.38 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    9.177    24.23 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    8.758    23.12 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    8.542    22.55 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    8.697    22.96 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    8.909    23.52 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    8.844    23.35 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    9.545    25.20 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    9.237    24.39 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    8.891    23.48 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    8.072    21.31 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    8.459    22.33 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    8.905    23.51 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    8.206    21.67 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |     9.09    24.00 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |     8.62    22.76 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    8.589    22.68 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    9.057    23.91 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    8.741    23.08 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    9.102    24.03 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    8.911    23.53 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    9.109    24.05 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |      8.4    22.18 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    7.868    20.77 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    9.159    24.18 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    9.061    23.92 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    8.575    22.64 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    8.719    23.02 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    8.468    22.36 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    9.828    25.95 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    9.461    24.98 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    7.872    20.78 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    8.832    23.32 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    9.266    24.46 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    9.086    23.99 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    8.983    23.72 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    9.594    25.33 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    8.486    22.40 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    9.205    24.30 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    9.456    24.97 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    9.035    23.85 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    8.517    22.49 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    8.198    21.64 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    8.785    23.19 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    8.721    23.03 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    9.004    23.77 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    8.592    22.68 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |     8.79    23.21 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    9.685    25.57 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    9.114    24.06 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |     8.95    23.63 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    8.759    23.12 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    9.078    23.97 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    8.704    22.98 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    9.024    23.83 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    9.025    23.83 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    8.542    22.55 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    8.583    22.66 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    9.258    24.44 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    8.681    22.92 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    7.625    20.13 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |      8.5    22.44 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    9.127    24.10 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    9.015    23.80 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    8.466    22.35 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    8.301    21.91 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    9.337    24.65 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    9.459    24.97 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    8.902    23.50 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    8.934    23.59 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    9.202    24.29 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    9.325    24.62 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    8.743    23.08 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    9.035    23.85 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    9.513    25.12 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |     8.98    23.71 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    8.364    22.08 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    9.512    25.11 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    9.245    24.41 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    9.142    24.14 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    8.849    23.36 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    8.504    22.45 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    8.861    23.40 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    8.836    23.33 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    9.103    24.03 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    9.323    24.61 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    9.036    23.86 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |     9.48    25.03 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    7.907    20.88 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    9.519    25.13 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    8.322    21.97 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    9.005    23.77 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |     9.86    26.03 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    9.156    24.17 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    9.118    24.07 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    9.872    26.06 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    8.932    23.58 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    8.512    22.47 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    9.044    23.88 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |      8.5    22.44 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    9.143    24.14 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    8.847    23.36 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    7.336    19.37 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    8.604    22.72 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    8.863    23.40 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    9.219    24.34 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |     8.87    23.42 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    8.709    22.99 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    8.837    23.33 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    8.582    22.66 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    8.841    23.34 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    8.774    23.16 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    8.494    22.43 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    9.101    24.03 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    7.889    20.83 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    9.193    24.27 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |     9.18    24.24 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    9.059    23.92 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    9.185    24.25 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    9.296    24.54 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    9.236    24.39 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    8.949    23.63 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    8.618    22.75 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    8.627    22.78 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    8.751    23.10 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    8.791    23.21 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    9.096    24.02 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    8.335    22.01 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    9.223    24.35 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    8.771    23.16 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    9.372    24.74 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    8.722    23.03 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    8.604    22.72 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    9.355    24.70 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    8.418    22.23 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |     8.69    22.94 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    9.162    24.19 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    8.937    23.60 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    9.103    24.03 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    9.211    24.32 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    9.387    24.78 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    8.012    21.15 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    9.192    24.27 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    8.687    22.94 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    8.798    23.23 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    9.013    23.80 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    8.865    23.41 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    9.442    24.93 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    8.616    22.75 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    9.231    24.37 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    8.948    23.63 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    8.458    22.33 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    8.947    23.62 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    9.148    24.15 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    8.435    22.27 |
##      |      Out-of-bag   |
## Tree |      MSE  %Var(y) |
##  300 |    8.699    22.97 |
```

```r
# Using mice package
imputed <- mice(extinct.imp, maxit=20, m=50, print=FALSE, method = c("", "", "", "rf", "", "", "polr")) # polr
# use default imputation method for bodysize and polr instead of default polyreg (abu is an ordered factor)
plot(imputed, c("svl", "abu_cat")) # check convergence of the predictor algorithm
```

![](figures/imputation-1.jpeg)<!-- -->

```r
# combine the multiple iterations into one mean imputed value
temp <- complete(imputed, action="broad", include=TRUE)
imputation_mice_svl <- temp[,grepl(pattern = "svl.[1-9]", x = names(temp))] # grab all imputed svl columns
imputation_mice_abu <- temp[,grepl(pattern = "abu_cat.[1-9]", x = names(temp))] # grab all imputed abu columns

# Impossible values?
table((imputation_rf_svl<=0))
```

```
## 
## FALSE 
## 17700
```

```r
table((imputation_mice_svl<=0))
```

```
## 
## FALSE 
## 17700
```

```r
# PLOTS
## plot densities to check if imputations are reasonable
grid.arrange(
ggplot(melt(imputation_rf_svl), aes(x=value))+
  geom_density(aes(group=X2, col="orange"), show.legend = FALSE)+
  geom_density(data=extinct.imp, aes(x=svl), col="blue"),
ggplot(melt(imputation_mice_svl), aes(x=value))+
  geom_density(aes(group=variable, col="orange"), show.legend = FALSE)+
  geom_density(data=extinct.imp, aes(x=svl), col="blue"))
```

```
## Using  as id variables
```

![](figures/imputation-2.jpeg)<!-- -->

```r
grid.arrange(
ggplot(melt(imputation_rf_abu), aes(x=value))+
  geom_density(aes(group=X2, col="orange"), show.legend = FALSE)+
  geom_density(data=extinct.imp, aes(x=as.numeric(as.character(extinct.imp$abu_cat))), col="blue"),
ggplot(melt(as.matrix(imputation_mice_abu)), aes(x=value))+
  geom_density(aes(group=X2, col="orange"), show.legend = FALSE)+
  geom_density(data=extinct.imp, aes(x=as.numeric(as.character(extinct.imp$abu_cat))), col="blue"))
```

![](figures/imputation-3.jpeg)<!-- -->

```r
## Mean imputated values
par(mfrow=c(2,1))
which_svl_imp <- as.numeric(row.names(imputed$imp$svl))
boxplot(t(imputation_rf_svl[which_svl_imp,]), main="imputation random forest")
boxplot(t(imputation_mice_svl[which_svl_imp,]), main="imputation mice")
```

![](figures/imputation-4.jpeg)<!-- -->

```r
# ignore the numbering, first plot reasigns the row numbers, second keeps the old ones

imputation_mice_abu <- apply(imputation_mice_abu, 2, function(x) as.numeric(as.character(x)))
boxplot(t(imputation_rf_abu)); boxplot(t(imputation_mice_abu))
```

![](figures/imputation-5.jpeg)<!-- -->

```r
# check for sd of the imputed data. values==0 are the not imputed data
#imputation_rf_abu <- apply(imputation_rf_abu, 2, function(x) as.numeric(as.character(x)))
hist(apply(imputation_rf_svl, 1, sd)); hist(apply(imputation_mice_svl, 1, sd)) 
```

![](figures/imputation-6.jpeg)<!-- -->

```r
hist(apply(imputation_rf_abu, 1, sd), breaks=20); hist(apply(imputation_mice_abu, 1, sd), breaks=20)
```

![](figures/imputation-7.jpeg)<!-- -->

```r
psych::describe(apply(imputation_rf_abu, 1, sd), IQR=TRUE)
```

```
##    vars   n mean   sd median trimmed mad min  max range skew kurtosis   se
## X1    1 354 0.36 0.54      0    0.27   0   0 1.52  1.52 1.11    -0.39 0.03
##     IQR
## X1 0.65
```

```r
psych::describe(apply(imputation_mice_abu, 1, sd), IQR=TRUE)
```

```
##    vars   n mean   sd median trimmed  mad min  max range skew kurtosis
## X1    1 354 0.25 0.27   0.17    0.22 0.25   0 1.07  1.07 0.52    -1.13
##      se  IQR
## X1 0.01 0.48
```

```r
par(mfrow=c(1,1))
plot(rowMeans(imputation_mice_svl), rowMeans(imputation_rf_svl), alpha=0.5)
text(100, 3000, round(cor(rowMeans(imputation_mice_svl), rowMeans(imputation_rf_svl)),2))
```

![](figures/imputation-8.jpeg)<!-- -->

```r
plot(rowMeans(imputation_mice_abu), rowMeans(imputation_rf_abu))
text(4, 1.2, round(cor(rowMeans(imputation_mice_abu), rowMeans(imputation_rf_abu)),2))
```

![](figures/imputation-9.jpeg)<!-- -->

```r
# Add the imputed data
extinct.imp$svl <- rowMeans(imputation_mice_svl)

extinct.imp$abu_cat  <- as.factor(apply(imputation_mice_abu, 1, 
                                        function(x) names(sort(table(x), decreasing = TRUE))[1]))

extinct.imp <- cbind(extinct.imp, extinct.raw[,c("species", "order", "family", "genus", "complete_case")])
imp <- extinct.imp[,c("ma_range", "lat_range", "gcd", "svl", "mean_lat",
                 "min_lat", "abu_cat")]
```
Data imputation with mice takes the categorical and numeric characteristics of abundance and bodysize into account and allows for multiple methods. Imputed body size with randomForest has smaller sd for multiple imputations, but the mice density distribution of the imputations follows the real data better (Although both use a randomforest algorithm). The correlation between both imputation methods is high. 
Abundance is on average predicted higher with randomForest than with mice and correlates poorly between both methods. The sd for randomforest imputations is smaller (when treated as a numeric variable) in mean and median values, the maximum sd is higher.
We chose to use the mice::mice function for data imputation.


### Analyze data imputation 

```r
svl_imputed <- extinct$svl==extinct.imp$svl
svl_imputed <- !is.na(svl_imputed)
abu_cat_imputed <- extinct$abu_cat==extinct.imp$abu_cat
abu_cat_imputed <- !is.na(abu_cat_imputed)
extinct.imp <- cbind(extinct.imp, svl_imputed, abu_cat_imputed) 

round(tapply(extinct.imp$svl_imputed, extinct.raw$order, sum)/
        tapply(extinct.imp$svl_imputed, extinct.raw$order, length),2)
```

```
##   Allocaudata  Lepospondyli Parabatrachia     Salientia Temnospondyli 
##          0.91          0.67          0.00          0.39          0.57 
##       Urodela 
##          0.54
```

```r
round(tapply(extinct.imp$abu_cat_imputed, extinct.raw$order, sum)/
        tapply(extinct.imp$abu_cat_imputed, extinct.raw$order, length),2)
```

```
##   Allocaudata  Lepospondyli Parabatrachia     Salientia Temnospondyli 
##          0.82          0.64          0.00          0.36          0.47 
##       Urodela 
##          0.51
```

```r
ggplot(extinct.imp[is.na(extinct.imp$order)==FALSE,], aes(svl, fill=svl_imputed))+
  geom_histogram()+
  scale_fill_hue("svl imputed")+
  xlab("svl length")+
  theme_classic()+
  facet_grid(order ~ .)
```

```
## `stat_bin()` using `bins = 30`. Pick better value with `binwidth`.
```

![](figures/imputation_analysis-1.jpeg)<!-- -->

```r
ggplot(extinct.imp[is.na(extinct.imp$order)==FALSE,], aes(abu_cat, fill=abu_cat_imputed))+
  geom_bar()+
  scale_fill_hue("abundance imputed")+
  xlab("abundance category")+
  theme_classic()+
  facet_grid(order ~ .)
```

![](figures/imputation_analysis-2.jpeg)<!-- -->

Data imputed is only data on abundance and body size.

## Distribution check

```r
my_data <- extinct$ma_range
plot(my_data, pch=20)
```

![](figures/distribution check-1.jpeg)<!-- -->

```r
plotdist(my_data, histo=TRUE, demp=TRUE)
```

![](figures/distribution check-2.jpeg)<!-- -->

```r
descdist(my_data, discrete=FALSE, boot=500)
```

![](figures/distribution check-3.jpeg)<!-- -->

```
## summary statistics
## ------
## min:  0   max:  55 
## median:  0 
## mean:  1.926554 
## estimated sd:  6.163056 
## estimated skewness:  5.197434 
## estimated kurtosis:  36.43398
```
According to fitdistrplus::descdist the response variable shows a beta distribution.




## Generalized additive model
GAM was fitted to the data to allow for non-linear relationships between the predictor variables and the species duration. 
Normality (qq plot) and homogeneity are violated (residuals vs. fitted values (linear predictor)).

Family for the model: nb theta estimation does not work so I can only get the gebin(x) working, which vastly overfits the model and results in just 2 variables being significant. As normal distribution is the worst choice here, i do poisson without log-transformation of the duration data.

Zuur on chosing a smoother: "In practise, the difference between cubic regression splines, thin plate regression splines, B-splines, P-splines, etc., is rather small". 

method and select of the mgcv::gam() are being chosen using the caret::train() function.



```r
# logging the skewed variables
imp2 <- log(imp[,c("ma_range", "lat_range", "gcd", "svl")]+1)
imp2$mean_lat <- imp$mean_lat; imp2$min_lat <- imp$min_lat; imp2$abu_cat <- imp$abu_cat;
extinct2 <- log(extinct[,c("ma_range", "lat_range", "gcd", "svl")]+1)
extinct2$mean_lat <- extinct$mean_lat; extinct2$min_lat <- extinct$min_lat; extinct2$abu_cat <- extinct$abu_cat;

gam.incomp <- gam(data=extinct, ma_range ~ s(lat_range) + s(gcd) + s(svl) + s(mean_lat) +
                  s(min_lat) + s(as.numeric(as.character(abu_cat)), k=4))
gam.incomp.log <- gam(data=extinct2, ma_range ~ s(lat_range) + s(gcd) + s(svl) + s(mean_lat) +
                  s(min_lat) + s(as.numeric(as.character(abu_cat)), k=4))
gam.imp <- gam(data=imp, ma_range ~ s(lat_range) + s(gcd) + s(svl) + s(mean_lat) +
                s(min_lat) + s(as.numeric(as.character(abu_cat)), k=4))
gam.imp.log <- gam(data=imp2, ma_range ~ s(lat_range) + s(gcd) + s(svl) + s(mean_lat) +
                s(min_lat) + s(as.numeric(as.character(abu_cat)), k=4))

summary(gam.incomp)
```

```
## 
## Family: gaussian 
## Link function: identity 
## 
## Formula:
## ma_range ~ s(lat_range) + s(gcd) + s(svl) + s(mean_lat) + s(min_lat) + 
##     s(as.numeric(as.character(abu_cat)), k = 4)
## 
## Parametric coefficients:
##             Estimate Std. Error t value Pr(>|t|)    
## (Intercept)   2.7818     0.4963   5.605 9.12e-08 ***
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## Approximate significance of smooth terms:
##                                        edf Ref.df      F  p-value    
## s(lat_range)                         1.000  1.000  0.231 0.631536    
## s(gcd)                               1.689  2.095  0.728 0.515516    
## s(svl)                               1.000  1.000  0.172 0.679293    
## s(mean_lat)                          1.000  1.000 14.832 0.000169 ***
## s(min_lat)                           1.000  1.000 13.971 0.000257 ***
## s(as.numeric(as.character(abu_cat))) 1.000  1.000  0.092 0.761784    
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## R-sq.(adj) =    0.2   Deviance explained = 23.3%
## GCV = 42.631  Scale est. = 40.645    n = 165
```

```r
summary(gam.incomp.log)
```

```
## 
## Family: gaussian 
## Link function: identity 
## 
## Formula:
## ma_range ~ s(lat_range) + s(gcd) + s(svl) + s(mean_lat) + s(min_lat) + 
##     s(as.numeric(as.character(abu_cat)), k = 4)
## 
## Parametric coefficients:
##             Estimate Std. Error t value Pr(>|t|)    
## (Intercept)  0.58956    0.06206   9.499   <2e-16 ***
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## Approximate significance of smooth terms:
##                                        edf Ref.df      F  p-value    
## s(lat_range)                         3.328  4.056  0.672 0.631941    
## s(gcd)                               5.547  6.638  2.491 0.017673 *  
## s(svl)                               1.000  1.000  0.129 0.720418    
## s(mean_lat)                          1.000  1.000 14.204 0.000232 ***
## s(min_lat)                           1.000  1.000 13.458 0.000335 ***
## s(as.numeric(as.character(abu_cat))) 1.000  1.000  0.001 0.972482    
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## R-sq.(adj) =  0.355   Deviance explained = 40.6%
## GCV = 0.69391  Scale est. = 0.63556   n = 165
```

```r
summary(gam.imp)
```

```
## 
## Family: gaussian 
## Link function: identity 
## 
## Formula:
## ma_range ~ s(lat_range) + s(gcd) + s(svl) + s(mean_lat) + s(min_lat) + 
##     s(as.numeric(as.character(abu_cat)), k = 4)
## 
## Parametric coefficients:
##             Estimate Std. Error t value Pr(>|t|)    
## (Intercept)   1.9266     0.2508   7.682 1.81e-13 ***
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## Approximate significance of smooth terms:
##                                        edf Ref.df      F  p-value    
## s(lat_range)                         9.000  9.000  8.090 5.51e-11 ***
## s(gcd)                               8.890  8.994 10.054 6.20e-14 ***
## s(svl)                               1.573  1.956  0.818    0.486    
## s(mean_lat)                          1.000  1.000 48.053 1.94e-11 ***
## s(min_lat)                           1.000  1.000 47.074 3.02e-11 ***
## s(as.numeric(as.character(abu_cat))) 2.326  2.655  2.425    0.150    
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## R-sq.(adj) =  0.414   Deviance explained = 45.3%
## GCV =  23.94  Scale est. = 22.263    n = 354
```

```r
summary(gam.imp.log)
```

```
## 
## Family: gaussian 
## Link function: identity 
## 
## Formula:
## ma_range ~ s(lat_range) + s(gcd) + s(svl) + s(mean_lat) + s(min_lat) + 
##     s(as.numeric(as.character(abu_cat)), k = 4)
## 
## Parametric coefficients:
##             Estimate Std. Error t value Pr(>|t|)    
## (Intercept)  0.42572    0.03575   11.91   <2e-16 ***
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## Approximate significance of smooth terms:
##                                        edf Ref.df      F  p-value    
## s(lat_range)                         4.177  5.072  1.591    0.164    
## s(gcd)                               7.412  8.370  7.000 8.49e-09 ***
## s(svl)                               4.336  5.365  1.752    0.104    
## s(mean_lat)                          1.000  1.000 24.028 1.46e-06 ***
## s(min_lat)                           1.000  1.000 22.839 2.61e-06 ***
## s(as.numeric(as.character(abu_cat))) 1.000  1.000  0.029    0.864    
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## R-sq.(adj) =  0.381   Deviance explained = 41.4%
## GCV = 0.4794  Scale est. = 0.45241   n = 354
```

```r
par(mfrow=c(2,2))
gam.check(gam.incomp)
```

![](figures/gam-1.jpeg)<!-- -->

```
## 
## Method: GCV   Optimizer: magic
## Smoothing parameter selection converged after 18 iterations.
## The RMS GCV score gradient at convergence was 6.749388e-07 .
## The Hessian was positive definite.
## Model rank =  49 / 49 
## 
## Basis dimension (k) checking results. Low p-value (k-index<1) may
## indicate that k is too low, especially if edf is close to k'.
## 
##                                        k'  edf k-index p-value
## s(lat_range)                         9.00 1.00    1.07    0.84
## s(gcd)                               9.00 1.69    1.03    0.56
## s(svl)                               9.00 1.00    1.08    0.88
## s(mean_lat)                          9.00 1.00    1.00    0.33
## s(min_lat)                           9.00 1.00    1.09    0.93
## s(as.numeric(as.character(abu_cat))) 3.00 1.00    1.07    0.81
```

```r
gam.check(gam.incomp.log)
```

![](figures/gam-2.jpeg)<!-- -->

```
## 
## Method: GCV   Optimizer: magic
## Smoothing parameter selection converged after 16 iterations.
## The RMS GCV score gradient at convergence was 2.973255e-08 .
## The Hessian was positive definite.
## Model rank =  49 / 49 
## 
## Basis dimension (k) checking results. Low p-value (k-index<1) may
## indicate that k is too low, especially if edf is close to k'.
## 
##                                        k'  edf k-index p-value
## s(lat_range)                         9.00 3.33    1.13    0.96
## s(gcd)                               9.00 5.55    1.01    0.47
## s(svl)                               9.00 1.00    1.08    0.85
## s(mean_lat)                          9.00 1.00    1.00    0.37
## s(min_lat)                           9.00 1.00    1.06    0.71
## s(as.numeric(as.character(abu_cat))) 3.00 1.00    0.97    0.32
```

```r
gam.check(gam.imp)
```

![](figures/gam-3.jpeg)<!-- -->

```
## 
## Method: GCV   Optimizer: magic
## Smoothing parameter selection converged after 28 iterations.
## The RMS GCV score gradient at convergence was 5.401205e-07 .
## The Hessian was positive definite.
## Model rank =  49 / 49 
## 
## Basis dimension (k) checking results. Low p-value (k-index<1) may
## indicate that k is too low, especially if edf is close to k'.
## 
##                                        k'  edf k-index p-value
## s(lat_range)                         9.00 9.00    1.00    0.39
## s(gcd)                               9.00 8.89    1.02    0.64
## s(svl)                               9.00 1.57    1.06    0.92
## s(mean_lat)                          9.00 1.00    1.03    0.70
## s(min_lat)                           9.00 1.00    0.99    0.28
## s(as.numeric(as.character(abu_cat))) 3.00 2.33    1.00    0.47
```

```r
gam.check(gam.imp.log)
```

![](figures/gam-4.jpeg)<!-- -->

```
## 
## Method: GCV   Optimizer: magic
## Smoothing parameter selection converged after 17 iterations.
## The RMS GCV score gradient at convergence was 6.093325e-08 .
## The Hessian was positive definite.
## Model rank =  49 / 49 
## 
## Basis dimension (k) checking results. Low p-value (k-index<1) may
## indicate that k is too low, especially if edf is close to k'.
## 
##                                        k'  edf k-index p-value  
## s(lat_range)                         9.00 4.18    1.00    0.46  
## s(gcd)                               9.00 7.41    0.97    0.27  
## s(svl)                               9.00 4.34    1.02    0.58  
## s(mean_lat)                          9.00 1.00    1.04    0.72  
## s(min_lat)                           9.00 1.00    0.92    0.07 .
## s(as.numeric(as.character(abu_cat))) 3.00 1.00    0.96    0.19  
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
```

```r
par(mfrow=c(1,1))

# Chose model gam.imp. Adjust family?
gam.imp <- gam(data=imp, ma_range ~ s(lat_range) + s(gcd) + s(svl) + s(mean_lat) +
                s(min_lat) + s(as.numeric(as.character(abu_cat)), k=4), method="REML")
gam.imp.new <- gam(data=imp, ma_range ~ s(lat_range) + s(gcd) + s(svl) + s(mean_lat) +
                s(min_lat) + s(as.numeric(as.character(abu_cat)), k=4),
               family = nb())
summary(gam.imp.new)
```

```
## 
## Family: Negative Binomial(0.205) 
## Link function: log 
## 
## Formula:
## ma_range ~ s(lat_range) + s(gcd) + s(svl) + s(mean_lat) + s(min_lat) + 
##     s(as.numeric(as.character(abu_cat)), k = 4)
## 
## Parametric coefficients:
##             Estimate Std. Error z value Pr(>|z|)  
## (Intercept)  -0.2979     0.1421  -2.097    0.036 *
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## Approximate significance of smooth terms:
##                                        edf Ref.df Chi.sq  p-value    
## s(lat_range)                         1.000  1.000  1.216   0.2701    
## s(gcd)                               3.064  3.651 49.063 8.35e-10 ***
## s(svl)                               2.703  3.368  7.442   0.0795 .  
## s(mean_lat)                          1.600  1.981 44.041 2.74e-10 ***
## s(min_lat)                           1.002  1.003 42.172 8.66e-11 ***
## s(as.numeric(as.character(abu_cat))) 1.862  2.163  2.288   0.3488    
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## R-sq.(adj) =  -2.1e+06   Deviance explained = 79.1%
## -REML = 432.11  Scale est. = 1         n = 354
```

```r
par(mfrow=c(2,2))
gam.check(gam.imp.new)
```

![](figures/gam-5.jpeg)<!-- -->

```
## 
## Method: REML   Optimizer: outer newton
## full convergence after 11 iterations.
## Gradient range [-0.0004003171,2.627854e-05]
## (score 432.1067 & scale 1).
## Hessian positive definite, eigenvalue range [9.1961e-06,45.14962].
## Model rank =  49 / 49 
## 
## Basis dimension (k) checking results. Low p-value (k-index<1) may
## indicate that k is too low, especially if edf is close to k'.
## 
##                                        k'  edf k-index p-value
## s(lat_range)                         9.00 1.00    0.71    0.40
## s(gcd)                               9.00 3.06    0.68    0.13
## s(svl)                               9.00 2.70    0.72    0.46
## s(mean_lat)                          9.00 1.60    0.70    0.32
## s(min_lat)                           9.00 1.00    0.67    0.12
## s(as.numeric(as.character(abu_cat))) 3.00 1.86    0.73    0.59
```

```r
par(mfrow=c(1,1))
plot(imp$ma_range~gam.imp.new$fitted.values, xlim=c(0,20))
```

![](figures/gam-6.jpeg)<!-- -->

```r
# Choose standard family, as negative binomial looks overfitted (very high deviance explained), has huuuge outliers.
# The r squared value points, despite the better AIC and deviance, to a fitting problem
final.gam <- gam.imp

# Predict
predict.gam <- predict.gam(gam.imp, newdata = extant)
range(predict.gam) # there is lots of negative predictions in the gam; adjust:
```

```
## [1] -89.6096  25.3663
```

```r
predict.gam <- predict.gam+abs(min(predict.gam))

res <- extant
res$Red.List.status <- ordered(res$Red.List.status, levels = c("DD", "LC", "NT", "VU", "EN", "CR", "EW", "EX"))
res$predict.gam <- predict.gam

library(ggthemes)
theme=theme_set(theme_minimal()) 

(gam.fin <- ggplot(res, aes(x=Red.List.status, y=log(predict.gam)))+
    geom_boxplot(outlier.colour=NULL, colour="#FF9999", fill="#FF9999")+
    scale_y_continuous("predicted duration (log ma)")+
    stat_summary(geom = "crossbar", 
                 width=0.65, fatten=.5, 
                 color="black", 
                 fun.data = function(x){return(c(y=median(x), ymin=median(x), ymax=median(x)))})
)  
```

![](figures/gam-7.jpeg)<!-- -->

```r
library(reshape)
res2 <- melt(res[,c("Red.List.status", "predict.gam")])
```

```
## Using Red.List.status as id variables
```

```r
kruskal.test(res$predict.gam, res$Red.List.status)
```

```
## 
## 	Kruskal-Wallis rank sum test
## 
## data:  res$predict.gam and res$Red.List.status
## Kruskal-Wallis chi-squared = 43.754, df = 6, p-value = 8.271e-08
```

```r
pairwise.wilcox.test(res$predict.gam, res$Red.List.status, p.adjust.method = "fdr")
```

```
## 
## 	Pairwise comparisons using Wilcoxon rank sum test 
## 
## data:  res$predict.gam and res$Red.List.status 
## 
##    DD     LC     NT     VU     EN     CR    
## LC 0.0390 -      -      -      -      -     
## NT 0.3189 0.2849 -      -      -      -     
## VU 0.3385 0.0019 0.3915 -      -      -     
## EN 0.9800 0.0019 0.1510 0.5250 -      -     
## CR 1.0000 0.0717 0.3385 0.3645 0.9428 -     
## EX 0.9428 0.3295 0.3500 0.3385 0.9800 0.5250
## 
## P value adjustment method: fdr
```



## Random Forest

```r
# Set seeds and parameters for cross validation for parameter tuning with caret::train()
set.seed(432)
mySeeds <- sapply(simplify = FALSE, 1:31, function(u) sample(10^4, 5))

fitControl <- trainControl(method = "repeatedcv", number = 10,
                           repeats = 3, seeds = mySeeds,
                           returnResamp = "all",
                           savePredictions = "final") ## 3 times 10-fold CV
rfFit1 <- train(ma_range ~ ., data = imp, method = "rf", 
                trControl = fitControl, verbose = FALSE,
                na.action = na.pass,
                tuneGrid=data.frame(mtry=c(2,3,4,5,6)),
                importance=TRUE)
rfFit1
```

```
## Random Forest 
## 
## 354 samples
##   6 predictors
## 
## No pre-processing
## Resampling: Cross-Validated (10 fold, repeated 3 times) 
## Summary of sample sizes: 318, 320, 318, 319, 318, 319, ... 
## Resampling results across tuning parameters:
## 
##   mtry  RMSE      Rsquared 
##   2     5.263615  0.2341438
##   3     5.361011  0.2316503
##   4     5.434592  0.2286159
##   5     5.492875  0.2254948
##   6     5.548529  0.2175984
## 
## RMSE was used to select the optimal model using  the smallest value.
## The final value used for the model was mtry = 2.
```

```r
rfFit1$finalModel
```

```
## 
## Call:
##  randomForest(x = x, y = y, mtry = param$mtry, importance = TRUE,      verbose = FALSE) 
##                Type of random forest: regression
##                      Number of trees: 500
## No. of variables tried at each split: 2
## 
##           Mean of squared residuals: 33.95086
##                     % Var explained: 10.36
```

```r
ggplot(rfFit1)
```

![](figures/random forest-1.jpeg)<!-- -->

```r
plot(rfFit1$finalModel)
```

![](figures/random forest-2.jpeg)<!-- -->

```r
varImpPlot(rfFit1$finalModel)
```

![](figures/random forest-3.jpeg)<!-- -->

```r
### PREDICTION ####
if(class(extant$abu_cat)=="integer"){extant$abu_cat <- as.factor(extant$abu_cat)}
predict.rf <- predict(rfFit1, newdata = extant)
res$predict.rf <- predict.rf

res2 <- melt(res[,c("Red.List.status", "predict.gam", "predict.rf")])
```

```
## Using Red.List.status as id variables
```

```r
theme=theme_set(theme_minimal()) 

ggplot(res2, aes(x=Red.List.status, y=log(value)))+
 geom_boxplot(aes(fill=variable))
```

![](figures/random forest-4.jpeg)<!-- -->

```r
#   geom_boxplot(outlier.colour=NULL, aes(fill=variable, colour=variable))+
#  scale_y_continuous("predicted duration (log ma)")+
#  stat_summary(geom = "crossbar", 
#               width=0.65, fatten=1, 
#               color="black", 
#               fun.data = function(x){return(c(y=median(x), ymin=median(x), ymax=median(x)))})

kruskal.test(res$predict.rf, res$Red.List.status)
```

```
## 
## 	Kruskal-Wallis rank sum test
## 
## data:  res$predict.rf and res$Red.List.status
## Kruskal-Wallis chi-squared = 65.361, df = 6, p-value = 3.64e-12
```

```r
pairwise.wilcox.test(res$predict.rf, res$Red.List.status, p.adjust.method = "fdr")
```

```
## 
## 	Pairwise comparisons using Wilcoxon rank sum test 
## 
## data:  res$predict.rf and res$Red.List.status 
## 
##    DD     LC      NT     VU     EN     CR    
## LC 0.0086 -       -      -      -      -     
## NT 0.1510 0.0533  -      -      -      -     
## VU 0.6000 2.2e-05 0.2111 -      -      -     
## EN 1.0000 8.1e-05 0.0533 0.3933 -      -     
## CR 0.9000 0.0115  0.3933 0.9303 0.9000 -     
## EX 1.0000 0.2358  0.9000 0.9000 1.0000 1.0000
## 
## P value adjustment method: fdr
```

Imputing the data does neither change prediction results or the importance of the single variables too much, but it does increase the variance explained and R squared






## Generalized boosted model ##
Generalized boosted models are regular regression models that are being boosted, means that they are being repeated according to the error parameters of the previous model, again and again. The cross validation can be performed by classic division of data into training and evaluation set. These models do not care about missing data, that`s a plus. They make minimal assumptions about the parameters that are being entered, however collinearity can be a problem, GBMs proof to be relatively tolerant to multicolinearity for prediction (Finnegan 2015 [see ref. 73])

```r
# parameter tuning using caret
gbmControl <- trainControl(method = "repeatedcv", number = 10,
                           repeats = 3, savePredictions = "final")

gbmGrid <-  expand.grid(interaction.depth = c(1, 2, 3), 
                        n.trees = (1:10)*50, 
                        shrinkage = c(0.1, 0.01, 0.001),
                        n.minobsinnode = c(5, 10, 15))
set.seed(825)
gbmFit1 <- train(ma_range ~ ., data = imp, method = "gbm", 
                 trControl = gbmControl, verbose=FALSE,
                 tuneGrid=gbmGrid)
```

```
## Loading required package: plyr
```

```
## 
## Attaching package: 'plyr'
```

```
## The following objects are masked from 'package:reshape':
## 
##     rename, round_any
```

```r
gbmFit1
```

```
## Stochastic Gradient Boosting 
## 
## 354 samples
##   6 predictors
## 
## No pre-processing
## Resampling: Cross-Validated (10 fold, repeated 3 times) 
## Summary of sample sizes: 319, 318, 318, 319, 319, 318, ... 
## Resampling results across tuning parameters:
## 
##   shrinkage  interaction.depth  n.minobsinnode  n.trees  RMSE    
##   0.001      1                   5               50      5.605163
##   0.001      1                   5              100      5.559465
##   0.001      1                   5              150      5.517857
##   0.001      1                   5              200      5.480377
##   0.001      1                   5              250      5.447842
##   0.001      1                   5              300      5.416862
##   0.001      1                   5              350      5.387715
##   0.001      1                   5              400      5.362395
##   0.001      1                   5              450      5.338372
##   0.001      1                   5              500      5.316571
##   0.001      1                  10               50      5.612696
##   0.001      1                  10              100      5.573844
##   0.001      1                  10              150      5.537296
##   0.001      1                  10              200      5.504829
##   0.001      1                  10              250      5.475036
##   0.001      1                  10              300      5.447982
##   0.001      1                  10              350      5.422151
##   0.001      1                  10              400      5.398595
##   0.001      1                  10              450      5.377055
##   0.001      1                  10              500      5.357297
##   0.001      1                  15               50      5.625832
##   0.001      1                  15              100      5.599432
##   0.001      1                  15              150      5.575159
##   0.001      1                  15              200      5.553472
##   0.001      1                  15              250      5.532720
##   0.001      1                  15              300      5.511804
##   0.001      1                  15              350      5.492605
##   0.001      1                  15              400      5.475848
##   0.001      1                  15              450      5.460186
##   0.001      1                  15              500      5.444751
##   0.001      2                   5               50      5.602179
##   0.001      2                   5              100      5.555109
##   0.001      2                   5              150      5.510976
##   0.001      2                   5              200      5.471475
##   0.001      2                   5              250      5.435647
##   0.001      2                   5              300      5.402392
##   0.001      2                   5              350      5.372567
##   0.001      2                   5              400      5.344813
##   0.001      2                   5              450      5.321260
##   0.001      2                   5              500      5.299511
##   0.001      2                  10               50      5.611396
##   0.001      2                  10              100      5.571658
##   0.001      2                  10              150      5.535332
##   0.001      2                  10              200      5.501482
##   0.001      2                  10              250      5.470786
##   0.001      2                  10              300      5.442165
##   0.001      2                  10              350      5.415263
##   0.001      2                  10              400      5.391145
##   0.001      2                  10              450      5.369274
##   0.001      2                  10              500      5.348651
##   0.001      2                  15               50      5.624245
##   0.001      2                  15              100      5.596624
##   0.001      2                  15              150      5.569926
##   0.001      2                  15              200      5.545401
##   0.001      2                  15              250      5.523111
##   0.001      2                  15              300      5.501663
##   0.001      2                  15              350      5.482453
##   0.001      2                  15              400      5.464618
##   0.001      2                  15              450      5.447532
##   0.001      2                  15              500      5.431266
##   0.001      3                   5               50      5.599737
##   0.001      3                   5              100      5.551412
##   0.001      3                   5              150      5.507288
##   0.001      3                   5              200      5.464635
##   0.001      3                   5              250      5.426414
##   0.001      3                   5              300      5.393739
##   0.001      3                   5              350      5.363828
##   0.001      3                   5              400      5.335359
##   0.001      3                   5              450      5.309366
##   0.001      3                   5              500      5.289029
##   0.001      3                  10               50      5.610701
##   0.001      3                  10              100      5.570717
##   0.001      3                  10              150      5.531879
##   0.001      3                  10              200      5.497775
##   0.001      3                  10              250      5.465941
##   0.001      3                  10              300      5.436857
##   0.001      3                  10              350      5.410174
##   0.001      3                  10              400      5.385587
##   0.001      3                  10              450      5.362303
##   0.001      3                  10              500      5.342285
##   0.001      3                  15               50      5.622732
##   0.001      3                  15              100      5.592428
##   0.001      3                  15              150      5.564786
##   0.001      3                  15              200      5.539034
##   0.001      3                  15              250      5.514862
##   0.001      3                  15              300      5.492999
##   0.001      3                  15              350      5.473198
##   0.001      3                  15              400      5.454841
##   0.001      3                  15              450      5.438059
##   0.001      3                  15              500      5.421868
##   0.010      1                   5               50      5.322292
##   0.010      1                   5              100      5.187253
##   0.010      1                   5              150      5.130191
##   0.010      1                   5              200      5.112889
##   0.010      1                   5              250      5.119117
##   0.010      1                   5              300      5.133489
##   0.010      1                   5              350      5.148607
##   0.010      1                   5              400      5.164539
##   0.010      1                   5              450      5.181879
##   0.010      1                   5              500      5.191232
##   0.010      1                  10               50      5.362211
##   0.010      1                  10              100      5.224149
##   0.010      1                  10              150      5.159759
##   0.010      1                  10              200      5.132096
##   0.010      1                  10              250      5.122248
##   0.010      1                  10              300      5.118436
##   0.010      1                  10              350      5.124471
##   0.010      1                  10              400      5.132253
##   0.010      1                  10              450      5.135777
##   0.010      1                  10              500      5.138579
##   0.010      1                  15               50      5.445286
##   0.010      1                  15              100      5.340344
##   0.010      1                  15              150      5.292097
##   0.010      1                  15              200      5.278744
##   0.010      1                  15              250      5.273917
##   0.010      1                  15              300      5.269486
##   0.010      1                  15              350      5.271263
##   0.010      1                  15              400      5.273252
##   0.010      1                  15              450      5.275722
##   0.010      1                  15              500      5.282523
##   0.010      2                   5               50      5.301197
##   0.010      2                   5              100      5.168308
##   0.010      2                   5              150      5.132114
##   0.010      2                   5              200      5.145415
##   0.010      2                   5              250      5.159392
##   0.010      2                   5              300      5.184854
##   0.010      2                   5              350      5.215587
##   0.010      2                   5              400      5.240548
##   0.010      2                   5              450      5.262412
##   0.010      2                   5              500      5.286341
##   0.010      2                  10               50      5.340573
##   0.010      2                  10              100      5.216220
##   0.010      2                  10              150      5.167399
##   0.010      2                  10              200      5.154427
##   0.010      2                  10              250      5.167932
##   0.010      2                  10              300      5.179468
##   0.010      2                  10              350      5.195727
##   0.010      2                  10              400      5.210540
##   0.010      2                  10              450      5.223080
##   0.010      2                  10              500      5.236616
##   0.010      2                  15               50      5.431538
##   0.010      2                  15              100      5.332804
##   0.010      2                  15              150      5.289567
##   0.010      2                  15              200      5.269839
##   0.010      2                  15              250      5.262228
##   0.010      2                  15              300      5.265435
##   0.010      2                  15              350      5.267054
##   0.010      2                  15              400      5.276487
##   0.010      2                  15              450      5.285219
##   0.010      2                  15              500      5.287051
##   0.010      3                   5               50      5.299795
##   0.010      3                   5              100      5.179256
##   0.010      3                   5              150      5.168113
##   0.010      3                   5              200      5.185212
##   0.010      3                   5              250      5.206540
##   0.010      3                   5              300      5.240838
##   0.010      3                   5              350      5.272037
##   0.010      3                   5              400      5.298454
##   0.010      3                   5              450      5.333953
##   0.010      3                   5              500      5.357137
##   0.010      3                  10               50      5.334781
##   0.010      3                  10              100      5.211004
##   0.010      3                  10              150      5.166421
##   0.010      3                  10              200      5.160059
##   0.010      3                  10              250      5.178471
##   0.010      3                  10              300      5.185893
##   0.010      3                  10              350      5.202004
##   0.010      3                  10              400      5.217828
##   0.010      3                  10              450      5.239018
##   0.010      3                  10              500      5.264740
##   0.010      3                  15               50      5.421258
##   0.010      3                  15              100      5.312650
##   0.010      3                  15              150      5.263817
##   0.010      3                  15              200      5.244519
##   0.010      3                  15              250      5.251463
##   0.010      3                  15              300      5.256120
##   0.010      3                  15              350      5.259939
##   0.010      3                  15              400      5.269348
##   0.010      3                  15              450      5.281525
##   0.010      3                  15              500      5.293848
##   0.100      1                   5               50      5.203202
##   0.100      1                   5              100      5.265515
##   0.100      1                   5              150      5.296143
##   0.100      1                   5              200      5.367586
##   0.100      1                   5              250      5.372631
##   0.100      1                   5              300      5.439335
##   0.100      1                   5              350      5.457869
##   0.100      1                   5              400      5.489729
##   0.100      1                   5              450      5.483688
##   0.100      1                   5              500      5.529803
##   0.100      1                  10               50      5.158348
##   0.100      1                  10              100      5.198039
##   0.100      1                  10              150      5.235587
##   0.100      1                  10              200      5.277901
##   0.100      1                  10              250      5.321213
##   0.100      1                  10              300      5.350139
##   0.100      1                  10              350      5.386084
##   0.100      1                  10              400      5.416890
##   0.100      1                  10              450      5.466735
##   0.100      1                  10              500      5.493886
##   0.100      1                  15               50      5.299063
##   0.100      1                  15              100      5.316021
##   0.100      1                  15              150      5.323238
##   0.100      1                  15              200      5.348075
##   0.100      1                  15              250      5.379108
##   0.100      1                  15              300      5.410009
##   0.100      1                  15              350      5.419586
##   0.100      1                  15              400      5.461447
##   0.100      1                  15              450      5.495956
##   0.100      1                  15              500      5.516323
##   0.100      2                   5               50      5.352393
##   0.100      2                   5              100      5.569807
##   0.100      2                   5              150      5.738393
##   0.100      2                   5              200      5.848566
##   0.100      2                   5              250      5.921056
##   0.100      2                   5              300      5.994098
##   0.100      2                   5              350      6.004003
##   0.100      2                   5              400      6.017122
##   0.100      2                   5              450      6.069513
##   0.100      2                   5              500      6.087923
##   0.100      2                  10               50      5.265978
##   0.100      2                  10              100      5.399872
##   0.100      2                  10              150      5.477848
##   0.100      2                  10              200      5.588102
##   0.100      2                  10              250      5.658410
##   0.100      2                  10              300      5.715897
##   0.100      2                  10              350      5.794971
##   0.100      2                  10              400      5.862982
##   0.100      2                  10              450      5.878925
##   0.100      2                  10              500      5.943179
##   0.100      2                  15               50      5.333035
##   0.100      2                  15              100      5.403669
##   0.100      2                  15              150      5.473180
##   0.100      2                  15              200      5.523738
##   0.100      2                  15              250      5.624905
##   0.100      2                  15              300      5.644179
##   0.100      2                  15              350      5.680548
##   0.100      2                  15              400      5.740048
##   0.100      2                  15              450      5.749209
##   0.100      2                  15              500      5.786526
##   0.100      3                   5               50      5.322513
##   0.100      3                   5              100      5.600502
##   0.100      3                   5              150      5.768975
##   0.100      3                   5              200      5.857717
##   0.100      3                   5              250      5.944835
##   0.100      3                   5              300      6.013028
##   0.100      3                   5              350      6.057148
##   0.100      3                   5              400      6.085787
##   0.100      3                   5              450      6.124215
##   0.100      3                   5              500      6.122977
##   0.100      3                  10               50      5.317132
##   0.100      3                  10              100      5.464197
##   0.100      3                  10              150      5.594652
##   0.100      3                  10              200      5.643843
##   0.100      3                  10              250      5.720586
##   0.100      3                  10              300      5.791919
##   0.100      3                  10              350      5.862619
##   0.100      3                  10              400      5.898135
##   0.100      3                  10              450      5.955745
##   0.100      3                  10              500      5.979040
##   0.100      3                  15               50      5.322978
##   0.100      3                  15              100      5.466425
##   0.100      3                  15              150      5.561197
##   0.100      3                  15              200      5.628576
##   0.100      3                  15              250      5.670272
##   0.100      3                  15              300      5.732181
##   0.100      3                  15              350      5.760360
##   0.100      3                  15              400      5.812099
##   0.100      3                  15              450      5.846973
##   0.100      3                  15              500      5.905863
##   Rsquared 
##   0.3059685
##   0.3054747
##   0.3088077
##   0.3077237
##   0.3057773
##   0.3026761
##   0.3032043
##   0.3042989
##   0.3065156
##   0.3056223
##   0.3023894
##   0.3046641
##   0.3054252
##   0.3039931
##   0.3011734
##   0.3000297
##   0.2987705
##   0.2972503
##   0.2955582
##   0.2965192
##   0.2473643
##   0.2426630
##   0.2404325
##   0.2359469
##   0.2334877
##   0.2338682
##   0.2346016
##   0.2350092
##   0.2339825
##   0.2336326
##   0.3008326
##   0.3036014
##   0.3091681
##   0.3085306
##   0.3036175
##   0.3022603
##   0.3003536
##   0.2998260
##   0.2986176
##   0.2972051
##   0.2712052
##   0.2714313
##   0.2714888
##   0.2730400
##   0.2728924
##   0.2724026
##   0.2728234
##   0.2719951
##   0.2712880
##   0.2710635
##   0.2122548
##   0.2085314
##   0.2105456
##   0.2115014
##   0.2101094
##   0.2100425
##   0.2098805
##   0.2102002
##   0.2114401
##   0.2129665
##   0.2993209
##   0.2950707
##   0.2915867
##   0.2951472
##   0.2940882
##   0.2919921
##   0.2923419
##   0.2921577
##   0.2927655
##   0.2915575
##   0.2624865
##   0.2657629
##   0.2675844
##   0.2656840
##   0.2655110
##   0.2657452
##   0.2638103
##   0.2629000
##   0.2626120
##   0.2625264
##   0.2037069
##   0.2084225
##   0.2102382
##   0.2117492
##   0.2122878
##   0.2116296
##   0.2114290
##   0.2108291
##   0.2108005
##   0.2109416
##   0.2969285
##   0.2943698
##   0.2924744
##   0.2898121
##   0.2871183
##   0.2837095
##   0.2801371
##   0.2765985
##   0.2734022
##   0.2714625
##   0.2972112
##   0.2892902
##   0.2774565
##   0.2738584
##   0.2708423
##   0.2721500
##   0.2720792
##   0.2686642
##   0.2680701
##   0.2672341
##   0.2299578
##   0.2301689
##   0.2267484
##   0.2221560
##   0.2218093
##   0.2223506
##   0.2229590
##   0.2234965
##   0.2230823
##   0.2216925
##   0.3029598
##   0.2904517
##   0.2886013
##   0.2801129
##   0.2746964
##   0.2668765
##   0.2613365
##   0.2541868
##   0.2498908
##   0.2451819
##   0.2715232
##   0.2677677
##   0.2638189
##   0.2609887
##   0.2564870
##   0.2535616
##   0.2487105
##   0.2453221
##   0.2430565
##   0.2395595
##   0.2126489
##   0.2157785
##   0.2176785
##   0.2191907
##   0.2211429
##   0.2198740
##   0.2209105
##   0.2190789
##   0.2183579
##   0.2175159
##   0.2805188
##   0.2709842
##   0.2653442
##   0.2597128
##   0.2561171
##   0.2517651
##   0.2440892
##   0.2384797
##   0.2326046
##   0.2266652
##   0.2661990
##   0.2596543
##   0.2570171
##   0.2553022
##   0.2483251
##   0.2470998
##   0.2442995
##   0.2419248
##   0.2374581
##   0.2321846
##   0.2075181
##   0.2153718
##   0.2209196
##   0.2225212
##   0.2194342
##   0.2165793
##   0.2179774
##   0.2174484
##   0.2160250
##   0.2140885
##   0.2715455
##   0.2589597
##   0.2450118
##   0.2340720
##   0.2307871
##   0.2188290
##   0.2122412
##   0.2049275
##   0.2062742
##   0.1980714
##   0.2603267
##   0.2554861
##   0.2475984
##   0.2458624
##   0.2380312
##   0.2342775
##   0.2270984
##   0.2218421
##   0.2065921
##   0.2089739
##   0.2239802
##   0.2128581
##   0.2075894
##   0.2108336
##   0.2036261
##   0.1992301
##   0.1975846
##   0.1895564
##   0.1864055
##   0.1789938
##   0.2420596
##   0.1990901
##   0.1685627
##   0.1571348
##   0.1509498
##   0.1451764
##   0.1467836
##   0.1493281
##   0.1412390
##   0.1390236
##   0.2318060
##   0.2147426
##   0.2030677
##   0.1826870
##   0.1778021
##   0.1701295
##   0.1656909
##   0.1533908
##   0.1545283
##   0.1480472
##   0.1998800
##   0.1901495
##   0.1796980
##   0.1701850
##   0.1609119
##   0.1601579
##   0.1631831
##   0.1564318
##   0.1544755
##   0.1482028
##   0.2310018
##   0.1875826
##   0.1695945
##   0.1589152
##   0.1515917
##   0.1442190
##   0.1366912
##   0.1394292
##   0.1360775
##   0.1393602
##   0.2227512
##   0.1990749
##   0.1851494
##   0.1701563
##   0.1614537
##   0.1555395
##   0.1444392
##   0.1428105
##   0.1344132
##   0.1376585
##   0.2071086
##   0.1879573
##   0.1731068
##   0.1707157
##   0.1690714
##   0.1655083
##   0.1627309
##   0.1587614
##   0.1534124
##   0.1474612
## 
## RMSE was used to select the optimal model using  the smallest value.
## The final values used for the model were n.trees = 200,
##  interaction.depth = 1, shrinkage = 0.01 and n.minobsinnode = 5.
```

```r
gbm.perf(gbmFit1$finalModel)
```

```
## Using OOB method...
```

![](figures/generalized boosted regression models-1.jpeg)<!-- -->

```
## [1] 147
```

```r
ggplot(gbmFit1, nameInStrip = TRUE)
```

![](figures/generalized boosted regression models-2.jpeg)<!-- -->

```r
ggplot(as.data.frame(summary(gbmFit1)),
                  aes(x=var, y=rel.inf))+
  geom_col()
```

![](figures/generalized boosted regression models-3.jpeg)<!-- -->![](figures/generalized boosted regression models-4.jpeg)<!-- -->

```r
## Prediction
predict.gbm1 <- predict(gbmFit1, newdata = extant, n.trees = gbmFit1$bestTune$n.trees)
res$predict.gbm1 <- predict.gbm1

ggplot(res, aes(x=Red.List.status, y=predict.gbm1))+
  geom_boxplot(varwidth=TRUE)+
  scale_y_log10("predicted duration (log ma)")
```

![](figures/generalized boosted regression models-5.jpeg)<!-- -->

```r
#### add to other model results
res2 <- melt(res[,c("Red.List.status", "predict.gam", "predict.rf", 
                    "predict.gbm1")])
```

```
## Using Red.List.status as id variables
```

```r
ggplot(res2, aes(x=Red.List.status, y=value))+
  geom_boxplot(aes(fill=variable))+
  scale_y_log10("predicted duration (log ma)")#+
```

![](figures/generalized boosted regression models-6.jpeg)<!-- -->

```r
#  facet_wrap(~variable)

kruskal.test(res$predict.gbm1, res$Red.List.status)
```

```
## 
## 	Kruskal-Wallis rank sum test
## 
## data:  res$predict.gbm1 and res$Red.List.status
## Kruskal-Wallis chi-squared = 63.483, df = 6, p-value = 8.799e-12
```

```r
pairwise.wilcox.test(res$predict.gbm1, res$Red.List.status, p.adjust.method = "fdr")
```

```
## 
## 	Pairwise comparisons using Wilcoxon rank sum test 
## 
## data:  res$predict.gbm1 and res$Red.List.status 
## 
##    DD    LC      NT    VU    EN    CR   
## LC 0.008 -       -     -     -     -    
## NT 0.243 0.245   -     -     -     -    
## VU 0.560 1.1e-05 0.202 -     -     -    
## EN 1.000 7.9e-05 0.243 0.703 -     -    
## CR 0.840 0.013   0.471 0.840 0.828 -    
## EX 0.840 0.243   0.516 0.560 0.467 0.560
## 
## P value adjustment method: fdr
```


Models are quite immune to overfitting and can also deal with correlations of variables. GBM also handles missing data. GBMs make minimal assumptions about the relationship between predictors and response and prioritize predictive performance over probabilistic inference about the model itself.


# More cross validation, and taxonomic-group level mean bias?
The calibration here can basically be done with any other model as well. For now I am using gbm() as I follow the supplementary material of Finnegan et al. 2015 (Science). 
Assessing the prediction quality is done by using only part of the data to build the model and evaluate it on the remaining data.


Note that the predicted values are always smaller than the observed ones. The reason is likely the skewed response variable. Removing 50\% of the data causes the model to be likely fitted on small duration species only. Using more data on building the model to increase the chance of including a broader variety of the response variable values does not change this however.

### Cross validation bootstrap

```r
size_modelset <- 1/2
fin <- c()
n <- 500
set.seed(346)
interval.range <- 10
interval.size <- 0.5

for(i in 1:n){
  sub <- extinct.imp[sample(seq(1:nrow(extinct.imp)), nrow(extinct.imp)*size_modelset, replace = FALSE),]
  eval <- extinct.imp[-as.numeric(row.names(sub)),]
  gbm.sub <- gbm(ma_range ~ lat_range+gcd+svl+mean_lat+min_lat+abu_cat
                 , data = sub,
                 n.trees=gbmFit1$finalModel$n.trees, 
                 shrinkage = gbmFit1$finalModel$shrinkage,
                 interaction.depth=gbmFit1$finalModel$interaction.depth)
  best.iter.sub <- gbm.perf(gbm.sub, method="OOB", plot.it=FALSE)
  pre <- predict.gbm(gbm.sub, eval, best.iter.sub)
    # manually assign every prediction smaller than 0 to be 0 for technical reasons
  pre[pre<0] <- 0
  
  # group the predicted durations into bins
  g <- findInterval(pre, seq(0, interval.range, interval.size))
  cc <- data.frame(prediction=pre, interval=g, species=eval$species, ma_range=eval$ma_range, order=eval$order)
  
  # now calculate what was the actual observed duration of the species in these bins
  medians_predicted <- tapply(cc$prediction, cc$interval, median)
  m.df <- data.frame(medians_predicted, interval=as.numeric(names(medians_predicted)))
  medians_observed <- tapply(cc$ma_range, cc$interval, median)
  m.df <- data.frame(m.df, medians_observed)
  temp <- merge(cc, m.df, by="interval", all.x=TRUE)
  temp <- data.frame(temp, run=rep(i, nrow(temp)))
  # add interval name
  temp$interval2 <- seq(0, interval.range, interval.size)[temp$interval]
  # save stuff 
  if(i==1){fin <- temp}else{fin <- rbind(fin, temp)}
  # print progress
   if(i %% 10==0) { cat(paste0("iteration: ", i, "\n")) }
} # the bootstrap
```

```
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## iteration: 10
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## iteration: 20
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## iteration: 30
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## iteration: 40
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## iteration: 50
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## iteration: 60
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## iteration: 70
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## iteration: 80
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## iteration: 90
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## iteration: 100
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## iteration: 110
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## iteration: 120
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## iteration: 130
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## iteration: 140
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## iteration: 150
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## iteration: 160
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## iteration: 170
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## iteration: 180
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## iteration: 190
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## iteration: 200
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## iteration: 210
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## iteration: 220
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## iteration: 230
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## iteration: 240
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## iteration: 250
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## iteration: 260
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## iteration: 270
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## iteration: 280
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## iteration: 290
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## iteration: 300
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## iteration: 310
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## iteration: 320
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## iteration: 330
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## iteration: 340
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## iteration: 350
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## iteration: 360
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## iteration: 370
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## iteration: 380
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## iteration: 390
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## iteration: 400
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## iteration: 410
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## iteration: 420
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## iteration: 430
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## iteration: 440
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## iteration: 450
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## iteration: 460
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## iteration: 470
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## iteration: 480
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## iteration: 490
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## Distribution not specified, assuming gaussian ...
## iteration: 500
```

```r
# Add the frequency per interval for weighting the regression:
weights <- data.frame(table(fin$interval2))
fin <- merge(fin, weights, by.x="interval2", by.y="Var1", all.x=TRUE)

# Figure Model calibration 2, supplement of Finnegan et al. 2015 - Paleontological baselines
ggplot(fin[!is.na(fin$order),], aes(x=interval2, y=medians_observed, weight=Freq))+
  geom_point(alpha=1/50)+
#  geom_bin2d()+
  scale_x_continuous("gbm predicted duration (ma)")+
  scale_y_continuous("median observed duration per interval (ma)")+
  geom_smooth()+
  facet_wrap(~order)
```

```
## `geom_smooth()` using method = 'gam'
```

![](figures/gbm cross validation bootstrap-1.jpeg)<!-- -->

```r
ggplot(fin[!is.na(fin$order),], aes(x=prediction, y=ma_range))+
  geom_point(alpha=1/50)+
#  geom_bin2d()+
  scale_x_continuous("gbm predicted duration (ma)")+
  scale_y_continuous("median observed duration per interval (ma)")+
  geom_smooth()+
  facet_wrap(~order)
```

```
## `geom_smooth()` using method = 'gam'
```

![](figures/gbm cross validation bootstrap-2.jpeg)<!-- -->

```r
# Get the taxonomic group level bias for each prediction bin. Take the predicted duration value for a living species from the gbm.predict and extract the empirically observed duration from the gam fit
formula = y ~ s(x, bs = "cs")
gam.boot.salientia <- gam(data=fin[fin$order=="Salientia",], medians_observed~s(interval2, bs="cs"), weights=Freq)
gam.boot.urodela <- gam(data=fin[fin$order=="Urodela",], medians_observed~s(interval2, bs="cs"), weights=Freq)

res$predict.gbm1.anura_correction <-  predict(gam.boot.salientia, data.frame(interval2=res$predict.gbm1))
res$predict.gbm1.caudata_correction <-  predict(gam.boot.urodela, data.frame(interval2=res$predict.gbm1))

# plot the effect
par(mfrow=c(1,2))
plot(res$predict.gbm1.anura_correction[res$order=="ANURA"]~res$predict.gbm1[res$order=="ANURA"],
     xlim=c(0,15), ylim=c(0,50), main="Anura", xlab="gbm duration (ma)", ylab="corrected gbm duration (ma)")
abline(a=0, b=1, lty=2)
plot(res$predict.gbm1.caudata_correction[res$order=="CAUDATA"]~res$predict.gbm1[res$order=="CAUDATA"],
     xlim=c(0,15), ylim=c(0,50), main="Caudata", xlab="gbm duration (ma)", ylab="corrected gbm duration (ma)")
abline(a=0, b=1, lty=2)
```

![](figures/gbm cross validation bootstrap-3.jpeg)<!-- -->

```r
par(mfrow=c(1,1))

# Combine corrected predictions
predict.gbm1.comb <- c()
for(i in 1:nrow(res)){
  if(res$order[i]=="ANURA"){predict.gbm1.comb <- c(predict.gbm1.comb, res$predict.gbm1.anura_correction[i])}else{
    predict.gbm1.comb <- c(predict.gbm1.comb, res$predict.gbm1.caudata_correction[i])
  }
}
res$predict.gbm1.comb <- predict.gbm1.comb
ggplot(res, aes(x=Red.List.status, y=predict.gbm1.comb))+
  geom_boxplot(varwidth=TRUE)+
  scale_y_log10()
```

![](figures/gbm cross validation bootstrap-4.jpeg)<!-- -->

```r
# add to other model results
res2 <- melt(res[,c("Red.List.status", "predict.gam", "predict.rf",
                    "predict.gbm1", "predict.gbm1.comb")])
```

```
## Using Red.List.status as id variables
```

```r
ggplot(res2, aes(x=Red.List.status, y=value))+
  geom_boxplot(aes(fill=variable))+
  scale_fill_discrete(name = "model types")+
  scale_y_log10("predicted duration (log ma)")#+
```

![](figures/gbm cross validation bootstrap-5.jpeg)<!-- -->

```r
#  facet_wrap(~variable)

kruskal.test(res$predict.gbm1.comb, res$Red.List.status)
```

```
## 
## 	Kruskal-Wallis rank sum test
## 
## data:  res$predict.gbm1.comb and res$Red.List.status
## Kruskal-Wallis chi-squared = 25.781, df = 6, p-value = 0.0002445
```

```r
pairwise.wilcox.test(res$predict.gbm1.comb, res$Red.List.status, p.adjust.method = "fdr")
```

```
## 
## 	Pairwise comparisons using Wilcoxon rank sum test 
## 
## data:  res$predict.gbm1.comb and res$Red.List.status 
## 
##    DD     LC     NT     VU     EN     CR    
## LC 0.3892 -      -      -      -      -     
## NT 0.7303 0.8842 -      -      -      -     
## VU 0.7303 0.0758 0.7303 -      -      -     
## EN 1.0000 0.0097 0.5694 0.8278 -      -     
## CR 1.0000 0.3892 0.7303 0.8497 0.8842 -     
## EX 0.8842 0.3892 0.7303 0.7303 0.6667 0.7303
## 
## P value adjustment method: fdr
```



## Phylogenetic bias

```r
ggplot(extinct.raw[!is.na(extinct.raw$order),], aes(x=order, y=ma_range))+
  geom_boxplot()+
  scale_y_continuous("duration (ma)")
```

![](figures/phylogenetic bias-1.jpeg)<!-- -->

```r
pairwise.wilcox.test(extinct.raw$ma_range, extinct.raw$order, p.adjust.method = "fdr")
```

```
## 
## 	Pairwise comparisons using Wilcoxon rank sum test 
## 
## data:  extinct.raw$ma_range and extinct.raw$order 
## 
##               Allocaudata Lepospondyli Parabatrachia Salientia
## Lepospondyli  0.0054      -            -             -        
## Parabatrachia 0.2648      0.6300       -             -        
## Salientia     0.0121      0.2279       0.4586        -        
## Temnospondyli 0.0110      0.2279       0.4586        0.7282   
## Urodela       0.1919      0.0263       0.3896        0.1651   
##               Temnospondyli
## Lepospondyli  -            
## Parabatrachia -            
## Salientia     -            
## Temnospondyli -            
## Urodela       0.0882       
## 
## P value adjustment method: fdr
```
There is a phylogenetic bias on the duration with Allocaudata having longer durations than Lepospondlyi, Salientia and Temnospondyli. Temnospondyli show shorter duations than Urodela. Allocaudata and Urodela seem to have slightly longer durations on average.

### Lissamphibian model

```r
liss.raw <- extinct.imp[extinct.imp$order %in% c("Urodela", "Salientia", "Parabatrachia"),]
nrow(liss.raw)
```

```
## [1] 121
```

```r
liss <- liss.raw[,c("ma_range", "lat_range", "gcd", "svl", "mean_lat",
                 "min_lat", "abu_cat")]

set.seed(825)
gbmFit_liss <- train(ma_range ~ ., data = liss, method = "gbm", 
                 trControl = gbmControl, verbose=FALSE,
                 tuneGrid=gbmGrid)

gbmFit_liss
```

```
## Stochastic Gradient Boosting 
## 
## 121 samples
##   6 predictors
## 
## No pre-processing
## Resampling: Cross-Validated (10 fold, repeated 3 times) 
## Summary of sample sizes: 108, 108, 108, 110, 110, 109, ... 
## Resampling results across tuning parameters:
## 
##   shrinkage  interaction.depth  n.minobsinnode  n.trees  RMSE    
##   0.001      1                   5               50      5.151781
##   0.001      1                   5              100      5.107968
##   0.001      1                   5              150      5.068369
##   0.001      1                   5              200      5.030791
##   0.001      1                   5              250      4.995991
##   0.001      1                   5              300      4.964664
##   0.001      1                   5              350      4.936992
##   0.001      1                   5              400      4.911663
##   0.001      1                   5              450      4.888481
##   0.001      1                   5              500      4.866792
##   0.001      1                  10               50      5.164041
##   0.001      1                  10              100      5.134089
##   0.001      1                  10              150      5.105179
##   0.001      1                  10              200      5.079169
##   0.001      1                  10              250      5.053667
##   0.001      1                  10              300      5.029123
##   0.001      1                  10              350      5.005779
##   0.001      1                  10              400      4.983073
##   0.001      1                  10              450      4.961906
##   0.001      1                  10              500      4.941802
##   0.001      1                  15               50      5.173938
##   0.001      1                  15              100      5.151044
##   0.001      1                  15              150      5.130114
##   0.001      1                  15              200      5.109303
##   0.001      1                  15              250      5.090280
##   0.001      1                  15              300      5.072800
##   0.001      1                  15              350      5.056116
##   0.001      1                  15              400      5.039475
##   0.001      1                  15              450      5.024664
##   0.001      1                  15              500      5.009694
##   0.001      2                   5               50      5.145425
##   0.001      2                   5              100      5.095363
##   0.001      2                   5              150      5.051089
##   0.001      2                   5              200      5.008172
##   0.001      2                   5              250      4.970606
##   0.001      2                   5              300      4.936905
##   0.001      2                   5              350      4.907186
##   0.001      2                   5              400      4.880468
##   0.001      2                   5              450      4.857882
##   0.001      2                   5              500      4.836250
##   0.001      2                  10               50      5.159942
##   0.001      2                  10              100      5.124951
##   0.001      2                  10              150      5.093095
##   0.001      2                  10              200      5.063883
##   0.001      2                  10              250      5.035384
##   0.001      2                  10              300      5.008856
##   0.001      2                  10              350      4.985566
##   0.001      2                  10              400      4.962586
##   0.001      2                  10              450      4.941185
##   0.001      2                  10              500      4.921414
##   0.001      2                  15               50      5.170878
##   0.001      2                  15              100      5.144960
##   0.001      2                  15              150      5.122548
##   0.001      2                  15              200      5.098718
##   0.001      2                  15              250      5.078609
##   0.001      2                  15              300      5.060163
##   0.001      2                  15              350      5.041819
##   0.001      2                  15              400      5.025573
##   0.001      2                  15              450      5.011988
##   0.001      2                  15              500      4.998094
##   0.001      3                   5               50      5.141408
##   0.001      3                   5              100      5.091875
##   0.001      3                   5              150      5.045659
##   0.001      3                   5              200      5.005374
##   0.001      3                   5              250      4.968309
##   0.001      3                   5              300      4.936689
##   0.001      3                   5              350      4.906957
##   0.001      3                   5              400      4.879919
##   0.001      3                   5              450      4.853741
##   0.001      3                   5              500      4.831898
##   0.001      3                  10               50      5.159093
##   0.001      3                  10              100      5.125534
##   0.001      3                  10              150      5.091890
##   0.001      3                  10              200      5.060796
##   0.001      3                  10              250      5.032236
##   0.001      3                  10              300      5.005730
##   0.001      3                  10              350      4.980922
##   0.001      3                  10              400      4.956804
##   0.001      3                  10              450      4.934292
##   0.001      3                  10              500      4.913823
##   0.001      3                  15               50      5.170830
##   0.001      3                  15              100      5.145867
##   0.001      3                  15              150      5.123342
##   0.001      3                  15              200      5.102918
##   0.001      3                  15              250      5.083300
##   0.001      3                  15              300      5.063279
##   0.001      3                  15              350      5.045730
##   0.001      3                  15              400      5.027852
##   0.001      3                  15              450      5.012348
##   0.001      3                  15              500      4.997911
##   0.010      1                   5               50      4.861312
##   0.010      1                   5              100      4.738211
##   0.010      1                   5              150      4.740661
##   0.010      1                   5              200      4.760895
##   0.010      1                   5              250      4.783970
##   0.010      1                   5              300      4.823751
##   0.010      1                   5              350      4.862513
##   0.010      1                   5              400      4.869516
##   0.010      1                   5              450      4.885312
##   0.010      1                   5              500      4.900630
##   0.010      1                  10               50      4.941012
##   0.010      1                  10              100      4.808040
##   0.010      1                  10              150      4.748940
##   0.010      1                  10              200      4.735957
##   0.010      1                  10              250      4.742606
##   0.010      1                  10              300      4.765423
##   0.010      1                  10              350      4.776537
##   0.010      1                  10              400      4.783001
##   0.010      1                  10              450      4.804474
##   0.010      1                  10              500      4.813111
##   0.010      1                  15               50      5.014233
##   0.010      1                  15              100      4.909046
##   0.010      1                  15              150      4.855421
##   0.010      1                  15              200      4.825991
##   0.010      1                  15              250      4.822547
##   0.010      1                  15              300      4.838161
##   0.010      1                  15              350      4.846526
##   0.010      1                  15              400      4.851257
##   0.010      1                  15              450      4.864223
##   0.010      1                  15              500      4.874054
##   0.010      2                   5               50      4.860213
##   0.010      2                   5              100      4.745887
##   0.010      2                   5              150      4.716490
##   0.010      2                   5              200      4.728285
##   0.010      2                   5              250      4.734519
##   0.010      2                   5              300      4.761183
##   0.010      2                   5              350      4.771590
##   0.010      2                   5              400      4.783801
##   0.010      2                   5              450      4.808675
##   0.010      2                   5              500      4.824164
##   0.010      2                  10               50      4.930533
##   0.010      2                  10              100      4.800334
##   0.010      2                  10              150      4.741220
##   0.010      2                  10              200      4.720221
##   0.010      2                  10              250      4.723171
##   0.010      2                  10              300      4.737065
##   0.010      2                  10              350      4.731882
##   0.010      2                  10              400      4.739559
##   0.010      2                  10              450      4.749299
##   0.010      2                  10              500      4.752391
##   0.010      2                  15               50      4.998283
##   0.010      2                  15              100      4.895648
##   0.010      2                  15              150      4.844153
##   0.010      2                  15              200      4.814364
##   0.010      2                  15              250      4.799589
##   0.010      2                  15              300      4.804031
##   0.010      2                  15              350      4.806028
##   0.010      2                  15              400      4.811370
##   0.010      2                  15              450      4.821339
##   0.010      2                  15              500      4.840264
##   0.010      3                   5               50      4.832440
##   0.010      3                   5              100      4.717958
##   0.010      3                   5              150      4.701030
##   0.010      3                   5              200      4.716896
##   0.010      3                   5              250      4.741200
##   0.010      3                   5              300      4.766031
##   0.010      3                   5              350      4.782086
##   0.010      3                   5              400      4.804911
##   0.010      3                   5              450      4.821026
##   0.010      3                   5              500      4.832670
##   0.010      3                  10               50      4.924781
##   0.010      3                  10              100      4.786709
##   0.010      3                  10              150      4.736473
##   0.010      3                  10              200      4.724077
##   0.010      3                  10              250      4.715710
##   0.010      3                  10              300      4.719808
##   0.010      3                  10              350      4.731117
##   0.010      3                  10              400      4.744784
##   0.010      3                  10              450      4.745655
##   0.010      3                  10              500      4.756951
##   0.010      3                  15               50      5.001787
##   0.010      3                  15              100      4.897473
##   0.010      3                  15              150      4.851526
##   0.010      3                  15              200      4.817320
##   0.010      3                  15              250      4.809136
##   0.010      3                  15              300      4.809461
##   0.010      3                  15              350      4.801007
##   0.010      3                  15              400      4.799350
##   0.010      3                  15              450      4.816406
##   0.010      3                  15              500      4.814972
##   0.100      1                   5               50      4.913033
##   0.100      1                   5              100      5.025342
##   0.100      1                   5              150      5.217527
##   0.100      1                   5              200      5.200649
##   0.100      1                   5              250      5.273530
##   0.100      1                   5              300      5.322692
##   0.100      1                   5              350      5.451695
##   0.100      1                   5              400      5.477491
##   0.100      1                   5              450      5.530602
##   0.100      1                   5              500      5.574798
##   0.100      1                  10               50      4.833781
##   0.100      1                  10              100      4.859547
##   0.100      1                  10              150      4.956792
##   0.100      1                  10              200      4.971221
##   0.100      1                  10              250      4.985527
##   0.100      1                  10              300      5.077689
##   0.100      1                  10              350      5.095698
##   0.100      1                  10              400      5.133362
##   0.100      1                  10              450      5.174534
##   0.100      1                  10              500      5.223511
##   0.100      1                  15               50      4.922724
##   0.100      1                  15              100      4.984202
##   0.100      1                  15              150      5.013982
##   0.100      1                  15              200      5.013035
##   0.100      1                  15              250      5.109897
##   0.100      1                  15              300      5.170597
##   0.100      1                  15              350      5.201405
##   0.100      1                  15              400      5.222074
##   0.100      1                  15              450      5.269003
##   0.100      1                  15              500      5.309133
##   0.100      2                   5               50      4.852773
##   0.100      2                   5              100      4.951709
##   0.100      2                   5              150      5.034978
##   0.100      2                   5              200      5.154728
##   0.100      2                   5              250      5.298801
##   0.100      2                   5              300      5.433460
##   0.100      2                   5              350      5.498272
##   0.100      2                   5              400      5.529705
##   0.100      2                   5              450      5.638165
##   0.100      2                   5              500      5.699677
##   0.100      2                  10               50      4.862900
##   0.100      2                  10              100      4.959724
##   0.100      2                  10              150      5.048410
##   0.100      2                  10              200      5.095885
##   0.100      2                  10              250      5.122081
##   0.100      2                  10              300      5.199953
##   0.100      2                  10              350      5.278523
##   0.100      2                  10              400      5.319562
##   0.100      2                  10              450      5.368004
##   0.100      2                  10              500      5.389978
##   0.100      2                  15               50      4.827060
##   0.100      2                  15              100      4.980601
##   0.100      2                  15              150      5.043596
##   0.100      2                  15              200      5.120451
##   0.100      2                  15              250      5.203814
##   0.100      2                  15              300      5.284726
##   0.100      2                  15              350      5.292331
##   0.100      2                  15              400      5.312455
##   0.100      2                  15              450      5.370310
##   0.100      2                  15              500      5.384013
##   0.100      3                   5               50      4.918106
##   0.100      3                   5              100      5.041806
##   0.100      3                   5              150      5.064491
##   0.100      3                   5              200      5.201781
##   0.100      3                   5              250      5.323136
##   0.100      3                   5              300      5.412534
##   0.100      3                   5              350      5.481882
##   0.100      3                   5              400      5.566936
##   0.100      3                   5              450      5.638158
##   0.100      3                   5              500      5.673085
##   0.100      3                  10               50      4.797438
##   0.100      3                  10              100      4.932378
##   0.100      3                  10              150      5.094742
##   0.100      3                  10              200      5.183312
##   0.100      3                  10              250      5.293177
##   0.100      3                  10              300      5.391055
##   0.100      3                  10              350      5.454896
##   0.100      3                  10              400      5.521141
##   0.100      3                  10              450      5.507500
##   0.100      3                  10              500      5.552724
##   0.100      3                  15               50      4.890675
##   0.100      3                  15              100      5.017776
##   0.100      3                  15              150      5.040664
##   0.100      3                  15              200      5.117249
##   0.100      3                  15              250      5.144499
##   0.100      3                  15              300      5.181790
##   0.100      3                  15              350      5.185292
##   0.100      3                  15              400      5.223517
##   0.100      3                  15              450      5.265624
##   0.100      3                  15              500      5.316793
##   Rsquared 
##   0.2786453
##   0.2822754
##   0.2805006
##   0.2813157
##   0.2791320
##   0.2773037
##   0.2782897
##   0.2792016
##   0.2804056
##   0.2818172
##   0.2471336
##   0.2465684
##   0.2526887
##   0.2537531
##   0.2566063
##   0.2572989
##   0.2585141
##   0.2618709
##   0.2622631
##   0.2637153
##   0.1969870
##   0.2040778
##   0.2016339
##   0.1998287
##   0.2001326
##   0.2007236
##   0.2034685
##   0.2056350
##   0.2065992
##   0.2098293
##   0.2764593
##   0.2848740
##   0.2823923
##   0.2842986
##   0.2851640
##   0.2857702
##   0.2862315
##   0.2853684
##   0.2842109
##   0.2836630
##   0.2577675
##   0.2556485
##   0.2520172
##   0.2526104
##   0.2545183
##   0.2556343
##   0.2563782
##   0.2586403
##   0.2593021
##   0.2613476
##   0.1839958
##   0.1912919
##   0.1930255
##   0.2001395
##   0.2036263
##   0.2058953
##   0.2062418
##   0.2074846
##   0.2080675
##   0.2107667
##   0.2808200
##   0.2846831
##   0.2876435
##   0.2888865
##   0.2876261
##   0.2874236
##   0.2864676
##   0.2872292
##   0.2898833
##   0.2900394
##   0.2509143
##   0.2532347
##   0.2562736
##   0.2587174
##   0.2609908
##   0.2613401
##   0.2639028
##   0.2652213
##   0.2672041
##   0.2678067
##   0.1889903
##   0.1931657
##   0.1934100
##   0.1933166
##   0.1954602
##   0.1989340
##   0.2013627
##   0.2047790
##   0.2063582
##   0.2090916
##   0.2678154
##   0.2739213
##   0.2769547
##   0.2825305
##   0.2878954
##   0.2896751
##   0.2863023
##   0.2864538
##   0.2862314
##   0.2847848
##   0.2584944
##   0.2689950
##   0.2756727
##   0.2784629
##   0.2818567
##   0.2816714
##   0.2829859
##   0.2854902
##   0.2840921
##   0.2848236
##   0.2061658
##   0.2186377
##   0.2283102
##   0.2382400
##   0.2433218
##   0.2447354
##   0.2455004
##   0.2470624
##   0.2479503
##   0.2479255
##   0.2723209
##   0.2782710
##   0.2844303
##   0.2931153
##   0.2956367
##   0.2962065
##   0.2983867
##   0.3004706
##   0.3000281
##   0.2991272
##   0.2575880
##   0.2733246
##   0.2856368
##   0.2898165
##   0.2899853
##   0.2951204
##   0.3039890
##   0.3072270
##   0.3106152
##   0.3144648
##   0.1962389
##   0.2233355
##   0.2349642
##   0.2425643
##   0.2486327
##   0.2523321
##   0.2572704
##   0.2620728
##   0.2655851
##   0.2655584
##   0.2972343
##   0.2987308
##   0.3000251
##   0.3053635
##   0.3061305
##   0.3035629
##   0.3077148
##   0.3089102
##   0.3112473
##   0.3088799
##   0.2582663
##   0.2674289
##   0.2758022
##   0.2819030
##   0.2895013
##   0.2964653
##   0.2993704
##   0.2993121
##   0.3023343
##   0.3087198
##   0.2113519
##   0.2258153
##   0.2376906
##   0.2475041
##   0.2507195
##   0.2531050
##   0.2620631
##   0.2673363
##   0.2692835
##   0.2708677
##   0.2925212
##   0.2910958
##   0.2832950
##   0.2724639
##   0.2604291
##   0.2601216
##   0.2552230
##   0.2486623
##   0.2472989
##   0.2460392
##   0.2996974
##   0.2898294
##   0.2866503
##   0.2840631
##   0.2824861
##   0.2760173
##   0.2734527
##   0.2693185
##   0.2602657
##   0.2575669
##   0.2398565
##   0.2537690
##   0.2576777
##   0.2597334
##   0.2584729
##   0.2554245
##   0.2531780
##   0.2603263
##   0.2574556
##   0.2481711
##   0.3017983
##   0.3143584
##   0.2991984
##   0.3087664
##   0.2955082
##   0.2925052
##   0.2900922
##   0.2798038
##   0.2748530
##   0.2734029
##   0.2934689
##   0.3139942
##   0.3167194
##   0.3210059
##   0.3179900
##   0.3104208
##   0.3104080
##   0.3098007
##   0.3096956
##   0.3058195
##   0.2627498
##   0.2661142
##   0.2582158
##   0.2625875
##   0.2599190
##   0.2687975
##   0.2595283
##   0.2664485
##   0.2592477
##   0.2620232
##   0.2998517
##   0.3009830
##   0.2993425
##   0.2887229
##   0.2870826
##   0.2880649
##   0.2999639
##   0.2876219
##   0.2842539
##   0.2820203
##   0.3157800
##   0.3057288
##   0.2995754
##   0.2881220
##   0.2875959
##   0.2827975
##   0.2803524
##   0.2701823
##   0.2757406
##   0.2778902
##   0.2682670
##   0.2667121
##   0.2687449
##   0.2804388
##   0.2854356
##   0.2802373
##   0.2889976
##   0.2896011
##   0.2902973
##   0.2853463
## 
## RMSE was used to select the optimal model using  the smallest value.
## The final values used for the model were n.trees = 150,
##  interaction.depth = 3, shrinkage = 0.01 and n.minobsinnode = 5.
```

```r
gbm.perf(gbmFit_liss$finalModel)
```

```
## Using OOB method...
```

![](figures/lissamphibia-1.jpeg)<!-- -->

```
## [1] 81
```

```r
ggplot(gbmFit_liss, nameInStrip = TRUE)
```

![](figures/lissamphibia-2.jpeg)<!-- -->

```r
ggplot(as.data.frame(summary(gbmFit_liss)),
                  aes(x=var, y=rel.inf))+
  geom_col()
```

![](figures/lissamphibia-3.jpeg)<!-- -->![](figures/lissamphibia-4.jpeg)<!-- -->

```r
## Prediction
predict.gbm.liss <- predict(gbmFit_liss, newdata = extant, n.trees = gbmFit_liss$bestTune$n.trees)
res$predict.gbm.liss <- predict.gbm.liss

res2 <- melt(res[,c("Red.List.status", "predict.gam", "predict.rf",
                    "predict.gbm1", "predict.gbm1.comb", "predict.gbm.liss")])
```

```
## Using Red.List.status as id variables
```

```r
ggplot(res2, aes(x=Red.List.status, y=value))+
  geom_boxplot(aes(fill=variable))+
  scale_fill_discrete(name = "model types")+
  scale_y_log10("predicted duration (log ma)")+
  facet_wrap(~variable)
```

![](figures/lissamphibia-5.jpeg)<!-- -->

```r
kruskal.test(res$predict.gbm.liss, res$Red.List.status)
```

```
## 
## 	Kruskal-Wallis rank sum test
## 
## data:  res$predict.gbm.liss and res$Red.List.status
## Kruskal-Wallis chi-squared = 63.91, df = 6, p-value = 7.202e-12
```

```r
pairwise.wilcox.test(res$predict.gbm.liss, res$Red.List.status, p.adjust.method = "fdr")
```

```
## 
## 	Pairwise comparisons using Wilcoxon rank sum test 
## 
## data:  res$predict.gbm.liss and res$Red.List.status 
## 
##    DD     LC      NT     VU     EN     CR    
## LC 0.0071 -       -      -      -      -     
## NT 0.0499 0.8889  -      -      -      -     
## VU 0.2039 1.3e-05 0.0424 -      -      -     
## EN 0.5147 3.8e-05 0.0255 0.2039 -      -     
## CR 0.3231 0.0083  0.0658 0.2039 0.8889 -     
## EX 0.8889 0.2039  0.4422 0.7372 0.8889 0.8889
## 
## P value adjustment method: fdr
```


```r
set.seed(825)
imp_hab <- merge(extinct.imp, extinct.raw[,c("species", "hab.cat.b")])
imp_hab <- imp_hab[,c("ma_range", "lat_range", "gcd", "svl", "mean_lat", "min_lat", "abu_cat", "hab.cat.b" )]
gbmFit_hab <- train(ma_range ~ ., data = imp_hab, method = "gbm", 
                 trControl = gbmControl, verbose=FALSE,
                 tuneGrid=gbmGrid)

gbmFit_hab
```

```
## Stochastic Gradient Boosting 
## 
## 354 samples
##   7 predictors
## 
## No pre-processing
## Resampling: Cross-Validated (10 fold, repeated 3 times) 
## Summary of sample sizes: 319, 318, 318, 319, 319, 318, ... 
## Resampling results across tuning parameters:
## 
##   shrinkage  interaction.depth  n.minobsinnode  n.trees  RMSE    
##   0.001      1                   5               50      5.605163
##   0.001      1                   5              100      5.559504
##   0.001      1                   5              150      5.517887
##   0.001      1                   5              200      5.480424
##   0.001      1                   5              250      5.447939
##   0.001      1                   5              300      5.416948
##   0.001      1                   5              350      5.387911
##   0.001      1                   5              400      5.362534
##   0.001      1                   5              450      5.338538
##   0.001      1                   5              500      5.316795
##   0.001      1                  10               50      5.612777
##   0.001      1                  10              100      5.574116
##   0.001      1                  10              150      5.537643
##   0.001      1                  10              200      5.505340
##   0.001      1                  10              250      5.475589
##   0.001      1                  10              300      5.448679
##   0.001      1                  10              350      5.422966
##   0.001      1                  10              400      5.399351
##   0.001      1                  10              450      5.377952
##   0.001      1                  10              500      5.358083
##   0.001      1                  15               50      5.626029
##   0.001      1                  15              100      5.599746
##   0.001      1                  15              150      5.575535
##   0.001      1                  15              200      5.553771
##   0.001      1                  15              250      5.533101
##   0.001      1                  15              300      5.512147
##   0.001      1                  15              350      5.492921
##   0.001      1                  15              400      5.476074
##   0.001      1                  15              450      5.460346
##   0.001      1                  15              500      5.444898
##   0.001      2                   5               50      5.602192
##   0.001      2                   5              100      5.555219
##   0.001      2                   5              150      5.511059
##   0.001      2                   5              200      5.471470
##   0.001      2                   5              250      5.435659
##   0.001      2                   5              300      5.402356
##   0.001      2                   5              350      5.372529
##   0.001      2                   5              400      5.344509
##   0.001      2                   5              450      5.320823
##   0.001      2                   5              500      5.299035
##   0.001      2                  10               50      5.611456
##   0.001      2                  10              100      5.571741
##   0.001      2                  10              150      5.535512
##   0.001      2                  10              200      5.501792
##   0.001      2                  10              250      5.470981
##   0.001      2                  10              300      5.442272
##   0.001      2                  10              350      5.415457
##   0.001      2                  10              400      5.391254
##   0.001      2                  10              450      5.369275
##   0.001      2                  10              500      5.348507
##   0.001      2                  15               50      5.624352
##   0.001      2                  15              100      5.596758
##   0.001      2                  15              150      5.570099
##   0.001      2                  15              200      5.545543
##   0.001      2                  15              250      5.523423
##   0.001      2                  15              300      5.502081
##   0.001      2                  15              350      5.482876
##   0.001      2                  15              400      5.465092
##   0.001      2                  15              450      5.448006
##   0.001      2                  15              500      5.431794
##   0.001      3                   5               50      5.599824
##   0.001      3                   5              100      5.551304
##   0.001      3                   5              150      5.507052
##   0.001      3                   5              200      5.464277
##   0.001      3                   5              250      5.426078
##   0.001      3                   5              300      5.393428
##   0.001      3                   5              350      5.363584
##   0.001      3                   5              400      5.335318
##   0.001      3                   5              450      5.309232
##   0.001      3                   5              500      5.288563
##   0.001      3                  10               50      5.610961
##   0.001      3                  10              100      5.571066
##   0.001      3                  10              150      5.532323
##   0.001      3                  10              200      5.498252
##   0.001      3                  10              250      5.466515
##   0.001      3                  10              300      5.437366
##   0.001      3                  10              350      5.410505
##   0.001      3                  10              400      5.385918
##   0.001      3                  10              450      5.362692
##   0.001      3                  10              500      5.342800
##   0.001      3                  15               50      5.622856
##   0.001      3                  15              100      5.592679
##   0.001      3                  15              150      5.565219
##   0.001      3                  15              200      5.539706
##   0.001      3                  15              250      5.515555
##   0.001      3                  15              300      5.493870
##   0.001      3                  15              350      5.474203
##   0.001      3                  15              400      5.455888
##   0.001      3                  15              450      5.438969
##   0.001      3                  15              500      5.422554
##   0.010      1                   5               50      5.323232
##   0.010      1                   5              100      5.186959
##   0.010      1                   5              150      5.129842
##   0.010      1                   5              200      5.112785
##   0.010      1                   5              250      5.120309
##   0.010      1                   5              300      5.134248
##   0.010      1                   5              350      5.149328
##   0.010      1                   5              400      5.164966
##   0.010      1                   5              450      5.181728
##   0.010      1                   5              500      5.191003
##   0.010      1                  10               50      5.363194
##   0.010      1                  10              100      5.221903
##   0.010      1                  10              150      5.156792
##   0.010      1                  10              200      5.127921
##   0.010      1                  10              250      5.117725
##   0.010      1                  10              300      5.113775
##   0.010      1                  10              350      5.120028
##   0.010      1                  10              400      5.127875
##   0.010      1                  10              450      5.131879
##   0.010      1                  10              500      5.133791
##   0.010      1                  15               50      5.444677
##   0.010      1                  15              100      5.338901
##   0.010      1                  15              150      5.289694
##   0.010      1                  15              200      5.274762
##   0.010      1                  15              250      5.267702
##   0.010      1                  15              300      5.263386
##   0.010      1                  15              350      5.264545
##   0.010      1                  15              400      5.265713
##   0.010      1                  15              450      5.266504
##   0.010      1                  15              500      5.273438
##   0.010      2                   5               50      5.300814
##   0.010      2                   5              100      5.167023
##   0.010      2                   5              150      5.129743
##   0.010      2                   5              200      5.143117
##   0.010      2                   5              250      5.158925
##   0.010      2                   5              300      5.182760
##   0.010      2                   5              350      5.214140
##   0.010      2                   5              400      5.238969
##   0.010      2                   5              450      5.260239
##   0.010      2                   5              500      5.283319
##   0.010      2                  10               50      5.339463
##   0.010      2                  10              100      5.213372
##   0.010      2                  10              150      5.160871
##   0.010      2                  10              200      5.147382
##   0.010      2                  10              250      5.160231
##   0.010      2                  10              300      5.171138
##   0.010      2                  10              350      5.183503
##   0.010      2                  10              400      5.196990
##   0.010      2                  10              450      5.208051
##   0.010      2                  10              500      5.224178
##   0.010      2                  15               50      5.431832
##   0.010      2                  15              100      5.332827
##   0.010      2                  15              150      5.287918
##   0.010      2                  15              200      5.267178
##   0.010      2                  15              250      5.259539
##   0.010      2                  15              300      5.261817
##   0.010      2                  15              350      5.263961
##   0.010      2                  15              400      5.271929
##   0.010      2                  15              450      5.282084
##   0.010      2                  15              500      5.282646
##   0.010      3                   5               50      5.298414
##   0.010      3                   5              100      5.176340
##   0.010      3                   5              150      5.164396
##   0.010      3                   5              200      5.182729
##   0.010      3                   5              250      5.207789
##   0.010      3                   5              300      5.238485
##   0.010      3                   5              350      5.269755
##   0.010      3                   5              400      5.293268
##   0.010      3                   5              450      5.324984
##   0.010      3                   5              500      5.346960
##   0.010      3                  10               50      5.335110
##   0.010      3                  10              100      5.206848
##   0.010      3                  10              150      5.156849
##   0.010      3                  10              200      5.144447
##   0.010      3                  10              250      5.161603
##   0.010      3                  10              300      5.168500
##   0.010      3                  10              350      5.179994
##   0.010      3                  10              400      5.196497
##   0.010      3                  10              450      5.214380
##   0.010      3                  10              500      5.244145
##   0.010      3                  15               50      5.421342
##   0.010      3                  15              100      5.310530
##   0.010      3                  15              150      5.259723
##   0.010      3                  15              200      5.240158
##   0.010      3                  15              250      5.242925
##   0.010      3                  15              300      5.247125
##   0.010      3                  15              350      5.250150
##   0.010      3                  15              400      5.257202
##   0.010      3                  15              450      5.269672
##   0.010      3                  15              500      5.280879
##   0.100      1                   5               50      5.201527
##   0.100      1                   5              100      5.255496
##   0.100      1                   5              150      5.294519
##   0.100      1                   5              200      5.374560
##   0.100      1                   5              250      5.381212
##   0.100      1                   5              300      5.429862
##   0.100      1                   5              350      5.468132
##   0.100      1                   5              400      5.486696
##   0.100      1                   5              450      5.492513
##   0.100      1                   5              500      5.528030
##   0.100      1                  10               50      5.149115
##   0.100      1                  10              100      5.180571
##   0.100      1                  10              150      5.221645
##   0.100      1                  10              200      5.261281
##   0.100      1                  10              250      5.293670
##   0.100      1                  10              300      5.310706
##   0.100      1                  10              350      5.346239
##   0.100      1                  10              400      5.373618
##   0.100      1                  10              450      5.425299
##   0.100      1                  10              500      5.450878
##   0.100      1                  15               50      5.294678
##   0.100      1                  15              100      5.309037
##   0.100      1                  15              150      5.324599
##   0.100      1                  15              200      5.344473
##   0.100      1                  15              250      5.374798
##   0.100      1                  15              300      5.410142
##   0.100      1                  15              350      5.411980
##   0.100      1                  15              400      5.457357
##   0.100      1                  15              450      5.491405
##   0.100      1                  15              500      5.517198
##   0.100      2                   5               50      5.351524
##   0.100      2                   5              100      5.552493
##   0.100      2                   5              150      5.712973
##   0.100      2                   5              200      5.834899
##   0.100      2                   5              250      5.890772
##   0.100      2                   5              300      5.976743
##   0.100      2                   5              350      6.015216
##   0.100      2                   5              400      6.032528
##   0.100      2                   5              450      6.060531
##   0.100      2                   5              500      6.097030
##   0.100      2                  10               50      5.278378
##   0.100      2                  10              100      5.398376
##   0.100      2                  10              150      5.474753
##   0.100      2                  10              200      5.559575
##   0.100      2                  10              250      5.637967
##   0.100      2                  10              300      5.709138
##   0.100      2                  10              350      5.746668
##   0.100      2                  10              400      5.801759
##   0.100      2                  10              450      5.822843
##   0.100      2                  10              500      5.894364
##   0.100      2                  15               50      5.315347
##   0.100      2                  15              100      5.376382
##   0.100      2                  15              150      5.454999
##   0.100      2                  15              200      5.527174
##   0.100      2                  15              250      5.615044
##   0.100      2                  15              300      5.632799
##   0.100      2                  15              350      5.676379
##   0.100      2                  15              400      5.734682
##   0.100      2                  15              450      5.741054
##   0.100      2                  15              500      5.778122
##   0.100      3                   5               50      5.337677
##   0.100      3                   5              100      5.586837
##   0.100      3                   5              150      5.766124
##   0.100      3                   5              200      5.878348
##   0.100      3                   5              250      5.951234
##   0.100      3                   5              300      6.003656
##   0.100      3                   5              350      6.050870
##   0.100      3                   5              400      6.097294
##   0.100      3                   5              450      6.119800
##   0.100      3                   5              500      6.145311
##   0.100      3                  10               50      5.282722
##   0.100      3                  10              100      5.434540
##   0.100      3                  10              150      5.572347
##   0.100      3                  10              200      5.618117
##   0.100      3                  10              250      5.705222
##   0.100      3                  10              300      5.784528
##   0.100      3                  10              350      5.866490
##   0.100      3                  10              400      5.911005
##   0.100      3                  10              450      5.979297
##   0.100      3                  10              500      6.004153
##   0.100      3                  15               50      5.318337
##   0.100      3                  15              100      5.439142
##   0.100      3                  15              150      5.526364
##   0.100      3                  15              200      5.595986
##   0.100      3                  15              250      5.639064
##   0.100      3                  15              300      5.691669
##   0.100      3                  15              350      5.725899
##   0.100      3                  15              400      5.772600
##   0.100      3                  15              450      5.806203
##   0.100      3                  15              500      5.865374
##   Rsquared 
##   0.3059685
##   0.3056031
##   0.3095421
##   0.3082412
##   0.3062405
##   0.3028897
##   0.3027492
##   0.3038451
##   0.3061993
##   0.3054709
##   0.3032433
##   0.3058050
##   0.3065745
##   0.3041834
##   0.3014848
##   0.3007610
##   0.2995933
##   0.2982148
##   0.2963851
##   0.2970075
##   0.2390777
##   0.2389329
##   0.2378706
##   0.2348303
##   0.2331379
##   0.2342226
##   0.2349928
##   0.2353141
##   0.2344316
##   0.2343090
##   0.3012445
##   0.3042470
##   0.3100356
##   0.3095573
##   0.3044599
##   0.3030340
##   0.3010886
##   0.3007620
##   0.2995461
##   0.2981395
##   0.2720910
##   0.2724052
##   0.2721533
##   0.2737564
##   0.2737238
##   0.2733374
##   0.2737774
##   0.2729440
##   0.2723768
##   0.2722583
##   0.2134374
##   0.2096255
##   0.2115502
##   0.2125762
##   0.2108901
##   0.2107922
##   0.2106151
##   0.2107589
##   0.2121153
##   0.2134339
##   0.3003477
##   0.2965936
##   0.2930094
##   0.2964202
##   0.2952123
##   0.2928212
##   0.2932187
##   0.2929428
##   0.2933826
##   0.2923722
##   0.2619106
##   0.2657316
##   0.2676112
##   0.2660926
##   0.2658905
##   0.2666172
##   0.2648952
##   0.2640021
##   0.2638337
##   0.2636530
##   0.2044418
##   0.2095795
##   0.2110004
##   0.2122665
##   0.2128904
##   0.2122216
##   0.2119818
##   0.2111982
##   0.2113510
##   0.2117784
##   0.2950521
##   0.2941720
##   0.2929474
##   0.2898887
##   0.2869646
##   0.2841895
##   0.2807267
##   0.2776831
##   0.2747801
##   0.2728238
##   0.2952855
##   0.2913659
##   0.2802452
##   0.2770133
##   0.2742351
##   0.2763950
##   0.2765226
##   0.2732178
##   0.2728803
##   0.2723797
##   0.2319421
##   0.2307905
##   0.2275726
##   0.2246793
##   0.2252480
##   0.2255488
##   0.2263503
##   0.2273059
##   0.2276754
##   0.2263779
##   0.3027966
##   0.2908982
##   0.2888779
##   0.2802556
##   0.2746435
##   0.2676821
##   0.2618746
##   0.2556103
##   0.2516703
##   0.2471766
##   0.2738624
##   0.2713927
##   0.2676603
##   0.2643038
##   0.2602503
##   0.2576256
##   0.2537091
##   0.2507930
##   0.2490158
##   0.2450490
##   0.2140951
##   0.2168394
##   0.2194757
##   0.2211403
##   0.2234371
##   0.2220537
##   0.2227854
##   0.2212386
##   0.2200104
##   0.2197052
##   0.2819083
##   0.2729362
##   0.2671399
##   0.2602956
##   0.2554639
##   0.2523192
##   0.2451145
##   0.2415175
##   0.2361859
##   0.2306676
##   0.2668473
##   0.2629292
##   0.2617718
##   0.2615909
##   0.2549201
##   0.2536894
##   0.2525864
##   0.2496718
##   0.2470184
##   0.2407330
##   0.2083260
##   0.2173507
##   0.2235045
##   0.2242551
##   0.2221459
##   0.2195779
##   0.2213224
##   0.2218880
##   0.2199737
##   0.2183616
##   0.2745810
##   0.2636899
##   0.2538550
##   0.2385598
##   0.2350176
##   0.2269300
##   0.2155330
##   0.2096149
##   0.2105223
##   0.2020019
##   0.2691288
##   0.2665893
##   0.2577707
##   0.2572391
##   0.2527549
##   0.2464777
##   0.2405639
##   0.2360151
##   0.2235289
##   0.2222290
##   0.2289863
##   0.2188862
##   0.2128536
##   0.2163770
##   0.2085629
##   0.2034973
##   0.2022218
##   0.1959913
##   0.1927569
##   0.1847960
##   0.2386095
##   0.2032353
##   0.1839932
##   0.1651187
##   0.1588529
##   0.1546551
##   0.1501971
##   0.1539590
##   0.1476079
##   0.1438109
##   0.2325431
##   0.2195439
##   0.2093069
##   0.1917493
##   0.1901441
##   0.1753847
##   0.1769018
##   0.1665910
##   0.1614939
##   0.1520044
##   0.2081302
##   0.2014106
##   0.1886900
##   0.1767034
##   0.1676554
##   0.1700500
##   0.1719420
##   0.1641129
##   0.1624161
##   0.1574329
##   0.2266454
##   0.1852466
##   0.1651925
##   0.1507261
##   0.1423358
##   0.1363996
##   0.1330362
##   0.1312701
##   0.1293438
##   0.1276362
##   0.2362824
##   0.2093548
##   0.1990572
##   0.1868939
##   0.1791607
##   0.1692357
##   0.1600479
##   0.1566061
##   0.1481947
##   0.1497112
##   0.2082098
##   0.1976506
##   0.1860141
##   0.1818220
##   0.1756808
##   0.1753356
##   0.1730554
##   0.1676218
##   0.1612181
##   0.1555158
## 
## RMSE was used to select the optimal model using  the smallest value.
## The final values used for the model were n.trees = 200,
##  interaction.depth = 1, shrinkage = 0.01 and n.minobsinnode = 5.
```

```r
ggplot(as.data.frame(summary(gbmFit_hab)),
                  aes(x=var, y=rel.inf))+
  geom_col()
```

![](figures/habitat model-1.jpeg)<!-- -->![](figures/habitat model-2.jpeg)<!-- -->



```r
# remember to set resamples="final" in the fitControl
resamps <- resamples(list(GBM = gbmFit1,
                          GBM_LISS = gbmFit_liss,
                          RF = rfFit1,
                          GBM_HAB = gbmFit_hab))
summary(resamps)
ggplot(data.frame)
bwplot(resamps, layout = c(2, 1))
# transform to ggplot

difValues <- diff(resamps)
difValues

summary(difValues)
bwplot(difValues, layout = c(2, 1))

gbmFit1$results[which.min(gbmFit1$results$RMSE),]
gbmFit_liss$results[which.min(gbmFit_liss$results$RMSE),]
gbmFit_hab$results[which.min(gbmFit_hab$results$RMSE),]
rfFit1$results[which.min(rfFit1$results$RMSE),]
```




## Null model
Our null hypothesis is that we expect no connection between traits and extinction risk. A null model should represent a fit to a random dataset. However, the dataset does not have to be entirely random as this would create species trait combinations that do not make sense (being very rare but extreme widely distributed), just random for the response variable "duration". 


```r
null.data <- imp

set.seed(2)
null.data$ma_range <- sample(null.data$ma_range, replace=FALSE)
  #rnorm(nrow(null.data), mean=mean(extinct$ma_range), sd=sd(extinct$ma_range))
gbm.null <- gbm(data=null.data, log(ma_range+1) ~  lat_range + gcd + svl + mean_lat
                      + min_lat + hab.cat.b + abu_cat, n.trees=n.trees, 
                 shrinkage = shrinkage, interaction.depth=interaction.depth)
summary(gbm.null)

## Prediction
predict.gbm.null <- predict(gbm.null, newdata = extant, best.iter)
res$predict.gbm.null <- predict.gbm.null
(gbm.null <- ggplot(res, aes(x=Red.List.status, y=predict.gbm.null))+
  geom_boxplot(varwidth=TRUE)+
  scale_y_log10()+
  theme_classic())


#### add to other model results
res2 <- melt(res[,c("Red.List.status", "fit", "predict.gam1", "predict.gam.poisson",
                    "predict.gam.nb", "predict.rf1", "predict.rf2", "predict.gam1.imp",
                    "predict.gam.comb", "predict.gbm1", "predict.gbm.poisson", "predict.gbm1.comb",
                    "predict.gbm.null")])
ggplot(res2, aes(x=Red.List.status, y=value))+
  geom_boxplot(aes(fill=variable))+
  scale_y_log10()+
  theme_classic()+
  facet_wrap(~variable)

kruskal.test(res$predict.gbm.null, res$Red.List.status)
pairwise.wilcox.test(res$predict.gbm.null, res$Red.List.status, p.adjust.method = "fdr")

# Bootstrap
store_kw <- c()
store_median <- matrix(ncol=8, nrow=500)
for(i in 1:500){
  null.data <- extinct
  null.data$ma_range <- sample(null.data$ma_range, replace=FALSE)
  gbm.null.boot <- gbm(data=null.data, log(ma_range+1) ~  lat_range + gcd + svl + mean_lat
                      + min_lat + hab.cat.b + abu_cat, n.trees=100, 
                 shrinkage = shrinkage, interaction.depth=interaction.depth)
  predict.gbm.null.boot <- predict(gbm.null.boot, newdata = extant, n.trees=100)#
  temp <- data.frame(prediction=predict.gbm.null.boot, group=extant$Red.List.status)
  store_median[i,] <- tapply(temp$prediction, temp$group, median)
  store_kw <- c(store_kw, kruskal.test(predict.gbm.null.boot, extant$Red.List.status)$p.value)
  # print progress
   if(i %% 10==0) { cat(paste0("iteration: ", i, "\n")) }
}
hist(store_kw, breaks=80, xlim=c(0,0.1))
boxplot(store_median, names=c("DD", "LC", "NT", "VU", "EN", "CR", "EW", "EX"),
        main="bootstrap null model prediction, n=500",
        ylab="Median duration predicted (log)")
boot.k <- melt(store_median)
kruskal.test(boot.k$value, boot.k$X2)
```
