
# Airbnb NYC Urban Tourism Challenge

## Motivation:
In a world that is becoming increasingly global, traveling has become an integral part of everyone’s lives. There is a plethora of locations from mountains to islands, from quaint towns to bustling cities made easily accessible by commute and accommodation options. While the internet has allowed for thousands of gigabytes of information sharing regarding stays, discounts, picturesque spots that are social-media worthy, it has also made it that much harder for the users to narrow down their search for the ideal travel accommodation.

<p align="center">
  <img width="560" height="400" src="https://media.giphy.com/media/PusBKwc3wHzWw/giphy.gif">
</p>

## Project Flow:
1. [**Objective**](#1-objective)
2. [**Computational Steps**](#2-computational-steps)
  - [**Decision Tree**](#decision-tree)
  - [**Clustering**](#clustering)
  - [**Dynamic Programming**](#dynamic-programming)
    - [**Optimal Solution**](#optimal-solution)
    - [**Greedy Algorithm**](#greedy-algorithm)
    - [**Random Selection**](#random-selection)
  - [**Linear Regression**](#linear-regression)
  - [**Time Complexity and Comparison**](#time-complexity-and-comparison)
3. [**Results**](#3-results)
4. [**Conclusion/Recommendations**](#4-conclusionrecommendations)

## 1. Objective:
The objective of the project is to design a framework that allows for **computing optimal AirBnB listing(s) based on user inputs such as their budget and number of days of stay, and aligning those with the listing availability and pricing.**

### But why Airbnb?
AirBnB, with about 150 million users worldwide [1], is tremendously popular now, primarily because of its affordability and open platform. New York is one of the most visited cities in the world - it attracted 13.1 international tourists in 2017, [2] which is why the included computational methods are focused on data generated from AirBnBs in New York City.

[![Welcome to the Airbnb Youtube Channel](https://github.com/akshay-madar/airbnb-nyc-urban-tourism-challenge/blob/master/airbnb.PNG)](https://www.youtube.com/watch?v=-XSAqfK_UwY "Click to visit the Airbnb Youtube Channel")


## 2. Computational Steps:
  - **Data:** The dataset ‘New York City Airbnb Open Data’ was taken from www.kaggle.com. There were 48895 observations.
  - **Data Cleaning:** The data was reasonably clean with ~49k rows. There were blank ~12k rows in columns Last_review and reveiwes_per_month. These rows were deleted. Host_ID and Host_Name were irrelevant to our analysis, hence they were dropped. In addition, the data did not have the text reviews of the customer. Due to the same, we have scrapped the file from internet containing the reviews for New York
  - **Data Scraping of Reviews:** The data was scraped from Airbnb’s website. The data was posted on the website as an attachment. Urllib package was used to download the data. WordCloud is created using the data, this would help Airbnb owners to identify the success parameters and keywords responsible for the success of their property.
  - **Visualization:** Folium package was used to create a heat map of each listing ID by iterating the latitude and longitude coordinates in a ‘for’ loop. Seaborn package was used to obtain a scatter plot of the listing ID, grouped by their neighborhood groups.
  
![Heatmap](https://github.com/akshay-madar/airbnb-nyc-urban-tourism-challenge/blob/master/airbnb_heatmap.PNG)

Clicking on markers to display the listing ID was attempted using folium. While it worked for small samples of the dataset, it took about 30 seconds to execute for the entire dataset. It was found that it fails at 3000 markers.

## Decision Tree:
To understand the impact of features of Airbnb listings on its price, Decision tree is used. It is used because:
* Trees have high degree of interpretability, and are easy to explain to airbnb owners and travallers
* They can handle qualitative predictors, without the need of dummy variables
* They do not involve eucledian distances. So feature scaling is not required for splits.
* NOTE: DTs have low predictive power, and high variance. Hence, other ML approaches or methods like bagging, boosting, RF could be used.

Following are the top features that impact the price of Airbnb:
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
  - **Moderately Priced Popular Properties:** This gave 262 listings. They were moderately priced
and had low availability across the year
  - **Expensive and Unpopular Properties:** With 6886 listings, these were highly priced and not
rented out enough. Their availability was high.

![elbow](https://github.com/akshay-madar/airbnb-nyc-urban-tourism-challenge/blob/master/elbow_plot.PNG)

## Dynamic Programming:
*Business Problem*- A travel blogger wants to stay at multiple Airbnbs during the course of his/her
vacation until his/her budget is exhausted. The travel blogger has a budget constraint. The objective is
to provide the best possible AirBNBs based on Availability and Price.
To tackle the business problem and provide recommendations to the travel logger, 3
different approaches are used.

*Input data* - Object of each row in the dataframe was created with ID, min_price and value and put
in the list.

  - **Availability** = availability_365 / 365
  - **Min_price** = price * minimum_nights
  - **Value** = availability / min_price

### Optimal Solution: 
Optimal Solution using Dynamic Programming was used to select
airbnbs to maximize Value with budget as the constraint. However, this method had a high
run-time when the number of listings exceed 10,000. The relationship with time taken and
row size was linear. This challenge was mitigated using Sorting and the Greedy algorithm.

![optimal](https://github.com/akshay-madar/airbnb-nyc-urban-tourism-challenge/blob/master/optimal_solution.PNG)

### Greedy Algorithm:
The object was then sorted based on Value in a list using np.sort and
the Greedy Algorithm was used. This result gave the AirBnB that had the best value with
respect to the parameters considered.
### Random Selection: 
An option for travelers to randomly select Airbnbs based on their
availability and budget was also given. This was done using a loop, which selected Airbnbs randomly using np.random.choice based on their availability (higher the availability, the
higher the chance of it being selected). The loop continued until the budget was exhausted.

![random](https://github.com/akshay-madar/airbnb-nyc-urban-tourism-challenge/blob/master/random_selection.PNG)

## Linear Regression:
In order to identify the parameters responsible for increase in the price of the
Airbnb, regression was run. The output of the equation would help the owner identify the best
parameter suitable for their property. The output can also be used by owner to benchmark their
prices based on the service and quality of the property.
randomly using np.random.choice based on their availability (higher the availability, the
higher the chance of it being selected). The loop continued until the budget was exhausted.

![regression](https://github.com/akshay-madar/airbnb-nyc-urban-tourism-challenge/blob/master/linear_regression.PNG)

## Time complexity and comparison:
Below is the chart representing the time taken for different components of the project to run. Generating
the world cloud chart was the slowest part of the project since it uses google translation from internet for
each review that the program reads.

![time](https://github.com/akshay-madar/airbnb-nyc-urban-tourism-challenge/blob/master/time_complexity.PNG)

## 3. Results:
  - *Travellers’ preferences:*
    - Most travellers book Airbnb for short stays.
    - Travellers prefer moderately priced Airbnbs
  - *Listings:*
    - Expensive properties go unbooked in NYC
    - Airbnbs in Manhattan area are priced higher than Airbnbs in other parts of NYC
    - Neighbourhood in Manhattan is particularly strong, as compared to other boroughs, in
determining the price. This perceived premium with respect to location, results in higher
prices and low bookings.

## 4. Conclusion/Recommendations:
  - Although most of the AirBnbs are unbooked in NYC, long stay listings are particularly not
popular among travellers. Having shorter minimum stay period could lead to an increase in the
number of bookings that such properties accumulate over the year.
  - Expensive listings are not preferred by travellers, particularly when New York in general is an
expensive city to live in. Airbnb could look at cheaper staggered pricing during certain times of
the year, to increase adoption rates among budget travellers.
  - For further analysis, a sentimental analysis can be done to understand the features that are most
important to the travellers. Also, travellers’ ratings and reviews can be used to refine segments of
the listings to understand best and worst listings.
  - We could look at commute options around the listed properties. Availability of cheap public
transport like subway, and proximity from the airport are prime concerns for any traveller.
  - An analysis of included benefits, like kitchen, free city tours, etc could help in identifying
additional factors that influence travellers when deciding about accommodations.

### Citations:
  - [1] Airbnb Statistics: User & Market Growth Data. (2019, November). Retrieved from https://ipropertymanagement.com/airbnb-statistics/
  - [2] Sea The City. (2019, December 31). NYC Tourism Facts & Statistics. Retrieved from https://www.seathecity.com/nyc-tourism-facts-statistics/

### Instructions:
Please run the following jupyter notebook ["code.ipynb"](https://github.com/akshay-madar/airbnb-nyc-urban-tourism-challenge/blob/master/code.ipynb)

