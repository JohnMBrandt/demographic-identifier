# demographic-identifier
Computer vision and NLP to identify age, race, and gender in photographs

## Installation

This Python + R toolkit requires a Python 3.6 virtual environment with the `cv2`, `dlib`, `numpy`, `keras`, and `tensorflow` modules, as well as the R packages `tidyverse`, `gender`, `plyr`, and `jsonlite` packages. The virtualenv included in this repository shows the barebones file structures for the virtualenv, but does not include the actual `.so` files, as they exceed the github size limit.

## Useage

The input data should be in the form of a compressed streaming json file returned from the Twitter API. The `download_data.R` file will identify all the user profile images from the API results and download every image to the `img` folder. When run in order, the `age-gender-image.py`, `process_results.R`, and `calc_gender_age.R`, scripts will return a CSV in the `results` folder that contains the twitter handle and associated estimated age and gender.

## Details

This uses a combination of the age-gender-estimation project found [here](https://github.com/yu4u/age-gender-estimation) and the gender R package found [here](https://github.com/ropensci/gender). The age-gender-estimation project has been reworked to be optimized for twitter images, and works as an rmask-CNN ran through Keras that has learned age and gender for 500,000 training images. The mean error is 3 years for age, and the accuracy rate for gender is 95%. These estimates are validated by matching the name, when available, to US census data on gender percentiles by first name. In more than 95% of cases, these two estimates match. When they do not, the highest confidence estimate is used as the gender prediction. Pairing these two modes of estimating gender allows an estimate where only one of the two data sources are available (User image containing a face, or first name). 
