# Is there a pattern to the numbers drawn in the UK National Lottery?

## Introduction

This project investigates the UK National Lottery draws from year it went live (1994) to the latest draw dates to see if there is a pattern to the numbers that have been drawn. The odds of winning the UK National Lottery are 1 in 45 million, there has been no duplicate lines since the draw went live but people have won more than once, even with the high odds.
The data only includes the ‘Lotto’ not the other draw types that are available.

## Executive Summary

Sadly, but expected, this project cannot predict the numbers of the next upcoming draw. However, with the data, the project provides insight into the most commonly occurring balls, validates the draws mechanism’s integrity and randomness over time. The purpose of this project is to validate the claims that the lottery is random and that there is no pattern associated with the numbers that are drawn. The insight from the data has provided some interesting analysis of the draws.
The K-means clustering model, using decade-based groupings helps segment a pattern of historical draws to enable insights from the balls drawn from the C.3000 draws since 1994. The insights gathered are as follows:

  *	Frequency of individual ball (most to least)
  *	Common decade-based grouping
  *	Silhouette scores
  
Using this insight, it allows the user to add variables to suit their needs for creating ‘Lucky dip style lines’, such as:

  *	No consecutive numbers (1,2,3,4,5,6)
  *	No duplicate draws from previous (some draws have shared 5 of 6 numbers but never a perfect match)
  *	Specific lines such as most reoccurring number versus the least reoccurring number
  *	Names of machines that are used (This is not known pre to selection of numbers)
  *	Set of balls (This is not known pre to selection of numbers)
  
Using this approach, provides a data-led decision making of generating a ‘Lucky dip’ versus a national lottery generated Lucky dip’ purchased at a relator or online.

## Data-Set
The data set is publicly available and updated after every draw. The dataset used can be found here - UK National Lotto Winning Numbers
Using Python via Google Colab helped create a workbook to enable users to adjust the script, add new data easily and create a PDF of the findings including visuals. 
The data is extracted from the website as a CSV format **(Figure 1)** but is then changed to a PDF for the purpose of this project. The PDF provides a universal option for different types of operation systems. The data is structured and of high quality as there is a consistent formatting, no missing main balls and no duplication across the draws. The code below shows how the data is obtained and can be updated with the latest draw to keep the output relevant. **(Figure 2)**

### Figure 1 - Data set Txt file
<img width="634" height="312" alt="image" src="https://github.com/user-attachments/assets/f973139e-7c83-41f1-8094-39579131c89e" />

### Figure 2 - Storing and adding latest data to maintain consistency
<img width="671" height="183" alt="image" src="https://github.com/user-attachments/assets/945487a9-0b46-452b-a26c-31e68ee9004a" />

### Figure 3 – This code parsed the data to split out the value of the ball
<img width="940" height="491" alt="image" src="https://github.com/user-attachments/assets/b48b2948-fa6a-42ce-9034-dd851504f4d5" />

The EDA process in this script evaluates the data by stripping the joined numbers into individual values, recognising the date value, confirming the correct volumes on numbers and then turning the number values into integers. This format helps make sure the data is reviewed on every refresh to ensure accuracy and quality of data. “High-quality data enables confident, informed choices. **“When data quality fails, it undermines customer service, productivity, governance, and strategy” (Myles Suer, Sept 2023)**.
The next stage in the script is to create a data frame, since the data is publicly owned there is a chance there could be errors to which this segment of code provide a preview of the data to establish accuracy within the script. The data frame shown (Figure 4) shows the latest data applied and the format needed to run the model. This helps the user review newly added data from the latest draws to ensure accuracy.

### Figure 4

<img width="684" height="571" alt="image" src="https://github.com/user-attachments/assets/ab2786cc-c464-4d26-9f06-2790bddf17b7" />

The script shown in Figure 3 also produces a CSV file of the draws so this data can be processed in Excel or moved to Power-Bi to suit users’ requirements or capabilities.  

## Analysis

The data set is now decided; the format and structure has provided a baseline for how the data looks and how it needs to be analysed. Since the data is made up of 6 balls and a bonus ball, the values will all differ due to the first ball isn’t guaranteed to be < 10 and like the next 5 balls in its place. The data set needs to be adjusted to factor these variables which is why a ‘Decade based grouping’ option was added to capture the random selection of the balls. 
The need to clusters these values establishes a pattern to be able to model the data. “Clustering is a solution for classifying enormous data when there is not any early knowledge about classes” (Saeed Aghabozorgi, Ali Seyed Shirkhorshidi, The Ying Wah – Nov 2015). This in turn groups the ball values into workable data clusters to establish pattern likelihood, not guaranteed individual outcome, in this case, the actual ball value.

## Modelling

After reviewing the dataset and the structure of how the data is provided, the next steps were to choose a machine learning model to analyse the data accurately. Since the data is based on random integers and no set outcome, Logistic and Linear regression was excluded. The data required segments based on the ball values to review potential patterns but to also confirm the randomness of the draws.
Using the insights gained from the analysis, the ‘decade-based grouping’ leaned more towards K-Means using the cluster centroids rather than Time series; however they are both similar and the data content could be moved to Time series for future reviews. 

Using the full data set, the cluster count needs to be decided using either the Silhouette score or the Elbow cure.

**Elbow Curve**

The Elbow curve is designed to provide a point where the data indicates a change in direction but isn’t always clear and most just look like a glide path from top left to bottom right.**”  It works by choosing a range of K values (usually 1 through n, where n is a chosen number), and finding the within-cluster sum of squares (WCSS) value for each K value in the range.” (Anmol Tomar / Brennan Whitfield 2025)**

**Silhouette score**

The Silhouette score is to look at a value based on the K clusters to get as close to 1 as possible. **“The Silhouette score is a very useful method to find the number of K when the elbow method doesn’t show a clear elbow point”  (Anmol Tomar / Brennan Whitfield 2025)**
Based on the Elbow curves none defining point, the Silhouette score proves the highest point by using 2 clusters. (Figure 5)

### (Figure 5) – Last 3000 Draws
<img width="762" height="591" alt="image" src="https://github.com/user-attachments/assets/b334a704-b1b2-441f-b876-754a193790a5" />

The K-means process requires a cluster value to enable a silhouette score that fits with an acceptable range. **“The silhouette coefficient is an internal validation metric widely used in unsupervised machine learning to evaluate the quality of clustering when ground truth labels are unavailable for assessment” (Muhammad Waqas, Zahid Halim, Sakshi Kaushal, Francisco B. Rodriguez - 2022)**.
The ideal ‘Silhouette Score’ should be greater than 0.5, based on the number of clusters picked. On average 5 is normally selected and with this data and the number of balls, 5-6 would have been an ideal selection. The data set has provided a score of 0.212, using 5 clusters (Figure 6) which would suggest that there are some weak grouping patterns, but nothing very distinct. This makes sense with the fact that the Lotto numbers are expected to be random and strong natural clusters would not be expected.

### Figure 6 - Heatmap - Centroids
<img width="933" height="472" alt="image" src="https://github.com/user-attachments/assets/3121335e-5df6-4add-91d6-b58146d8ffb1" />

## Results

### Figure 7 - 2 Cluster points

<img width="878" height="366" alt="image" src="https://github.com/user-attachments/assets/eeb62f8c-2f81-469f-b25f-1021ebc1ccf1" />

**Figure 7** shows the average ball values based on the 2 clusters chosen which provides two ends of the spectrum. As expected, the ball value / position will fall withing a similar decade as the balls will be put into numerical order once draw. This is evident from Cluster 0 ball2 and ball3 and the same with Cluster 1 ball3 and ball4.

## Figure 8 – Frequency of the balls are very balanced. The low 50’s is due to them being added Oct 2015 but still balanced within themselves.

<img width="940" height="352" alt="image" src="https://github.com/user-attachments/assets/3b6c3f16-741c-4505-ba6e-2d5886a3b514" />

<img width="430" height="164" alt="image" src="https://github.com/user-attachments/assets/a7e01872-ba0e-4bc2-b40a-a39eecddf201" />

## Conclusion
There are no patterns to the National Lottery, it is completely random based on all the draws so far from start to current date. However, from what the data has showed, there have been no 6 numbers repeated, and that there are some common and least common numbers that have been drawn over the time which could be used to try the odds. 
This review was based on the full draws from start to finish. If the data was reduced to a segment of the draws (the last 500 for example), the Silhouette score does improve by 0.001.
There is a script provided that can create a list of lucky dip numbers that can be tailored to work more data-led but there is no guarantee, it is pure chance.

## Support
As stated, this does not guarantee a selection of winning lines and is for academic purposes not for gambling. 
If you require support or have concerns of potential gambling addiction, please find below a list of supportive networks.
www.Gambleaware.org
www.gamcare.org.uk	












