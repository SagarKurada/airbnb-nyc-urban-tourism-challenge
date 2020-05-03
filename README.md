
# Airbnb NYC Urban Tourism Challenge

## Motivation:
In a world that is becoming increasingly global, traveling has become an integral part of everyone’s lives. There is a plethora of locations from mountains to islands, from quaint towns to bustling cities made easily accessible by commute and accommodation options. While the internet has allowed for thousands of gigabytes of information sharing regarding stays, discounts, picturesque spots that are social-media worthy, it has also made it that much harder for the users to narrow down their search for the ideal travel accommodation.

## Objective:
The objective of the project is to design a framework that allows for **computing optimal AirBnB listing(s) based on user inputs such as their budget and number of days of stay, and aligning those with the listing availability and pricing.**

## But why Airbnb?
AirBnB, with about 150 million users worldwide [1], is tremendously popular now, primarily because of its affordability and open platform. New York is one of the most visited cities in the world - it attracted 13.1 international tourists in 2017, [2] which is why the included computational methods are focused on data generated from AirBnBs in New York City.

## Computational Steps:
  - **Data:** The dataset ‘New York City Airbnb Open Data’ was taken from www.kaggle.com. There were 48895 observations.
  - **Data Cleaning:** The data was reasonably clean with ~49k rows. There were blank ~12k rows in columns Last_review and reveiwes_per_month. These rows were deleted. Host_ID and Host_Name were irrelevant to our analysis, hence they were dropped. In addition, the data did not have the text reviews of the customer. Due to the same, we have scrapped the file from internet containing the reviews for New York
  - **Data Scraping of Reviews:** The data was scraped from Airbnb’s website. The data was posted on the website as an attachment. Urllib package was used to download the data. WordCloud is created using the data, this would help Airbnb owners to identify the success parameters and keywords responsible for the success of their property.
  - **Visualization:** Folium package was used to create a heat map of each listing ID by iterating the latitude and longitude coordinates in a ‘for’ loop. Seaborn package was used to obtain a scatter plot of the listing ID, grouped by their neighborhood groups.
  
![Heatmap](https://github.com/akshay-madar/airbnb-nyc-urban-tourism-challenge/blob/master/airbnb_heatmap.PNG)

Clicking on markers to display the listing ID was attempted using folium. While it worked for small samples of the dataset, it took about 30 seconds to execute for the entire dataset. It was found that it fails at 3000 markers.

## Decision Tree:
To understand the impact of features of Airbnb listings on its price, Decision tree is used. Following are the top features that impact the price of Airbnb:
  - **Room type:** An apartment or entire house will lead to higher price for obvious reason that it can accommodate a higher number of people than a private room
  - **Availability_365:** The number of days that a listing is available in a year plays another important factor in determining the price of a listing. We observe that the listings with high availability in a year lead to lower price.
  - **Calulated_host_listing_cost:** Unsurprisingly, amount of listing per host leads to higher price in listings in Airbnb
  
## Clustering:
To segment all the Airbnbs based on user specific criteria w.r.t the attributes of the Airbnb such as price, minimum number of nights that must be booked, availability in a year, clustering was done. This was executed in 2.5 seconds. Six clusters were formed as follows:
  - **Economical Short Stay:** This cluster gave 1421 listings and had those properties that were highly economical and required smaller duration of minimum number of nights to be booked which meant the guest could use this for a short vacation too. It also had a high
number of reviews which can be thought of as high number of traveling renting these properties. Their average availability in a year was also high.
  - **Economical Long Stay:** With 8336 listings, this cluster had economical listings with a long
duration of minimum number of nights requirement
  - **Expensive Long Stay:** This gave 3646 listings. These were expensive and had long duration
requirement of minimum number of days. There were not many guests at these properties.
  - **Moderately Priced Short Stay:** With 11970, these were moderately priced, and did not
require long durations of minimum stay. Based on number of reviews, there were not many
guests at these properties
