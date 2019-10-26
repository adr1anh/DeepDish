# Visualizing Disctricts in the City of Chicago through Food Safety Inspections

## Abstract:


The City of Chicago provides a dataset containing the results of food inspections it conducted since January 1st 2010. In total, there are almost 200'000 observations including information about the establishment and inspection results. 
As a first step, we will visualize this information in maps. Our aim will be to find patterns exhibited in the data. Then, using clustering techniques, we can redefine disctricts.
Later, we will also incorporate the Yelp Open Dataset to better categorize the different establishments. This could give us another risk indicator, which could be used to asses whether to perform an inspection.
Finally and if time allows us to go further, we hope to use other available datasets from the [Chicago Data Portal](https://data.cityofchicago.org) and explore relations to other socio-economic factors.

<!--Our goal in this project is to visualize the city of Chicago as a graph of the food violation in an appealing and concise way in order to analyse the streets where the most violation occurs. In a second part we can thus use another dataset provided by the Chicago Data Portal such as Crimes - 2001 to present and look for correlation between th district with high crime and food violation.  Through this we hope to gain deeper insight into how the city of Chicago can be analyzed and which implications on the population can be inferred by food violation.-->

## Research Questions:
- Are there geographical patterns with respect to food quality?
- Do we get a different representation of the districts of Chicago, when looking at the food establishments and their inspection score?
- Is there a consistent way of redesigning the districts of the city with respect to food quality, across establishment types?
- How accurate are internet reviews in predicting the risk level?
- Can this data be used to indicate the need for a new inspection?

## Dataset 
- [Chicago Food Inspections](https://www.kaggle.com/chicago/chicago-food-inspections)
- [Yelp Open Dataset](https://www.yelp.com/dataset)

## Internal Milestones
- General data cleaning.
	- Set the right types for each column (categories, geolocation data. 
	- Check for duplicates.
- Find a way to visualize information on a map, according the adresses or geolocation.
	- Make a heatmap of risky establishments according to facitlty type and risk category.
	- Find best conditions to categorize establishments into seperate disctricts.
- Explore the Yelp data base to add information for each establishment.
	- Customer reviews can be interesting to correlate with actual inspection results.
	- Get information about the type of establishment such as food type, price, and popularity.
 	- Analyse reviews for mentions of food safety.
	- Can we get predictions of the health inspection score using only reviews? This would allow the health inspectors to more efficently do their jobs. 
	- Do reviews correctly represent the risk rating of an establishment.
- Potentially find other datasets provided by the City of Chicago.

## Questions for TAs
- Given the big number of datasets made available by the City of Chicago, it would make a lot of sense to include some extra information. To what extent should we explore other datasets in contrast to focusing more on the current one?
