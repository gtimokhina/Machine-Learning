
1.	Data preparation, data cleaning of original dataset “cdc_zika.csv” from Kaggle
    Drop columns with all null values
    Fixed missing data
    Created country column, city, county, province for future needs(getting accurate lat/long values)
    Fixed some data and names for locations, countries
    Fixed incorrect data format
    groupby/summarize all occurrences per location and date
    save output cleaned data file as ‘zika_cleaned_data.csv’ for future needs
2.	Amalgamation:
    1.	Get latitude, longitude data using geopy.geocoders  API.  Since API takes a long time to run and has some limits, we          got data for each country separately and then merged it.
    2.	Get weather data( temperature, dewpoint, precipitation, wind)  from https://www.wunderground.com/ using api:                  https://api.darksky.net
    3.	Get population Density from https://beta.sedac.ciesin.columbia.edu/data/set/gpw-v4-population-density                       (SOCIOECONOMIC DATA AND APPLICATIONS CENTER (SEDAC). Downloaded tif file with population densities encoded in the           file, then rocess file to get data and saved in csv file.
    4.	Get Aedes aegypti and Aedes albopictus (mosquitos species that carry Zika virus)
        occurrences were from Dryad (https://datadryad.org/stash/dataset/doi:10.5061/dryad.47v3c
        get data only for year >=2006

3.	Our research showed that some locations did not have any occurrences of Zika.
    We decided to create new columns based on that observation called “zika_confirmed”. 
    If number of cases for location is 0 then zika_confirmed = 0 and we take first available report_date for that location.
    If any number of cases > 0 for specified location, we assigned zika_confirmed = 1 and we took first report_date where       number of cases > 0. 

    This new column will help us to predict Zika outbreak in certain location.
    All classifications algorithms gave very good results.( Accuracy > 80%)

Our latent variables are temperature, humidity, mosquito occurrence and density population.
