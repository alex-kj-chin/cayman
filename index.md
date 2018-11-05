---
layout: default
---
The code used to make these findings can be found [here](https://github.com/alex-kj-chin/capital_one_challenge).

# Questions (1-4)

The following subsections are organized so as to match up to Questions 1-4 on the MindSumo website and facillitate ease of checking the requirements ahve been met.

## Data Visualizations

Asside from the guidelines of the project, I was interested in investigating how the usage broke down by day of the week. The first thing I investigated was simply the number of rides by day of the week

![weekday_usage](/assets/weekday_usage.png)

The main takeaway from this graph is that individuals are about 10%-15% more likely to bike on Thursday/Friday than Monday. However, we can add a layer of depth here by examining how many of these rides are Walk-Up (single-day riders).

![walk_usage](/assets/walk_usage.png)

Interestingly here, we see that there are about double the number of Walk-Up riders on the weekend compared to the weekdays (and correspondingly fewer regular riders on the weekends). This makes a lot of sense, as we can see from the LA Metro website, a major [selling point](https://bikeshare.metro.net/buy-in-bulk/) of these Walk-Up passes is that hotels or other tourist-industry businesses can purchase and give them out to guests. Tourists are more likely to come during the weekend, which explains this large difference. Another interesting result appears when we take a look at the duration of the rides as opposed to just the number of rides. Although the number of rides taken during the weekend is only slightly more than those taken during the week, the total duration of those rides is substantially higher (more than double). Since individuals have more time to bike on the weekends, this makes sense. A secondary cause may be that since tourists are only biking once--as opposed to commuting every day to work--they are more likely to take one long bike ride (people who need to commute a long distance every weekday may switch to other methods of transportation due to fatigue).

![duration_usage](/assets/duration_usage.png)

The next facet of the problem I wanted to investigate was bike mileage. My expectation was that the distribution of mileages would semi-gaussian but with a large pileup at a certain mileage where bikes start to break down. I calculated bike mileages with a similar schema to how I calculate average distance traveled (see that section for more information on the methodology). I found the below graph

![bike_miles](/assets/bike_mileages.png)

As expected, the distribution was relatively normal, but contrary to my expectation, there does not seem to be an evident pileup. I find two possible explanation. The first is that since this data is only . The second is that bikes can be repaired to extend their lifetime almost infinitely, and when they are reentered into the system with the same Bike ID. This means there is no real cutoff on bike lifetimes--if this is the case, LA Metro might consider reentering bikes with a new ID so that it is easier to do analyses of bike lifetimes to estimate repair costs and the like.

Often companies want to see where their revenue sources are coming from. The revenue model for LA Metro is broken down into subscription fees and fees for rides over 30 minutes. Since the data was lacking user ids or other information to identify unique users, I chose to only visualize the fees occuring from rides over 30 minutes long (otherwise the validity of my analysis might be compromised). We will see that just visualizing a single part of the revenue model is enough to motivate policy recommendations. Below is a pie chart of where the fees for rides over 30 minutes (henceforth referred to as overtime charges) are from.

![rev_pie](/assets/revenue_pie.png)

We see that the majority are from Walk-Up customers. In fact, about $85,150 overtime charges come from Walk-Up customers, while the second largest--Monthly Pass--only accounts for a little over $23,000. An interesting follow-up question is to see if a small number of Walk-Up customers are taking extremely long rides or if in general Walk-Up customers are just more likely to go over the 30 minute limit. Below is a pie chart of all the overtime customers, how many of them come from each segment (the chart above is the percentage of overtime revenue derived from each segment).

![overtime_pie](/assets/overtime_pie.png)

This tells us that Walk-Up customers are very likely to incur overtime charges, and it's not just a small subpopulation taking extremely long rides. Either way, this data indicates that LA Metro is most effective in gaining overtime charges from Walk-Up customers, so they should continue to find more opportunities to increase that customer segment.

A variety of other visualizations will be provided to answer questions throughout.

### Start/Stop Stations Popularity

I chose to cross-reference the keys in the provided data set with the [station metadata](https://bikeshare.metro.net/about/data/) so as to be able to provide the plain-text names of the most popular stations. Since different stations were opened at different times (and some have since closed), it is not sufficient to simply sum the arrivals and departures. Instead, we should find the average number of arrivals and departures per day for each station. Thus, I ran through the data to keep track of arrivals, departures, and opening and closing dates of stations (calculated as first and last recorded trip). These were used to calculate the stations with highest arrival and departure rates.

The five most popular stations for arrival were

1. Broadway & 3rd (4.4%, 28.7 per day)
2. 7th & Flower (4.3%, 23.5 per day)
3. Traction & Rose (4%, 22 per day)
4. 7th & Spring (3.8%, 20.7 per day)
5. Union Station West Portal (3.7%, 20.2 per day)

Similarly, the five most popular stations for departure were

1. 3rd & Rose(4.4%, 24.1 per day)
2. Broadway & 3rd (3.5%, 19.3 per day)
3. Main & 1st (3.5%, 18.9 per day)
4. 7th & Flower (3.4%, 18.3 per day)
5. Traction & Rose (3.4%, 18.2 per day)

One might notice that there is a good amount of overlap between the most common points of departure and arrival. In fact, all 10 arrival and departure locations are the same. This makes a lot of sense, as individuals who depart from one location and arrive at another are likely to later depart from their initial arrival station and arrive at their initial departure station. I also chose to do a general aggregation of the data. Below I present histograms of the number of arrivals and departures (data is binned into 50 subdivisions)

![departures_hist](/assets/departure_hist.png)

![arrivals_hist](/assets/arrivals_hist.png)

We see that overall there are a couple of stations with higher arrival and departure rates, but the majority of stations have a relatively lower arrival and departure rates. It is also helpful to see these laid out geographically

## Average Distance Traveled

Before doing anything, I cleane the data here. There were a couple of trips where the latitude and longitude data were incorrect. This resulted in ride distances of thousands of miles, which were clearly incorrect.

The methodology here was to use the distance between stations as the distance traveled on a bike ride. However, an issue arrises when a round trip is registered. My initial idea was to utilize the non-round-trips to calculate the average speed for a biker and then for round trips multiply the trip duration by the average speed of a biker to get the distance traveled on that trip. However, this resulted in non-round trips having an average distance of close to 1.2 miles and round trips having an average distance of close to 12 miles (we would expect to this to be about double, but a factor of 4 is a little much). Furthermore, this method of calculation resulte in trips of over 300 miles. The main issue is that sometimes a person who rents a bike for a round trip may take it to somewhere there is not a nearby bike station, so they may lock it somewhere where they go to work, and then all of this time is being treated as riding time by my first counting schema.

Thus, I modified my counting schema to impose a maximum on the round-trip time. After conducting [research](https://mobilitylab.org/2017/02/27/how-far-bike-work/), it seems that it is unreasonable to bike more than about 20 miles per day to work so I imposed this as a maximum on round trip distances (there will most likely be some outliers cut off by this maximum, but the fundamental idea is that it is a better representation of the data because it makes the majority of the data points more accurate). After imposing this bound, I saw that the average distance traveled was **1.4** miles.

To those who object that the error handling here is a too rough, I would point out that less than 10% of the data represents round trips, and only about 1% of data represents round trips that were of length >20 miles. Thus, even if I were to increase the maximum round trip distance to 50, this only increased the average distance traveled to **1.6** miles (this is also because many trips are less than a mile, so they greatly drag down the average).

## Number of Riders Including Bike Sharing as Regular Part of Commute

Examining the provided data, we see that riders have one of four types of passes: Monthly Pass, Flex Pass, Walk-up, and Staff Annual. Of these, we presume that (as was noted on the MindSumo website) that the Walk-Up users are temporary or sporadic users, whereas the other three categories represent more regular users. Additionally, since there is no identifying information for bikers, it is assumed that each bike ride represents a single user (also an assumption that was approved on MindSumo)--alternatively, one could attempt to map trips going in opposite directions in the morning and evening to a single person, but this could end up confounding results more than helping if done poorly. As a final assumption, we calculate the regular ridership as a daily occurence, and when a bike rentalcrosses between two days, we allocate it to the day it started on. It is important to state assumptions in data analysis as sometimes only slight differences in assumptions cause major differences in results.

We see that the average number of bike sharing users per day is about **340**. However, the standard deviation of users per day is **127**, which is exceptionally high. In fact, if we graph the daily ridership, we see that this is highly volatile. We would expect overall fluctuation over time of ridership (as accompanying bike stations have opened and closed), but even within this long-term variation, there is a high amount of variation.

![daily_bike_usage](/assets/bike_usage_daily.png)

One possible cause is that there is variability over the days of the week. We can test this theory by aggregating to get total regular ridership broken down by week. We see that this reduces variance slightly as in the below graph.

![weekly_bike_usage](/assets/bike_usage_weekly_no.png)

We can at least check our assumption here that excluding the Walk-Up riders . Indeed, we see in the graph below the weekly "ridership" including Walk-Up riders is much more variant (and the variance is also higher). Thus, it was a good assumption to exclude Walk-Up riders in the counting of regular users.

![weekly_bike_total](/assets/bike_usage_weekly.png)

# Additional Questions

## Ridership Change over Seasons

We see, as expected, that there is high variance in bike usage depending on season. First, we calculate the nuber of riders per day in different seasons. Since the timeframe is not uniformly distributed accross the seasons, it's important to normalize over the number of days in each season in our data set. Nonetheless, we see that summer is by far the most popular season to use LA Metro for bike rides.

![seasonal_usage](/assets/bike_usage_seasonally.png)

Next, we want to look at the types of memberships used during the seasons. We exclude the Annual Staff usage because this is rare--so rare in fact that it does not occur meaningfully during the 11 days of spring included in the dataset.

![seasonal_stacked](/assets/seasonal_stacked.png)

We see that higher ride rates in the summer are driven both by increased riders using their monthly passes and walk-up. This makes sesnse, as locals with more time will be more likely to purchase monthly passes, and tourists visiting during the summer will be more likely to purchase walk-up tickets.

## Net Change in Bikes



## Trip Route Category-Passholder

A good way to view the intersection of various different labels is a heatmap. I use seaborn to generate the following heatmap to visualize the common intersections between Trip-Route Category and Passholder.

![heatmap](/assets/heatmap.png)

By far the most common combination is monthly users taking one-way trips. This makes sense, as the majority of users are monthly users, and in general they use their bikes to get to and from the place they are commuting, but rack the bikes in between. The other popular one-way trip user are walk-up users. Since this is the second biggest customer segment (in terms of numbers of rides), it makes sense that this is also a popular combination. It is hard to distinguish, but the only relevant intersection with round-trip users is walk-up users. This supports our findings on revenue sources (from the **Data Visualizations** section), as round-trips are more likely to run overtime charge since they are in general longer. More interestingly, even though the monthly users are the biggest segment, they are not the most likely to do round trips. This makes sense because if you take a round-trip, then either **A)** you don't get anywhere which is only useful for tourists or **B)** there is no station near where you are commuting so you pay exhorbitant overtime charges. Neither of these are prefereable situations, so an individual would not be incentivized to buy a monthly pass if this would be their use case. Thus for round-trips, mostly we see walk-up users.

