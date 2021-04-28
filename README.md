Predicting US Vacancy Rates by Zip Code
==============================

Springboard Capstone 2

**the problem**
*What is the current vacancy rate in a certain zip code?*

Lack of specific current vacancy rate data hampers real estate investors ability to definitively know a key factor in their decision for where to invest. Currently many investors rely on local knowledge of an area - ie. local real estate agents, property managers etc. for this knowledge - so the info is hard to get and hard to tell if accurate.  There is vacancy rate data for the US as a country in up to the current year on the Federal Reserve of Economic Development website (FRED). There is also vacancy rate data by zip code available up to 2018 through the American Housing Community, but currently there does not seem to be vacancy rate data by zipcode for the current year.

**the approach**
The goal was to predict current vacancy rate by zip code using housing market indicators and other econometrics.

**the findings** 
- I found vacancy rates had different trends/correlations between econometric variables depending on the different time periods. This was interesting to see that during different economic periods in US history the variables had very different relationships.
- The best performing model was the Random Forest regressor, with R2 on the test set of  .92. However Adjusted R2 on test data showed a score of .78 which seems to suggest some of performance is skewed by the large number of variables, and that some of these variables may be unnecessary to the model. Not only did this model have the highest performance, it also took shorter to run compared to the models where hyperparameters were optimized.
- From the Lasso Regression model it seems that the top 10 features in predicting vacancy rate comprise:  zip code, rent price, year, size rank, home price, State(s).
- When examining projected 2020 vacancy rate data, results seem to suggest tourist areas near beaches have the highest vacancy rates while wealthier, faster growing suburbs outside major cities have the least vacancy. This seems to make sense generally and also with trends witnessed during the COVID-19 Pandemic.
- When examining vacancy adjusted rent/price ratios, a metric used for rental real estate investment, results seem to show that places that may be good to invest are in cities with low home prices, relatively higher vacancy rates. More suburban areas with higher home prices (especially in CA), may be less desirable in terms of potential areas to invest in real estate. But real estate investors should also be sure to consider other variables when choosing an area to invest (ie. crime rate, unemployment, population and job growth etc.)

**ideas for further research**

- The current model is only predicting vacancy rates for ~10% of US zipcodes and 43/51 US states, this is because I do not have 2019-2020 rent price data for all the zip codes, only the ~3,000 zip codes from Zilllow. In the future if I wanted to be able to predict vacancy rate for all US zip codes I would either need: 
    - to create a model to predict rent prices by zip code (which seems do-able because home prices are so correlated with rent prices, and Zillow has current home price data on around > 30,000 zip codes). This would then allow me to update my current model and predict vacancy rates for the rest of the zip codes. 
    - A simple way to preserve more zip codes would be to instead of simply dropping all NaNs could be to group by year and zip code, and then linear fill the data for home/rent prices. This change would add only a few zip codes, not a meaningful amount.
    - Another thought would be to drop rent prices from the model altogether and see how much the model’s predictive ability is impacted. If it is not by much then it would be very easy to have have the model predict ~30k zip codes because we have that many variables from zillow’s home price data
- Another idea would be to measure the current model’s performance’s predictions as the real vacancy rate data comes out from ACS, ie. as the ACS releases their 2019 results I could test and see how accurate the 2019 predictions were. As needed I could update the model to improve performance.
- Because it seems that geographical factors are important in the ability to predict a specific zip codes vacancy rate, I could consider creating different models for different regions, ie. northeast, southwest, etc. or whatever divisions would yield the most predictive models. 
- I could try running the model with less variables to see if the difference between R2 & adjusted R2 scores gets smaller.
- Also I could go back and look for more data/variables to improve the model. Current economic and housing market data for the US nationally is plentifully available, and I could possibly incorporate that or try to impute data by zip code for some variables (ie. ACS has zip code level data for median income, unemployment from 20111-2018). Possibly adding in some of these variables that we used in the US national model may yield better predictive results.
- It would be interesting to see which areas have had the most vacancy rate change from 2014-2018 (by zip code, county, metro area, and city)
- I could also use the current vacancy rate data I have created in a larger real estate investor dataframe where I have other information by zip code that real estate investors utilize when choosing areas to invest (ie. unemployment, price to rent ratios, crime rates,  job growth and diversity, population growth etc.). This could be  a useful tool to help explore/identify areas that seem good places for potential investment.

**recommendations on how a client can use these findings**

____________________________________________________________________________________________
*Background on using vacancy rate data to determine areas for potential real estate investing with a rent/price ratio adjusted for vacancy:*
 
Many times real estate investors will use a rent to price ratio to determine if an area or property may be a good place to invest. They would use the gross annual rent divided by the home price to get this ratio. A higher ratio is better as investors look for higher rents and lower home prices, which generally yield greater rental income. Generally ratios above 12% are good places to do more research and look into.
 
However if real estate investors only use rent/price ratios they are missing an incredibly important factor: how vacancy eats into their annual rental income. So a more nuanced statistic is rent/price ratio adjusted for vacancy, calculated as such:
 
((avg. monthly rent * 12) * (1 - vacancy rate) )/ avg. home price 
 
This is one of the indicators I would use when selecting zip codes for potential real estate investments. Here is an example of how this statistic can be important:
 
Two homes A&B:
Both homes rent for $1000/month
Home A sale price at $125k (9.6% rent/price ratio)
Home B sale price at $100k (12% rent/price ratio)
At this point if I stopped here I would go for Home B as it should give higher returns on my investment, but looking at average vacancy rates in the area:
Home A vacancy rate - 5% (now a 9.12% ratio adjusted for vacancy)
Home B vacancy rate - 35%  (now a 7.8% rent/price ratio adjusted for vacancy)
Now I would choose Home B and look deeper into why the vacancy rate in Home B's neighborhood is so high.
Some times higher vacancy may mean higher crime rate, higher turnover in renters, more potential for vandalism (ie. higher home insurance premiums), and more truly vacant (abandoned or otherwise) properties in the area.  

_________________________________________________________________________________________
**1. Places to potentially invest**
- States: Mississippi, Michigan, Kentucky,  Ohio, Nebraska
- Counties: Lucas County, OH; Luzerne County, PA; Wayne County, MI; Baltimore City, MD; DeSoto County, MS
- Cities: Jennings, MO; Detroit, MI; Hampton Bays, NY; Northwoods, MO; Park Forest, IL
 
**2. Places to you may to avoid when investing**
- States: Hawaii; Washington, DC; California; Washington; Oregon
- Counties: El Dorado County, CA; Santa Clara County, CA; Marin County, CA; San Francisco County, CA; San Mateo County, CA
- Cities: Cupertino, CA; Los Alamitos, CA; Redwood City, CA; Burlingame, CA, Wynnewood, PA

As noted above, data seems to show that places that may be good to invest are in cities with low home prices, relatively higher vacancy rates. Conversely, areas that are more suburban with higher home prices (especially in CA), seem to be not as good potential areas to invest in real estate. 

*Note: Rent/Price ratios are only one factor when looking for potential areas to invest, one would also want to consider a variety of other factors (ie. unemployment, crime rate, job/population growth, etc)* 

**3. Use the current predicted vacancy rate data in a larger real estate investor dataframe with other information by zip code to create an “investability” metric for each zip code.** Rent prices, home prices, and vacancy rates would be a few of the data points you would want to collect when deciding to invest in an area. Other variables could include:

- crime rates
- unemployment rates
- variation in job types (higher variation shows job security in a market)
- avg. yearly rent/median income
- Population growth, etc.

You could combine and weight these features to develop some type of single “investability” metric for each zip code that aggregates all your individual variables. For example you could scale all the variables and then add them together (while giving the more important metrics higher weights). So if you believe rent/price ratio adjusted for vacancy and crime rate are more important you may choose to weigh these higher than unemployment. This would then give you a quick and easy to access database that would give you the best potential areas to invest but also the background statistics that make up that larger “investability” metric. You could also have it automatically update as this data came in from zillow etc. This could save considerable time and money, and generate considerable potential profits, while allowing investors to expand their real estate portfolio across the USA.




Project Organization
------------

    ├── LICENSE
    ├── Makefile           <- Makefile with commands like `make data` or `make train`
    ├── README.md          <- The top-level README for developers using this project.
    ├── data
    │   ├── external       <- Data from third party sources.
    │   ├── interim        <- Intermediate data that has been transformed.
    │   ├── processed      <- The final, canonical data sets for modeling.
    │   └── raw            <- The original, immutable data dump.
    │
    ├── docs               <- A default Sphinx project; see sphinx-doc.org for details
    │
    ├── models             <- Trained and serialized models, model predictions, or model summaries
    │
    ├── notebooks          <- Jupyter notebooks. Naming convention is a number (for ordering),
    │                         the creator's initials, and a short `-` delimited description, e.g.
    │                         `1.0-jqp-initial-data-exploration`.
    │
    ├── references         <- Data dictionaries, manuals, and all other explanatory materials.
    │
    ├── reports            <- Generated analysis as HTML, PDF, LaTeX, etc.
    │   └── figures        <- Generated graphics and figures to be used in reporting
    │
    ├── requirements.txt   <- The requirements file for reproducing the analysis environment, e.g.
    │                         generated with `pip freeze > requirements.txt`
    │
    ├── setup.py           <- makes project pip installable (pip install -e .) so src can be imported
    ├── src                <- Source code for use in this project.
    │   ├── __init__.py    <- Makes src a Python module
    │   │
    │   ├── data           <- Scripts to download or generate data
    │   │   └── make_dataset.py
    │   │
    │   ├── features       <- Scripts to turn raw data into features for modeling
    │   │   └── build_features.py
    │   │
    │   ├── models         <- Scripts to train models and then use trained models to make
    │   │   │                 predictions
    │   │   ├── predict_model.py
    │   │   └── train_model.py
    │   │
    │   └── visualization  <- Scripts to create exploratory and results oriented visualizations
    │       └── visualize.py
    │
    └── tox.ini            <- tox file with settings for running tox; see tox.readthedocs.io


--------

<p><small>Project based on the <a target="_blank" href="https://drivendata.github.io/cookiecutter-data-science/">cookiecutter data science project template</a>. #cookiecutterdatascience</small></p>
