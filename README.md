
<!-- README.md is generated from README.Rmd. Please edit that file -->

# The effectiveness of population-wide screening in reducing SARS-CoV-2 infection prevalence in Slovakia

This repository contains the data and code for our manuscript:

Pavelka S, Van-Zandvoort K, Abbott S, Sherratt K, Majdan M, CMMID
COVID-19 working group, Jarčuška P, Krajčí M, Flasche S*, Funk S* (\*:
equal contribution), *The effectiveness of population-wide screening in
reducing SARS-CoV-2 infection prevalence in Slovakia*. Available at
<https://cmmid.github.io/topics/covid19/Slovakia.html>.

### How to download or install

You can download the compendium as a zip from from this URL:
<https://github.com/sbfnk/covid19.slovakia.mass.testing/archive/master.zip>.

Or you can install this compendium as an R package,
`covid19.slovakia.mass.testing`, from GitHub with:

``` r
# install.packages("devtools")
remotes::install_github("sbfnk/covid19.slovakia.mass.testing")
```

### Included data sets

The repository contains three data sets:

The testing data set `ms.tst` can be loaded with

``` r
data(ms.tst)
```

Incidence of cases confirmed by PCR per county `PCR.inc` can be accessed
with

``` r
data(PCR.inc)
```

The `Rt.county` data set contains the estimated median reproduction
number in each county on 22 October 2020.

``` r
data(Rt.county)
```

This data set can be re-created using the The
[EpiNow2](https://epiforecasts.io/EpiNow2/) R package by running (noting
that it can take a long time to run depending on the hardware
available).

``` r
source(here::here("data-raw", "scripts", "rt.r"))
source(here::here("data-raw", "scripts", "convert_data.r"))
```

The [EpiNow2](https://epiforecasts.io/EpiNow2/) R package that is used
to estimate the reproduction numbers uses generation times and delay
distributions saved in `data-raw/data`. They can be re-generated by
running.

``` r
source(here::here("data-raw", "scripts", "rt-distributions.r"))
```

The Google mobility data set for Slovakia `mob.slo` visualised in
Supplementary Figure S4 can be accessed with

``` r
data(mob.slo)
```

### Figures and tables

To regenerate Table 1, run

``` r
county_table(here::here("figures", "table1.pdf"))
```

To regenerate Fig. 1, run

``` r
p <- pcr_incidence()
ggsave(here::here("figures", "fig1.pdf"), p, width = 7, height = 3)
```

To regenerate Fig. 2, run

``` r
rr <- risk_ratios()

ggsave(here::here("figures", "fig2a.pdf"), rr$figures$a,
       width = 7.5, height = 7, device = cairo_pdf)
ggsave(here::here("figures", "fig2b.pdf"), rr$figures$b,
       width = 7, height = 4, device = cairo_pdf)
ggsave(here::here("figures", "fig2c.pdf"), rr$figures$c,
       width = 7, height = 4, device = cairo_pdf)
rr$tables
```

To generate Table S1 and estimate the adjusted prevalence ratio, run

``` r
r <- regression("tableS1.pdf")
```

To regenerate Fig. S1 and estimate minimum specificity, run

``` r
spec <- estimate_min_specificity()
ggsave(here::here("figures", "figS1.png"), spec$figure,
       width = 3, height = 4, dpi = 600)
spec$estimate
#> [1] 0.9984521
```

To regenerate Fig. S4, run

``` r
p <- mobility()
ggsave(here::here("figures", "figS4.png"), p, width = 10, height = 6.5,
       dpi = 600)
```

To regenerate Fig. S6, run

``` r
p <- bed_occupancy()
ggsave(here::here("figures", "figS6.png"), p, width = 4, height = 3,
       dpi = 600)
```

To regenerate Fig. S7, run

``` r
p <- prevalence()
ggsave(here::here("figures", "figS7.png"), p, width = 6, height = 10,
       dpi = 600)
```

