Assignment 04: Tidy Data & Joins
================
Icíar Fernández Boyano
07/10/2019

##### Full instructions for this assignment can be found **[here](https://stat545.stat.ubc.ca/evaluation/hw04/hw04/).**

### *Set up*

``` r
library(tidyverse)
```

    ## ── Attaching packages ───────────────────────────────────────────────────────────────────────────────── tidyverse 1.2.1 ──

    ## ✔ ggplot2 3.2.1     ✔ purrr   0.3.2
    ## ✔ tibble  2.1.3     ✔ dplyr   0.8.3
    ## ✔ tidyr   1.0.0     ✔ stringr 1.4.0
    ## ✔ readr   1.3.1     ✔ forcats 0.4.0

    ## ── Conflicts ──────────────────────────────────────────────────────────────────────────────────── tidyverse_conflicts() ──
    ## ✖ dplyr::filter() masks stats::filter()
    ## ✖ dplyr::lag()    masks stats::lag()

``` r
library(gapminder)
library(gt) # I used this package to format tables for presentation, as an alternative to knitr
library(wesanderson) # This package contains color palettes from Wes Anderson movies (used in 1.2)
```

### **Exercise 1: Univariate Data Reshaping**

#### **Univariate Option 1**

##### 1\. Make a tibble with one row per year, and columns for life expectancy for two or more countries.

*Notes*

  - I used the package **‘gt’** to produce a nice-looking table instead
    of the usual knitr::kable. I used
    [this](https://gt.rstudio.com/articles/intro-creating-gt-tables.html),
    and the package is available for download
    [here](https://github.com/rstudio/gt).

<!-- end list -->

``` r
gapminder_wide <-
  gapminder %>%
  pivot_wider(id_cols = year,
              names_from = "country",
              values_from = lifeExp) %>% # At this point, we have columns for all countries showing life exp
  select(year, Spain, Canada) %>% # Selecting two countries
  gt() %>%
  tab_header(title = "Life Expectancy over time in Spain and Canada")

gapminder_wide # prints table
```

<!--html_preserve-->

<style>html {
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Helvetica Neue', 'Fira Sans', 'Droid Sans', Arial, sans-serif;
}

#lxhpqbjdlu .gt_table {
  display: table;
  border-collapse: collapse;
  margin-left: auto;
  margin-right: auto;
  color: #333333;
  font-size: 16px;
  background-color: #FFFFFF;
  /* table.background.color */
  width: auto;
  /* table.width */
  border-top-style: solid;
  /* table.border.top.style */
  border-top-width: 2px;
  /* table.border.top.width */
  border-top-color: #A8A8A8;
  /* table.border.top.color */
  border-bottom-style: solid;
  /* table.border.bottom.style */
  border-bottom-width: 2px;
  /* table.border.bottom.width */
  border-bottom-color: #A8A8A8;
  /* table.border.bottom.color */
}

#lxhpqbjdlu .gt_heading {
  background-color: #FFFFFF;
  /* heading.background.color */
  border-bottom-color: #FFFFFF;
}

#lxhpqbjdlu .gt_title {
  color: #333333;
  font-size: 125%;
  /* heading.title.font.size */
  padding-top: 4px;
  /* heading.top.padding - not yet used */
  padding-bottom: 4px;
  border-bottom-color: #FFFFFF;
  border-bottom-width: 0;
}

#lxhpqbjdlu .gt_subtitle {
  color: #333333;
  font-size: 85%;
  /* heading.subtitle.font.size */
  padding-top: 0;
  padding-bottom: 4px;
  /* heading.bottom.padding - not yet used */
  border-top-color: #FFFFFF;
  border-top-width: 0;
}

#lxhpqbjdlu .gt_bottom_border {
  border-bottom-style: solid;
  /* heading.border.bottom.style */
  border-bottom-width: 2px;
  /* heading.border.bottom.width */
  border-bottom-color: #D3D3D3;
  /* heading.border.bottom.color */
}

#lxhpqbjdlu .gt_column_spanner {
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
  padding-top: 4px;
  padding-bottom: 4px;
}

#lxhpqbjdlu .gt_col_heading {
  color: #333333;
  background-color: #FFFFFF;
  /* column_labels.background.color */
  font-size: 16px;
  /* column_labels.font.size */
  font-weight: initial;
  /* column_labels.font.weight */
  vertical-align: middle;
  padding: 5px;
  margin: 10px;
  overflow-x: hidden;
}

#lxhpqbjdlu .gt_columns_top_border {
  border-top-style: solid;
  border-top-width: 2px;
  border-top-color: #D3D3D3;
}

#lxhpqbjdlu .gt_columns_bottom_border {
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
}

#lxhpqbjdlu .gt_sep_right {
  border-right: 5px solid #FFFFFF;
}

#lxhpqbjdlu .gt_group_heading {
  padding: 8px;
  /* row_group.padding */
  color: #333333;
  background-color: #FFFFFF;
  /* row_group.background.color */
  font-size: 16px;
  /* row_group.font.size */
  font-weight: initial;
  /* row_group.font.weight */
  border-top-style: solid;
  /* row_group.border.top.style */
  border-top-width: 2px;
  /* row_group.border.top.width */
  border-top-color: #D3D3D3;
  /* row_group.border.top.color */
  border-bottom-style: solid;
  /* row_group.border.bottom.style */
  border-bottom-width: 2px;
  /* row_group.border.bottom.width */
  border-bottom-color: #D3D3D3;
  /* row_group.border.bottom.color */
  vertical-align: middle;
}

#lxhpqbjdlu .gt_empty_group_heading {
  padding: 0.5px;
  color: #333333;
  background-color: #FFFFFF;
  /* row_group.background.color */
  font-size: 16px;
  /* row_group.font.size */
  font-weight: initial;
  /* row_group.font.weight */
  border-top-style: solid;
  /* row_group.border.top.style */
  border-top-width: 2px;
  /* row_group.border.top.width */
  border-top-color: #D3D3D3;
  /* row_group.border.top.color */
  border-bottom-style: solid;
  /* row_group.border.bottom.style */
  border-bottom-width: 2px;
  /* row_group.border.bottom.width */
  border-bottom-color: #D3D3D3;
  /* row_group.border.bottom.color */
  vertical-align: middle;
}

#lxhpqbjdlu .gt_striped {
  background-color: #8080800D;
}

#lxhpqbjdlu .gt_from_md > :first-child {
  margin-top: 0;
}

#lxhpqbjdlu .gt_from_md > :last-child {
  margin-bottom: 0;
}

#lxhpqbjdlu .gt_row {
  padding: 8px;
  /* row.padding */
  margin: 10px;
  border-top-style: solid;
  border-top-width: 1px;
  border-top-color: #D3D3D3;
  vertical-align: middle;
  overflow-x: hidden;
}

#lxhpqbjdlu .gt_stub {
  border-right-style: solid;
  border-right-width: 2px;
  border-right-color: #D3D3D3;
  padding-left: 12px;
}

#lxhpqbjdlu .gt_summary_row {
  color: #333333;
  background-color: #FFFFFF;
  /* summary_row.background.color */
  padding: 8px;
  /* summary_row.padding */
  text-transform: inherit;
  /* summary_row.text_transform */
}

#lxhpqbjdlu .gt_grand_summary_row {
  color: #333333;
  background-color: #FFFFFF;
  /* grand_summary_row.background.color */
  padding: 8px;
  /* grand_summary_row.padding */
  text-transform: inherit;
  /* grand_summary_row.text_transform */
}

#lxhpqbjdlu .gt_first_summary_row {
  border-top-style: solid;
  border-top-width: 2px;
  border-top-color: #D3D3D3;
}

#lxhpqbjdlu .gt_first_grand_summary_row {
  border-top-style: double;
  border-top-width: 6px;
  border-top-color: #D3D3D3;
}

#lxhpqbjdlu .gt_table_body {
  border-top-style: solid;
  /* table_body.border.top.style */
  border-top-width: 2px;
  /* table_body.border.top.width */
  border-top-color: #D3D3D3;
  /* table_body.border.top.color */
  border-bottom-style: solid;
  /* table_body.border.bottom.style */
  border-bottom-width: 2px;
  /* table_body.border.bottom.width */
  border-bottom-color: #D3D3D3;
  /* table_body.border.bottom.color */
}

#lxhpqbjdlu .gt_footnotes {
  border-top-style: solid;
  /* footnotes.border.top.style */
  border-top-width: 2px;
  /* footnotes.border.top.width */
  border-top-color: #D3D3D3;
  /* footnotes.border.top.color */
}

#lxhpqbjdlu .gt_footnote {
  font-size: 90%;
  /* footnote.font.size */
  margin: 0px;
  padding: 4px;
  /* footnote.padding */
}

#lxhpqbjdlu .gt_sourcenotes {
  border-top-style: solid;
  /* sourcenotes.border.top.style */
  border-top-width: 2px;
  /* sourcenotes.border.top.width */
  border-top-color: #D3D3D3;
  /* sourcenotes.border.top.color */
}

#lxhpqbjdlu .gt_sourcenote {
  font-size: 90%;
  /* sourcenote.font.size */
  padding: 4px;
  /* sourcenote.padding */
}

#lxhpqbjdlu .gt_center {
  text-align: center;
}

#lxhpqbjdlu .gt_left {
  text-align: left;
}

#lxhpqbjdlu .gt_right {
  text-align: right;
  font-variant-numeric: tabular-nums;
}

#lxhpqbjdlu .gt_font_normal {
  font-weight: normal;
}

#lxhpqbjdlu .gt_font_bold {
  font-weight: bold;
}

#lxhpqbjdlu .gt_font_italic {
  font-style: italic;
}

#lxhpqbjdlu .gt_super {
  font-size: 65%;
}

#lxhpqbjdlu .gt_footnote_marks {
  font-style: italic;
  font-size: 65%;
}
</style>

<div id="lxhpqbjdlu" style="overflow-x:auto;overflow-y:auto;width:auto;height:auto;">

<table class="gt_table">

<thead>

<tr>

<th colspan="3" class="gt_heading gt_title gt_font_normal gt_center gt_bottom_border" style>

Life Expectancy over time in Spain and
Canada

</th>

</tr>

</thead>

<tr>

<th class="gt_col_heading gt_columns_bottom_border gt_columns_top_border gt_center" rowspan="1" colspan="1">

year

</th>

<th class="gt_col_heading gt_columns_bottom_border gt_columns_top_border gt_center" rowspan="1" colspan="1">

Spain

</th>

<th class="gt_col_heading gt_columns_bottom_border gt_columns_top_border gt_center" rowspan="1" colspan="1">

Canada

</th>

</tr>

<body class="gt_table_body">

<tr>

<td class="gt_row gt_center">

1952

</td>

<td class="gt_row gt_right">

64.940

</td>

<td class="gt_row gt_right">

68.750

</td>

</tr>

<tr>

<td class="gt_row gt_center gt_striped">

1957

</td>

<td class="gt_row gt_right gt_striped">

66.660

</td>

<td class="gt_row gt_right gt_striped">

69.960

</td>

</tr>

<tr>

<td class="gt_row gt_center">

1962

</td>

<td class="gt_row gt_right">

69.690

</td>

<td class="gt_row gt_right">

71.300

</td>

</tr>

<tr>

<td class="gt_row gt_center gt_striped">

1967

</td>

<td class="gt_row gt_right gt_striped">

71.440

</td>

<td class="gt_row gt_right gt_striped">

72.130

</td>

</tr>

<tr>

<td class="gt_row gt_center">

1972

</td>

<td class="gt_row gt_right">

73.060

</td>

<td class="gt_row gt_right">

72.880

</td>

</tr>

<tr>

<td class="gt_row gt_center gt_striped">

1977

</td>

<td class="gt_row gt_right gt_striped">

74.390

</td>

<td class="gt_row gt_right gt_striped">

74.210

</td>

</tr>

<tr>

<td class="gt_row gt_center">

1982

</td>

<td class="gt_row gt_right">

76.300

</td>

<td class="gt_row gt_right">

75.760

</td>

</tr>

<tr>

<td class="gt_row gt_center gt_striped">

1987

</td>

<td class="gt_row gt_right gt_striped">

76.900

</td>

<td class="gt_row gt_right gt_striped">

76.860

</td>

</tr>

<tr>

<td class="gt_row gt_center">

1992

</td>

<td class="gt_row gt_right">

77.570

</td>

<td class="gt_row gt_right">

77.950

</td>

</tr>

<tr>

<td class="gt_row gt_center gt_striped">

1997

</td>

<td class="gt_row gt_right gt_striped">

78.770

</td>

<td class="gt_row gt_right gt_striped">

78.610

</td>

</tr>

<tr>

<td class="gt_row gt_center">

2002

</td>

<td class="gt_row gt_right">

79.780

</td>

<td class="gt_row gt_right">

79.770

</td>

</tr>

<tr>

<td class="gt_row gt_center gt_striped">

2007

</td>

<td class="gt_row gt_right gt_striped">

80.941

</td>

<td class="gt_row gt_right gt_striped">

80.653

</td>

</tr>

</body>

</table>

</div>

<!--/html_preserve-->

##### 2\. Take advantage of this new data shape to scatterplot life expectancy for one country against that of another.

*Notes*

  - I used the package [‘wes
    anderson’](https://github.com/karthik/wesanderson) that has
    different colour palettes for each of his movies to add colour to
    this scatterplot.

<!-- end list -->

``` r
LifeExp.plot <-
  gapminder_wide %>%
  ggplot(aes(Spain, Canada)) +
  geom_point(color=wes_palette("GrandBudapest1", 12, type = "continuous")) +
  ggtitle("Life Expectancy in Spain and Canada from 1952 to 2007") +
  xlab("Life Expectancy in Spain") +
  ylab("Life Expectancy in Canada") +
  theme_bw() +
  theme(text = element_text(size = 12)) 

LifeExp.plot # Prints plot
```

![](hw04_tidydatajoins_files/figure-gfm/unnamed-chunk-3-1.png)<!-- -->
\#\#\#\#\# 3. Re-lengthen the data.

``` r
gapminder_length <- 
  gapminder_wide %>%
  pivot_longer(cols = -year, 
               names_to = "country", 
               values_to = "lifeExp") %>%
  DT::datatable()

gapminder_length # Print
```

    ## PhantomJS not found. You can install it with webshot::install_phantomjs(). If it is installed, please make sure the phantomjs executable can be found via the PATH variable.

<!--html_preserve-->

<div id="htmlwidget-174bc224071caaf4fecd" class="datatables html-widget" style="width:100%;height:auto;">

</div>

<script type="application/json" data-for="htmlwidget-174bc224071caaf4fecd">{"x":{"filter":"none","data":[["1","2","3","4","5","6","7","8","9","10","11","12","13","14","15","16","17","18","19","20","21","22","23","24"],[1952,1952,1957,1957,1962,1962,1967,1967,1972,1972,1977,1977,1982,1982,1987,1987,1992,1992,1997,1997,2002,2002,2007,2007],["Spain","Canada","Spain","Canada","Spain","Canada","Spain","Canada","Spain","Canada","Spain","Canada","Spain","Canada","Spain","Canada","Spain","Canada","Spain","Canada","Spain","Canada","Spain","Canada"],[64.94,68.75,66.66,69.96,69.69,71.3,71.44,72.13,73.06,72.88,74.39,74.21,76.3,75.76,76.9,76.86,77.57,77.95,78.77,78.61,79.78,79.77,80.941,80.653]],"container":"<table class=\"display\">\n  <thead>\n    <tr>\n      <th> <\/th>\n      <th>year<\/th>\n      <th>country<\/th>\n      <th>lifeExp<\/th>\n    <\/tr>\n  <\/thead>\n<\/table>","options":{"columnDefs":[{"className":"dt-right","targets":[1,3]},{"orderable":false,"targets":0}],"order":[],"autoWidth":false,"orderClasses":false}},"evals":[],"jsHooks":[]}</script>

<!--/html_preserve-->

### **Exercise 2: Multivariate Data Reshaping**

#### **Multivariate Option 1**

##### 1\. Make a tibble with one row per year, and columns for life expectancy and GDP per capita (or two other numeric variables) for two or more countries.

``` r
# Reshaping data
gapminder_reshape <- 
  gapminder %>%
  pivot_wider(id_cols  = year, 
              names_from = country,
              names_sep = "_", 
              values_from = c("lifeExp", "gdpPercap")) %>% # At this point, data is for all countries
  select(year, lifeExp_Spain, lifeExp_Canada, gdpPercap_Spain, gdpPercap_Canada) 

# Making a nice looking table for presentation

gapminder_reshape %>%
  rename("Life.Spain" = lifeExp_Spain, "Life.Canada" = lifeExp_Canada, "GDP.Spain" = gdpPercap_Spain, "GDP.Canada" = gdpPercap_Canada) %>%
  gt() %>%
  tab_header(title = "Exploring two variables from the Gapminder dataset",
             subtitle = "From 1952 to 2007") %>%
  tab_spanner(label = "Life Expectancy",
              columns = vars(Life.Spain, Life.Canada)) %>%
  tab_spanner(label = "GDP Per Capita",
              columns = vars(GDP.Spain, GDP.Canada))
```

<!--html_preserve-->

<style>html {
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Helvetica Neue', 'Fira Sans', 'Droid Sans', Arial, sans-serif;
}

#xlcehkunoi .gt_table {
  display: table;
  border-collapse: collapse;
  margin-left: auto;
  margin-right: auto;
  color: #333333;
  font-size: 16px;
  background-color: #FFFFFF;
  /* table.background.color */
  width: auto;
  /* table.width */
  border-top-style: solid;
  /* table.border.top.style */
  border-top-width: 2px;
  /* table.border.top.width */
  border-top-color: #A8A8A8;
  /* table.border.top.color */
  border-bottom-style: solid;
  /* table.border.bottom.style */
  border-bottom-width: 2px;
  /* table.border.bottom.width */
  border-bottom-color: #A8A8A8;
  /* table.border.bottom.color */
}

#xlcehkunoi .gt_heading {
  background-color: #FFFFFF;
  /* heading.background.color */
  border-bottom-color: #FFFFFF;
}

#xlcehkunoi .gt_title {
  color: #333333;
  font-size: 125%;
  /* heading.title.font.size */
  padding-top: 4px;
  /* heading.top.padding - not yet used */
  padding-bottom: 4px;
  border-bottom-color: #FFFFFF;
  border-bottom-width: 0;
}

#xlcehkunoi .gt_subtitle {
  color: #333333;
  font-size: 85%;
  /* heading.subtitle.font.size */
  padding-top: 0;
  padding-bottom: 4px;
  /* heading.bottom.padding - not yet used */
  border-top-color: #FFFFFF;
  border-top-width: 0;
}

#xlcehkunoi .gt_bottom_border {
  border-bottom-style: solid;
  /* heading.border.bottom.style */
  border-bottom-width: 2px;
  /* heading.border.bottom.width */
  border-bottom-color: #D3D3D3;
  /* heading.border.bottom.color */
}

#xlcehkunoi .gt_column_spanner {
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
  padding-top: 4px;
  padding-bottom: 4px;
}

#xlcehkunoi .gt_col_heading {
  color: #333333;
  background-color: #FFFFFF;
  /* column_labels.background.color */
  font-size: 16px;
  /* column_labels.font.size */
  font-weight: initial;
  /* column_labels.font.weight */
  vertical-align: middle;
  padding: 5px;
  margin: 10px;
  overflow-x: hidden;
}

#xlcehkunoi .gt_columns_top_border {
  border-top-style: solid;
  border-top-width: 2px;
  border-top-color: #D3D3D3;
}

#xlcehkunoi .gt_columns_bottom_border {
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
}

#xlcehkunoi .gt_sep_right {
  border-right: 5px solid #FFFFFF;
}

#xlcehkunoi .gt_group_heading {
  padding: 8px;
  /* row_group.padding */
  color: #333333;
  background-color: #FFFFFF;
  /* row_group.background.color */
  font-size: 16px;
  /* row_group.font.size */
  font-weight: initial;
  /* row_group.font.weight */
  border-top-style: solid;
  /* row_group.border.top.style */
  border-top-width: 2px;
  /* row_group.border.top.width */
  border-top-color: #D3D3D3;
  /* row_group.border.top.color */
  border-bottom-style: solid;
  /* row_group.border.bottom.style */
  border-bottom-width: 2px;
  /* row_group.border.bottom.width */
  border-bottom-color: #D3D3D3;
  /* row_group.border.bottom.color */
  vertical-align: middle;
}

#xlcehkunoi .gt_empty_group_heading {
  padding: 0.5px;
  color: #333333;
  background-color: #FFFFFF;
  /* row_group.background.color */
  font-size: 16px;
  /* row_group.font.size */
  font-weight: initial;
  /* row_group.font.weight */
  border-top-style: solid;
  /* row_group.border.top.style */
  border-top-width: 2px;
  /* row_group.border.top.width */
  border-top-color: #D3D3D3;
  /* row_group.border.top.color */
  border-bottom-style: solid;
  /* row_group.border.bottom.style */
  border-bottom-width: 2px;
  /* row_group.border.bottom.width */
  border-bottom-color: #D3D3D3;
  /* row_group.border.bottom.color */
  vertical-align: middle;
}

#xlcehkunoi .gt_striped {
  background-color: #8080800D;
}

#xlcehkunoi .gt_from_md > :first-child {
  margin-top: 0;
}

#xlcehkunoi .gt_from_md > :last-child {
  margin-bottom: 0;
}

#xlcehkunoi .gt_row {
  padding: 8px;
  /* row.padding */
  margin: 10px;
  border-top-style: solid;
  border-top-width: 1px;
  border-top-color: #D3D3D3;
  vertical-align: middle;
  overflow-x: hidden;
}

#xlcehkunoi .gt_stub {
  border-right-style: solid;
  border-right-width: 2px;
  border-right-color: #D3D3D3;
  padding-left: 12px;
}

#xlcehkunoi .gt_summary_row {
  color: #333333;
  background-color: #FFFFFF;
  /* summary_row.background.color */
  padding: 8px;
  /* summary_row.padding */
  text-transform: inherit;
  /* summary_row.text_transform */
}

#xlcehkunoi .gt_grand_summary_row {
  color: #333333;
  background-color: #FFFFFF;
  /* grand_summary_row.background.color */
  padding: 8px;
  /* grand_summary_row.padding */
  text-transform: inherit;
  /* grand_summary_row.text_transform */
}

#xlcehkunoi .gt_first_summary_row {
  border-top-style: solid;
  border-top-width: 2px;
  border-top-color: #D3D3D3;
}

#xlcehkunoi .gt_first_grand_summary_row {
  border-top-style: double;
  border-top-width: 6px;
  border-top-color: #D3D3D3;
}

#xlcehkunoi .gt_table_body {
  border-top-style: solid;
  /* table_body.border.top.style */
  border-top-width: 2px;
  /* table_body.border.top.width */
  border-top-color: #D3D3D3;
  /* table_body.border.top.color */
  border-bottom-style: solid;
  /* table_body.border.bottom.style */
  border-bottom-width: 2px;
  /* table_body.border.bottom.width */
  border-bottom-color: #D3D3D3;
  /* table_body.border.bottom.color */
}

#xlcehkunoi .gt_footnotes {
  border-top-style: solid;
  /* footnotes.border.top.style */
  border-top-width: 2px;
  /* footnotes.border.top.width */
  border-top-color: #D3D3D3;
  /* footnotes.border.top.color */
}

#xlcehkunoi .gt_footnote {
  font-size: 90%;
  /* footnote.font.size */
  margin: 0px;
  padding: 4px;
  /* footnote.padding */
}

#xlcehkunoi .gt_sourcenotes {
  border-top-style: solid;
  /* sourcenotes.border.top.style */
  border-top-width: 2px;
  /* sourcenotes.border.top.width */
  border-top-color: #D3D3D3;
  /* sourcenotes.border.top.color */
}

#xlcehkunoi .gt_sourcenote {
  font-size: 90%;
  /* sourcenote.font.size */
  padding: 4px;
  /* sourcenote.padding */
}

#xlcehkunoi .gt_center {
  text-align: center;
}

#xlcehkunoi .gt_left {
  text-align: left;
}

#xlcehkunoi .gt_right {
  text-align: right;
  font-variant-numeric: tabular-nums;
}

#xlcehkunoi .gt_font_normal {
  font-weight: normal;
}

#xlcehkunoi .gt_font_bold {
  font-weight: bold;
}

#xlcehkunoi .gt_font_italic {
  font-style: italic;
}

#xlcehkunoi .gt_super {
  font-size: 65%;
}

#xlcehkunoi .gt_footnote_marks {
  font-style: italic;
  font-size: 65%;
}
</style>

<div id="xlcehkunoi" style="overflow-x:auto;overflow-y:auto;width:auto;height:auto;">

<table class="gt_table">

<thead>

<tr>

<th colspan="5" class="gt_heading gt_title gt_font_normal gt_center" style>

Exploring two variables from the Gapminder
dataset

</th>

</tr>

<tr>

<th colspan="5" class="gt_heading gt_subtitle gt_font_normal gt_center gt_bottom_border" style>

From 1952 to
2007

</th>

</tr>

</thead>

<tr>

<th class="gt_col_heading gt_center gt_columns_bottom_border" rowspan="2" colspan="1">

year

</th>

<th class="gt_col_heading gt_center gt_columns_top_border gt_column_spanner gt_sep_right" rowspan="1" colspan="2">

Life
Expectancy

</th>

<th class="gt_col_heading gt_center gt_columns_top_border gt_column_spanner" rowspan="1" colspan="2">

GDP Per
Capita

</th>

</tr>

<tr>

<th class="gt_col_heading gt_columns_bottom_border gt_center" rowspan="1" colspan="1">

Life.Spain

</th>

<th class="gt_col_heading gt_columns_bottom_border gt_center" rowspan="1" colspan="1">

Life.Canada

</th>

<th class="gt_col_heading gt_columns_bottom_border gt_center" rowspan="1" colspan="1">

GDP.Spain

</th>

<th class="gt_col_heading gt_columns_bottom_border gt_center" rowspan="1" colspan="1">

GDP.Canada

</th>

</tr>

<body class="gt_table_body">

<tr>

<td class="gt_row gt_center">

1952

</td>

<td class="gt_row gt_right">

64.940

</td>

<td class="gt_row gt_right">

68.750

</td>

<td class="gt_row gt_right">

3834.035

</td>

<td class="gt_row gt_right">

11367.16

</td>

</tr>

<tr>

<td class="gt_row gt_center gt_striped">

1957

</td>

<td class="gt_row gt_right gt_striped">

66.660

</td>

<td class="gt_row gt_right gt_striped">

69.960

</td>

<td class="gt_row gt_right gt_striped">

4564.802

</td>

<td class="gt_row gt_right gt_striped">

12489.95

</td>

</tr>

<tr>

<td class="gt_row gt_center">

1962

</td>

<td class="gt_row gt_right">

69.690

</td>

<td class="gt_row gt_right">

71.300

</td>

<td class="gt_row gt_right">

5693.844

</td>

<td class="gt_row gt_right">

13462.49

</td>

</tr>

<tr>

<td class="gt_row gt_center gt_striped">

1967

</td>

<td class="gt_row gt_right gt_striped">

71.440

</td>

<td class="gt_row gt_right gt_striped">

72.130

</td>

<td class="gt_row gt_right gt_striped">

7993.512

</td>

<td class="gt_row gt_right gt_striped">

16076.59

</td>

</tr>

<tr>

<td class="gt_row gt_center">

1972

</td>

<td class="gt_row gt_right">

73.060

</td>

<td class="gt_row gt_right">

72.880

</td>

<td class="gt_row gt_right">

10638.751

</td>

<td class="gt_row gt_right">

18970.57

</td>

</tr>

<tr>

<td class="gt_row gt_center gt_striped">

1977

</td>

<td class="gt_row gt_right gt_striped">

74.390

</td>

<td class="gt_row gt_right gt_striped">

74.210

</td>

<td class="gt_row gt_right gt_striped">

13236.921

</td>

<td class="gt_row gt_right gt_striped">

22090.88

</td>

</tr>

<tr>

<td class="gt_row gt_center">

1982

</td>

<td class="gt_row gt_right">

76.300

</td>

<td class="gt_row gt_right">

75.760

</td>

<td class="gt_row gt_right">

13926.170

</td>

<td class="gt_row gt_right">

22898.79

</td>

</tr>

<tr>

<td class="gt_row gt_center gt_striped">

1987

</td>

<td class="gt_row gt_right gt_striped">

76.900

</td>

<td class="gt_row gt_right gt_striped">

76.860

</td>

<td class="gt_row gt_right gt_striped">

15764.983

</td>

<td class="gt_row gt_right gt_striped">

26626.52

</td>

</tr>

<tr>

<td class="gt_row gt_center">

1992

</td>

<td class="gt_row gt_right">

77.570

</td>

<td class="gt_row gt_right">

77.950

</td>

<td class="gt_row gt_right">

18603.065

</td>

<td class="gt_row gt_right">

26342.88

</td>

</tr>

<tr>

<td class="gt_row gt_center gt_striped">

1997

</td>

<td class="gt_row gt_right gt_striped">

78.770

</td>

<td class="gt_row gt_right gt_striped">

78.610

</td>

<td class="gt_row gt_right gt_striped">

20445.299

</td>

<td class="gt_row gt_right gt_striped">

28954.93

</td>

</tr>

<tr>

<td class="gt_row gt_center">

2002

</td>

<td class="gt_row gt_right">

79.780

</td>

<td class="gt_row gt_right">

79.770

</td>

<td class="gt_row gt_right">

24835.472

</td>

<td class="gt_row gt_right">

33328.97

</td>

</tr>

<tr>

<td class="gt_row gt_center gt_striped">

2007

</td>

<td class="gt_row gt_right gt_striped">

80.941

</td>

<td class="gt_row gt_right gt_striped">

80.653

</td>

<td class="gt_row gt_right gt_striped">

28821.064

</td>

<td class="gt_row gt_right gt_striped">

36319.24

</td>

</tr>

</body>

</table>

</div>

<!--/html_preserve-->

##### 2\. Re-lengthen the data.

``` r
gapminder_reshape %>%
  pivot_longer(cols = -year,
               names_to = c(".value", "country"),
               names_sep = "_") %>%
  DT::datatable()
```

<!--html_preserve-->

<div id="htmlwidget-ae880c793576097567b9" class="datatables html-widget" style="width:100%;height:auto;">

</div>

<script type="application/json" data-for="htmlwidget-ae880c793576097567b9">{"x":{"filter":"none","data":[["1","2","3","4","5","6","7","8","9","10","11","12","13","14","15","16","17","18","19","20","21","22","23","24"],[1952,1952,1957,1957,1962,1962,1967,1967,1972,1972,1977,1977,1982,1982,1987,1987,1992,1992,1997,1997,2002,2002,2007,2007],["Spain","Canada","Spain","Canada","Spain","Canada","Spain","Canada","Spain","Canada","Spain","Canada","Spain","Canada","Spain","Canada","Spain","Canada","Spain","Canada","Spain","Canada","Spain","Canada"],[64.94,68.75,66.66,69.96,69.69,71.3,71.44,72.13,73.06,72.88,74.39,74.21,76.3,75.76,76.9,76.86,77.57,77.95,78.77,78.61,79.78,79.77,80.941,80.653],[3834.034742,11367.16112,4564.80241,12489.95006,5693.843879,13462.48555,7993.512294,16076.58803,10638.75131,18970.57086,13236.92117,22090.88306,13926.16997,22898.79214,15764.98313,26626.51503,18603.06452,26342.88426,20445.29896,28954.92589,24835.47166,33328.96507,28821.0637,36319.23501]],"container":"<table class=\"display\">\n  <thead>\n    <tr>\n      <th> <\/th>\n      <th>year<\/th>\n      <th>country<\/th>\n      <th>lifeExp<\/th>\n      <th>gdpPercap<\/th>\n    <\/tr>\n  <\/thead>\n<\/table>","options":{"columnDefs":[{"className":"dt-right","targets":[1,3,4]},{"orderable":false,"targets":0}],"order":[],"autoWidth":false,"orderClasses":false}},"evals":[],"jsHooks":[]}</script>

<!--/html_preserve-->

### **Exercise 3: Table Joins**

Read in the made-up wedding guestlist and email addresses using the
following lines (go ahead and copy-paste these):

    ## Parsed with column specification:
    ## cols(
    ##   party = col_double(),
    ##   name = col_character(),
    ##   meal_wedding = col_character(),
    ##   meal_brunch = col_character(),
    ##   attendance_wedding = col_character(),
    ##   attendance_brunch = col_character(),
    ##   attendance_golf = col_character()
    ## )

    ## Parsed with column specification:
    ## cols(
    ##   guest = col_character(),
    ##   email = col_character()
    ## )

##### **3.1: For each guest in the guestlist (guest tibble), add a column for email address, which can be found in the email tibble.**

###### *Notes*

  - I found [this
    thread](https://stackoverflow.com/questions/13773770/split-comma-separated-strings-in-a-column-into-separate-rows)
    particularly useful to solve this question, as I got a bit stuck
    with organising the email
tibble.

<!-- end list -->

``` r
# Splitting the comma-divided rows into individual columns and renaming 'guest' to 'name' so that tables can be joined
email_sep <- email %>%
  separate_rows(email, guest, sep = ", ") %>%
  rename(name = guest)

# Joining the tibbles
guest %>%
  left_join(email_sep, by = "name") %>% # Merge by name variable
  select(name, email) %>% # Only keep the guest names & emails 
  DT::datatable() # Tibble presentation
```

<!--html_preserve-->

<div id="htmlwidget-04c918cddb769d5ec8ac" class="datatables html-widget" style="width:100%;height:auto;">

</div>

<script type="application/json" data-for="htmlwidget-04c918cddb769d5ec8ac">{"x":{"filter":"none","data":[["1","2","3","4","5","6","7","8","9","10","11","12","13","14","15","16","17","18","19","20","21","22","23","24","25","26","27","28","29","30"],["Sommer Medrano","Phillip Medrano","Blanka Medrano","Emaan Medrano","Blair Park","Nigel Webb","Sinead English","Ayra Marks","Atlanta Connolly","Denzel Connolly","Chanelle Shah","Jolene Welsh","Hayley Booker","Amayah Sanford","Erika Foley","Ciaron Acosta","Diana Stuart","Cosmo Dunkley","Cai Mcdaniel","Daisy-May Caldwell","Martin Caldwell","Violet Caldwell","Nazifa Caldwell","Eric Caldwell","Rosanna Bird","Kurtis Frost","Huma Stokes","Samuel Rutledge","Eddison Collier","Stewart Nicholls"],["sommm@gmail.com","sommm@gmail.com","sommm@gmail.com","sommm@gmail.com","bpark@gmail.com","bpark@gmail.com","singlish@hotmail.ca","marksa42@gmail.com",null,null,null,"jw1987@hotmail.com","jw1987@hotmail.com","erikaaaaaa@gmail.com","erikaaaaaa@gmail.com","shining_ciaron@gmail.com","doodledianastu@gmail.com",null,null,"caldwellfamily5212@gmail.com","caldwellfamily5212@gmail.com","caldwellfamily5212@gmail.com","caldwellfamily5212@gmail.com","caldwellfamily5212@gmail.com","rosy1987b@gmail.com","rosy1987b@gmail.com","humastokes@gmail.com","humastokes@gmail.com","eddison.collier@gmail.com","eddison.collier@gmail.com"]],"container":"<table class=\"display\">\n  <thead>\n    <tr>\n      <th> <\/th>\n      <th>name<\/th>\n      <th>email<\/th>\n    <\/tr>\n  <\/thead>\n<\/table>","options":{"order":[],"autoWidth":false,"orderClasses":false,"columnDefs":[{"orderable":false,"targets":0}]}},"evals":[],"jsHooks":[]}</script>

<!--/html_preserve-->

##### **3.2: Who do we have emails for, yet are not on the guestlist?**

``` r
email_sep %>%
  anti_join(guest, by = "name") %>%
  knitr::kable()
```

| name            | email                             |
| :-------------- | :-------------------------------- |
| Turner Jones    | <tjjones12@hotmail.ca>            |
| Albert Marshall | <themarshallfamily1234@gmail.com> |
| Vivian Marshall | <themarshallfamily1234@gmail.com> |

##### **3.3: Make a guestlist that includes everyone we have emails for (in addition to those on the original guestlist).**

###### *Notes*

  - Guests Atlanta and Denzel Connolly, Chanelle Shah, Cosmo Dunkley,
    and Cai Mcdaniel are on the guest list but do not have emails - we
    can see this with full\_join.

<!-- end list -->

``` r
full_join(guest, email_sep, by = "name") %>%
  DT::datatable()
```

<!--html_preserve-->

<div id="htmlwidget-5f654c613b9b148e9e18" class="datatables html-widget" style="width:100%;height:auto;">

</div>

<script type="application/json" data-for="htmlwidget-5f654c613b9b148e9e18">{"x":{"filter":"none","data":[["1","2","3","4","5","6","7","8","9","10","11","12","13","14","15","16","17","18","19","20","21","22","23","24","25","26","27","28","29","30","31","32","33"],[1,1,1,1,2,2,3,4,5,5,5,6,6,7,7,8,9,10,11,12,12,12,12,12,13,13,14,14,15,15,null,null,null],["Sommer Medrano","Phillip Medrano","Blanka Medrano","Emaan Medrano","Blair Park","Nigel Webb","Sinead English","Ayra Marks","Atlanta Connolly","Denzel Connolly","Chanelle Shah","Jolene Welsh","Hayley Booker","Amayah Sanford","Erika Foley","Ciaron Acosta","Diana Stuart","Cosmo Dunkley","Cai Mcdaniel","Daisy-May Caldwell","Martin Caldwell","Violet Caldwell","Nazifa Caldwell","Eric Caldwell","Rosanna Bird","Kurtis Frost","Huma Stokes","Samuel Rutledge","Eddison Collier","Stewart Nicholls","Turner Jones","Albert Marshall","Vivian Marshall"],["PENDING","vegetarian","chicken","PENDING","chicken",null,"PENDING","vegetarian","PENDING","fish","chicken",null,"vegetarian",null,"PENDING","PENDING","vegetarian","PENDING","fish","chicken","PENDING","PENDING","chicken","chicken","vegetarian","PENDING",null,"chicken","PENDING","chicken",null,null,null],["PENDING","Menu C","Menu A","PENDING","Menu C",null,"PENDING","Menu B","PENDING","Menu B","Menu C",null,"Menu C","PENDING","PENDING","Menu A","Menu C","PENDING","Menu C","Menu B","PENDING","PENDING","PENDING","Menu B","Menu C","PENDING",null,"Menu C","PENDING","Menu B",null,null,null],["PENDING","CONFIRMED","CONFIRMED","PENDING","CONFIRMED","CANCELLED","PENDING","PENDING","PENDING","CONFIRMED","CONFIRMED","CANCELLED","CONFIRMED","CANCELLED","PENDING","PENDING","CONFIRMED","PENDING","CONFIRMED","CONFIRMED","PENDING","PENDING","PENDING","CONFIRMED","CONFIRMED","PENDING","CANCELLED","CONFIRMED","PENDING","CONFIRMED",null,null,null],["PENDING","CONFIRMED","CONFIRMED","PENDING","CONFIRMED","CANCELLED","PENDING","PENDING","PENDING","CONFIRMED","CONFIRMED","CANCELLED","CONFIRMED","PENDING","PENDING","PENDING","CONFIRMED","PENDING","CONFIRMED","CONFIRMED","PENDING","PENDING","PENDING","CONFIRMED","CONFIRMED","PENDING","CANCELLED","CONFIRMED","PENDING","CONFIRMED",null,null,null],["PENDING","CONFIRMED","CONFIRMED","PENDING","CONFIRMED","CANCELLED","PENDING","PENDING","PENDING","CONFIRMED","CONFIRMED","CANCELLED","CONFIRMED","PENDING","PENDING","PENDING","CONFIRMED","PENDING","CONFIRMED","CONFIRMED","PENDING","PENDING","PENDING","CONFIRMED","CONFIRMED","PENDING","CANCELLED","CONFIRMED","PENDING","CONFIRMED",null,null,null],["sommm@gmail.com","sommm@gmail.com","sommm@gmail.com","sommm@gmail.com","bpark@gmail.com","bpark@gmail.com","singlish@hotmail.ca","marksa42@gmail.com",null,null,null,"jw1987@hotmail.com","jw1987@hotmail.com","erikaaaaaa@gmail.com","erikaaaaaa@gmail.com","shining_ciaron@gmail.com","doodledianastu@gmail.com",null,null,"caldwellfamily5212@gmail.com","caldwellfamily5212@gmail.com","caldwellfamily5212@gmail.com","caldwellfamily5212@gmail.com","caldwellfamily5212@gmail.com","rosy1987b@gmail.com","rosy1987b@gmail.com","humastokes@gmail.com","humastokes@gmail.com","eddison.collier@gmail.com","eddison.collier@gmail.com","tjjones12@hotmail.ca","themarshallfamily1234@gmail.com","themarshallfamily1234@gmail.com"]],"container":"<table class=\"display\">\n  <thead>\n    <tr>\n      <th> <\/th>\n      <th>party<\/th>\n      <th>name<\/th>\n      <th>meal_wedding<\/th>\n      <th>meal_brunch<\/th>\n      <th>attendance_wedding<\/th>\n      <th>attendance_brunch<\/th>\n      <th>attendance_golf<\/th>\n      <th>email<\/th>\n    <\/tr>\n  <\/thead>\n<\/table>","options":{"columnDefs":[{"className":"dt-right","targets":1},{"orderable":false,"targets":0}],"order":[],"autoWidth":false,"orderClasses":false}},"evals":[],"jsHooks":[]}</script>

<!--/html_preserve-->

  - If we want to only include those guests that have email addresses
    from both tibbles (email and guest), we can omit those rows that
    have NA values for the email column in the full\_join tibble.

<!-- end list -->

``` r
full_join(guest, email_sep, by = "name") %>%
  select(name, email) %>%
  na.omit() %>%
  knitr::kable()
```

| name               | email                             |
| :----------------- | :-------------------------------- |
| Sommer Medrano     | <sommm@gmail.com>                 |
| Phillip Medrano    | <sommm@gmail.com>                 |
| Blanka Medrano     | <sommm@gmail.com>                 |
| Emaan Medrano      | <sommm@gmail.com>                 |
| Blair Park         | <bpark@gmail.com>                 |
| Nigel Webb         | <bpark@gmail.com>                 |
| Sinead English     | <singlish@hotmail.ca>             |
| Ayra Marks         | <marksa42@gmail.com>              |
| Jolene Welsh       | <jw1987@hotmail.com>              |
| Hayley Booker      | <jw1987@hotmail.com>              |
| Amayah Sanford     | <erikaaaaaa@gmail.com>            |
| Erika Foley        | <erikaaaaaa@gmail.com>            |
| Ciaron Acosta      | <shining_ciaron@gmail.com>        |
| Diana Stuart       | <doodledianastu@gmail.com>        |
| Daisy-May Caldwell | <caldwellfamily5212@gmail.com>    |
| Martin Caldwell    | <caldwellfamily5212@gmail.com>    |
| Violet Caldwell    | <caldwellfamily5212@gmail.com>    |
| Nazifa Caldwell    | <caldwellfamily5212@gmail.com>    |
| Eric Caldwell      | <caldwellfamily5212@gmail.com>    |
| Rosanna Bird       | <rosy1987b@gmail.com>             |
| Kurtis Frost       | <rosy1987b@gmail.com>             |
| Huma Stokes        | <humastokes@gmail.com>            |
| Samuel Rutledge    | <humastokes@gmail.com>            |
| Eddison Collier    | <eddison.collier@gmail.com>       |
| Stewart Nicholls   | <eddison.collier@gmail.com>       |
| Turner Jones       | <tjjones12@hotmail.ca>            |
| Albert Marshall    | <themarshallfamily1234@gmail.com> |
| Vivian Marshall    | <themarshallfamily1234@gmail.com> |
