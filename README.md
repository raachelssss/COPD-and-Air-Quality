# Predictive Analysis of COPD and Air Quality

#### Disclaimer:
Jupyter Notebook uploaded in this repo may occasionally show **render failure** due to github issues. If it happens, please refer to the link below to access Jupyter Notebook via nbviewer.
[**Link to Jupyter Notebook**](https://nbviewer.org/github/raachelssss/COPD-and-Air-Quality/blob/main/COPD_and_Low_Air_Quality.ipynb)

### Introduction
- This project aims to predict the onset of Chronic Obstructive Pulmonary Disease (COPD) by **analyzing risk factors that disproportionately affect underserved populations.** Key features include:
  - **Air Quality**: Research shows that poor air quality significantly increases the risk of COPD, with underserved communities often facing higher exposure.
  - **Race**: Data indicates that people of color are more likely to live in areas with poorer air quality [(Link to Article)](https://www.nytimes.com/2021/04/28/climate/air-pollution-minorities.html)
  - **Smoking**: Research suggests that smoking population is at more risk than non-smoking population
- ML/AI Techniques Used:
  - Causal Inference (Outcome Regression, Inverse Propensity Weighting)
  - Random Forest Model
  - Frequentist & Bayesian General Linear Model (GLM) 

**By exploring these variables, this project seeks to contribute insights that could inform targeted interventions, particularly for those facing health inequities and limited access to quality care.**

### EDA:

#### Data Overview: 
- U.S. Chronic Disease Indicators: Chronic Obstructive Pulmonary Disease
- CDC: Daily Census-Tract PM 2.5 Concentration (allows checking of air pollution levels)
- CDC: Daily Census-Tract Ozone Concentrations
- State-level Population Density (2010-2019)
- County-level Smoking Prevalence Census
#### Data Visualization: 
- Relationship between smoking population and COPD incidence
- Comparing smoking population by race and gender with COPD patients
<img width="806" alt="image" src="https://github.com/raachelssss/COPD-and-Air-Quality/assets/88609253/e6879d82-ab26-4311-a97a-15f9ae3ce919">

- Comparing Ozone ppb, PM 2.5 Concentration, and COPD Prevalence Rate by state using Geo Maps
    - It was observed that COPD prevalence rate distributions differ by gender and race.
<img width="826" alt="image" src="https://github.com/raachelssss/COPD-and-Air-Quality/assets/88609253/e8694bc4-39de-4c5f-9763-975f0bd82642">

- Is there a difference in air pollution between areas with predominantly minority populations and areas with predominantly White populations?
    - It was observed that areas with predominantly White populations have relatively lower air pollution compared to areas with predominantly minority populations.
<img width="829" alt="image" src="https://github.com/raachelssss/COPD-and-Air-Quality/assets/88609253/382fb0d2-4645-48fb-bbb8-6c74a65a0f1d">



### Research Question 1: Does air pollution cause COPD (chronic obstructive pulmonary disease)?
- Causal inference was used to verify the existence of causality.
  
**Outcome Regression:**
-   Fit a linear model of the following form:
<img width="869" alt="image" src="https://github.com/raachelssss/COPD-and-Air-Quality/assets/88609253/808c3628-d374-466f-ac25-59c82647a7f3">

- Confidence Interval at 5% Significance Level = [-0.661, 1.067]
- Due to its proximity to zero, the Outcome Regression could not establish a causal relationship.
- We assumed unconfoundedness that there are only 6 confounding variables that cause both treatment and outcome. There might be missing confounders not taken care of by the data and the model which lead us to this decision. Also, it is not clear that confounding variables would all have a linear effect on the prevalence of COPD. This leads us to an uncertainty that our linear model does not model any interactions between the variables.

  
**Inverse Propensity Weighting:**
- Propensity Score: P(State has a bad air quality | confounding variables) using logistic regression
- <img width="529" alt="image" src="https://github.com/raachelssss/COPD-and-Air-Quality/assets/88609253/27b28bd7-ffd5-47b7-9f13-5822373a9d41">
<img width="546" alt="image" src="https://github.com/raachelssss/COPD-and-Air-Quality/assets/88609253/c5c29616-e04b-439a-97b2-1576e4a133a5">

  - IPW demonstrates the causal relationship between poor air quality and the onset of COPD under two assumptions:
  - 1) age-adjusted prevalence of COPD among adults is unconfounded given the variables
  - 2) propensity score is a good model of the probability of states that has a bad air quality given the listed confounding variables
  - IPW estimate means that **poor air quality causes people to have a 6.83% more prevalence** of being diagnosed with COPD than people who reside in good air quality.

    

### Research Question 2: Can we predict COPD occurrence based on a person's residential area?
As the causal relationship between air pollution and COPD could not be verified, the research direction was shifted to investigate whether COPD occurrence can be predicted based on residential area and race information.

Firstly, Bayesian GLM and Frequentist GLM models were adopted and trained.


**Bayesian GLM:**
- <img width="853" alt="image" src="https://github.com/raachelssss/COPD-and-Air-Quality/assets/88609253/3bac208d-655a-44e3-a50d-86698bc13c9b">
- The Bayesian GLM model shows a possibility of overfitting.
- Hispanic individuals have the lowest probability of COPD compared to Multiracial individuals.
- The population living at a lower latitude and higher longitude may be more vulnerable to COPD.


**Frequentist GLM:**
- <img width="842" alt="image" src="https://github.com/raachelssss/COPD-and-Air-Quality/assets/88609253/d728b791-cd4f-488b-8f4e-218bf79d8187">
- Hispanic, Multiracial, and White variables have p-values smaller than 0.05, indicating statistical significance.
- However, considering the high Pearson chi-squared value, the model may not fit the data well.

GLM has several inherent limitations. Firstly, it does not select features to incorporate into its model, but instead uses all the features provided. Taking all the features provided might be the reason why our model overfit to the data. Moreover, it has strict assumptions about the distributions’ shapes. Finally, it is sensitive to outliers and have lower predictive power than nonparametric models. 
We then chose the random forest model because it is less prone to overfitting compared to logistic regression GLMs because random forest consists of many classifiers that are independently trained on different subsets of the training data. Random forest, as an ensemble model that uses feature bagging, is less likely to overfit because it has low variance. 

**Random Forest Model:**
- <img width="858" alt="image" src="https://github.com/raachelssss/COPD-and-Air-Quality/assets/88609253/b5b0a363-06cb-436f-b9a9-749a11d64cc3">
- <img width="859" alt="image" src="https://github.com/raachelssss/COPD-and-Air-Quality/assets/88609253/9e48c01c-a263-4538-9261-483d3f70c846">

- The Feature Importance of variables indicating race is very low compared to latitude and longitude, suggesting that predicting COPD occurrence solely based on population demographics is challenging.
- It is regrettable that the performance of the model did not improve significantly even if different variables were adopted instead of race.
- The model showed an accuracy of around 98% on the train set and 82% on the test
  - **Limitation:**
    - One major limitation of random forest is that it cannot extrapolate. In other words, its prediction is only a mean of formerly observed labels. For instance, as shown in our EDA, the prevalence of COPD shows a yearly increasing trend up until 2017, and gradually decreases in the following years. Since the model cannot extrapolate, if the training data is missing year data, the model will likely under-predict or over-predict. For instance, New Jersey's COPD data is missing for 2019, when the overall state's COPD prevalence was decreasing. Likely, our model could not make accurate predictions in cases like this.

### Conclusion
- **Causal Inference:**
  - identified the causal effect of air quality on the prevalence of COPD, although the relationship is relevant to 2011 (our dataset) 
- **Predictive Analysis:**
  - Results from the Bayesian model suggest that it can predict that multiracial individuals are most likely to have COPD, given the same location. It also can be predict that the hispanic individuals are least likely to have COPD compared to multiracial individuals. 
  - Key finding we were able to identify using Random Forest was that we can predict whether people have COPD by using longitude and latitude data. As suggested by feature importance, we could not predict whether people have COPD by using racial features. They had little to no feature importance, which means that geographical data alone suffice to predict COPD. This also means that excluding racial features will have little to no impact on the accuracy of the model.
 
### Discussion: Rooms for Improvement, Implications for Public Health & Society: 
- **Poor air quality causes COPD. Now what?**
  - The states with bad air quality can improve their legislation that regulates air pollutants generated by transportation, and manufacturers, or place more air filtering technologies to control air pollutants generated from wildfires. So that individuals could be less exposed to ozone and  pm 2.5 concentration which also decreases the prevalence of COPD.
- **We can predict the onset of COPD using geographical location. Now what?**
  - Based on random forest results, we have identified that we can predict the onset of COPD from geographical location. Hence, medical institutions and the federal government could further investigate geographical attributes of different locations to predict areas that are most likely to be prone to COPD. Through prediction, they can plan medical interventions in these areas, such as periodic diagnostic assessment, recommendation of clinic visit, symptom checks, and more. 


#### Want to learn more about the background of the story, how and why we chose these models, and more? Check out the Written Final Report below!


### 🛠️ Link to Final Report 
[Written Report](https://drive.google.com/file/d/1BsE3aeGkDo0m1LDiIxZam5Y_y11_iBsZ/view?usp=sharing)
