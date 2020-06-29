# Conflict Model
### Primary Modeler: Yared Hurisa
### Jira Epic: MOD-133

## Overview

Violent conflicts between non-state actors are pervasive in East African countries such as South Sudan and Ethiopia. This is manifested through conflict among groups with different ethnic, religious, and other identities heightened by-elections and the implementation of controversial land tenure policies, federalism,  and the unintended effects of public and private investments.  As a result, millions of people have been displaced due to unrest on a continuous basis.

Appropriate early-warning systems that can meaningfully predict the onset of communal conflict is important to respond to the crises in a timely manner. This will have a significant impact on reducing the devastating consequence of conflict in terms of loss of lives, livelihoods, and infrastructure.

The ACLED project tracks conflict events on a real-time basis and identifies communal conflicts as armed and violent events happening among groups in different communities, ethnicity, region, religion, or livelihood. Our modeling work involves the use of communal conflicts as an outcome variable extracted from the ACLED dataset. Communal conflicts are characterized by brief and sporadic events as compared to state-based conflicts that span long duration. Out model forecast communal conflicts in East African countries at the admin2 level as well as one year ahead of time and on a monthly basis.

### Outputs

Forecasted monthly values of communal conflict at admin2 level


### Inputs

Political: Political parties and movements, voting, assassinations, protests, martial law, etc.

Military: Deployments, invasions, border skirmishes, training exercises

Economic: Poverty, trade changes, CPI, PPI, real household income, etc.

Social: Racial, demographics, linguistic, tribes, other cultural boundaries, social movements, disease, etc.

Information: Propaganda prevalence, internet, and cellular penetration, education levels

Infrastructure: Cities/towns/population centers, roads, railroads, and ports

Physical Environment: Land use/land cover, Seasons/climates, temperature, weather

## Methodology

We evaluated different forms of time-series and tree-based algorithms that include Classical Random forests, Logistic regression (classifier), as well as Recurrent Neural Networks (RNNs). We find that autoencoder, a type of RNNs perform better than the other type of classifiers considered for this problem. 

### Autoencoder 

Autoencoder classification performs similar to anomaly detection where anything that doesn't follow the normal pattern is classified as an anomaly. Communal conflict is a type of event that rarely happens compared to the peaceful months and years in a particular place. This makes the algorithm suitable to solve the conflict classification problem.  