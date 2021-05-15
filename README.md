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

This is to mimic user information if the data was organically obtained. My data also has clickthrough and purchase/conversion fields as well.

