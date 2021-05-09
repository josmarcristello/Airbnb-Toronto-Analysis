# Prediction of Airbnb prices with Machine Learning in the Region of Toronto, Ontario, Canada

## Introduction
The notebooks in this repository are a case study of the properties listed in Toronto, Ontario, Canada as of 2021, February 08. The model uses data from [Airbnb](https://news.airbnb.com/about-us/), but also uses geolocation data ([MapQuest](https://business.mapquest.com/company)) and natural language processing though [VADER lexicon](https://github.com/cjhutto/vaderSentiment) Lexicon. The repository is fully open-sourced under the [MIT License](https://choosealicense.com/licenses/mit/).

This study was originally submitted by the author as a capstone project to obtain the title of Scientist of Data Scientist at PUC/MG University (Pontíficia Universidade Católica de Minas Gerais, Brazil).


## Table of Contents
1. [Installation](#Installation)
2. [Usage](#Usage)
3. [File Descriptions](#File-Descriptions)
4. [Results](#Results)
5. [Limitations](#Limitations)
6. [Acknowledgements](#Acknowledgements)


## Installation
All necessary libraries are shown in the beginning of each notebook. The code was tested with [Python 3.9.1 64-bit](https://www.python.org/downloads/release/python-391/), but should work with version 3.x. 

The recommended way to install the libraries is with [Pypi](https://pypi.org), using pip:
```bash
> pip install <libraryname>
```
Before opening an issue, make sure your libraries are updated:
```bash
> pip install --upgrade <libraryname>
```

## Usage
Either: 

* Clone the repository, which will give you all the data sources used in the original study. Please see [Acknowledgements](#Acknowledgements) for licensing of each data source information.

* Use the notebooks, which will download and process all the data, and additionally allow for selecting different dates or regions.

## File Descriptions

1. [**download_airbnb.ipynb**](./1-source/download_airbnb.ipynb) - First notebook to run. Downloads data from [InsideAirbnb.com](http://insideairbnb.com/about.html). If necessary, configure a different region and/or dates here.

2. [**GEO_process_coordinates.ipynb**](./1-source/GEO_process_coordinates.ipynb) - Query [MapQuest](https://business.mapquest.com/company) API to obtain geography data about each property longitude-latitude pair. Please note that free accounts are limited to 15k requests/month.

3. [**NLP_process_descriptions.ipynb**](./1-source/NLP_process_descriptions.ipynb) and [**NLP_process_reviews.ipynb**](./1-source/NLP_process_reviews.ipynb) - Apply sentiment analysis using [VADER lexicon](https://github.com/cjhutto/vaderSentiment) on, respectively, descriptions and reviews text.

4. [**analysis.ipynb**](./1-source/analysis.ipynb) - Requires all notebooks to have been successfully run (or repository to be cloned), and is responsible for all the data cleaning, merging of previously generated data sources, exploratory data analysis (EDA), feature engineering, model creation, training and results.

5. [**TCC_PUCMG_Report.pdf**](./3-report/TCC_PUCMG_Report.pdf) and [**TCC_PUCMG_Presentation.pptx**](./4-presentation/TCC_PUCMG_Presentation.pptx.pdf) - Respectively, the report and presentation of this study. Both in Portuguese (PT-BR). Rest of the repository is in English.

## Results
The selected model used Gradient Boosting (XGBoost Library) and had a R² of 0.691 with MSE of 0.125. The notebook had a very extensive data analysis, and contains recommendations for a host that wants to maximize their profit, or a guest that wants to maximize their cost-benefit when renting a place. For the guest example, in Toronto:
* Always rent a place for the exact number of people traveling with you.
    - E.g. In general, its cheaper (price per person) to rent a place sized for 3-people while traveling with 3 people than travelling alone and renting a smaller place for one person.
* Properties in the south of Toronto City are more expensive (Particularly in [Old Toronto](https://upload.wikimedia.org/wikipedia/commons/9/9a/Toronto_map.png)).
* Houses are cheaper than apartments. Hotel rooms seemed to be in between, but they are not numerous enough for this conclusion to be statistically significant.
* Renting Shared rooms is cheaper than renting private rooms which is also cheaper than renting the entire property.
* If possible, always choose listings from [Superhosts](https://www.airbnb.com/help/article/829/how-do-i-become-a-superhost). Surprisingly, this does not have a significant impact on pricing, and is a good way to get a more guaranteed quality of service.
* Exclude amenities that aren't going to be used.
    - E.g. If you do not intend to use the building's Gym, try to get a property without. Other amenities with significant price impact: Dishwasher, TV, Dryer, Pool.


## Limitations
The '**price**' variable available in the dataset is, exclusively, the listing price at the moment of collection. This is a problem because Airbnb uses dynamic pricing, and also because it is disconsidering all of historical data. For example, there may be situations where a host started with a lower pricing to rack up many good reviews, and gradually increased pricing to current value. Such cases would not be considered by the model, since historical prices are not available. This is, in the opinion of the author, the biggest difficulty in achieving a higher precision with the model.

## Acknowledgements

* [InsideAirbnb.com](http://insideairbnb.com/about.html) for open-sourcing under [Creative Commons CC0](https://choosealicense.com/licenses/cc0-1.0/) all the Airbnb data of the listings in toronto and of the reviews as well.
* [MapQuest](https://business.mapquest.com/company) for all the reverse geolocation data through their API. Data is not open source, but their free account allow for up to [15k queries](https://developer.mapquest.com/plans) per month.
* [C.J. Hutto](https://github.com/cjhutto) for developing and open-sourcing under [MIT License](https://choosealicense.com/licenses/mit/) the [VADER lexicon](https://github.com/cjhutto/vaderSentiment) used for sentiment analysis.