# Affect of mobility trend on spread of COVID-19
Understaing how change in movement of people, like staying at home, going to work and flying affect spread of COVID-19 in United States. 
A dashboard to track mobility trend of people in United States, due to effects of COVID-19. Mobility data is being provided by Google. 

## Table of content 

1. [Data sources](https://github.com/abhatt95/COVID-19-mobility-impact#data-sources) 
2. [Data processing](https://github.com/abhatt95/COVID-19-mobility-impact#data-processing) 
3. [Results](https://abhipbhatt.medium.com/mobility-and-travel-impact-on-spread-of-covid-19-902f8f283e67) 
4. [Helper functions created](https://github.com/abhatt95/COVID-19-mobility-impact#helper-functions)  


### Data sources
*  [Google COVID-19 Community Mobility Reports](https://www.google.com/covid19/mobility/)
*  [NYT COVID19 data](https://github.com/nytimes/covid-19-data)
*  [TSA checkpoint travel numbers for 2020 and 2019](https://www.tsa.gov/coronavirus/passenger-throughput)

### Data processing 
*   Processing Google COVID-19 Mobility data -
    *   getGoogleMobilityData() is created to fetch data and return dataframe containing mobility data for USA. 
    *   Google_mobility (DataFrame) contains mobility trend like residential_percent_change_from_baseline where baseline being data from previous year. It contains state, county and countrywide data. 
    * For initial assement, country wide data for United States (US) is being filtered into US_trend. 
    * Few columns like sub_region_1 which wouldn't be applicable for country level assement are being discarded. Enruring no null value seeps into US_trend. 

*   Processing data from New York Times (NYT) COVID-19 cases and mortality tracker -
    *   getNYTdata() is created to fetch data and return dataframe containing cases and mortality count (realted to COVID-19) in USA. 
    *   processNYTData() converts absolute case and death count to per day count, which is a better indicator of trend (compared to absolute numbers). 
    *   Data doesn't contain any null values, thanks to the fact that getNYTdata() discards null values when it scrapes from web. 

*   Processing flight travel data from Transportation Security Administration (TSA) -
    *   getTSAdata() is created to fetch, parse and return dataframe conatining date wise flyer numbers across USA. 
    *   Class TSACheckInTuple is used as a helper class to maintain structure of data, help validate it before being added to list and creating a dataframe. 
    *   Using TSACheckInTuple reduces need for cleaning data as only valid records are being added. 
  
### Results
*   [Medium article explaining results in detail](https://abhipbhatt.medium.com/mobility-and-travel-impact-on-spread-of-covid-19-902f8f283e67)

### Helper functions 
*  getCorelation(Label1 = '', 
                  Label2 = 'cases', 
                  OffsetDays = 14,
                  Data = mega_frame)
    *   returns correlation between label1 and label2 in Data (dataframe), using differnce of OffsetDays between label1 and label2. 
*  plotTrend(Source = US_trend,
              title = 'Residence trend',
              isPercentage = True,
              dateColumnHeader = 'date',
              labels = ['residential_percent_change_from_baseline'],
              credits = '')
    *    returns a plot of trends passed in labels on yaxis with dates on yaxis. Annotations like title and credits can be passed. Additional plot grooming is being performed to make figure aesthetically pleasing. 


