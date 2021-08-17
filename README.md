# Text Clustering for Customer Complaints on Financial Products or Services
This project focus on Text Analysis and Clustering of complaint narratives that consumers sent to the Consumer Financial Protection Bureau.

Models tested were : 
- Kmeans
- Gaussian Mixture Model(GMM)

Tools :
- Python 

## Problem Statement
Complaints narratives can be a valuable source of information for Financial companies. However,due to the unstructured nature of the data, it is time consuming to manually examine vast amount of complaints narratives. Text analysis can help financial companies to find out :
- prime concerns of their customers (e.g. any large clusters of similar complaints?)
- prominent weakness in their processes that need to be addressed
- shift in customer needs over time

This project aims to explore the use of text analysis with various clustering techniques to cluster unstructured customer feedback. The clusters will then be further analyzed to identify the underlying customer needs and problem areas.

## Data Source
For the purpose of this study, Consumer Complaints Data from the Consumer Financial Protection Bureau (https://catalog.data.gov/dataset/consumer-complaint-database) were used. This dataset has close to 2 million entries collected from year 2011 to 2017 from various Financial Institutions from various states in the United States of America.

## Methodology
The CRISP-DM (Cross Industry Standard Process for Data Mining) is the methodology used for this project.
![image](https://user-images.githubusercontent.com/88966179/129724335-8bc7c0c8-8f08-44eb-a9db-761d8d66e710.png)

## Exploratory Data Analysis

### Missing Data
Firstly, the data was examined for missing data.The number of missing data per column were analyzed via a bar plot(Figure 1). The key column to look out for will be ‘Customer Complaint Narrative’. If this column is mostly blank, it will be challenging for this project to proceed.

![image](https://user-images.githubusercontent.com/88966179/129739430-efcbf179-6a20-4a03-a640-693f87d2c21c.png)
The number of records with missing narratives is a lot but there are still sufficient data for analysis.

### Number of Complaints
As shown in the Figure 2 below, there is gradual increase in the number over the years, with 2 abrupt sharp spikes within year 2017.
![image](https://user-images.githubusercontent.com/88966179/129740023-9655de5b-437a-4778-a3a3-b79d6f12d37e.png)

The following figure shows the Top Few Financial Institutes with the most complaints:
![image](https://user-images.githubusercontent.com/88966179/129740356-ee3b2f2e-7724-4aa2-92c7-4efe7e896b36.png)

There were a total of 4711 financial institutes captured in the dataset. Each financial institution offers different services, for example, Equifax is a credit report agency and hence it’s complaints will mostly focus on credit reports as compared to Citibank, which offers a much wider variety of financial products. Therefore, it will make sense to analyze complaints separately for each financial institution.

### Data Preparation
This pre-processing step is to breakdown long text in customer complaints into modular phrases or words, so that they can be formatted as individual variables for modelling.

Using Python, the following text pre-processing tasks were performed, using ‘nltk’ package:
- Convert all text to lower case
- Breakdown all text into tokens (Tokenization)
- Remove:
-- stop words
-- punctuations
-- any word that contains digits
-- ‘XXX..’ noise terms used to anonymize details
- Lemmatization – reducing all words into their contextual base form e.g. ‘caring’ to ‘care’(base form)
- Vectorization based on TF-IDF
- Reduce dimensionality to 2 principal components 

Figure 4 below summarized the entire data preparation process:
![image](https://user-images.githubusercontent.com/88966179/129741905-05455518-fc4b-4378-9a97-0d725a7ac17d.png)



