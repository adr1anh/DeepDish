# DeepDish: Using food safety data to visualize Chicago

## Abstract:




To ensure food quality and safety to their fellow citizens, the Chicago Department of Public Health (CDPH) conducts regular inspections of every establishment providing food. We provide an analysis of food violations in Chicago and analyze results of these inspections to assess the most critical food violations. Afterwards, we take a look at the most representative comments arising from failed inspections through NLP. Then, we forecast the evolution of failed inspections for the next year. Moreover, we complement the dataset with data collected through Yelp.


## Research Questions:

- Do the sanitary conditions of food establishments vary with respect to geography and can we observe new geographical patterns?
- How do user-generated online reviews help us understand whether an establishment passes or not its inspection?
	- Is there a clear difference in establishments that fail their inspections?
	- Can we predict the result given its online rating?
- What information can we extract from inspector's comments using NLP techniques to complement the existing features of the dataset?
	- What are the most significant words in failed inspection comments?
	- Are there strong dependencies between geographical locations and certain words.
- Can we preidct the future percentage of failed inspections using temporal data?
- Are violations 1-14 indeed the most serious as asserted in the dataset description?


## Dataset 
### [Chicago Food Inspections](https://www.kaggle.com/chicago/chicago-food-inspections)

We present a section of the raw dataset. 

<table border="1" class="dataframe">  <thead>    <tr style="text-align: right;">      <th></th>      <th>Inspection ID</th>      <th>DBA Name</th>      <th>AKA Name</th>      <th>License #</th>      <th>Facility Type</th>      <th>Risk</th>      <th>Address</th>      <th>City</th>      <th>State</th>      <th>Zip</th>      <th>Inspection Date</th>      <th>Inspection Type</th>      <th>Results</th>      <th>Violations</th>      <th>Latitude</th>      <th>Longitude</th>      <th>Location</th>      <th>Historical Wards 2003-2015</th>      <th>Zip Codes</th>      <th>Community Areas</th>      <th>Census Tracts</th>      <th>Wards</th>    </tr>  </thead>  <tbody>    <tr>      <th>0</th>      <td>2320315</td>      <td>SERENDIPITY CHILDCARE</td>      <td>SERENDIPITY CHILDCARE</td>      <td>2216009.0</td>      <td>Daycare Above and Under 2 Years</td>      <td>Risk 1 (High)</td>      <td>1300 W 99TH ST</td>      <td>CHICAGO</td>      <td>IL</td>      <td>60643.0</td>      <td>2019-10-23T00:00:00.000</td>      <td>License Re-Inspection</td>      <td>Pass</td>      <td>NaN</td>      <td>41.714168</td>      <td>-87.655291</td>      <td>{\'longitude\': \'41.7141680989703\', \'latitude\': \'-87.65529116028439\'}</td>      <td>NaN</td>      <td>NaN</td>      <td>NaN</td>      <td>NaN</td>      <td>NaN</td>    </tr>    <tr>      <th>1</th>      <td>2320342</td>      <td>YOLK TEST KITCHEN</td>      <td>YOLK TEST KITCHEN</td>      <td>2589655.0</td>      <td>Restaurant</td>      <td>Risk 1 (High)</td>      <td>1767 N MILWAUKEE AVE</td>      <td>CHICAGO</td>      <td>IL</td>      <td>60647.0</td>      <td>2019-10-23T00:00:00.000</td>      <td>Canvass</td>      <td>Pass w/ Conditions</td>      <td>23. PROPER DATE MARKING AND DISPOSITION - Comments: ... </td>      <td>41.913588</td>      <td>-87.682203</td>      <td>{\'longitude\': \'41.9135877900482\', \'latitude\': \'-87.68220283542529\'}</td>      <td>NaN</td>      <td>NaN</td>      <td>NaN</td>      <td>NaN</td>      <td>NaN</td>    </tr>    <tr>      <th>2</th>      <td>2320328</td>      <td>LAS ASADAS MEXICAN GRILL</td>      <td>LAS ASADAS MEXICAN GRILL</td>      <td>2583309.0</td>      <td>Restaurant</td>      <td>Risk 1 (High)</td>      <td>3834 W 47TH ST</td>      <td>CHICAGO</td>      <td>IL</td>      <td>60632.0</td>      <td>2019-10-23T00:00:00.000</td>      <td>Canvass</td>      <td>Out of Business</td>      <td>NaN</td>      <td>41.808025</td>      <td>-87.720037</td>      <td>{\'longitude\': \'41.80802515275297\', \'latitude\': \'-87.72003743037237\'}</td>      <td>NaN</td>      <td>NaN</td>      <td>NaN</td>      <td>NaN</td>      <td>NaN</td>    </tr>    <tr>      <th>3</th>      <td>2320319</td>      <td>LA PALAPITA</td>      <td>LA PALAPITA</td>      <td>2694702.0</td>      <td>Restaurant</td>      <td>Risk 1 (High)</td>      <td>3834 W 47TH ST</td>      <td>CHICAGO</td>      <td>IL</td>      <td>60632.0</td>      <td>2019-10-23T00:00:00.000</td>      <td>License</td>      <td>Pass</td>      <td>47. FOOD &amp; NON-FOOD CONTACT SURFACES CLEANABLE, PROPERLY DESIGNED, CONSTRUCTED &amp; USED - Comments: ...</td>      <td>41.808025</td>      <td>-87.720037</td>      <td>{\'longitude\': \'41.80802515275297\', \'latitude\': \'-87.72003743037237\'}</td>      <td>NaN</td>      <td>NaN</td>      <td>NaN</td>      <td>NaN</td>      <td>NaN</td>    </tr>    <tr>      <th>4</th>      <td>2320228</td>      <td>47TH ST CANTINA</td>      <td>47TH ST CANTINA</td>      <td>2678250.0</td>      <td>Liquor</td>      <td>Risk 3 (Low)</td>      <td>4311 W 47TH ST</td>      <td>CHICAGO</td>      <td>IL</td>      <td>60632.0</td>      <td>2019-10-22T00:00:00.000</td>      <td>License</td>      <td>Pass w/ Conditions</td>      <td>3. MANAGEMENT, FOOD EMPLOYEE AND CONDITIONAL EMPLOYEE; KNOWLEDGE, RESPONSIBILITIES AND REPORTING - Comments: ...</td>      <td>41.807662</td>      <td>-87.731480</td>      <td>{\'longitude\': \'41.80766199360051\', \'latitude\': \'-87.73148027311129\'}</td>      <td>NaN</td>      <td>NaN</td>      <td>NaN</td>      <td>NaN</td>      <td>NaN</td>    </tr>  </tbody></table>

There 196'030 rows, with observations dated from 2010 until this year. All establishments are characterized by two names (**D**oing **B**usiness **A**s (DBA) and **A**lso **K**nown **A**s (AKA)) and a complete address including GPS coordinates.

For each inspection, we are given an identifier, an *a priori* risk level, the result of the inspection as well as the nature of it (business opening, random check, following a complaint, ...), and sometimes some comments left by the inspector.

We explore in further details the contents of the dataset in the next section explaining data cleaning process.



### [Yelp Fusion API](https://www.yelp.com/developers/documentation/v3)

Unfortunately, the Yelp Dataset available to academics is only a subset of their full database and does not include information about establishents in the city of Chicago. We asked Yelp what our options were and they directed us towards their *Fusion API*.

The first step was using the business matching endpoint to relate a Yelp business ID to each unique establishment found in the dataset. 
By only sending *name*, *address*, *city*, *state* and *country*, we receive back a *business ID*, *GPS coordinates*, *address*, *zip code* and others features. This information is not very usefull yet, because the original data already included much of this information. 

From the scrapping we were able to perform, Yelp was able to match about 66% of the businesses in the data. 

Once we have theses business IDs, we can query the API again and get the full information for a business including *is_closed*, *rating*, *review count*, *food categories* and *price*.

One of our research goals was to use the reviews to infer somethings from the inspection score. This might no longer be possible as we can only get 3 reviews per establishment, with some text cropped. Due to the limited number of API calls, we have not gone forward with this idea.

One problem with this approach is that we are limited to 5'000 API calls per day, and each call to a *business match query*, *business query*, and *review query* counts for one call. With 32'374 unique businesses, we would need about 78'000 API calls. We are in contact with Yelp to increase our limit. If this is not possible we can consider only doing analyses on a subset of the full dataset.

## Individual Contributions

- Adrian: Yelp data scrapping and analyis, data cleaning, finalizing submission.
- Edouard: Cleaning data, exploratory data analysis and plotting heatmaps, finalizing submission.
- Marc: Creating Choropleth maps, Classification and time series forecasting
- Rayan: Data Cleaning, feature importance and NLP insight for violations

Everybody contributed to writing the report and the finalization of the submission. We will also work together to prepare the final presentation.

## Updates on Previous Milestone:

### Map visualization:

Here we updated our previous two approaches to take into account the dates of the inspections. To do so we have created new heatmaps charaterized by risk level as before and looked at the number of establishment with those risk through time. The plot can be found in the Nbviewer notebook. Furthermore we have created Time Slider Choropleth Maps to visualize the evolution through time of the violation level in each Zip codes areas.

### Predicting inspection outcome:

For this section we have considered two approaches: 

First we cleaned the violation column in our data-set and gave a numerical value to each violations. Using this we fitted a random Forest algorithm to predict the outcome of an inspection considering only Pass or Fail as a result. We can see that we obtain a very high accuracy(92%). We then used our algorithm to do feature importance and looked at which vioaltions gives the higher risk to fail an exam and have found some differences with the result proposed by the Chicago Department of Public Health’s Food Protection for which violations are considered more dangerous.

Secondly we wanted to look to forecast the percentage of fail exams in each month for the year 2020. To do so, we created a time series containing the percentage of failed exam in each month and looked at the trend and seasonality of the dataset. We then decided to fit a seasonal exponential smoothing algorithm that fitted well our data and used it to forecast the percentage of failed exam in the next year.

### NLP Insigth:


We further explored the comments in the violations to see what new information we could get about failed inspections and which words are the most significant in this context. Moreover, we begin to highlight geographical dependencies among these comments through several plots.

### Updating Yelp Dataset:

We were able to complete the matching and scrapping of all establishments. We found 12'100 unique establishments out of 32'374 total unique entries, or about 37%. With a complete dataset, we combined both sources and focused particularly on the price, rating, and review count features. Our analysis shows that restaurants in the $30 or more range have an average score difference of 0.4 between those passing or failing the latest inspection. We also tried fitting logistic models without much success. 


Example
Edouard : Cleaning Data, Exploratory data analysis and plotting Heatmaps;
Rayan : Data Cleaning, feature importance and NLP insight for violations;
Marc : Creating Choropleth maps, Classification and time series forecasting;
Eve: : Web-scrapping, cleaning Yelp Dataset and predictions through Yelp;

## Previous Milestone 

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

