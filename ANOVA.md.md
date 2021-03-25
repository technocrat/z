---
date: 2021-01-03T03:11
---
# ANOVA

[[[stattests]]]
[[Statistics]]
[[R]]
[[review]]

[source](https://statsandr.com/blog/anova-in-r/#fnref2)

[textbook](file:///home/roc/Documents/pdf/oneway_anova_basics.pdf)

> ANOVA: test to determine whether two or more population *means* are different^[ANOVA is a special case of a linear model].

    * Student t-test is used to compare 2 groups;
    * ANOVA generalizes the t-test beyond 2 groups, so it is used to compare 3 or more groups.

Besides one-way ANOVA^[one way as in one variable]: two-way ANOVA, mixed ANOVA, repeated measures ANOVA, etc.

Compares the two variances $\frac{variance_{between}}{variance_{within}}$ ratio compared to [Fisher probability distribution](https://en.wikipedia.org/wiki/Fisher%27s_exact_test).

Three categorical (modalities, treatments, factor in R) and on quantitative variables. $H_0$ *all* categories have equal mean. $H_1$ *at least one* has a different mean.

Assumes

* independence within and between groups
* normality of residuals in each group (histogram  or qqplot) Shapiro-Wilk or Kolmogorov-Smirnov test^[$H_0$: data come from a normal distribution] NB:  large N datasets almost always [depart from normality](https://stats.stackexchange.com/questions/2492/is-normality-testing-essentially-useless); question is whether it departs *enough* to make a particular test inappropriate.


* if not normal, Welch test^[transformation(s) may need to be applied on the raw data in the hope that residuals would better fit a normal distribution, or you would need to use the non-parametric version of the ANOVA—the Kruskal-Wallis test]
* to relieve normality assumption use non-paramentric Kruskal-Wallis test
* homodescasity of variance Durbin-Watson test ^[$H_0$ autocorrelation coefficient = 0$]

Assuming residuals follow a normal distribution, check whether the variances are equal across category or not. Boxplot range is a proxy for dispersion (variance). Confirm with Levene test^[$H_0$ variances are equal].

ANOVA can be calculated different ways

* oneway.test^[$H_0 = no difference; confirm]
* summary of aov()

ANOVA used when variances are equal; Welch test used when variances are unequal. oneway.test gives more complete statistics with argument `var.equal = FALSE` for Welch.

If $H_0$ rejected, that's it. If not, proceed to find out *which* group differs from the others with *post-hoc* pairwise tests.

Multiple testing problem: with as few as 3 tests being considered, 0.1426 chance of observing at least one significant result by chance, even if all of the tests are actually not significant. Approaches 0.99 with 14 groups. Post-hoc tests adjust $\alpha$ to give a "gloval" significance level.

* Tukey HSD^[Honest Significant Difference] is used to compare all groups to each other (so all possible comparisons of 2 groups)^[$H_0$ two groups are equal &there4; if p-value < $\alpha$ it is rejected]
* Dunnett is used to make comparisons with a reference group^[Same null evaluation]. For example, consider 2 treatment groups and one control group. If you only want to compare the 2 treatment groups with respect to the control group, and you do not want to compare the 2 treatment groups to each other, the Dunnett’s test is preferred.^[The reference category can be changed with the relevel() function (or with the {questionr} addin).] 
* other p-values adjustment methods use `the pairwise.t.test()`

``` r
suppressPackageStartupMessages({
  library(car)
  library(dplyr)
  library(ggplot2)
  library(ggpubr)
  library(multcomp)
  library(palmerpenguins)
  library(patchwork)
})

dat <- penguins %>% dplyr::select(species, flipper_length_mm)

summary(dat)
#>       species    flipper_length_mm
#>  Adelie   :152   Min.   :172.0
#>  Chinstrap: 68   1st Qu.:190.0
#>  Gentoo   :124   Median :197.0
#>                  Mean   :200.9
#>                  3rd Qu.:213.0
#>                  Max.   :231.0
#>                  NA's   :2

p1 <- ggplot(dat) +
  aes(x = species, y = flipper_length_mm, color = species) +
  geom_jitter() +
  theme(legend.position = "none") +
  theme_minimal()

p2 <- ggplot(dat) +
  aes(x = species, y = flipper_length_mm, color = species) +
  geom_boxplot() +
  theme(legend.position = "none") +
  theme_minimal()

p3 <- ggplot(dat) +
  aes(flipper_length_mm, fill = species) +
  geom_dotplot(method = "histodot", binwidth = 1.5) +
  theme(legend.position = "none") +
  theme_minimal()

p1 + p2 + p3
#> Warning: Removed 2 rows containing missing values (geom_point).
#> Warning: Removed 2 rows containing non-finite values (stat_boxplot).
#> Warning: Removed 2 rows containing non-finite values (stat_bindot).
```

![](https://i.imgur.com/4Dat15D.png)

``` r
res_aov <- aov(flipper_length_mm ~ species, data = dat)

resids <- data.frame(.resid = res_aov$residuals)

# histogram
p4 <- ggplot(resids, aes(.resid)) +
  geom_histogram(color = "black", fill = "grey") +
  theme_minimal()

p5 <- ggplot(resids, aes(sample = .resid)) +
  stat_qq() +
  stat_qq_line() +
  theme_minimal()

p4 + p5
#> `stat_bin()` using `bins = 30`. Pick better value with `binwidth`.
```

![](https://i.imgur.com/XbZSjhK.png)

``` r
shapiro.test(res_aov$residuals)
#>
#>  Shapiro-Wilk normality test
#>
#> data:  res_aov$residuals
#> W = 0.99452, p-value = 0.2609

leveneTest(flipper_length_mm ~ species, data = dat)
#> Levene's Test for Homogeneity of Variance (center = median)
#>        Df F value Pr(>F)
#> group   2  0.3306 0.7188
#>       339

aggregate(flipper_length_mm ~ species,
  data = dat,
  function(x) round(c(mean = mean(x), sd = sd(x)), 2)
)
#>     species flipper_length_mm.mean flipper_length_mm.sd
#> 1    Adelie                 189.95                 6.54
#> 2 Chinstrap                 195.82                 7.13
#> 3    Gentoo                 217.19                 6.48

group_by(dat, species) %>%
  summarise(
    mean = mean(flipper_length_mm, na.rm = TRUE),
    sd = sd(flipper_length_mm, na.rm = TRUE)
  )
#> `summarise()` ungrouping output (override with `.groups` argument)
#> # A tibble: 3 x 3
#>   species    mean    sd
#>   <fct>     <dbl> <dbl>
#> 1 Adelie     190.  6.54
#> 2 Chinstrap  196.  7.13
#> 3 Gentoo     217.  6.48

oneway.test(flipper_length_mm ~ species,
  data = dat,
  var.equal = TRUE # assuming equal variances
)
#>
#>  One-way analysis of means
#>
#> data:  flipper_length_mm and species
#> F = 594.8, num df = 2, denom df = 339, p-value < 2.2e-16

res_aov <- aov(flipper_length_mm ~ species,
  data = dat
)

summary(res_aov)
#>              Df Sum Sq Mean Sq F value Pr(>F)
#> species       2  52473   26237   594.8 <2e-16 ***
#> Residuals   339  14953      44
#> ---
#> Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
#> 2 observations deleted due to missingness

oneway.test(flipper_length_mm ~ species,
  data = dat,
  var.equal = FALSE # assuming unequal variances
)
#>
#>  One-way analysis of means (not assuming equal variances)
#>
#> data:  flipper_length_mm and species
#> F = 614.01, num df = 2.00, denom df = 172.76, p-value < 2.2e-16

post_test <- glht(res_aov,
  linfct = mcp(species = "Tukey")
)

summary(post_test)
#>
#>   Simultaneous Tests for General Linear Hypotheses
#>
#> Multiple Comparisons of Means: Tukey Contrasts
#>
#>
#> Fit: aov(formula = flipper_length_mm ~ species, data = dat)
#>
#> Linear Hypotheses:
#>                         Estimate Std. Error t value Pr(>|t|)
#> Chinstrap - Adelie == 0   5.8699     0.9699   6.052 6.65e-09 ***
#> Gentoo - Adelie == 0     27.2333     0.8067  33.760  < 1e-09 ***
#> Gentoo - Chinstrap == 0  21.3635     1.0036  21.286  < 1e-09 ***
#> ---
#> Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
#> (Adjusted p values reported -- single-step method)

par(mar = c(3, 8, 3, 3))
plot(post_test)
```

![](https://i.imgur.com/CFJVdbM.png)

``` r

TukeyHSD(res_aov)
#>   Tukey multiple comparisons of means
#>     95% family-wise confidence level
#>
#> Fit: aov(formula = flipper_length_mm ~ species, data = dat)
#>
#> $species
#>                       diff       lwr       upr p adj
#> Chinstrap-Adelie  5.869887  3.586583  8.153191     0
#> Gentoo-Adelie    27.233349 25.334376 29.132323     0
#> Gentoo-Chinstrap 21.363462 19.000841 23.726084     0

plot(TukeyHSD(res_aov))
```

![](https://i.imgur.com/dLIbETS.png)

``` r
# Dunnett's test:
post_test <- glht(res_aov,
  linfct = mcp(species = "Dunnett")
)

summary(post_test)
#>
#>   Simultaneous Tests for General Linear Hypotheses
#>
#> Multiple Comparisons of Means: Dunnett Contrasts
#>
#>
#> Fit: aov(formula = flipper_length_mm ~ species, data = dat)
#>
#> Linear Hypotheses:
#>                         Estimate Std. Error t value Pr(>|t|)
#> Chinstrap - Adelie == 0   5.8699     0.9699   6.052 7.59e-09 ***
#> Gentoo - Adelie == 0     27.2333     0.8067  33.760  < 1e-10 ***
#> ---
#> Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
#> (Adjusted p values reported -- single-step method)

par(mar = c(3, 8, 3, 3))
plot(post_test)
```

![](https://i.imgur.com/WFzv7a0.png)

``` r
# Change reference category:
dat$species <- relevel(dat$species, ref = "Gentoo")

# Check that Gentoo is the reference category:
levels(dat$species)
#> [1] "Gentoo"    "Adelie"    "Chinstrap"

res_aov2 <- aov(flipper_length_mm ~ species,
  data = dat
)

# Dunnett's test:
post_test <- glht(res_aov2,
  linfct = mcp(species = "Dunnett")
)

summary(post_test)
#>
#>   Simultaneous Tests for General Linear Hypotheses
#>
#> Multiple Comparisons of Means: Dunnett Contrasts
#>
#>
#> Fit: aov(formula = flipper_length_mm ~ species, data = dat)
#>
#> Linear Hypotheses:
#>                         Estimate Std. Error t value Pr(>|t|)
#> Adelie - Gentoo == 0    -27.2333     0.8067  -33.76   <1e-10 ***
#> Chinstrap - Gentoo == 0 -21.3635     1.0036  -21.29   <1e-10 ***
#> ---
#> Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
#> (Adjusted p values reported -- single-step method)

par(mar = c(3, 8, 3, 3))
plot(post_test)
```

![](https://i.imgur.com/EAsc25A.png)

``` r
pairwise.t.test(dat$flipper_length_mm, dat$species,
  p.adjust.method = "holm"
)
#>
#>  Pairwise comparisons using t tests with pooled SD
#>
#> data:  dat$flipper_length_mm and dat$species
#>
#>           Gentoo  Adelie
#> Adelie    < 2e-16 -
#> Chinstrap < 2e-16 3.8e-09
#>
#> P value adjustment method: holm

# Edit from here
x <- which(names(dat) == "species") # name of grouping variable
y <- which(
  names(dat) == "flipper_length_mm" # names of variables to test
)
method1 <- "anova" # one of "anova" or "kruskal.test"
method2 <- "t.test" # one of "wilcox.test" or "t.test"
my_comparisons <- list(c("Chinstrap", "Adelie"), c("Gentoo", "Adelie"), c("Gentoo", "Chinstrap")) # comparisons for post-hoc tests
# Edit until here


# Edit at your own risk
for (i in y) {
  for (j in x) {
    p <- ggboxplot(dat,
      x = colnames(dat[j]), y = colnames(dat[i]),
      color = colnames(dat[j]),
      legend = "none",
      palette = "npg",
      add = "jitter"
    )
    print(
      p + stat_compare_means(aes(label = paste0(..method.., ", p-value = ", ..p.format..)),
        method = method1, label.y = max(dat[, i], na.rm = TRUE)
      )
      + stat_compare_means(comparisons = my_comparisons, method = method2, label = "p.format") # remove if p-value of ANOVA or Kruskal-Wallis test >= alpha
    )
  }
}
#> Warning: Removed 2 rows containing non-finite values (stat_boxplot).
#> Warning: Removed 2 rows containing non-finite values (stat_compare_means).
#> Warning: Removed 2 rows containing non-finite values (stat_signif).
#> Warning: Removed 2 rows containing missing values (geom_point).
```

![](https://i.imgur.com/edHr9Jc.png)
