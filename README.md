# Predictive Analysis of Policial Party using COVID-19 Data

## Project Details

### Data Cleaning:

1. Preprocessing raw data (size: 5-7GB per file) provided by government agencies such as the CDC and press releases in regards to safety protocols by each state
2. Removing duplicate, null, or irrelevant data
3. Filtering outliers

### EDA:

1. Examining the relationship between the Mask-wearing population proportion and the corresponding state's COVID-19 cases 

<img width="773" alt="image" src="https://github.com/raachelssss/COPD-and-Air-Quality/assets/88609253/3d25255d-44d9-451f-a9fe-96f7681c8036">


2. Relationship between each state's political party and its safety protocols/COVID restrictions
    1. Concluded that there exists difference in the number of confirmed COVID-19 cases between Democratic and Republican states.

### Research Question:

Is it possible to predict whether a state is Democratic or Republican by providing parameters related to state-specific parameters?

### Classification Model:

Model: Logistic Regression Model

Parameters: daily rate of vaccination/cases/tests/deaths per capita

### Model Improvement:

<img width="785" alt="image" src="https://github.com/raachelssss/COPD-and-Air-Quality/assets/88609253/91b2018c-aa2d-4d4f-bb11-31a9f157de0a">

                                Improved Accuracy of Classification Model from 51% to 71% 

**How?**

- 5-fold cross validation
- Add more relevant features 

### Result

- By training a model using safety and hygiene guidelines that have a significant impact on the rate of COVID-19 cases, predicted the political party of each state with an accuracy of 71%.
- However, it is regrettable that the accuracy was not higher. It raises the question of whether a more focused dataset, specifically examining the differing initial responses of each state before COVID-19 spread nationwide, could have yielded more insightful results.

### 🛠️ Specification

- Python (pandas, sklearn)
- Data Visualization
- Data Analysis
- Data Cleansing
- Predictive Modeling

### **[📎](https://emojipedia.org/paperclip/)** Written Report

https://drive.google.com/file/d/1ZK41CXvbkP_LTtPPU7PH_y7JG0bMfneX/view?usp=sharing
