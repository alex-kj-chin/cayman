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

Examining the provided data, we see that riders have one of four types of passes: Monthly Pass, Flex Pass, Walk-up, and Staff Annual. Of these, we presume that (as was noted on the MindSumo website) that the Walk-Up users are temporary or sporadic users, whereas the other three categories represent more regular users.

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
