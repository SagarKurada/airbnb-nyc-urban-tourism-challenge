
# Airbnb NYC Urban Tourism Challenge

## Motivation:
In a world that is becoming increasingly global, traveling has become an integral part of everyone’s lives. There is a plethora of locations from mountains to islands, from quaint towns to bustling cities made easily accessible by commute and accommodation options. While the internet has allowed for thousands of gigabytes of information sharing regarding stays, discounts, picturesque spots that are social-media worthy, it has also made it that much harder for the users to narrow down their search for the ideal travel accommodation.

## Objective:
The objective of the project is to design a framework that allows for **computing optimal AirBnB listing(s) based on user inputs such as their budget and number of days of stay, and aligning those with the listing availability and pricing.**

## But why Airbnb:
AirBnB, with about 150 million users worldwide [1], is tremendously popular now, primarily because of its affordability and open platform. New York is one of the most visited cities in the world - it attracted 13.1 international tourists in 2017, [2] which is why the included computational methods are focused on data generated from AirBnBs in New York City.

## Computational Steps:
  • **Data:** The dataset ‘New York City Airbnb Open Data’ was taken from www.kaggle.com. There were 48895 observations.
  • **Data Cleaning:** The data was reasonably clean with ~49k rows. There were blank ~12k rows in columns Last_review and reveiwes_per_month. These rows were deleted. Host_ID and Host_Name were irrelevant to our analysis, hence they were dropped. In addition, the data did not
have the text reviews of the customer. Due to the same, we have scrapped the file from internet containing the reviews for New York
  • **Data Scraping of Reviews:** The data was scraped from Airbnb’s website. The data was posted on the website as an attachment. Urllib package was used to download the data. WordCloud is created using the data, this would help Airbnb owners to identify the success parameters and keywords responsible for the success of their property.
  • **Visualization:** Folium package was used to create a heat map of each listing ID by iterating the latitude and longitude coordinates in a ‘for’ loop. Seaborn package was used to obtain a scatter plot of the listing ID, grouped by their neighborhood groups.
  
![Heatmap](https://github.com/akshay-madar/airbnb-nyc-urban-tourism-challenge/blob/master/airbnb_heatmap.PNG)

Clicking on markers to display the listing ID was attempted using folium. While it worked for small samples of the dataset, it took about 30 seconds to execute for the entire dataset. It was found that it fails at 3000 markers.
  
