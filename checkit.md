---
date: 2020-12-16T16:13
---

# Checkit

[[[top]]] 

[plurr haskell blog](https://plurrrr.com/archive/2020/05/22.html)

[Power of test](https://predictivehacks.com/how-to-get-the-power-of-test-in-hypothesis-testing-with-binomial-distribution/)

[Announcing Ema - Static Sites in Haskell](https://notes.srid.ca/ema-announce)

[clock: low-level datetime api](https://clock.r-lib.org/articles/articles/motivations.html)

[latex2exp for base and ggplot2](https://github.com/stefano-meschiari/latex2exp)

[Effect of duplicated values](https://www.r-bloggers.com/2021/04/a-curious-fact-on-the-diamonds-dataset/)

[Alternative to correlation coefficient that works also for categorical variables](https://rviews.rstudio.com/2021/04/15/an-alternative-to-the-correlation-coefficient-that-works-for-numeric-and-categorical-variables/)

[Geographic functions in zipcodeR](https://gavinrozzi.github.io/zipcodeR/articles/geographic.html)

[TSForecasting](https://github.com/rakshitha123/TSForecasting#tsforecasting)

[Do Judge a Test by its CoverCombining Combinatorial and Property-Based Testing](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC7984547/pdf/978-3-030-72019-3_Chapter_10.pdf/?tool=EBI)

[ggh4x ggplot hacks](https://cran.r-project.org/web/packages/ggh4x/index.html)

[cvCovEst: Cross-Validated Covariance Matrix Estimation](https://cran.r-project.org/web/packages/cvCovEst/vignettes/using_cvCovEst.html)

[crosstable](https://cran.r-project.org/web/packages/crosstable/vignettes/crosstable.html)

[geom atlas](https://ivelasq.rbind.io/blog/other-geoms/)

[hmisc explainer](https://www.nicholas-ollberding.com/post/an-introduction-to-the-harrell-verse-predictive-modeling-using-the-hmisc-and-rms-packages/)

[torch](https://blogs.rstudio.com/ai/posts/2021-03-10-forecasting-time-series-with-torch_1/)

[Go in R](https://github.com/rgonomic/rgo)

[data table](https://hutsons-hacks.info/data-table-everything-you-need-to-know-to-get-you-started-in-r)

[Data Explorer](https://theautomatic.net/2021/03/03/faster-data-exploration-with-dataexplorer/?utm_source=rss&utm_medium=rss&utm_campaign=faster-data-exploration-with-dataexplorer)

[ppsr](https://paulvanderlaken.com/2021/03/02/ppsr-live-on-cran/)

[XGBoost](https://datageeek.com/2021/03/02/time-series-forecasting-with-xgboost-and-feature-importance/)

[ADAM forecasting packages](https://openforecast.org/adam/index.html)

[rfast](https://github.com/RfastOfficial/Rfast)

[blogdown changes](https://community.rstudio.com/t/announcing-blogdown-v1-0/93449)

[autostsm](https://cran.r-project.org/web/packages/autostsm/vignettes/autostsm_vignette.html)

[cachem](https://cran.r-project.org/web/packages/cachem/index.html)

[eList: List Comprehension and Tools](https://cran.r-project.org/web/packages/eList/index.html)

[rtables](https://cran.r-project.org/web/packages/rtables/vignettes/introduction.html)

[OTrecod: Data Fusion using Optimal Transportation Theory](https://cran.r-project.org/web/packages/OTrecod/index.html)

[spark](https://blogs.rstudio.com/ai/posts/2020-12-14-sparklyr-1.5.0-released/)

[viz course](https://wilkelab.org/SDS375/syllabus.html)

[regression as master template for common statistical tests](https://lindeloev.github.io/tests-as-linear/)

[svglite](https://www.tidyverse.org/blog/2021/02/svglite-2-0-0/)

[case_when, joins and fcase](https://themockup.blog/posts/2021-02-13-joins-vs-casewhen-speed-and-memory-tradeoffs/)

[box](https://github.com/klmr/box)

[ConfusionTableR](https://hutsons-hacks.info/confusiontabler-a-package-to-tidy-outputs-of-confusion-matrix-objects-for-storage-in-databases)

[ragg fonts](https://www.tidyverse.org/blog/2021/02/modern-text-features/)

[R Advanced Solutions](https://advanced-r-solutions.rbind.io/)

[{target}](https://ropensci.org/blog/2021/02/03/targets/)

[{ networktree}](https://www.zeileis.org/news/networktree100/)

[{wrapr}](https://win-vector.com/2021/02/05/introducing-wraprbc/)

[changepoint detection](https://www.marinedatascience.co/blog/2019/09/28/comparison-of-change-point-detection-methods/)

[target workflow package](https://ropensci.org/technotes/2021/02/03/targets/)

[AMZ Athena](https://rud.is/b/2021/02/02/amazon-athena-dbplyr-implicit-usage-of-presto-functions-and-making-json-casting-great-again/)

[interesting packages](https://github.com/ThinkR-open)

[Hypothesis checking](https://statsandr.com/blog/hypothesis-test-by-hand/)

[Anomoly detection](file://home/roc/Documents/Stats/Downloads/anomolies.pdf)

{sparkTable}

{ClustVarLV}

{cwgtools}

[Faraday](file:///home/roc/Documents/pdf/Faraway-PRA.pdf)

[Modelling Count Data in A Multilevel Framework](file:///home/roc/projects/countdata_modelling/index.html)

[Structural Equation Models](https://rviews.rstudio.com/2021/01/22/sem-time-series-modeling/)

[marginal effects](https://cran.r-project.org/web/packages/margins/vignettes/Introduction.html)

[mixed effects](https://strengejacke.github.io/ggeffects/)

[Overfitting](https://win-vector.com/2021/01/04/the-nature-of-overfitting/)

[regtools](https://cran.r-project.org/web/packages/regtools/index.html)

``` r
library(modeldata)
library(mgcv)
#> Loading required package: nlme
#> This is mgcv 1.8-33. For overview type 'help("mgcv-package")'.
#> Loading required package: nlme
#> This is mgcv 1.8-33. For overview type 'help("mgcv-package")'.

data("two_class_dat")

mod <- gam(Class ~ s(A) + s(B), data = two_class_dat, family = binomial)

# The `trans` argument puts them back on the probability scale

plot(mod, trans = function(x) binomial()$linkinv(x), pages = 1)
```

![](https://i.imgur.com/563xWaX.png)


[baseset](https://ropensci.org/blog/2021/01/19/introducing-baseset/)

[binomTools](https://user2011.r-project.org/TalkSlides/Contributed/18Aug_0950_FocusVI_3-GLM-3_Hansen.pdf)

[Strong typing](https://github.com/moodymudskipper/typed)

[PMCCRPlus](https://cran.r-project.org/web/packages/PMCMRplus/vignettes/QuickReferenceGuide.html) [paper](https://cran.r-project.org/web/packages/PMCMR/vignettes/PMCMR.pdf)

[Introduction to Econometrics with R](https://www.econometrics-with-r.org/index.html)

[Variable selection](https://win-vector.com/2021/01/12/variable-utility-is-not-intrinsic/) and [related code](https://github.com/WinVector/Examples/tree/main/Variable_Utility_is_not_Intrinsic)

[Augmented Dynamic Adaptive Model](https://forecasting.svetunkov.ru/en/2021/01/13/the-creation-of-adam-next-step-in-statistical-forecasting/)

[CRAN Task View: Functional Data Analysis](https://cran.r-project.org/web/views/FunctionalData.html)

[Dunbar's number](https://generativist.falsifiable.com/metaverse/dunbars-number-is-quadratic)

[A strategy to apply machine learning to small datasets](https://www.nature.com/articles/s41524-018-0081-z)

[predictive power score](https://paulvanderlaken.com/2021/01/12/ppsr-r-package-predictive-power-score/)

[logistic feature engineering](https://appsilon.com/r-logistic-regression/)

[smoothing](https://win-vector.com/2021/01/07/smoothing-isnt-always-safe/)

[rlist](https://github.com/tomasokal/rtist)

gitlab: enterprise platform

[gnome snippet synch](https://github.com/oae/gnome-shell-extensions-sync)

[basic classification](https://coreysparks.github.io/blog/demography-predictive-modeling-working-group-basic-methods-for-classification/)

[bootsrapping time series](https://datageeek.com/2020/12/14/bootstrapping-time-series-for-gold-rush/)

[Category theory relationships](https://www.johndcook.com/category_concepts.png)

[cd demographics](https://arilamstein.com/blog/2020/08/11/exploring-the-demographics-of-us-congressional-districts-in-r/)

[cluster analysis](https://coreysparks.github.io/blog/demographic-modeling-cluster-analysis/)

[cluster1](https://coreysparks.github.io/blog/demographic-modeling-cluster-analysis/)

[cluster2](https://coreysparks.github.io/blog/demography-predictive-modeling-working-group-basic-methods-for-classification/)

[co-variate covariating](https://shouldbewriting.netlify.app/posts/2020-08-11-when-predictors-covary/)

[code highlighting in Rmd](https://cran.r-project.org/web/packages/flair/vignettes/how_to_flair.html)

[cook's distance and other influence measures](https://cran.r-project.org/web/packages/olsrr/vignettes/influence_measures.html)

[data scrubbing](https://cran.r-project.org/web/packages/daqapo/vignettes/Introduction-to-DaQAPO.html)

[dendograms](https://rpubs.com/Kushan/384313)

[differences of time series](https://cran.r-project.org/web/packages/micompr/vignettes/paper.pdf)

[dissimilarity](https://cran.r-project.org/web/packages/IncDTW/vignettes/Theory_and_Applications_for_the_R_Package_IncDTW.pdf)

[dynamic time warping](https://cran.r-project.org/web/packages/IncDTW/vignettes/Theory_and_Applications_for_the_R_Package_IncDTW.pdf)

[easystats](https://easystats.github.io/easystats/)

[econometrics tutorial](https://hhsievertsen.github.io/applied_econ_with_r/#Welcome)

[evolving color palettes](http://gradientdescending.com/evolve-new-colour-palettes-in-r-with-evopalette/)

[forecast doc](https://cran.r-project.org/web/packages/forecastML/forecastML.pdf)

[front end to LaTeX sparklines](https://github.com/borisveytsman/ltxsparklines)

[geofacet](https://cran.r-project.org/web/packages/geofacet/geofacet.)

[ggframe wrapper for data frame plotting](https://github.com/moodymudskipper/ggframe)

[ggplot themes for rmarkdown](https://thomasadventure.blog/posts/mdthemes-is-on-cran-markdown-powered-themes-for-ggplot2/)

[gitHub - moodymudskipper/flow: View and Browse Code Using Flow Diagrams](https://github.com/moodymudskipper/flow)

[gower distance](https://cran.r-project.org/web/packages/gower/vignettes/intro.pdf)

[htmltable](https://www.r-bloggers.com/news-in-htmltable-2-0/)

[inline sparklines](https://github.com/leeper/sparktex)

[interactionR](https://cran.r-project.org/web/packages/interactionR/interactionR.pdf)

[kube framework](https://kube7.imperavi.com/)

[lists to Rmarkdown](https://cran.r-project.org/web/packages/listdown/vignettes/listdown.html)

[loess decomp](https://www.scb.se/contentassets/ca21efb41fee47d293bbee5bf7be7fb3/stl-a-seasonal-trend-decomposition-procedure-based-on-loess.pdf)

[markdown themes for ggplot](https://thomasadventure.blog/posts/mdthemes-is-on-cran-markdown-powered-themes-for-ggplot2/)

[matrix profiling method of time series](https://www.cs.ucr.edu/~eamonn/MatrixProfile.html)

[meta package](https://randr.rocks/post/pointblank-0-6/)

[meta-cognition](https://www.ribbonfarm.com/glossary/#legibility)

[nearcasting--forecasting methods](https://community.tibco.com/feed-items/nearcasting-comparison-covid-19-projection-methods)

[nimble R->C++ compiler](https://r-nimble.org/what-is-nimble)

> numb about equal operator 0.11.3 adds the %==% operator. %==% implements the base R function all.equal(), comparing two numeric or integer vectors for near-equality. Unlike all.equal, %==% returns a vector for every element of the left-hand and right-hand sides. This makes it useful in functions like which or dplyr::filter.

[one-hour package](https://www.pipinghotdata.com/posts/2020-10-25-your-first-r-package-in-1-hour/)

[outlier detection](https://www.statsandr.com/blog/outliers-detection-in-r/#additional-remarks)

[overfitting](https://datascience.stackexchange.com/questions/80868/overfitting-in-linear-regression  )

[package TSrepr](https://cran.r-project.org/web/packages/TSrepr/vignettes/TSrepr_representations_of_time_series.html)

[packette - Fraction Matrix Operations](https://www.stats-et-al.com/2020/06/r-packette-fraction-matrix-operations.html)

[packette](https://www.stats-et-al.com/2020/06/r-packette-fraction-matrix-operations.html)

[patchwork insets](https://www.data-imaginist.com/2020/insetting-a-new-patchwork-version/s)

[plotting multiple models](https://win-vector.com/2020/10/12/model-homotopies-in-the-wild/)

[power analysis](https://www.rips-irsp.com/articles/10.5334/irsp.181/)

[questionr](https://juba.github.io/questionr/reference/index.html)

[regression](https://freakonometrics.hypotheses.org/60146)

[representation of time series](https://cran.r-project.org/web/packages/TSrepr/vignettes/TSrepr_representations_of_time_series.html)

[rethinking](https://github.com/rmcelreath/statrethinking_winter2019)

[run-length encoding](https://github.com/coolbutuseless/purler)

[runchart](https://github.com/johnmackintosh/runcharter/)

[social science](https://fantasticanachronism.com/2020/09/11/whats-wrong-with-social-science-and-how-to-fix-it/)

[stacks: ensemble models](https://github.com/tidymodels/stacks)

[state space](https://cran.r-project.org/web/packages/KFAS/vignettes/KFAS.pdf)

[tidy modeling](https://www.tmwr.org/)

[two cultures](https://matloff.wordpress.com/2020/07/26/efron-updates-breimans-two-cultures-essay/)