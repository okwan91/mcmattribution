# Which Platform Rules Them All?
###### Multi-Channel Marketing Attribution 

### Background
A problem some companies face when trying to assess the best strategies for their advertisements and assessing which channels can lead them to a conversion. A conversion is When a user who has been exposed to an advertisement achieves the company’s desired goal. Examples of a conversion are a subscription, email sign up, or purchase. If a company utilizes a multi-channel marketing strategy and a purchase of the advertised product is made, which channel gets that credit, or also known as attribution? This project will explore how to utilize the Markov Chain method for channel attribution.

### The Data
I was unable to find a dataset that had user demographic data and their interactions with different marketing channels, so I made my own through data synthesis. My code used to create this data was built off of [this](https://github.com/ryan-kasi/mcm_synthetic_data/blob/main/mcm%20synthetic%20data.ipynb) as the starting point. The code takes the user through a funnel of assumed phases the consumer journeys through:
* Problem Recognition
* Information Search
* Evaluation Alternatives
* Purchase Decision
* Purchase
* Repurchase

There are four main marketing channels our users could interact with such as "YouTube, "Facebook", "Search", and "E-mail" and their timestamps. I also added a layer of user demographic information based off of the channel that they interacted with. For example, users who interact with Youtube are more likely to be between the ages of a child to a teenager of either gender. Facebook users were more likely to be male and likely in their mid 40s and above. For the sake of simplicity, I had user ages bucketed into four buckets:
* Boomer
* Millenial
* Gen Z
* Gen Alpha

This is to mimic user information if the data was organically obtained. My data also has clickthrough and purchase/conversion fields as well. Below is how our data looks thus far:
![screenshot](https://github.com/okwan91/mcmattribution/blob/main/Graphs/datascreen.png)

##### Data Details
* 6,822,360 rows 
* 9,993 users
* 53,897 clicks
* 16,855 purchases

### Exploratory Data Analysis
#### Visits by Channel
|     Channel    |      Visits     |
| -------------  |:---------------:|
| E-mail         | 565,854         |
| Facebook       | 2,079,124       |
| Search         | 2,088,900       |
| YouTube        | 2,088,483       |


Below is a table comparing the amount of clicks versus purchases:
![clicks vs purchases](https://github.com/okwan91/mcmattribution/blob/main/Graphs/clicksvspurch.png)
As expected, there is a significantly higher number amount of clicks versus purchases, except for e-mail which has a slightly higher amount of purchases compared to clicks. This could be a scenario where the user receives an e-mail with the ad with some sort of promotion and instead of clicking the e-mail the user navigates directly to the site to purchase. The lowest performer our weakest in performer for purchases actually turns out to be our strongest performer in clicks, YouTube. This is likely due to our assumptions that most YouTube users are children and are less likely to have their own money to make an online purchase and wouuld have to request permission from their parents. 

![impressions vs clicks](https://github.com/okwan91/mcmattribution/blob/main/Graphs/Channelimpvsclicks.png)
The above scatterplot compares the amount of views (or impressions) against the amount of clicks by channel. I assume that after a certain amount of impressions, that it can lead to a higher rate of clicks up to a certain degree. Then after we exceed this optimum level of impressions, our click rate drops off.

![impressions vs purchase](https://github.com/okwan91/mcmattribution/blob/main/Graphs/Channelimpvsbuy.png)
Similar to the previous plot, the above shows the rate of purchases/conversions against level of impressions.


