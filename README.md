# Which Platform Rules Them All?
###### Multi-Channel Marketing Attribution 
![war](https://github.com/okwan91/mcmattribution/blob/main/social-media-war.jpg)

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
* Boomer (ages 50 and up)
* Millenial (between mid 20s to mid 30s)
* Gen Z (early to mid 20s)
* Gen Alpha (teens and younger)

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

### Marketing Attribution
Depending on the company, some may distribute attribution based off of the first or last channel a user interacted with prior to a conversion, or even both. The below graph displays the comparison of channels with the highest and lowest levels of attribution based off of either the first or last touch method:

![First touch](https://github.com/okwan91/mcmattribution/blob/main/Graphs/firstvlast.png)

If I were to implement the first touch method, YouTube has the highest level of attribution while e-mail had the lowest. If we follow the last touch atrribution method, it is actually the reverse with e-mail with the highest level of attribution.

If we utilize the first AND last touch attribution method, we get the below results. The strongest pair was search and e-mail.

![first and last](https://github.com/okwan91/mcmattribution/blob/main/Graphs/firstalast.png)

Is it correct to assume that the first or the last channels our users interacted with are the actual causes of conversion though? Typically, users will go through several phases before they make the final decision and act upon that decision to make a purchase of a product. If a user interacts with more than one channel, then each channel plays some part in the funnel that leads to a successful conversion. This is why I implemented the Markov Chain method.

#### Markov Chain Method
The Markov Chain method is a form of reinforcement learning where we assume that prior actions affect the decision making for the current action. Through the Markov method I will follow users through their journey, called a path, that wil lead to either a successful conversion or nothing. This method is great because not only can you calculate each channel's level of attribution, you can also calculate the removal impact of those channels from your marketing campaign. After I noted each user's path, I then calculated a base conversion rate and created a transition matrix that displayed the average probability of a user moving from one channel to another. 

![transition matrix](https://github.com/okwan91/mcmattribution/blob/main/Graphs/transitionheatmap.png)

If we focus on just the conversion column, e-mail had the highest probability to lead to a conversion in comparison to other channels. When observing the other boxes of our heatmap the probability of a user going from one channel to another is relatively even. The column "end" is used when a conversion was not successful. It is worth nothing that while e-mail had the highest probability rate for a conversion, it also has the highest probabilty rate to lead to a failed conversion. 

![markov attribution](https://github.com/okwan91/mcmattribution/blob/main/Graphs/channelattlvls.png)

As shown below, the channel with the highest level of attribution was e-mail. This could be because e-mail's typically will have some sort of promotion, discount, or even just to remind you that you have something still sitting in your cart. Our weakest performer appears to be Youtube, which isn't too surprising as stated earlier that the main demographic of the YouTube audience are children. On top of finding the top channel with the highest level of attribution, I also wanted to know what would be the effect of removing a channel from my marketing campaign's conversion rate.

![removal](https://github.com/okwan91/mcmattribution/blob/main/Graphs/channelremoval.png)

To no surprise, removing e-mail from our marketing campaign showed the greatest affect on our conversion rate at 74%. Then it was followed by Facebook at 64%, Search at 63%, and YouTube at 57%. This was calculated by removing each channel and re-simulating the user journey to measure the change in conversion rates. 

### Conclusions
The Markov method is great because you're not attributing only one channel over the rest for successful conversions in a multi-channel marketing campaign, each channel has some level of impact on the user and their journey. This method can be utilized so that companies can implement more effective campaigns and know where their investments efforts lay and how to get the most returns out of their investments. 

As a reminder, these results are based off of a simulation of real world data. The performance of each channel was as expected due to how our data was synthesized. In the marketing funnel, the user had a higher probability of making a purchase during the purchase stage of the funnel when interacting with an e-mail advertisement. 


