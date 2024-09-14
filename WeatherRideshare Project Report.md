# Does weather have a major affect on rideshare trip counts?

People using rideshare apps, like Uber or Lyft, has increased so much in the past several years. Our data, [provided by the City of New York](https://www.nyc.gov/site/tlc/about/tlc-trip-record-data.page), show that High Volume For-Hire Vehicle (HVFHV) trips numbered over twenty million just for the month of June 2024! And HVFHV trips only cover larger companies, and exclude many more local and smaller rideshare services.

There are many reasons on why people decide to take out their phones and book a ride, and in this project we will try and see if weather plays a major role in it. Why weather specifically? Maybe it's raining, and you're caught out without an umbrella, instead of walking to where you want to go, you book a ride. The opposite might happen as well, it's a beautiful day, why not walk instead? While these are just small examples, we'll take a look and see if rideshare count changes noticeably depending on the weather.

But for now, let's take a broad overview of how many trips people booked for the month.

## How rideshare counts looked in June 2024

Let's take a look on how many people decided to book rides.
### Daily Trends

![[Daily Rideshare Demand.png]]

Like how Garfield hates Mondays, it seems to also apply for rideshare counts, at least for this specific month, as the dips always bottoms out at a Monday. While Saturdays are the most popular time to book rides.

### Weekly Trends

![[Avg. Weekly Demand.png]]

This time looking at the average trips based on the day of the week, it affirms our last finding where Saturday is the most popular day, and Monday the least.
### Hourly Trends

![[Avg. Hourly Demand.png]]

Taking an even deeper look in hourly trends, we can see quite the difference in habits, based on on the day of the week. On weekdays, peaks often coincides with rush hour. Do some people Uber to work and home every day? That sounds expensive. On the weekends, we don't see the rush hour peaks. Instead, we see a much larger count of trips during the early morning hours. People staying out much longer after hours.

## Is weather a major factor when people decide to book a ride?

![[Correlation Chart.png]]

So, back to our original question: do rideshare trips change based on the weather? Looking at the correlation table, the short answer is... maybe? Weather conditions themselves seem to have little to no impact on rideshare trip counts. Wind speed shows a weak correlation, while temperature has a slightly stronger but still mild correlation. But that's not enough to give us a definitive answer, so we decided to dig deeper by modeling the data to see just how much weather really matters.

We chose a Random Forest model for this analysis due to its ability to handle complex, non-linear relationships between multiple variables, such as weather conditions, time of day, and day of the week. The model achieved a high $R^2$ score of 0.97, indicating that it can explain 97% of the variation in rideshare counts for June 2024. This suggests the model is highly effective at capturing the patterns in the data. Additionally, when tested against historical data from June 2023, the model maintained a strong performance with an $R^2$ of 0.94, demonstrating its generalizability and robustness over different periods.

![[Feature Importance.png]]

Although temperature had the second strongest correlation with rideshare counts, the Random Forest model ranked it as having low importance relative to other features, such as the hour of pickup and day of the week. This suggests that, while there may be some correlation between temperature and rideshare demand, it is not a primary driver of the variation observed in our data.

That said, this doesn’t mean weather has zero effect; there will always be situations where the weather is a deciding factor in someone's choice to book a ride, like when it’s raining, and I’d rather stay home and sip tea by the window. But those cases are too few to make a noticeable impact on our current dataset.

I didn’t expect weather to have a major effect, but I thought there’d be at least some level of impact. So, it's surprising to see that weather didn’t even play a minor role. This unexpected finding raises some questions that we'll dive into in our discussion of limitations, like why weather might not have shown a significant effect and what other factors could be influencing rideshare behavior.
## Limitations and Future Research

The data collected only covered the month of June and only in 2024, so this entire report's accuracy is limited to summer months. It does not include other seasons, and other types of weather conditions like snow. Also, we did not factor in any events or holidays, which could skew the data, leading to more trips than the normal rate. Also, the data is only specific to New York City, and different trends or outcomes might occur in less urban areas.

So future research can be focused on using a larger dataset, covering an entire year. Also, specific focus on more extreme weather events like hurricanes or blizzards, from historical weather data and see if during those times rideshare trip counts are affected. Another idea is to examine weather impact on different types of rides (short vs long trips) and see if it affects them differently.

# Methodology

This analysis uses two sources of data, the official rideshare information given by the [City of New York](https://www.nyc.gov/site/tlc/about/tlc-trip-record-data.page) and the weather data was scraped from [Weather Underground](https://www.wunderground.com/) The weather station used to for the data was LaGuardia Airport Station (KLGA)

We created a [python script](https://github.com/RHardiyanto1/weather-underground-webscraper) which handled the webscraping and cleaning of the hourly weather data. The script goes day by day, collecting the observation table, which has the hourly weather information. Depending on the location, the timing of each hourly observation can differ (multiple observations per hour or not taken strictly at the start of the hour), which required additional processing. 

Additional cleaning of the weather data included filling in missing hourly data, which resulted from uneven observations from the weather station. The observation times were also rounded to the nearest hour, as KLGA reports their observations at the 51st minute of the hour. Another step was simplifying the weather conditions (fog, haze, mist being categorized into 'All_Fog')

Outlier removal focused on trips with unrealistically short durations (under 60 seconds or less than 0.05 miles) and those in the top 0.5% for distance or time. While the primary focus of this analysis is on the number of rides rather than trip length or duration, removing these outliers was necessary to ensure we were capturing typical rideshare behavior.

Rideshare data was then aggregated by date and time, in hourly buckets and merged with the corresponding weather data, from which the data was ready for analysis.

## Acknowledgements

- City of New York for providing rideshare data
- Weather Underground for historical weather data