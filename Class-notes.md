Class\_10\_10
================
Yongmei Huang
10/10/2019

``` r
url = "http://samhda.s3-us-gov-west-1.amazonaws.com/s3fs-public/field-uploads/2k15StateFiles/NSDUHsaeShortTermCHG2015.htm"
drug_use_xml = read_html(url)
view(drug_use_xml)

drug_use_xml %>%
  html_nodes(css = "table") #15 tables#
```

    ## {xml_nodeset (15)}
    ##  [1] <table class="rti" border="1" cellspacing="0" cellpadding="1" width ...
    ##  [2] <table class="rti" border="1" cellspacing="0" cellpadding="1" width ...
    ##  [3] <table class="rti" border="1" cellspacing="0" cellpadding="1" width ...
    ##  [4] <table class="rti" border="1" cellspacing="0" cellpadding="1" width ...
    ##  [5] <table class="rti" border="1" cellspacing="0" cellpadding="1" width ...
    ##  [6] <table class="rti" border="1" cellspacing="0" cellpadding="1" width ...
    ##  [7] <table class="rti" border="1" cellspacing="0" cellpadding="1" width ...
    ##  [8] <table class="rti" border="1" cellspacing="0" cellpadding="1" width ...
    ##  [9] <table class="rti" border="1" cellspacing="0" cellpadding="1" width ...
    ## [10] <table class="rti" border="1" cellspacing="0" cellpadding="1" width ...
    ## [11] <table class="rti" border="1" cellspacing="0" cellpadding="1" width ...
    ## [12] <table class="rti" border="1" cellspacing="0" cellpadding="1" width ...
    ## [13] <table class="rti" border="1" cellspacing="0" cellpadding="1" width ...
    ## [14] <table class="rti" border="1" cellspacing="0" cellpadding="1" width ...
    ## [15] <table class="rti" border="1" cellspacing="0" cellpadding="1" width ...

``` r
table_marj = 
  (drug_use_xml %>% html_nodes(css = "table")) %>% 
  .[[1]] %>%
  html_table() 

#First table#
table_marj = 
  (drug_use_xml %>% html_nodes(css = "table")) %>% 
  .[[1]] %>%
  html_table() %>%
  slice(-1) %>% 
  as_tibble()

table_marj
```

    ## # A tibble: 56 x 16
    ##    State `12+(2013-2014)` `12+(2014-2015)` `12+(P Value)` `12-17(2013-201~
    ##    <chr> <chr>            <chr>            <chr>          <chr>           
    ##  1 Tota~ 12.90a           13.36            0.002          13.28b          
    ##  2 Nort~ 13.88a           14.66            0.005          13.98           
    ##  3 Midw~ 12.40b           12.76            0.082          12.45           
    ##  4 South 11.24a           11.64            0.029          12.02           
    ##  5 West  15.27            15.62            0.262          15.53a          
    ##  6 Alab~ 9.98             9.60             0.426          9.90            
    ##  7 Alas~ 19.60a           21.92            0.010          17.30           
    ##  8 Ariz~ 13.69            13.12            0.364          15.12           
    ##  9 Arka~ 11.37            11.59            0.678          12.79           
    ## 10 Cali~ 14.49            15.25            0.103          15.03           
    ## # ... with 46 more rows, and 11 more variables: `12-17(2014-2015)` <chr>,
    ## #   `12-17(P Value)` <chr>, `18-25(2013-2014)` <chr>,
    ## #   `18-25(2014-2015)` <chr>, `18-25(P Value)` <chr>,
    ## #   `26+(2013-2014)` <chr>, `26+(2014-2015)` <chr>, `26+(P Value)` <chr>,
    ## #   `18+(2013-2014)` <chr>, `18+(2014-2015)` <chr>, `18+(P Value)` <chr>

``` r
#Second Table#
table_2 = 
  (drug_use_xml %>% html_nodes(css = "table")) %>% 
  .[[2]] %>%
  html_table() %>%
  slice(-1) %>% 
  as_tibble()

table_2
```

    ## # A tibble: 56 x 16
    ##    State `12+(2013-2014)` `12+(2014-2015)` `12+(P Value)` `12-17(2013-201~
    ##    <chr> <chr>            <chr>            <chr>          <chr>           
    ##  1 Tota~ 7.96a            8.34             0.001          7.22            
    ##  2 Nort~ 8.58a            9.28             0.001          7.68            
    ##  3 Midw~ 7.50a            7.92             0.009          6.64            
    ##  4 South 6.74a            7.02             0.044          6.31            
    ##  5 West  9.84             10.08            0.324          8.85            
    ##  6 Alab~ 5.57             5.35             0.510          4.98            
    ##  7 Alas~ 11.85a           14.38            0.002          9.19            
    ##  8 Ariz~ 8.80             8.51             0.570          8.30            
    ##  9 Arka~ 6.70             7.17             0.240          6.22            
    ## 10 Cali~ 9.20             9.67             0.158          8.74            
    ## # ... with 46 more rows, and 11 more variables: `12-17(2014-2015)` <chr>,
    ## #   `12-17(P Value)` <chr>, `18-25(2013-2014)` <chr>,
    ## #   `18-25(2014-2015)` <chr>, `18-25(P Value)` <chr>,
    ## #   `26+(2013-2014)` <chr>, `26+(2014-2015)` <chr>, `26+(P Value)` <chr>,
    ## #   `18+(2013-2014)` <chr>, `18+(2014-2015)` <chr>, `18+(P Value)` <chr>

Harry Potter Movies

``` r
knitr::opts_chunk$set(echo = TRUE)

hpsaga_html = 
  read_html("https://www.imdb.com/list/ls000630791/")


title_vec = 
  hpsaga_html %>%
  html_nodes(".lister-item-header a") %>%    #got info from selector 
  html_text()

gross_rev_vec = 
  hpsaga_html %>%
  html_nodes(".text-small:nth-child(7) span:nth-child(5)") %>%
  html_text()

runtime_vec = 
  hpsaga_html %>%
  html_nodes(".runtime") %>%
  html_text()

hpsaga_df = 
  tibble(
    title = title_vec,
    rev = gross_rev_vec,
    runtime = runtime_vec)
 view(hpsaga_df)
```

``` r
knitr::opts_chunk$set(echo = TRUE)

movie_saga_html = 
  read_html("https://www.amazon.com/product-reviews/B00005JNBQ/ref=cm_cr_arp_d_viewopt_rvwer?ie=UTF8&reviewerType=avp_only_reviews&sortBy=recent&pageNumber=1")


#talk to Jason on the selector bandget#
```

``` r
knitr::opts_chunk$set(echo = TRUE)

movie_saga_html = 
  read_html("https://www.amazon.com/product-reviews/B00005JNBQ/ref=cm_cr_arp_d_viewopt_rvwer?ie=UTF8&reviewerType=avp_only_reviews&sortBy=recent&pageNumber=1")


#talk to Jason on the selector bandget#
```

``` r
knitr::opts_chunk$set(echo = TRUE)

movie_saga_html = 
  read_html("https://www.amazon.com/product-reviews/B00005JNBQ/ref=cm_cr_arp_d_viewopt_rvwer?ie=UTF8&reviewerType=avp_only_reviews&sortBy=recent&pageNumber=1")


#talk to Jason on the selector bandget#
```

New York City Water

``` r
knitr::opts_chunk$set(echo = TRUE)

nyc_water_0 = 
  GET("https://data.cityofnewyork.us/resource/waf7-5gvc.csv") %>% 
  content("parsed")
```

    ## Parsed with column specification:
    ## cols(
    ##   year = col_double(),
    ##   new_york_city_population = col_double(),
    ##   nyc_consumption_million_gallons_per_day = col_double(),
    ##   per_capita_gallons_per_person_per_day = col_double()
    ## )

``` r
nyc_water = 
  GET("https://data.cityofnewyork.us/resource/waf7-5gvc.json") %>% 
  content("text") %>%
  jsonlite::fromJSON() %>%
  as_tibble()
```

Get another online database

``` r
knitr::opts_chunk$set(echo = TRUE)

brfss_smart2010 = 
  GET("https://data.cdc.gov/api/views/acme-vg9e/rows.csv?accessType=DOWNLOAD") %>% 
  content("parsed")
```

    ## Parsed with column specification:
    ## cols(
    ##   .default = col_character(),
    ##   Year = col_double(),
    ##   Sample_Size = col_double(),
    ##   Data_value = col_double(),
    ##   Confidence_limit_Low = col_double(),
    ##   Confidence_limit_High = col_double(),
    ##   Display_order = col_double(),
    ##   LocationID = col_logical()
    ## )

    ## See spec(...) for full column specifications.

``` r
head(brfss_smart2010, 20)
```

    ## # A tibble: 20 x 23
    ##     Year Locationabbr Locationdesc Class Topic Question Response
    ##    <dbl> <chr>        <chr>        <chr> <chr> <chr>    <chr>   
    ##  1  2010 AL           AL - Tuscal~ Heal~ Over~ How is ~ Excelle~
    ##  2  2010 AL           AL - Mobile~ Heal~ Over~ How is ~ Excelle~
    ##  3  2010 AL           AL - Jeffer~ Heal~ Over~ How is ~ Excelle~
    ##  4  2010 AL           AL - Mobile~ Heal~ Over~ How is ~ Very go~
    ##  5  2010 AL           AL - Jeffer~ Heal~ Over~ How is ~ Very go~
    ##  6  2010 AL           AL - Tuscal~ Heal~ Over~ How is ~ Very go~
    ##  7  2010 AL           AL - Tuscal~ Heal~ Over~ How is ~ Good    
    ##  8  2010 AL           AL - Mobile~ Heal~ Over~ How is ~ Good    
    ##  9  2010 AL           AL - Jeffer~ Heal~ Over~ How is ~ Good    
    ## 10  2010 AL           AL - Jeffer~ Heal~ Over~ How is ~ Fair    
    ## 11  2010 AL           AL - Tuscal~ Heal~ Over~ How is ~ Fair    
    ## 12  2010 AL           AL - Mobile~ Heal~ Over~ How is ~ Fair    
    ## 13  2010 AL           AL - Mobile~ Heal~ Over~ How is ~ Poor    
    ## 14  2010 AL           AL - Tuscal~ Heal~ Over~ How is ~ Poor    
    ## 15  2010 AL           AL - Jeffer~ Heal~ Over~ How is ~ Poor    
    ## 16  2010 AL           AL - Jeffer~ Heal~ Fair~ Health ~ Good or~
    ## 17  2010 AL           AL - Mobile~ Heal~ Fair~ Health ~ Good or~
    ## 18  2010 AL           AL - Tuscal~ Heal~ Fair~ Health ~ Good or~
    ## 19  2010 AL           AL - Tuscal~ Heal~ Fair~ Health ~ Fair or~
    ## 20  2010 AL           AL - Mobile~ Heal~ Fair~ Health ~ Fair or~
    ## # ... with 16 more variables: Sample_Size <dbl>, Data_value <dbl>,
    ## #   Confidence_limit_Low <dbl>, Confidence_limit_High <dbl>,
    ## #   Display_order <dbl>, Data_value_unit <chr>, Data_value_type <chr>,
    ## #   Data_Value_Footnote_Symbol <chr>, Data_Value_Footnote <chr>,
    ## #   DataSource <chr>, ClassId <chr>, TopicId <chr>, LocationID <lgl>,
    ## #   QuestionID <chr>, RESPID <chr>, GeoLocation <chr>

``` r
poke = 
  GET("http://pokeapi.co/api/v2/pokemon/1") %>%
  content()

poke$name
```

    ## [1] "bulbasaur"

``` r
poke$height
```

    ## [1] 7

``` r
poke$abilities
```

    ## [[1]]
    ## [[1]]$ability
    ## [[1]]$ability$name
    ## [1] "chlorophyll"
    ## 
    ## [[1]]$ability$url
    ## [1] "https://pokeapi.co/api/v2/ability/34/"
    ## 
    ## 
    ## [[1]]$is_hidden
    ## [1] TRUE
    ## 
    ## [[1]]$slot
    ## [1] 3
    ## 
    ## 
    ## [[2]]
    ## [[2]]$ability
    ## [[2]]$ability$name
    ## [1] "overgrow"
    ## 
    ## [[2]]$ability$url
    ## [1] "https://pokeapi.co/api/v2/ability/65/"
    ## 
    ## 
    ## [[2]]$is_hidden
    ## [1] FALSE
    ## 
    ## [[2]]$slot
    ## [1] 1

``` 


```
