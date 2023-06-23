# Predictive Analysis of COPD and Air Quality

#### Disclaimer:
Jupyter Notebook uploaded in this repo may occasionally show render failure due to github issues. If it happens, please refer to the link below to access Jupyter Notebook via nbviewer.
[Link to Jupyter Notebook](https://nbviewer.org/github/raachelssss/COPD-and-Air-Quality/blob/main/Predictive%20Analysis%20of%20COPD%20and%20Low%20Air%20Quality.ipynb)

### Introduction
- This project aims to predict the onset of Chronic Obstructive Pulmonary Disease (COPD) using the following features:
  - Air Quality: research suggests that poor air quality increases the risk of COPD
  - Race: research suggests that people of color are more exposed to poor air quality [(Link to Article)](https://www.nytimes.com/2021/04/28/climate/air-pollution-minorities.html)
  - Smoking: research suggests that smoking population is at more risk than non-smoking population
- ML/AI Techniques Used:
  - Causal Inference (Outcome Regression, Inverse Propensity Weighting)
  - Random Forest Model
  - Frequentist & Bayesian General Linear Model (GLM) 


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
- Outcome Regression:
-   Fit a linear model of the following form:
<img width="869" alt="image" src="https://github.com/raachelssss/COPD-and-Air-Quality/assets/88609253/808c3628-d374-466f-ac25-59c82647a7f3">


    - Confidence Interval at 5% Significance Level = [-0.661, 1.067]
    - Due to its proximity to zero, the Outcome Regression could not establish a causal relationship.
- Inverse Propensity Weighting
    - Propensity Score: P(State has a bad air quality | confounding variables) using logistic regression
    - <img width="529" alt="image" src="https://github.com/raachelssss/COPD-and-Air-Quality/assets/88609253/27b28bd7-ffd5-47b7-9f13-5822373a9d41">
    - <img width="546" alt="image" src="https://github.com/raachelssss/COPD-and-Air-Quality/assets/88609253/c5c29616-e04b-439a-97b2-1576e4a133a5">
    - Similar to Outcome Regression, no significant differences were observed in the distribution of the two groups, indicating the presence of unaccounted confounding variables.
    

### Research Question 2: Can we predict COPD occurrence based on a person's residential area?
As the causal relationship between air pollution and COPD could not be verified, the research direction was shifted to investigate whether COPD occurrence can be predicted based on residential area and race information.

Firstly, Bayesian GLM and Frequentist GLM models were adopted and trained.


**Bayesian GLM:**
- <img width="853" alt="image" src="https://github.com/raachelssss/COPD-and-Air-Quality/assets/88609253/3bac208d-655a-44e3-a50d-86698bc13c9b">
- The Bayesian GLM model shows a possibility of overfitting.
- Hispanic individuals have the lowest probability of COPD compared to Multiracial individuals.
- The population living at lower latitude and higher longitude may be more vulnerable to COPD.


**Frequentist GLM:**
- <img width="842" alt="image" src="https://github.com/raachelssss/COPD-and-Air-Quality/assets/88609253/d728b791-cd4f-488b-8f4e-218bf79d8187">
- Hispanic, Multiracial, and White variables have p-values smaller than 0.05, indicating statistical significance.
- However, considering the high Pearson chi-squared value, the model may not fit the data well.


**Random Forest Model:**
- <img width="858" alt="image" src="https://github.com/raachelssss/COPD-and-Air-Quality/assets/88609253/b5b0a363-06cb-436f-b9a9-749a11d64cc3">
- <img width="859" alt="image" src="https://github.com/raachelssss/COPD-and-Air-Quality/assets/88609253/9e48c01c-a263-4538-9261-483d3f70c846">

- The Feature Importance of variables indicating race is very low compared to latitude and longitude, suggesting that predicting COPD occurrence solely based on population demographics is challenging.
- It is regrettable that the performance of the model did not improve significantly even if different variables were adopted instead of race.
- The model showed an accuracy of around 99% on the train set and 82% on the test


### Conclusion
- d
- 

### 🛠️ Link to Final Report 
[Written Report](https://drive.google.com/file/d/1BsE3aeGkDo0m1LDiIxZam5Y_y11_iBsZ/view?usp=sharing)
