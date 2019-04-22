# Chocolate Bar Rating Model

I built a model which predicts the expected user rating of a chocolate bar given some independent variables. Theses independent variables were provided by the data source as properties of chocolates such as flavor, complexity, bitterness, etc. 

Using multiple linear regressions, a model was created with an R^2 value of 0.878, a mean squared error(MSE) of 0.160 and a root mean squared error(RMSE) of 0.400.

# Getting Data
You can find the webscrapping code in the jupyter notebook file titled "c-spot.ipynb" through the data/get_data/ pathways. The notebook walks through scrapping the website to get the information of individual chocolate bars: <br>
- Chocolate bar name (choco_bar_name)
- Chocolate bar maker (company_name)
- User rating of chocolate bar (rating)
- Company location (company_loc)
- Percentage of cocoa (cocoa_perc)
- Type of cocoa used (bean_type)
- Origin of cocoa beans used (bean_origin)
- Company intended flavor (company_flavor)
- CQ (CQ)
- Sweetness (sweetness)
- Acidity (acidity)
- Bitterness (bitterness)
- Roast (roast)
- Intensity (intensity)
- Complexity (complexity)
- Structure (structure)
- Length (length)
- Appearance (appearance)
- Aroma (aroma)
- Mouthfeel (mouthfeel)
- Flavor (flavor)
- Quality (quality)

A less descriptive dataset can be found on kaggle. This is already downloaded and was titled "flavors_of_cacao.csv" through the same pathway.

# Cleaning Data
The Data cleaning code with some description of a step by step cleaning process can be found in the jupyter notebook file titled "cocoa_clean.ipynb" through the data/ pathway.

- First portion the data with only the continuous variables. 
- Check if the datapoints make sense. The scoring system is from 0 to 100. Remove any dastapoints that go beyond that range.
- Explore possibility of replacing Nan values with the mean or meadian. 
- Replacing would only make the skewing and kurtosis worse and thus resulted into dropping all indexes with any Nan values leaving us with 1368 datapoints.

# Model in its Current State
(The code for the following sections will be located in the "Feature Engineering.ipynb" jupyter notebook file until noted.)<br>
Without changing anything, I received an R^2 of 0.846 and an adj. R^2 of 0.845 through the OLS method.
![UNADJUSTEDNONRAW_thumb_68](https://user-images.githubusercontent.com/45129935/56487316-c4c46780-64a8-11e9-89ec-15eaebf6a592.jpg)

  
## Multicollinearity
![Image 4-22-19 at 1 00 AM](https://user-images.githubusercontent.com/45129935/56487348-e887ad80-64a8-11e9-9337-3d400d6edf2b.jpg)

The variables flavor and quality are the only variables that have high correlational value. This indicates a possible multicollinearity. However, both flavor and quality are both also highly correlated with the target variable, rating. Thus, I will keep both variables.

## Interactions
Variables like flavor and aroma were found to have the most influence. Thus, they were split into their own respective categories to check for interactions between other variables such as aroma and structure, aroma and CQ, and aroma and mouthfeel.<br>
![Image 4-22-19 at 1 01 AM](https://user-images.githubusercontent.com/45129935/56487366-f3dad900-64a8-11e9-95f8-25bbc351f51b.jpg) <br>
When the aroma score is low, having a balanced mouthfeel score produces the highest ratings however, after around an aroma 
![Image 4-22-19 at 1 01 AM (1)](https://user-images.githubusercontent.com/45129935/56487369-f63d3300-64a8-11e9-8e61-2da5310c32ba.jpg) <br>
The lines look additive, there is no interaction here. <br>
![Image 4-22-19 at 1 02 AM](https://user-images.githubusercontent.com/45129935/56487371-f89f8d00-64a8-11e9-9689-3e2120046f73.jpg) <br>
It migth be slight, but there is an interaction here. The lines are not additive and we can say that the rating score is more affected by a structure score with a high aroma score.<br>
  
Thus, I decided to included the two interactions above along with two others: flavor/length and flavor/complexity as they both showed an interaction.

## Normality
![Image 4-22-19 at 2 06 AM](https://user-images.githubusercontent.com/45129935/56487459-4caa7180-64a9-11e9-9a28-cce64ae1510c.jpg) <br>
Here we try to find the variables that are heteroscedastic. We see that many variables are heteroscedastic which would violate our assumptions for a linear regression. Thus we employ transforming features such as the log function in order to achieve homoscesdasticity. <br>
  
Our model after all the addition of interactions and variable transformation looks like this now, with an OLS R^2 of 0.872.<br>
![Image 4-22-19 at 2 08 AM](https://user-images.githubusercontent.com/45129935/56487460-4ddb9e80-64a9-11e9-963b-94e8e2ae6329.jpg)

  
# Final Model
(The code for this last portion can be found in the "cocoa_pred.ipynb" jupyter notebook.)
Finally, to get to our last model, we drop all the values with a p-value less than 0.05. The final model has an R^2 of 0.881. <br>
![Image 4-22-19 at 2 17 AM](https://user-images.githubusercontent.com/45129935/56487530-80859700-64a9-11e9-9f90-2276b4bc6d63.jpg)

## Seeing how it Performs
The model performs as such that the mean squared error(MSE) is 0.157 and the root mena squared error(RMSE) is 0.397. This graph shows the predicted user rating given independent parameters, plotted against the actual ratings that the user gave to the chocolate bar. <br>
![Image 4-22-19 at 2 17 AM (1)](https://user-images.githubusercontent.com/45129935/56487539-8d09ef80-64a9-11e9-8865-74e16eb615e0.jpg) <br>

Similarly, it performed in the same manner when tested on the test data with a mean squared error(MSE) is 0.157 and the root mena squared error(RMSE) is 0.397. <br>
![Image 4-22-19 at 2 18 AM](https://user-images.githubusercontent.com/45129935/56487558-9c893880-64a9-11e9-96be-60444f5a371e.jpg)

  
## Interpretation
- An increase of 1 score in CQ leads to a score increase of 0.0029 in rating.
- An increase of 1 score in acidity leads to a score increase of 0.0016 in rating.
- An increase of 1 score in complexity leads to a score decrease of 0.0395 in rating.
- An increase of 1 score in structure leads to a score decrease of 0.0128 in rating.
- An increase of 1 score in length leads to a score decrease of 0.0330 in rating.
- An increase of 1 score in appearance leads to a score increase of 0.006 in rating.
- An increase of 1 score in quality leads to a score increase of 0.0193 in rating.
- An increase of 1 score in structure, given that the aroma score is high leads to a score increase of 0.0002 in rating.
- An increase of 1 score in mouthfeel, given that the aroma score is high leads to a score increase of 0.0002 in rating.
- An increase of 1 score in length, given that the flavor score is high leads to a score increase of 0.0002 in rating.
- An increase of 1 score in complexity, given that the flavor score is high leads to a score increase of 0.0002 in rating.





















