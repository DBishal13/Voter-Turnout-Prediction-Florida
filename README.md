# Predictive Modeling of Voter Turnout (2016) Distribution at Census Tract Level for Florida Using Forest-Based Classification and Regression

## Introduction

Voting is voluntary in the United States; voter turnout or participation levels play a significant role in election results, ultimately defining public policy. Voter turnout is a critical aspect of democratic elections, as it directly influences the legitimacy and representativeness of the electoral process. In the United States, voter turnout has been a concern for many years, with many states struggling to achieve high levels of participation among eligible voters. Florida is one state where voter turnout has been relatively low recently, with only around 61% of eligible voters participating in the 2020 presidential election (US Census Bureau). Modeling and understanding the prevalence of voter turnout at a granular census level, such as tracts, helps to perform outreach efforts to increase voter participation.

The science of geospatial data uses prediction extensively. It can downscale information (e.g., utilizing air quality data at the state level to predict that at the neighborhood level) or fill in missing values in a dataset using prediction or anticipating future values (e.g., projecting tomorrow's air quality for a specific place). In this report, I have used the Forest-based Classification and Regression tool in ArcGIS Pro to predict voter turnout at the US census tract level using data from the 2016 election at the county level. Using different data engineering and visualization techniques, I have calculated and prepared the map showing the distribution of the predictive surface. 

## Literature Review

Voter turnout prediction is an essential area of research in political science and data analytics. Researchers have recently turned to machine learning algorithms, such as random forests, to predict voter turnout at individual and aggregate levels. Alvarez (2016) provides a comprehensive overview of computational social science and its potential to advance our understanding of social phenomena. The article highlights the importance of interdisciplinary collaboration and the need for rigorous standards and ethical guidelines to ensure the responsible use of computational methods in social science research.

Rusch et al. (2012) explained how campaigns spend a significant portion of their budget on mobilizing voters by identifying and influencing as many potential voters as possible. They use statistical tools based on data to determine whom to target. A current framework called LORET (logistic regression trees) incorporates trees containing logistic regressions in every leaf, allowing for a combination of logistic regression and classification trees. This framework is more advanced than traditional techniques and can provide a more comprehensive approach to voter targeting.

Kim et al. (2020) applied fuzzy forests, a machine learning algorithm, to investigate the demographic and socioeconomic characteristics of voters who turned out to vote in the 2016 US presidential election. The authors identified age, education, income, and party affiliation as significant predictors of voter turnout. The findings highlight the importance of understanding the factors that drive voter behavior and can assist policymakers and campaigns in designing more effective voter outreach strategies.

The "Forest-based Classification and Regression" tool allows the creation of random forest and gradient-boosted tree models for classification and regression problems. The tool requires a training dataset with input features, the target variable, and a validation dataset for evaluating the model's performance. Various parameters for the model can be specified, such as the number of trees in the forest, the maximum depth of the trees, and the number of input features to consider at each split. Once trained, the model's performance can be evaluated using metrics like accuracy, kappa, and root mean squared error (RMSE). The tool can then be applied to new data using the "Apply Model" tool, which generates predictions for the target variable based on the input features.

Overall, the literature suggests that forest-based classification and regression can be a practical approach for predicting voter turnout at various levels of aggregation. Further research is needed to explore the potential of this approach for predicting voter turnout at the census tract level, particularly in the context of Florida. Accurate knowledge of voter turnout can help campaigns allocate resources effectively and target individuals more likely to vote. Moreover, campaigns can use this information to craft persuasive messages that motivate voters to participate in elections.

## Objectives

The primary objective of this project is to identify the factors that are most predictive of voter turnout in Florida and to assess their relative importance at the census tract level by predicting the voter turnout at that level. The following are the main objectives of this study:
1. To extract, enrich, edit, and explore data using data engineering and visualization techniques.
2. To develop an accurate predictive model of voter turnout at the census tract level in Florida using forest-based classification and regression by identifying the most significant predictors of voter turnout in Florida, USA.
3. To provide insights for political campaigns and policymakers on allocating resources and targeting voters more effectively to increase voter turnout in Florida.

## Data and Data Sources

I have used the USA census data from the US Census Bureau for this study. Using geo-enrichment and geocoding in the ArcGIS Pro data engineering tools, it was possible to add demographic data, such as median age, education level, household income, diversity index, etc., to the census data in 2016. I calculated the distance variable feature using county population data to calculate the distance from the major cities. The primary data sources are listed below:
1. [Esri Data Resources](https://www.esri.com/en-us/arcgis/products/data/resources)
2. [US Census Voting and Registration Data](https://www.census.gov/data/tables/time-series/demo/voting-and-registration/p20-580.html)

## Methodology

### 1. Study Area

Florida is suitable for studying predictive modeling of voter turnout distribution at the census tract level using forest-based classification and regression due to its diverse population, swing state status, history of close elections, many census tracts, advanced data infrastructure, and expertise in data analysis techniques. This study can provide valuable insights into predicting voter turnout in other parts of the country.

![Study Area](https://github.com/DBishal13/Voter-Turnout-Prediction-Florida/raw/main/Outputs/Study%20Area.jpg)

### 2. Data Preparation, Data Engineering, and Geo-enrichment

First, I downloaded the 2016 election data in .csv format from the US Census Bureau with the help of the Esri database; after using ArcGIS Notebook to integrate, clean, and transform the data, geocoding will be used to add the spatial location to the data.

Geo-enrichment uses the location of the data to add demographic information as attributes to the feature class. First, I set up the geoprocessing environment for the Business Analyst section to add data sources to the United States (Esri 2022) to run the geoprocessing tool in this controlled environment. From the data engineering contextual tab, the Enrich tool in the Integrate group was used to add variables such as Median Age, Average Household Income, Diversity Index, etc.

### 3. Data Exploration and Visualization

Data visualization assists in digesting the information using symbols, representing the data and categories. We can make inferences about the data or attributes about relative proportions, patterns, relationships, and trends. I have used ArcGIS Pro to visualize the data, tables, and charts.

![Distribution of Voter Turnout](https://github.com/DBishal13/Voter-Turnout-Prediction-Florida/raw/main/Outputs/Distribution_of_voter_turnout.jpg)

The bar chart summarizes the voter turnout values by county. Each bar represents a county, and the height corresponds to the mean turnout value as follows:

![Bar Chart of Voter Turnout Mean](https://github.com/DBishal13/Voter-Turnout-Prediction-Florida/raw/main/Outputs/BarchartVoterTurnoutMean.jpg)

We can use a scatter plot matrix to explore the variable relationships for the variables that define the voter turnout values. As we intend to predict voter turnout, we must examine the relationships between voter turnout and other variables in our data. Based on the importance of Pearson's R or R2, we can see the relationship between them. For instance, voter turnout vs. 2019 Per Capita income has an R2 value of 0.66, meaning they have a positive relationship.

![Scatter Plot](https://github.com/DBishal13/Voter-Turnout-Prediction-Florida/raw/main/Outputs/ScatterPlot.jpg)
We can also use the Local Bivariate Relationship Tool in ArcGIS Pro to show how the relationship types vary spatially in the given study area. The following map shows the bivariate relationship between voter turnout and 2019 per capita income. We can see that these two have a positive linear relationship for northern Florida; however, they have a concave relationship for southern regions.

![Voter Turnout vs Per Capita Income](https://github.com/DBishal13/Voter-Turnout-Prediction-Florida/raw/main/Outputs/VoterTurnoutVsPerCapIncome.jpg)

### 4. Creation of a Prediction Model

ArcGIS provides a geoprocessing tool under the Spatial Statistics Toolset that can handle a large dataset, such as census data, using a modified version of Leo Breiman and Adele Cutler's supervised machine learning technique, the random forest algorithm to build models and make predictions. Both continuous variables (regression) and categorical variables (classification) can be used to make predictions. Raster datasets, distance features used to generate proximity values and fields in the attribute table of the training features can all be used as additional variables for explanations. Predictions can be made to either parts or a prediction raster in addition to assessing model performance based on the training data.

First, I trained the model with only four variables: the 2019 Diversity Index, 2019 Median Age, 2019 Per Capita Income, and 2019 Education: High School/No Diploma: Percent. I obtained the validation R2 value of 0.69. The following box plot shows the distribution of variable importance.

![Distribution of Variable Importance - Train](https://github.com/DBishal13/Voter-Turnout-Prediction-Florida/raw/main/Outputs/DistributionofVariableImportance_Train.jpg)

### 5. Calculation of Distance Variables and Use in the Model

This aims to incorporate each county's urban and rural characteristics into the model to determine whether these variables improve voter turnout predictions. For this, I calculated the distance between each county and cities of various sizes. It assumes that rural counties are farther from the cities. Based on the city's population, Cities 1 has the lowest population, and Cities 4 has the highest population.

![Distance Variables](https://github.com/DBishal13/Voter-Turnout-Prediction-Florida/raw/main/Outputs/Distance_Variables.jpg)

After adding the distance variables to the model and many other variables, the validation R2 value increases to 0.72, meaning that the model predicted about 72 percent accuracy based on validation data. The following box plot shows the importance of these additional variables along with the previous four.

![Summary of Variable Importance - Train Only](https://github.com/DBishal13/Voter-Turnout-Prediction-Florida/raw/main/Outputs/SummaryofVariableImportanceTrainOnly.jpg)

### 6. Refine the Model

There are various ways to select the variables to include in a model. I tried with 1000 trees to improve the chance that each variable will be used in a decision tree, resulting in more accurate model prediction. In this case, the validation R2 value increased to 0.75. We can see the Model Out of Bag Errors, another diagnostic tool to validate the model. The % of variation explained indicates the percentage of variability in voter turnout that can be described using this model. It shows how much performance is gained by increasing the number of trees in the model. As we can see below, the percentage of variation explained increased from 71.012 to 71.571 when the number of trees increased from 500 to 1000, so it is unnecessary to increase the number.

## Results and Discussion

After training the model using the county data, I used the same model to predict voter turnout at the census tract level. With the values in this much higher resolution, it is easy to understand a more detailed spatial pattern of voter turnout. I changed the prediction type to Predict to Feature and inserted my Tract level demographics. By matching the explanatory variables between the two levels,s, we achieved the final predicted feature that contains predicted voter turnout values for each transfer. 

Looking at the summary variable importance table, we can conclude that 2019 Per Capita Income, 2019 Education: Bachelor's Degree: Percent, 2019 Education: High School/No Diploma: Percent are the top three contributors to the predicted values, whereas 2019 Population Age 70-74: Percent, Buying America is not necessary to me: Percent, Cities7, are the bottom three contributors. I removed the tracts that covered whole conservation areas during the prediction.

If we look at the below-predicted surface map, we can make inferences about the areas that must be focused on during the election. By studying the variable importance and voter turnout values at these tracts, we see that these areas (with blue) contain people with lower educational and economic levels. From the map, we can make inferences about the geographic location of the people who voted in the 2016 election. More coastal residents are likely to appear compared to the more inland populations. The southern middle areas with lower voter turnout value (blue) cover most conservation areas, explaining some reasons for low voter turnout. However, the Census Bureau must focus on inland and rural areas. Also, the northern portion of Florida needs more attention as well. This model not only helps to target the election campaigns but also helps to understand the socio-economic groups that live in those areas. After the election, the leader must focus on those areas to analyze the socio-economic groups and make policies to help improve their socio-economic status.

![Out Predicted Map](https://github.com/DBishal13/Voter-Turnout-Prediction-Florida/raw/main/Outputs/OutPredictedMap.jpg)

![Summary of Variable Importance - Final](https://github.com/DBishal13/Voter-Turnout-Prediction-Florida/raw/main/Outputs/SummaryofVariableImportanceFinal.jpg)

![Prediction Interval - Final](https://github.com/DBishal13/Voter-Turnout-Prediction-Florida/raw/main/Outputs/prediction_intervalfinal.jpg)

The prediction interval chart shows that the confidence intervals are much more significant for low and high voter turnout values. This indicates that the model could better predict high voter turnout than low turnout values. However, if we are modeling using the more localized model, we could expect more accuracy.

## References

1. Kim, Seo-young Silvia, R. Michael Alvarez, and Christina M. Ramirez. 2020. “Who Voted in 2016? Using Fuzzy Forests to Understand Voter Turnout.” APSA Preprints. doi: 10.33774/apsa-2020-xzx29.
2. Rusch, T., Lee, I., Hornik, K., Jank, W., & Zeileis, A. (2012). Influencing Elections with Statistics: Targeting Voters with Logistic Regression Trees. WU Vienna University of Economics and Business. Research Report Series / Department of Statistics and Mathematics No. 117
3. Alvarez, R. M. (2016). Computational social science: Discovery and prediction. Cambridge University.
4. ArcGIS documentation
5. [Esri Data Resources](https://www.esri.com/en-us/arcgis/products/data/resources)
6. [US Census Voting and Registration Data](https://www.census.gov/data/tables/time-series/demo/voting-and-registration/p20-580.html)
7. [Forest-based Classification and Regression Tool](https://pro.arcgis.com/en/pro-app/latest/tool-reference/spatial-statistics/forestbasedclassificationregression.htm)
8. [How Forest-Based Classification and Regression Works](https://pro.arcgis.com/en/pro-app/latest/tool-reference/spatial-statistics/how-forest-works.htm#ESRI_SECTION1_1B54DEFD180C404D844EAB95DD5B2FA)
