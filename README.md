# Air Quality Trends in the US

# Data:
This data was scraped from the US EPA website. It is a collection of air quality data from the years 2000-2016. It has data for four major pollutants (Nitrogen Dioxide, Sulphur Dioxide, Carbon Monoxide and Ozone). The origian dataset had 28 fields, including raw data by state and AQI (air-quality index). For my project, I focused on AQI for the pollutants. AQI has varying scales, but a lower score is always better. (i.e. A carbon monoxide AQI of 12 is much better air qualtiy than an AQI of 75.)

Here is how the original dataset looked:![data](https://user-images.githubusercontent.com/63068643/124906203-ceb4e100-dfb4-11eb-9f92-c8be01327945.JPG)

First I dropped the unnecessary columns: ![dropping unnecesary columns](https://user-images.githubusercontent.com/63068643/125204807-08077e00-e24d-11eb-8822-09372d560fe4.JPG)

I tried grouping by state and date to look at the top polluting states: ![aqi w state and date](https://user-images.githubusercontent.com/63068643/125204961-cf1bd900-e24d-11eb-9b59-7bbf3c12a563.JPG)
![grouped data exploration](https://user-images.githubusercontent.com/63068643/125204965-d511ba00-e24d-11eb-9305-d1fe07a38a29.JPG)

Then, I regrouped just by date to be able to run forecasting models:![grouped by date](https://user-images.githubusercontent.com/63068643/125204990-025e6800-e24e-11eb-965e-c0af4119b7c1.JPG)

I conducted initial plots to see the overall trends  in the country over time:
![no2 over time](https://user-images.githubusercontent.com/63068643/125205054-5a956a00-e24e-11eb-9de9-b51843b6232c.JPG)
![co2 over time](https://user-images.githubusercontent.com/63068643/125205066-67b25900-e24e-11eb-888e-59b59f836fd1.JPG)
![o3 aqi over time](https://user-images.githubusercontent.com/63068643/125205069-6da83a00-e24e-11eb-9030-bbb198c58db2.JPG)
![so2 over time](https://user-images.githubusercontent.com/63068643/125205082-7567de80-e24e-11eb-9159-cfe46180fccc.JPG)

From these visualizations, I could see there was clear seasonality to CO, NO2, and O3. Also, besides, ozone, all the pollutants had decreased over time. This was an unexpected and optimistic finding.

The first pollutant I analyzed was nitrogen dioxide (NO2). I conducted an augmented Dickey-Fuller test and confirmed that the series was not stationary as is:
![adf1](https://user-images.githubusercontent.com/63068643/125205273-6d5c6e80-e24f-11eb-8147-845b4aca1f3b.JPG)

I plotted the ACF and notices peaks at 1 and 12, indicating seasonality:![acf](https://user-images.githubusercontent.com/63068643/125205290-836a2f00-e24f-11eb-8dff-d40de0204650.JPG)

Now, I know I want to conduct a SARIMA model instead of a normal ARIMA because of the seasonality of the data.
Model:
![model set up](https://user-images.githubusercontent.com/63068643/125210559-832d5c00-e26e-11eb-9abd-4098683e518a.JPG)
![model run](https://user-images.githubusercontent.com/63068643/125210567-97715900-e26e-11eb-8dfd-e7c5da63b407.JPG)

Lowest AIC for NO2 model was -501, and the associated SARIMAX model numbers were (1,1,1)x(1,0,1,12)12.

Fitting the model:
![model fit](https://user-images.githubusercontent.com/63068643/125210641-1bc3dc00-e26f-11eb-92fb-e7208994c30e.JPG)

Results:
![4 no2 plots](https://user-images.githubusercontent.com/63068643/125210650-27170780-e26f-11eb-855b-fa3bb943bbd1.JPG)

![p val](https://user-images.githubusercontent.com/63068643/125210654-326a3300-e26f-11eb-808b-1ed64d4d0c41.JPG)

The Pro(Q) and Prob(JB) scores assure us that the data is random and normally distributed.

Now we predict one-step ahead:
![one-step ahead no2 plot](https://user-images.githubusercontent.com/63068643/125211870-91cc4100-e277-11eb-801f-dcf502c866d6.JPG)

And I can forecast further into the future:
![forecast code 1](https://user-images.githubusercontent.com/63068643/125211908-d821a000-e277-11eb-88e5-2b10627a4258.JPG)
![forecast code 2](https://user-images.githubusercontent.com/63068643/125211910-dce65400-e277-11eb-9dac-698d2f6fe868.JPG)
![forecasted no2 graph](https://user-images.githubusercontent.com/63068643/125211911-dfe14480-e277-11eb-87c9-d63275ce44c2.JPG)













