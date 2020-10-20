# 

## Background

The restrictions put in place to limit the diffusion and impacts of Covid-19 have had a widespread impact on people’s lives, and the way energy is used across entire economies.

One of the biggest impacts has been the reduction in passenger transport demand, due to a combination of government lockdowns and fears of contracting and spreading the virus when using mass transport modes. Therefore, a key question for the energy sector is whether changes to transport behaviours during the crisis may result in a permanent change in behaviour (and transport energy use) or if transport patterns will revert to ‘business as usual’ when the crisis ends. 

If and when demand for passenger transport returns to pre-crisis levels will depend on a range of factors including perception of risk, cost, convenience, and the availability of alternative transport modes, all of which affect people’s mobility decisions.


## Objectives

- Determine what factors may contribute to the change in bike path usage
- Determine the significance of each factor, especially COVID-19, in changing the bike path usage in Madison
- Develop a model to predict bicycle path usage in the near future


## Data sources

The data used for this analysis are collected from public online sources.<br>

- [Weather1](https://www.wunderground.com/history/daily/us/wi/madison/KMSN/date/2017-7-5)
- [Weather2](https://www.ncdc.noaa.gov/cdo-web/confirmation)
- [Covid cases](https://cityofmadison.maps.arcgis.com/apps/opsdashboard/index.html#/e22f5ba4f1f94e0bb0b9529dc82db6a3)

## Exploratory data analysis

> Week 10/12 (Haoming)

We first plot the distribution of target variable bike users count with histogram, probability plot, and box plot.



<img src = "images/correlation_with_count.png" width = 400>

<img src = "images/heatmap.png" width = 400>

## Preliminary Data Modeling



> Week 10/19 (Haoming)

After plotting the heatmap between numerical variables and the target variable (Count), we started to build simple linear regression to check if there is a linear relationship between each numerical variable and Count. The red lines in the scatter plots represent a simple linear regression fit. We can see both wind speed and gust follow a linear model, but have some outliers we may want to look into. For instance, there are multiple days with less than 20 new cases but have suspiciously high user counts, which is around 6000. We can see similar behavior in temp and dew both follow more of a quadratic fit. 

<img src = "images/Simple_lr_num.png">


Then I took the difference between prediction and the true value to examine the distribution of errors. It turns out that the error tends to have smaller variance when the windspeed and gust have a larger value. It implies that the prediction will be more stable when the input value of windspeed and gust are large. The error of temp and dew are not evenly distributed around the horizontal line, especially when the temp and dew have a small value. that is because the a linear relationship cannot capture the 

<img src = "images/Simple_lr_diff.png">

### Multiple Linear Regression

> Week 10/18 (Ian)

Having determined the factors that contribute to bicycle usage in Madison, a model can start to be developed. Figure 4 shows a comparison between the actual bike usage data in 2019 and the predicted results using a multiple regression model.

<img src = "images/Rough model 2019.png">
<em>Figure 4. Comparison between actual bike usage data from 2019 and the predicted values using a multiple regression model.<em>


Tested in this dataset, this model has a coefficient of determination or R^2 score of 0.78. This is not a very accurate model since some predicted values are off by a margin and can even be negative values, but it does a decent job of predicting and capturing the pattern in the dataset.

### Tree based Model
> Week 10/19 (Haoming)

We then tried a different approach to make the prediction and we will compare the performance of tree-based models against linear regression later. I only show the first three layers of the decision tree simply because the plot of a deeper tree cannot fit into the screen. It can be seen that the temp variable is used as the primary splitting criterion in the first layer and is also used multiple times in the following layer, which indicates the importance of temp in separating the target variable.  

<img src = "images/tree.png" width = 800>


Although the correlations are giving a good overview of the most important numeric variables and multicollinearity among those variables, I wanted to get an overview of the most important variables including the categorical variables.

The feature importance is calculated by its total contribution in reducing the impurity. In the context of the regression problem, the impurity is measured by the Mean Square Error within a node. The result of the tree-based model is almost consistent with the result of multiple linear regression, where weather information plays a dominant role in making prediction and information involves covid-19 are less determinant in both models. 

<img src = "images/feature_im_dt.png" width = 500>



