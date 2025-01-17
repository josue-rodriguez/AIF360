
<!-- README.md is generated from README.Rmd. Please edit that file -->

# AI Fairness 360 (AIF360) R Package

<!-- badges: start -->

[![CRAN_Status_Badge](http://www.r-pkg.org/badges/version/aif360)](https://cran.r-project.org/package=aif360)
<!-- badges: end -->

## Overview

The AI Fairness 360 toolkit is an open-source library to help detect and
mitigate bias in machine learning models. The AI Fairness 360 R package
includes a comprehensive set of metrics for datasets and models to test
for biases, explanations for these metrics, and algorithms to mitigate
bias in datasets and models.

## Installation

Install the CRAN version:

``` r
install.packages("aif360")
```

Or install the development version from GitHub:

``` r
# install.packages("devtools")
devtools::install_github("Trusted-AI/AIF360/aif360/aif360-r")
```

Then, use the install_aif360() function to install AIF360:

``` r
library(aif360)
install_aif360()
```

## Installation methods

AIF360 is distributed as a Python package and so needs to be installed
within a Python environment on your system. By default, the
install_aif360() function attempts to install AIF360 within an isolated
Python environment (“r-reticulate”).

You can check using `reticulate::conda_python()` and
`reticulate::py_config()`

### Suggested steps

1)  Install reticulate and check if you have miniconda installed. If you
    do, go to step 2.

``` r
install.packages("reticulate")
reticulate::conda_list()
```

If you get an error:
`Error: Unable to find conda binary. Is Anaconda installed?`, please
install miniconda

``` r
reticulate::install_miniconda()
```

If everything worked, you should get the message:

`* Miniconda has been successfully installed at '/home/rstudio/.local/share/r-miniconda'.`

You can double check:

    reticulate::conda_list()

You will get something like this:

              name                                                              python
    1  r-miniconda                   /home/rstudio/.local/share/r-miniconda/bin/python
    2 r-reticulate /home/rstudio/.local/share/r-miniconda/envs/r-reticulate/bin/python

2)  You can create a new conda env and then configure which version of
    Python to use:

``` r
reticulate::conda_create(envname = "r-test")
reticulate::use_miniconda(condaenv = "r-test", required = TRUE)
```

Check that everything is working `reticulate::py_config()`.

3)  If you haven’t yet, please install the aif360 package
    `install.packages("aif360")` and then install aif360 dependencies

``` r
aif360::install_aif360(envname = "r-test")
```

Note that this step should take a few minutes and the R session will
restart.

4)  You can now activate your Python environment

``` r
reticulate::use_miniconda(condaenv = "r-test", required = TRUE)
```

## Getting Started

``` r
library(aif360)
load_aif360_lib()
```

``` r
# load a toy dataset
data <- data.frame("feature1" = c(0,0,1,1,1,1,0,1,1,0),
                   "feature2" = c(0,1,0,1,1,0,0,0,0,1),
                   "label" = c(1,0,0,1,0,0,1,0,1,1))

# format the dataset
formatted_dataset <- aif360::aif_dataset(data_path = data,
                                          favor_label = 0,
                                          unfavor_label = 1,
                                          unprivileged_protected_attribute = 0,
                                          privileged_protected_attribute = 1,
                                          target_column = "label",
                                          protected_attribute = "feature1")
```

## Troubleshooting

If you encounter any errors during the installation process, look for
your issue here and try the solutions.

### Locked binding

If you get an error: `cannot change value of locked binding`, please
restart the R session. Then try reactivating your Python environment and
running the following commands exactly once:

``` r
library(aif360) 
load_aif360_lib()
```

## Contributing

If you’d like to contribute to the development of aif360, please read
[these guidelines](CONTRIBUTING.md).

Please note that the aif360 project is released with a [Contributor Code
of Conduct](CODEOFCONDUCT.md). By contributing to this project, you
agree to abide by its terms.
