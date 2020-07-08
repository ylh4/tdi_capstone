# Conflict Model: Forecasting the onset of Communal Conflict in the Horn of Africa
### Modeler: Yared Hurisa

## Introduction
### Overview

The goal of the Conflict model is to allow users to predict the onset of communal conflict (`cc_conflict`) at the sub-national level on a monthly basis. Conflict in this case can be defined as “identity conflict” which could be among religious groups, tribal/regional areas, communal and country specific areas at the local level. The model delivers to users a binary indicator of whether conflict is expected to be present in a geographic area. Upon completion, this model will allow users to see and predict the the presence of the conflict in space and a head of time. 

### Rationale

Communal conflicts are pervasive in East African countries such as South Sudan and Ethiopia due to a range of issues. These include the conflict that occur among groups with different ethnicity, religion, region, or livelihood backgrounds. The type of conflict is typically heightened by-elections, the implementation of controversial land tenure policies, federalism,  state use of force, and the unintended effects of public and private investments in the horn of Africa.  As a result, millions of people have been displaced and died in addition to the immeasurable economic losses incurred due to the conflict.

Appropriate early-warning systems that can meaningfully predict the onset of communal conflict is important to respond to the crisis ahead of time. This will have a significant impact on reducing the devastating consequence of conflict in terms of loss of lives, livelihoods, and infrastructure.

#### Outputs
The modeling work involves the use of `cc_conflict` as an outcome variable extracted from the ACLED dataset. The ACLED project tracks conflict events on a real-time basis and identifies communal conflicts as armed and violent events happening among groups in different communities, ethnicity, region, religion, or livelihood. Communal conflicts are characterized by brief and sporadic events as compared to state-based conflicts that span long duration. Our model forecasts communal conflicts in East African countries at the admin2 level as well as one year ahead of time and on a monthly basis.

More specifically, communal conflict (cc_onset) is a binary output variable representing 1, the presence of conflict; 0, otherwise. Communal conflict is defined as a conflict event occurring between identity militias (code 04), with the rest of actors in the ACLED dataset (government forces, civilience, protesters, or other identity groups).

#### Inputs
###### Political and Military
###### `actor_protesters`: 
Interaction of identity groups with protesters
###### `actor _rioters`: 
Interaction of identity groups with rioters
###### `actor_political_militias`: 
Interaction of identity groups with political militias
###### `actor_identity_militias`: 
Interaction identity groups with identity militias
###### `actor_civilians`: 
Interaction identity groups with civilians
###### `actor_others`: 
Interaction identity groups with others
###### `actor_state`: 
Interaction identity groups with government 
##### Economic
###### poverty: 
`poverty_index`
###### `cpi`: 
Commodity Price Index
###### `wheat_price`: 
Average price of wheat per kg
###### `maize_price`: 
Average price of maize per kg
###### `sorghum_price`: 
Average price of sorghum per kg
###### `education`: 
Percent of literate
###### `food_sc`: 
FEWSNET food security classification 
##### Social
###### `ethnic_boundary_km`: 
Distance to the nearest ethinic boundary in km
###### religion_group_islam: 
Percent of Islam in the population
###### `religion_group_christianity`: 
Percent of christianity in the population
###### `religion_group_catholic`: 
Percent of catholic in the population
###### `religion_group_other`: 
Percent of other religious groups in the population
###### `ethnic_group_1`: 
Percent of the largest ethnic group in the population
###### `ethnic_group_2`: 
Percent of the second largest ethnic group in the population
###### `ethnic_other`: 
Percent of the all other ethnic groups in the population
###### `youth`: 
Proportion of youth population
##### `Information`
###### mobile: 
share of population who use mobile phone
###### `internet`: 
share of population who use internet
###### radio: 
share of population who have access to radio broadcast
###### `television`: 
share of population who have access to tv broadcast
##### Infrastructure
###### `road_density`: 
Road length per area (admin2) in km2
###### `health_facility_access_km`: 
Number of health facilities per area (admin2)
###### `urbanization`: 
Proportion of urban population
##### Physical Environment
###### Land-use classification: 
Area under `crop/farm` land, `Urban`, `Rangeland`,`Forest` land, `Wetlands`, `Barren`
###### Climate: 
Mean `rainfall` (mm), `Temperature` (degrees celsius), `Ndvi` 

## Methodology
So far, I evaluated different forms of time-series and tree-based algorithms. These include classical random forests, logistic regression (classifier), mixed effect random forests, as well as Recurrent Neural Networks (RNNs). I FOUND that LSTM autoencoder, a type of RNNs, perform better than the other types of classifiers considered for this problem.
### LSTM Autoencoder
Autoencoder classification performs similar to anomaly detection where anything that doesn't follow the normal pattern is classified as an anomaly. Communal conflict is a type of event that rarely happens compared to the peaceful months and years in a particular place. This makes the algorithm suitable to solve the conflict classification problem.

Autoencoders are a special form of a neural network as they attempt to generate output using a reconstruction of the input they receive which gives them an advantage in the classification of rare events such as conflict events. Using an autoencoder two steps. First, we feed our input data into the autoencoder and tune it until it is well trained to reconstruct itself as an output with minimum error. Next, we calculate the mean square error that measures how far is the reconstructed data point from the actual data points. The second step is basically identifying the outliers from the mean squared error figures that represent anomaly (conflict) from the general trend (peace). This is done by codding 1 when the mean squared error surpasses a certain threshold, 0 otherwise. 
LSTM autoencoder is an improved version autoencoder designed to incorporate the temporal features in the data. The algorithm is capable of extracting effects of past events in the form of both long- and short-term effects. 

LSTM requires creating 3-dimensional arrays from the temporal data of monthly communal conflict event dataset. As we intend to predict conflict up to one year ahead of time (as well as on a monthly basis), we shift (create a lagged input dataset) up 12 times and merge the datasets together. This enable the classifier to monthly forecast for the coming one year.

