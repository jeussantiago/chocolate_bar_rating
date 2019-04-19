# Chocolate Bar Rating Model

I built a model which predicts the expected user rating of a chocolate bar given some independent variables. Theses independent variables were provided by the data source as properties of chocolates such as flavor, complexity, bitterness, etc. 

Using multiple linear regressions, a model was created with an R^2 value of 0.889, a mean squared error(MSE) of 0.146 and a root mean squared error(RMSE) of 0.383.

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

kaggle dataset
very little null values, those were dropped - still had empty strings though, so why?
numbers were changed to numbers
Many bean types contained the correct information but didn't have it in the correct format, had to edit that

c-spot dataset
I first made sure there were resonable datapoints. As the scoring system for the website was out of 100, I began by removing any datapoints which had results greater than 100. 
The dataset was clean for the most part, just some null values in the cocoa percentage column. I explored different possibilities to handle it such as replacing it with the median or mode, however, the kurtosis would then increase substantially. As the null values only accounted for around 10% of the dataset, I concluded to simply dropping those null rows.



















