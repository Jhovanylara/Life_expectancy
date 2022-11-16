# Latin-Data
## Final Project -Data 03- Henry
### Jhovany Lara, Rodrigo Ruiz, Pablo Poletti, José Toledo

Video: https://youtu.be/YbueLVxM3RA

## Contents:

1. [Development](#Development)
2. [Countries](#Countries)
3. [Indicators](#Indicators)
4. [Machine_Learning](#Machine_Learning)
5. [Architecture](#Architecture)
6. [Work_methodology](#Work_methodology)
7. [Documentation](#Documentation)


## Development

For this final project, Life Expectancy at birth was chosen. In the role of a data consultant, our potential client wants to know the different factors that have an impact on the result of Life expectancy at birth and, how they manifest themselves. For this, a framework was developed for data analysis, machine learning modeling and dashboard visualization.: https://latin-data.streamlit.app/.

## Countries

- A sample of countries for each continent was selected, the criteria used was by the most representative countries, with best quality in the historical information collected by the World Bank or WHO, so that we can work with its indicators.
- Initially, the status of "developed" vs. "developing" countries was used as a filter to differentiate the sample by continent, but taking into account the classification made by the United Nations, it was observed that both in Latin America, Africa and the Middle East, another level of classification needed to be included to improve differentiation.
- We decided to use the classification by income level carried out by the World Bank through the Gross National Income per capita (GNI) and thus be able to improve the differentiation of the effects of the different variables on life expectancy, depending on the country or continent under study.


## Indicators

- Socioeconomic and health factors will be taken into account for the indicators selection.
- In a first instance, the raw data had 38 indicators. After an exploratory analysis we found that the main problem with our data, was the missing values. 
- We decided to eliminatea those indicators with more than 20% of missing values, with this we were left with only 17 indicators, with an approximate percentage of 3% missing data. 
- Then for the rest of missing values we used a the K-nearest neighbors machine learning algorithm in order to complete the data.

## Machine_Learning

- For the statistical analysis of the mean life expectancy for each country, the first we determined that indicators type were time series and then study which predictive model was the most convenient. 
- Considering the different options, we decided that the best option was to take the most of the tools that data science offers and seek to automate statistical and predictive processes.
For this we used the Pycaret library, which gave us the possibility to project the life expectancy to 10 years ahead, using more than 30 algorithms; cross validation, assembly methods, hyperparameter optimization and mixture methods to select the best model for each case, according to the scaled absolute mean error.
- Then we selected 4 relevant variables, to analize their real effect projected versus an hipotetical improve of 10% annual for 5 years over the LE, differentiating between developed and developing countries. Assumptions were made so that this hypothetical improvement would have a greater positive effect on life expectancy in developing countries.


## Architecture

- The architecture follows five main steps: the first is to analyze the data sources, the second is for Extraction, Transformation (cleaning) and Load called by its acronym ETL. The third step is where the incremental load to the relational database is carried out, the fourth step is the incremental load and the last step is where the necessary queries are made to be used in ML models and dashboard visualization.

1. Data research and raw data analysis.
2. Raw data extraction, cleanup, and load (ETL). https://etl-latin-data.herokuapp.com/ deploy repository is: https://github.com/grupohenryds03/airflow-heroku
3. Tasks for incremental loading.
4. Data input to relational database.
5. Database queries to model progressions in machine learning and visualization on a dashboard.


- The work environment for the ETL is developed in AIRFLOW within a HEROKU cloud machine. API access: https://etl-latin-data.herokuapp.com/
- For the datalake assembly, the data was ingested in the SNOWFLAKE STAGE environment in .csv format compressed like .gz (they can also be json, parquet, xlsx).
- In the case of the relational database, SNOWFLAKE is used for the creation of a warehouse for its maintenance and incremental ingestion.
- For the machine learning modeling and data visualization, queries are made according to the client's requirements. 
- We used three types of encryption for the connection to the database: *secrets of streamlit, gitignore of github y variables of airflow*.

<img src="/imagenes/arquitetura_bueno.jpg"/>


- For the dashboard we used STREAMLIT: https://latin-data.streamlitapp.com/

- For the dashboard deploy we used the proper tool from STREAMLIT.

## Work_methodology

- In order to carry out collaborative work, the connection is established from a local visual studio code session of each member, to the shared GITHUB repository.

- In the terminal, the work environment is created to carry out the connection with snowflake in visual studio code on a local machine with phyton language, as follows:

```bash
 $ pip install conda #conda download
 $ conda create -n dbconnect python=3.8 #Environment creation
 $ conda activate dbconnect #Environment activation
 $ pip install snowflake-connector-python[pandas] #snowflake connector install
```

- To make the connection to the snowflake database, a snow.py file was created with the access data that is ignored with gitignore so we dont show important keys.

```python
import snowflake.connector # imports connector
from snow import * # imports access keys
conn = snowflake.connector.connect(
    user=snow_user,
    password=snow_pasoword,
    account=snow_account,
    warehouse=snow_warehouse,
    database=snow_database
    )
```

## Documentation

- AIRFLOW: https://airflow.apache.org/docs/
- PANDAS: https://pandas.pydata.org/docs/
- SNOWFLAKE: https://docs.snowflake.com/en/
- STREAMLIT:https://docs.streamlit.io/
- PYCARET: https://pycaret.gitbook.io/docs/
- WBAPI:https://pypi.org/project/wbgapi/
- PLOTLY:https://plotly.com/python/
- SKLEARN: https://scikit-learn.org/stable/user_guide.html
