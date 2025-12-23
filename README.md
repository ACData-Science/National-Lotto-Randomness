# Is There a Pattern to the Numbers Drawn in the UK National Lottery?

## Introduction

This project investigates whether historical UK National Lottery (Lotto) draw data exhibits any identifiable patterns. The UK National Lottery launched in 1994, with odds of winning the jackpot estimated at approximately 1 in 45 million. Despite these odds, individuals have won more than once, and public discourse frequently speculates about patterns or “lucky numbers”. This project evaluates such claims using data science techniques to assess whether observable structure exists in the draw outcomes.
The analysis focuses exclusively on the main Lotto draw and excludes other National Lottery products. The primary aim is not to predict future numbers, but to validate whether the draw mechanism behaves as expected under randomness.

## Executive Summary

As expected, this project finds that UK National Lottery numbers are random and cannot be predicted. However, analysis of historical draw data provides insight into frequency distributions, confirms the integrity of the draw mechanism, and demonstrates how data science can be used to validate randomness rather than exploit it.
Using exploratory data analysis and K-means clustering with decade-based grouping, the project analyses approximately 3,000 draws since 1994. Outputs include frequency analysis of individual balls, clustering behaviour across decades, and silhouette scores to assess model quality.

The findings show weak clustering, balanced frequency distributions, and no repeated six-number combinations. While these insights can be used to generate data-led “lucky dip” style selections, such as avoiding consecutive numbers or previously drawn combinations, they do not increase the probability of winning. The project therefore provides analytical transparency rather than predictive advantage.

## Dataset

The dataset used can be found here - UK National Lotto Winning Numbers
The dataset used is publicly available and updated after each draw. It contains all UK National Lottery Lotto results from launch to the most recent draw and is accessed in CSV format. The dataset is structured, consistent, and complete, with no missing main ball values and no duplicate draws.


[Figure 1: UK National Lottery dataset in CSV format]

<img width="634" height="312" alt="image" src="https://github.com/user-attachments/assets/d8332152-f89d-407d-be2d-bd3a33c2070d" />



 
Python, using Google Colab, was selected to process the data due to its accessibility, reproducibility, and strong data science ecosystem. The raw CSV is transformed into structured data frames and exported as analysis-ready outputs.
Because the data is publicly owned, there is a possibility of upstream data errors. For this reason, validation steps are included to preview and confirm data accuracy on each refresh. As noted by Suer (2023), “High-quality data enables confident, informed choices. When data quality fails, it undermines customer service, productivity, governance, and strategy.”

[Figure 2: Script logic for storing and appending the latest draw data]

<img width="671" height="183" alt="image" src="https://github.com/user-attachments/assets/045657f5-86a1-40d3-b4bb-9a67c007b371" />

 
## Data Engineering and Preparation
The extract–transform–load (ETL) process begins by ingesting the CSV file and parsing the joined ball values into individual integers. Draw dates are converted into datetime format, and validation checks ensure each draw contains the correct number of balls.

[Figure 3: Parsing joined ball values into individual integers]

<img width="940" height="491" alt="image" src="https://github.com/user-attachments/assets/87ef872f-48cb-43c6-a768-2b63d2f299ab" />

 
The exploratory data analysis process confirms numerical ranges, verifies record volumes, and ensures consistency across historical and newly added draws. The script also outputs a clean CSV file, enabling further analysis in tools such as Excel or Power BI.
A key transformation step is the introduction of decade-based grouping. Because balls are ordered numerically after each draw, positional bias exists. Grouping balls by decade mitigates this bias and allows more meaningful comparison across draws.

[Figure 4: Dataframe preview showing structured draw data]
<img width="684" height="571" alt="image" src="https://github.com/user-attachments/assets/0ed6f6c4-264d-4575-a650-648c1de4c8b8" />
 

## Exploratory Data Analysis
Initial analysis focuses on understanding frequency distributions and temporal behaviour. Each draw contains six main balls and a bonus ball, with values varying due to ordering rather than selection bias. Frequency plots show that ball occurrences are broadly balanced across the full dataset.
Slightly lower frequencies are observed for numbers above 49, explained by their later introduction in October 2015 rather than by bias. No duplicated six-number combinations are present in the dataset, although some draws share five out of six numbers.
This stage confirms that the data behaves as expected for a randomised process and informs appropriate model selection.

[Figure 5: Frequency distribution of lottery ball values]
<img width="762" height="591" alt="image" src="https://github.com/user-attachments/assets/ae293894-3606-4139-b633-a81a36e66805" />

 
## Modelling Approach
Given the absence of labelled outcomes and the random nature of lottery draws, supervised learning methods such as linear or logistic regression were not appropriate. Time-series modelling was considered but deprioritised due to the lack of temporal dependency between draws.

Alternative unsupervised methods such as hierarchical clustering and DBSCAN were considered. Hierarchical clustering scales poorly with large datasets and offers limited additional interpretability in the absence of natural separation. Density-based methods such as DBSCAN are designed to identify dense regions and outliers, which is unsuitable for uniformly distributed random data. K-means was therefore selected not because strong clustering was expected, but because it provides a transparent baseline for testing whether structure exists at all. 
“Clustering is a solution for classifying enormous data when there is not any early knowledge about classes” (Saeed Aghabozorgi, Ali Seyed Shirkhorshidi, The Ying Wah – Nov 2015).

## Model Evaluation

Two methods are used to evaluate cluster suitability: the Elbow Curve and the Silhouette Score.
The Elbow Curve assesses within-cluster sum of squares across different values of K. However, elbow plots often resemble a smooth glide path rather than a clear inflection point. 
“It works by choosing a range of K values (usually 1 through n, where n is a chosen number), and finding the within-cluster sum of squares (WCSS) value for each K value in the range.” (Anmol Tomar / Brennan Whitfield 2025)

[Figure 6: Elbow curve showing no clear inflection point]

<img width="933" height="472" alt="image" src="https://github.com/user-attachments/assets/57d15b95-ea86-4a94-b67a-4cfe1a6caddd" />
 
The Silhouette Score is therefore used to identify optimal cluster separation. “The Silhouette score is a very useful method to find the number of K when the elbow method doesn’t show a clear elbow point”  (Anmol Tomar / Brennan Whitfield 2025)

The highest silhouette score is achieved using two clusters. Further experimentation with five clusters yields an average silhouette score of approximately 0.212. This low value reinforces randomness rather than indicating model failure. “The silhouette coefficient is an internal validation metric widely used in unsupervised machine learning to evaluate the quality of clustering when ground truth labels are unavailable for assessment” (Muhammad Waqas, Zahid Halim, Sakshi Kaushal, Francisco B. Rodriguez - 2022).


[Figure 7: Silhouette score results for K-means clustering]

<img width="878" height="366" alt="image" src="https://github.com/user-attachments/assets/1d50c8e8-df3c-4324-a4fd-044a956f4a4e" />


## Results

Cluster centroids show that ball positions tend to fall within similar numerical decades due to post-draw sorting rather than selection bias. Frequency analysis confirms that individual balls are evenly distributed across the dataset.
Reducing the dataset to smaller time windows marginally improves silhouette scores, but not to a statistically meaningful extent. Overall, the results support the conclusion that no predictive patterns exist.

[Figure 8: Cluster centroids illustrating weak separation]
  
<img width="940" height="352" alt="image" src="https://github.com/user-attachments/assets/5fb8ae38-3898-47bc-a304-9a245643e180" />
<img width="430" height="164" alt="image" src="https://github.com/user-attachments/assets/70519030-def5-419d-8fbf-ac42e002bf10" />


## Ethical Considerations and Bias

The dataset contains no personal or sensitive data, and privacy risk is minimal. However, gambling-related data carries ethical sensitivity due to the risk of misinterpretation.

“Algorithmic fairness metrics and relevant toolkits may assist you in identifying and mitigating risks of unfair outcomes. However, fairness is not a goal that algorithms can achieve alone. Therefore, you should take a holistic approach, thinking about fairness across different dimensions and not just within the bounds of your model or statistical distributions” (ICO)

Cognitive biases such as the gambler’s fallacy and pattern illusion are addressed by demonstrating weak clustering and balanced frequencies. Methodological bias is mitigated through transparent reporting of low model performance and clear explanation of analytical limitations.

From a governance perspective, the dataset is externally managed and publicly released, meaning version control, data accuracy, and update frequency are outside the analyst’s control. Validation checks are applied at each refresh, and outputs are treated as indicative rather than authoritative. Clear communication of limitations forms part of responsible data governance.

## Data Visualisation and Communication
Visualisations include frequency charts, cluster plots, and evaluation curves. These are selected to support understanding rather than persuasion and are clearly labelled and logically sequenced. The report adopts an academic writing style appropriate for analytical validation and public data analysis.

## Conclusion
This project finds no evidence of meaningful patterns in UK National Lottery draws. The numbers are random, and clustering analysis confirms the absence of strong structure. While historical frequency insights can inform data-led “lucky dip” generation, they do not alter winning probabilities.
The value of this project lies in validating system integrity, demonstrating ethical data science practice, and addressing common misconceptions around randomness. It highlights how data science can be used to evaluate probabilistic systems responsibly rather than exploit them.

## Support
This project does not guarantee winning outcomes and is intended solely for academic analysis. If you have concerns regarding gambling behaviour, support is available at:
www.gambleaware.org
www.gamcare.org.uk












