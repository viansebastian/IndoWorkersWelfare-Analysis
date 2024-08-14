# ***Indonesia's Workers Welfare; and Indepth Analysis on Provincial and National Economic Performance***
---

![Infographic Poster](docs/poster.png?raw=true "Infographic Findings")
*fig 1: Infographic Poster Result*

***Introduction*** — Economic disparity among different regions within a country poses significant challenges to achieving sustainable development. Indonesia, in particular, is a vast archipelago with diverse socioeconomic landscapes where regional disparities in worker welfare are pronounced [1]. Understanding these disparities is crucial for the formulation of effective policies aimed at fostering inclusive economic growth. This project leverages machine learning techniques such as clustering and regression to analyze the welfare of workers across Indonesia's 34 provinces, utilizing data on wages, minimum wages, poverty lines, and expenses. By examining these variables, the project aims to provide insights that can inform government policies and interventions, in alignment with the United Nations Sustainable Development Goal (SDG) 1: No Poverty. Ensuring no poverty is foundational for improving worker welfare, as it directly influences employment opportunities, productivity, and overall economic well-being.

***Keywords*** — Clustering, Regression, Poverty Line, Wage, Minimum Wage, Expense, Trend

---

This is a repository for my final project in machine learning class. This time, my team and I decided to use traditional machine learning methods to perform deep data analysis on Indonesia's economic performance in regards of the minimum wage, wage, poverty line, and expense rate. The flowchart of this project can be seen in fig. 2 below.

![Project FlowChart](docs/flowchart.png?raw=true "Project FlowChart")
*fig 2: project flowchart*

Notice in our flowchart, we implemented both clustering and regression, and the details of this are as follows: 
1. The clustering are used to group provinces into three distinctive performance groups based on features in later sections. 
2. The regression aims to acquire predictions of said features from respective groups up to the year 2028. 

---
***Data Acquisition***

The dataset used in this project was taken from the [Kesejahteraan Pekerja Indonesia](https://www.kaggle.com/datasets/rezkyyayang/pekerja-sejahtera) dataset, where this dataset is originally scraped from the official [Badan Pusat Statistik](https://www.bps.go.id/id) website.

This dataset contains the data of the Expense, Minimum Wage, Poverty Line, and Wage of Indonesia's provinces from years varying between 2007 up to 2022.

![Dataset Card](docs/dataset.png?raw=true "Dataset Card")
*fig 3: dataset card*

The dataset we chose consists of the Garis Kemiskinan (Poverty Line), Pengeluaran (Expenses), UMP (Minimum Wage), and the Upah (Wage) tables. 
The detailed description of them are as follows: 
1. Poverty Line is defined using the formula below: 
    $$\text{PL} = \text{PLF} + \text{PLNF}$$
*where*:
    $$\text{PL} = Poverty Line$$
    $$\text{PLF} = Food Poverty Line$$
    $$\text{PLNF} = Non-Food Poverty Line$$
    
In essence, the poverty line is the minimum amount 
of money needed to fulfill both food needs (PLF) 
of 2100 kcals and non-food base needs such as 
housing and others. In all tables, the region is 
divided into village, urban, and suburban areas, and 
the period of survey is divided into March and 
September. The type consists of total (PL), food 
poverty line (PLF), and non-food poverty line 
(PLNF).

2. The expenses table consists of the expenses per 
capita data based on provincial, region, type and 
year. Both the region and type is the same as the 
poverty line table. 
3. The minimum wage and wage table consists of 
corresponding data based on provincial and year 
data. The minimum wage is the minimum wage per 
month, and the wage is in rupiah per hour. 

---
***Data Preprocessing***

The main issue in this dataset is different data formats, especially in the Poverty Line and Expenses table. These two tables contain information such as type, region, and periodes. On the other hand, the table format the team would like to use are Province, Year, and the target value. 

The solution of this is data aggregation. For both expenses and poverty line tables, only the “TOTAL” type is considered as it has correctly summed all other types in preceding rows. As for the regions, they are aggregated to the sum, to get the value of provincial output. Then the data is filtered to start from 2015 only, as some tables contain data as far as 2004 while others do not. The filtering decision is to uniform the analysis. Finally, the columns are renamed the columns for easier use. The details can be read in the report. 

---
***Exploratory Data Analysis (EDA)***

In this section, we simply visualized the data conditions, trends, and how they correlate with each other. We can see the results as follows.

![expenses-province img](docs/expenses-province.png?raw=true "expenses-province img")
*fig 4: Trend of Average Monthly Expenses for Every Province*

![minwage-province img](docs/minwage-province.png?raw=true "minwage-province img")
*fig 5: Trend of Average Monthly Minimum Wage for Every Province*

![povline-province img](docs/povline-province.png?raw=true "povline-province img")
*fig 6: Trend of Poverty Line for Every Province*

![wage-province img](docs/wage-province.png?raw=true "wage-province img")
*fig 7: Trend of Average Monthly Wage for Every Province*

It can be observed from fig. 8 and 9 that all features have an upward trend, with an exceptionally smooth trend on expenses and poverty line. This shows that in general, living costs have continued to increase, and will keep on increasing in the future. On the other hand, the minimum wage and wage have been moru fluctuative and volatile. 

![pairplot img](docs/pairplot.png?raw=true "pairplot img")
*fig 8: Pairplot Features*

![corr img](docs/corr.png?raw=true "corr img")
*fig 9: Correlation Matrix*

In the pairplot visualization, it can be observed that all features share a relatively positive correlation with each other, showing a positive skew. Backed with the correlation matrix, it can be inferred that all features have strong colinearity with each other, be it positively or negatively. Using this analysis, we will use the features without further processing.

---
***Modeling Part 1: Clustering***

The clustering is used for further analysis on each provinces. Given the data of average wages, expenses, poverty line, etc., we would like to know whether or not these provinces can be grouped into high performing and low performing ones. The analysis result aims to, ideally, give insights on which provinces require extra attention from the government. 

The method of clustering used will be the KMeans Clustering. After visualizing the initial data into a 3D Space, it can be observed that it does not separate into distince dense regions, making density-based methods ineffective. After performing the Elbow Method, we used k = 3, where the results can be seen in the 'Results and Discussion' section.

---
***Modeling Part 2: Regression***

The regression is performed to perform predictions on each features in the future. Since we have data from year 2015 to 2022, we will perform the predictions for the next 5 years.  

Considering the minimum amount of data, we initially went with the Linear Regression approach. But after further assessment, we decided to use the Polynomial Regression after once again observing the past data trends. As some of the features have fluctuative tendencies, the Polynomial Regression would be the best method for our problem. 

---
***Results and Interpretation***

Firstly, let us address the results of the Clustering. Fig. 10 shows the clustering results in 3D space, and fig. 11 shows the interpretation of the clusters.  

![3D Plot](docs/clustering.png?raw=true "3D Plot")
*fig 10: 3D Cluster plot after K-Means Clustering*

![cluster interpret](docs/cluster-interpret.png?raw=true "cluster interpret")
*fig 11: Clustering Interpretation*

Based on the clustering results, we can cluster the provinces into 3, High (cluster 1), Medium (cluster 2), and Low (cluster 3), where each are interpreted as they are named because of how high they are in each feature. 
In fig. 12, we can observe the results of the regression on Indonesia as a whole.

![national pred](docs/national-pred.png?raw=true "national pred")
*fig 12: National Prediction*

It can be seen that although expenses, minimum wage, and poverty line have a rather upward prediction, it is predicted that wages will **decrease** in the future. 
In addition to predicting Indonesia's performance as a whole, we have also predicted a province from each tier, which will be detailed in the PDF report. 

--- 
***Conclusion***

In this project, my team and I have performed deep analysis on the nation's economic performace using traditional machine learning methods. Our project naturally still have a lot of room of improvement, but we enjoyed working on this project! Indeed, the strength of our approach lies in simplicity, and to prove that interesting projects does not always have to be deep learning-based. 

For more detailed info, do read this repository as a whole, from the PDF report, until the notebooks. Feel free to contact me should you have inquiries or project opportunities!
