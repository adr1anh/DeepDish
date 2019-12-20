# DeepDish: Using food safety data to visualize Chicago

## Abstract:




The City of Chicago provides a dataset containing the results of food inspections it conducted since January 1st 2010. In total, there are almost 200'000 observations including information about the establishment and inspection results.

As a first step, we explore 

As a first step, we will visualize this information in maps. Our aim will be to find patterns exhibited in the data.
Using the Yelp API, we will complete the missing data and use their rating system to complement our analysis. This could give us another risk indicator, which could be used to assess whether to perform an inspection.
By analyzing the violation types and comments, we aim to build a model predicting the result of the inspection (pass / fail).
Finally and if time allows us to go further, we hope to use other available datasets from the [Chicago Data Portal](https://data.cityofchicago.org) and explore relations to other socio-economic factors.


## Research Questions:

##### NEW
- Do the sanitary conditions of food establishments vary with respect to geography?
	- Do new geographical pattern appear?
	- blabla
- How do user-generated online reviews help us understand whether an establishment passes or not its inspection?
	- Is there a clear difference in establishments that fail their inspections?
	- Can we predict the result given its online rating?
- What information can we extract from inspector's comments to complement the existing features of the dataset?
	- Do certain words clearly 
- How can we forecast and observe trends in these inspections over time?

##### OLD
- Are there geographical patterns with respect to food quality?
- Do we get a different representation of the districts of Chicago, when looking at the food establishments and their inspection score?
- How accurate are internet reviews in predicting the risk level?
- Are the comments and violation types from an inspection good predictors for the reuslt of the inspection?

## Dataset 
### [Chicago Food Inspections](https://www.kaggle.com/chicago/chicago-food-inspections)

We present a section of the raw dataset. 

<table border="1" class="dataframe">  <thead>    <tr style="text-align: right;">      <th></th>      <th>Inspection ID</th>      <th>DBA Name</th>      <th>AKA Name</th>      <th>License #</th>      <th>Facility Type</th>      <th>Risk</th>      <th>Address</th>      <th>City</th>      <th>State</th>      <th>Zip</th>      <th>Inspection Date</th>      <th>Inspection Type</th>      <th>Results</th>      <th>Violations</th>      <th>Latitude</th>      <th>Longitude</th>      <th>Location</th>      <th>Historical Wards 2003-2015</th>      <th>Zip Codes</th>      <th>Community Areas</th>      <th>Census Tracts</th>      <th>Wards</th>    </tr>  </thead>  <tbody>    <tr>      <th>0</th>      <td>2320315</td>      <td>SERENDIPITY CHILDCARE</td>      <td>SERENDIPITY CHILDCARE</td>      <td>2216009.0</td>      <td>Daycare Above and Under 2 Years</td>      <td>Risk 1 (High)</td>      <td>1300 W 99TH ST</td>      <td>CHICAGO</td>      <td>IL</td>      <td>60643.0</td>      <td>2019-10-23T00:00:00.000</td>      <td>License Re-Inspection</td>      <td>Pass</td>      <td>NaN</td>      <td>41.714168</td>      <td>-87.655291</td>      <td>{\'longitude\': \'41.7141680989703\', \'latitude\': \'-87.65529116028439\'}</td>      <td>NaN</td>      <td>NaN</td>      <td>NaN</td>      <td>NaN</td>      <td>NaN</td>    </tr>    <tr>      <th>1</th>      <td>2320342</td>      <td>YOLK TEST KITCHEN</td>      <td>YOLK TEST KITCHEN</td>      <td>2589655.0</td>      <td>Restaurant</td>      <td>Risk 1 (High)</td>      <td>1767 N MILWAUKEE AVE</td>      <td>CHICAGO</td>      <td>IL</td>      <td>60647.0</td>      <td>2019-10-23T00:00:00.000</td>      <td>Canvass</td>      <td>Pass w/ Conditions</td>      <td>23. PROPER DATE MARKING AND DISPOSITION - Comments: ... </td>      <td>41.913588</td>      <td>-87.682203</td>      <td>{\'longitude\': \'41.9135877900482\', \'latitude\': \'-87.68220283542529\'}</td>      <td>NaN</td>      <td>NaN</td>      <td>NaN</td>      <td>NaN</td>      <td>NaN</td>    </tr>    <tr>      <th>2</th>      <td>2320328</td>      <td>LAS ASADAS MEXICAN GRILL</td>      <td>LAS ASADAS MEXICAN GRILL</td>      <td>2583309.0</td>      <td>Restaurant</td>      <td>Risk 1 (High)</td>      <td>3834 W 47TH ST</td>      <td>CHICAGO</td>      <td>IL</td>      <td>60632.0</td>      <td>2019-10-23T00:00:00.000</td>      <td>Canvass</td>      <td>Out of Business</td>      <td>NaN</td>      <td>41.808025</td>      <td>-87.720037</td>      <td>{\'longitude\': \'41.80802515275297\', \'latitude\': \'-87.72003743037237\'}</td>      <td>NaN</td>      <td>NaN</td>      <td>NaN</td>      <td>NaN</td>      <td>NaN</td>    </tr>    <tr>      <th>3</th>      <td>2320319</td>      <td>LA PALAPITA</td>      <td>LA PALAPITA</td>      <td>2694702.0</td>      <td>Restaurant</td>      <td>Risk 1 (High)</td>      <td>3834 W 47TH ST</td>      <td>CHICAGO</td>      <td>IL</td>      <td>60632.0</td>      <td>2019-10-23T00:00:00.000</td>      <td>License</td>      <td>Pass</td>      <td>47. FOOD &amp; NON-FOOD CONTACT SURFACES CLEANABLE, PROPERLY DESIGNED, CONSTRUCTED &amp; USED - Comments: ...</td>      <td>41.808025</td>      <td>-87.720037</td>      <td>{\'longitude\': \'41.80802515275297\', \'latitude\': \'-87.72003743037237\'}</td>      <td>NaN</td>      <td>NaN</td>      <td>NaN</td>      <td>NaN</td>      <td>NaN</td>    </tr>    <tr>      <th>4</th>      <td>2320228</td>      <td>47TH ST CANTINA</td>      <td>47TH ST CANTINA</td>      <td>2678250.0</td>      <td>Liquor</td>      <td>Risk 3 (Low)</td>      <td>4311 W 47TH ST</td>      <td>CHICAGO</td>      <td>IL</td>      <td>60632.0</td>      <td>2019-10-22T00:00:00.000</td>      <td>License</td>      <td>Pass w/ Conditions</td>      <td>3. MANAGEMENT, FOOD EMPLOYEE AND CONDITIONAL EMPLOYEE; KNOWLEDGE, RESPONSIBILITIES AND REPORTING - Comments: ...</td>      <td>41.807662</td>      <td>-87.731480</td>      <td>{\'longitude\': \'41.80766199360051\', \'latitude\': \'-87.73148027311129\'}</td>      <td>NaN</td>      <td>NaN</td>      <td>NaN</td>      <td>NaN</td>      <td>NaN</td>    </tr>  </tbody></table>

Our goal for this first milestone was to make it as usable as possible for our analysis.



### [Yelp Fusion API](https://www.yelp.com/developers/documentation/v3)

Unfortunately, the Yelp Dataset available to academics is only a subset of their full database and does not include information about establishents in the city of Chicago. We asked Yelp what our options were and they directed us towards their *Fusion API*.

The first step was using the business matching endpoint to relate a Yelp business ID to each unique establishment found in the dataset. 
By only sending *name*, *address*, *city*, *state* and *country*, we receive back a *business ID*, *GPS coordinates*, *address*, *zip code* and others features. This information is not very usefull yet, because the original data already included much of this information. 

From the scrapping we were able to perform, Yelp was able to match about 66% of the businesses in the data. 

Once we have theses business IDs, we can query the API again and get the full information for a business including *is_closed*, *rating*, *review count*, *food categories* and *price*.

One of our research goals was to use the reviews to infer somethings from the inspection score. This might no longer be possible as we can only get 3 reviews per establishment, with some text cropped. We have still started scrapping these.

One problem with this approach is that we are limited to 5'000 API calls per day, and each call to a *business match query*, *business query*, and *review query* counts for one call. With 32'374 unique businesses, we would need about 78'000 API calls. We are in contact with Yelp to increase our limit. If this is not possible we can consider only doing analyses on a subset of the full dataset.


## Updates on Previous Milestone and New Goals 

How far have we gone with regards to the goals set at the previous milestone? We discuss this here and outline our goals for the next milestone. The main notebook is contained in the 'chicago_project.ipynb' file.

#### General data cleaning
We first looked into the NaN values of the dataset. We dealt with NaN values of the Zip column by scrapping the codes by using the Longitude and Latitude columns and the myGeocoder API. We then dealt with Nan Values of Longitude and Latitude by dropping them. Maybe we will try to scrap them by using the Adress column. 

We dealt with the Inspection Type and Facility Type columns by merging the least used ones into one called 'other' and by merging many different types into a more generic one (example: 'tavern', 'bar', 'diner' into 'restaurant' for Facility Type).

Each element of the Violations column is a big string containing all the violations noted during the inspection with comments. We converted it to a list of violations and we cleaned each type of violation to have the least number of violations.

As the Risk is an ordinal variable we converted it to an int variable and we merged the 'All' value with 'Risk 1 (High)'. We dropped every row without a Risk value.



#### Find a way to visualize information on a map, according the adresses or geolocation.

We did an introductory analysis to understand the distribution of the risk level and the number of inspections over time, then analyze the results. 

In order to visualize the data geographically, we followed two approaches. The first one is based on the Zip code number. Here we used Folium to split Chicago into 60 Zip codes and colored the map accordingly, using different metrics. The second approach was based on splitting the data by the risk variable and plotting resulting heatmaps. To go further in this analysis, we initially wanted to use the HeatMapWithTime plugin of Folium. However we encountered issues with it and discuss them in the notebook. 

We thus have made advances for our two first research questions and are able to engage in a more precise analysis and results for the next milestone, as we are now better acquainted with the data and the visulation tools.

As for the third research question posed in the last milestone *(Is there a consistent way of redesigning the districts of the city with respect to food quality, across establishment types?)*, it may not be interesting to engage in redesigning the districts of the city as there are yet no significant geographical distinctions. Furthermore, re-defining geographical partition appears very complicated. Indeed, we already had to find a .json file online to allow us to split the city by its zip codes, and building such a file seems quite complicated.

For the next milestone, we can look deeper at the visualization with regards to the violation categories and how it compares to the risk given to the establishment. We would also like to investigate geographical repartition as a function of the violations. 

	
#### Explore the Yelp data base to add information for each establishment.

This goal was established before realizing that the Yelp Open Dataset did not contain information about Chicago. By having to scrap this data instead, we were not yet able to persue these goals. We also note that some of them may no longer be possible.


- Analyzing the review text for food safety violations will prove harder since we will only get access to 3 per business. Moreover, we only get a snippet of the text.
- Popularity can still be assessed using the overall rating at review count.
- We can get access to a bit more information such as price range, food type, and if the establishment is still open for business.
- Fill in missing values in the dataset.


#### Potentially find other datasets provided by the City of Chicago.
We have not explored other dataset since we decided to focus on the current two.


#### Predicting inspection outcome

We would like to assess the predictive capability of the variables in the dataset in order to predict the outcome of the inspection (pass/fail). The new directions for data analysis highlighted in the sections above, specifically concerning the violation type and the comments associated will help us in this regard. 
This might involve some light natural language processing.

## Questions for TAs
- Given the big number of datasets made available by the City of Chicago, it would make a lot of sense to include some extra information. To what extent should we explore other datasets in contrast to focusing more on the current one?
-Using function HeatMapWithTime(): We have not been able to see our result using this function and have found that it maybe a current of the folium package:
https://github.com/python-visualization/folium/issues/1232
https://github.com/python-visualization/folium/issues/1231
If this is the case, is there any alternatives that you would recommend ?


