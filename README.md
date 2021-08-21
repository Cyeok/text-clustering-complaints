# Text Clustering Customer Complaints with Python
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

## Data Preparation
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

## Modelling
As mentioned before, complaint narratives were modelled separately for each Financial Institution. This allows us to visualized the nature of the complaints better, in specific context of the product range each financial organisation was selling.
The following 2 clustering models(unsupervised) were trained for the top 5 companies with the most number of complaint narratives:
- Kmeans (Scikit-learn)
- Gaussian Mixture Model (GMM, Scikit-learn)

5 were chosen as the number of clusters for both models as the word clouds showed more distinctive key words between clusters.

## Evaluation and Results
### Company : Equifax
Variety of products sold : Primarily 1 product (Credit report)

The following scatterplot shows the 2 principle components (of key words in complaints) before clustering :
![image](https://user-images.githubusercontent.com/88966179/130317282-359eade2-e17b-4769-b061-e361adeff1ed.png)


The scatterplot shows 1 large dense cluster with some sparsely distributed outlying points at the sides. This is not surprising given that Equifax is primarily only in the business of selling credit reports, and therefore their complaints will likely have very similar key words.

After clustering with the 2 models, the scatterplots are replotted as follows:
![image](https://user-images.githubusercontent.com/88966179/130317291-db1c1bfa-f6bc-4118-8965-95a90b964706.png)

The 'boundaries' were not very different between the models. Word clouds generated from the biggest clusters of Kmeans and GMM were compared:

![image](https://user-images.githubusercontent.com/88966179/130317098-ca72ef67-b4da-45c3-837b-fb1b20638300.png)![image](https://user-images.githubusercontent.com/88966179/130317105-1964bdb9-9c52-4607-97a6-6b185ad30098.png)

Both models revealed that the biggest concerns of Equifax's customers were related to security breaches and personal data.

### Company : Citibank
Variety of products sold : Multiple products (e.g. saving accounts, credit cards, mortgages etc

Let’s see if the modelling results will be similar for another company with a wider variety of products and hence is likely to receive more varied content for complaints. 'Citibank' was picked for this purpose.

![image](https://user-images.githubusercontent.com/88966179/130317496-23b892f9-2289-40f3-b249-fa16bfed36d6.png)

The above scatterplot reveals less concentration of data points in a single area. This make sense as Citibank provides more variety of products as compared to Equifax. Therefore, the key words of their complaint narratives should be more varied.

![image](https://user-images.githubusercontent.com/88966179/130317749-f6af5f5c-c6af-4923-927c-dd44f5f13921.png)

The clusters generated from Kmeans and GMM for Citibank seems to have slightly more differences as compared to that of Equifax. Let’s compare the word clouds for the 2 clustering algorithm :

![image](https://user-images.githubusercontent.com/88966179/130317784-3d3e3ba0-fc85-4ede-a57d-568dc1a64bf3.png)
![image](https://user-images.githubusercontent.com/88966179/130317808-8687e5a9-91cb-4fe2-a159-08c0511201b7.png)

From the word clouds of the biggest cluster(top), it seems that Citibank customers' biggest concerns were related to related to payments/interests for accounts, mortgages or cards. Perhaps, this is an area which the company need to address as first priority. The other cluster seems to point to unhappiness arising out of some promotions related to bonus for checking accounts. Therefore, the company may want to further investigate on this.

## Conclusion
In this project, I have explored the use of 2 clustering techniques to cluster customer complaints narratives for each company. The purpose of this project is to make use of the clustering results to identify pain points for each company and to provide enough information to know which area of weakness to focus on as first priority. In this case, both clustering techniques seem to yield similar relevant terms and similar cluster size. It can be seen here that either clustering model seems to work fine for both Equifax (with 1 core product offering) and Citibank(with several product offering). 
