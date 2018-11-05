---
layout: default
---
The code used to make these findings can be found [here](https://github.com/alex-kj-chin/capital_one_challenge).

# Questions (1-4)

The following subsections are organized so as to match up to Questions 1-4 on the MindSumo website and facillitate ease of checking the requirements ahve been met.

## Data Visualizations

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

## Number of Riders Including Bike Sharing as Regular Part of Commute

Examining the provided data, we see that riders have one of four types of passes: Monthly Pass, Flex Pass, Walk-up, and Staff Annual. Of these, we presume that (as was noted on the MindSumo website) that the Walk-Up users are temporary or sporadic users, whereas the other three categories represent more regular users. Additionally, since there is no identifying information for bikers, it is assumed that each bike ride represents a single user (also an assumption that was approved on MindSumo)--alternatively, one could attempt to map trips going in opposite directions in the morning and evening to a single person, but this could end up confounding results more than helping if done poorly. As a final assumption, we calculate the regular ridership as a daily occurence, and when a bike rentalcrosses between two days, we allocate it to the day it started on. It is important to state assumptions in data analysis as sometimes only slight differences in assumptions cause major differences in results.

We see that the average number of bike sharing users per day is about **340**. However, the standard deviation of users per day is **127**, which is exceptionally high. In fact, if we graph the daily ridership, we see that this is highly volatile. We would expect overall fluctuation over time of ridership (as accompanying bike stations have opened and closed), but even within this long-term variation, there is a high amount of variation.

![daily_bike_usage](/assets/bike_usage_daily.png)

One possible cause is that there is variability over the days of the week. We can test this theory by aggregating to get total regular ridership broken down by week. We see that this reduces variance slightly as in the below graph.

![weekly_bike_usage](/assets/bike_usage_weekly_no.png)

We can at least check our assumption here that excluding the Walk-Up riders . Indeed, we see in the graph below the weekly "ridership" including Walk-Up riders is much more variant (and the variance is also higher). Thus, it was a good assumption to exclude Walk-Up riders in the counting of regular users.

![weekly_bike_total](/assets/bike_usage_weekly.png)

###### Header 6

| head1        | head two          | three |
|:-------------|:------------------|:------|
| ok           | good swedish fish | nice  |
| out of stock | good and plenty   | nice  |
| ok           | good `oreos`      | hmm   |
| ok           | good `zoute` drop | yumm  |

### There's a horizontal rule below this.

* * *

### Here is an unordered list:

*   Item foo
*   Item bar
*   Item baz
*   Item zip

### And an ordered list:

1.  Item one
1.  Item two
1.  Item three
1.  Item four

### And a nested list:

- level 1 item
  - level 2 item
  - level 2 item
    - level 3 item
    - level 3 item
- level 1 item
  - level 2 item
  - level 2 item
  - level 2 item
- level 1 item
  - level 2 item
  - level 2 item
- level 1 item

### Small image

![Octocat](https://assets-cdn.github.com/images/icons/emoji/octocat.png)

### Large image

![Branching](https://guides.github.com/activities/hello-world/branching.png)


### Definition lists can be used with HTML syntax.

<dl>
<dt>Name</dt>
<dd>Godzilla</dd>
<dt>Born</dt>
<dd>1952</dd>
<dt>Birthplace</dt>
<dd>Japan</dd>
<dt>Color</dt>
<dd>Green</dd>
</dl>

```
Long, single-line code blocks should not wrap. They should horizontally scroll if they are too long. This line should be long enough to demonstrate this.
```

```
The final element.
```
