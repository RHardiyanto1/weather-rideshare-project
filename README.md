# Analyzing the Impact of Weather on Rideshare Trip Counts in NYC - June 2024

This project investigates whether weather conditions significantly impact rideshare trip counts in New York City, using data from June 2024. With over 20 million rides recorded in just one month, this analysis explores the potential effects of factors like temperature, precipitation, and wind speed on the volume of rideshare trips.

## Project Objective

To determine if weather conditions are a major factor influencing the number of rideshare bookings in NYC.

## Data Sources

- **Rideshare Data:** [City of New York - TLC Trip Record Data](https://www.nyc.gov/site/tlc/about/tlc-trip-record-data.page)
- **Weather Data:** Scraped from [Weather Underground](https://www.wunderground.com/) using data from the LaGuardia Airport Station (KLGA).
## Methods and Tools

- **Web Scraping:** Created own [webscraper](https://github.com/RHardiyanto1/weather-underground-webscraper) to collect and clean hourly weather data
- **Data Cleaning and Preprocessing:** Python, Pandas
- **Exploratory Data Analysis (EDA):** Visualizations using Matplotlib
- **Statistical Analysis:** Correlation analysis to examine the relationship between weather variables and trip counts
- **Machine Learning Model:** Random Forest Regression using scikit-learn to evaluate feature importance

## Key Findings

- **Low Correlation with Weather Conditions:** The correlation between weather conditions and rideshare trip counts is weak, with temperature having the strongest (though still minor) influence.
- **Dominant Factors Identified:** Hour of the day and day of the week are the most significant factors affecting rideshare demand.
- **Model Performance:** The Random Forest model achieved an $R^{2} = 0.97$, indicating it explains most variations in rideshare counts, with minimal impact from weather conditions.

## Full Analysis

For the full analysis, it's located at my [website](https://rhardiyanto1.github.io/posts/WeatherRideshare-Project-Report/).

## Repository Contents

- `data/`: Contains all data used (A sample of the cleaned rideshare dataset included, as the full dataset is too large)
- `notebooks/`: Jupyter notebooks with data cleaning, analysis, and modeling code
- `scripts/`: Python scripts for data scraping and preprocessing
- `images/`: Contains all the images used in the main report
## Future Research Directions

- Expand the dataset to cover all seasons and various weather conditions (e.g., snow, extreme heat).
- Analyze the impact of major events or holidays on rideshare demand.
- Investigate weather impact on different types of rides (e.g., short vs. long trips) to see if effects vary.

## Acknowledgements

- City of New York for providing rideshare data
- Weather Underground for historical weather data
