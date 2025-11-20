# Is there a pattern to the numbers drawn in the UK National Lottery?

## Introduction

This project investigates the UK National Lottery draws from year it went live (1994) to the latest draw dates to see if there is a pattern to the numbers that have been drawn. The odds of winning the UK National Lottery are 1 in 45 million, there has been no duplicate lines since the draw went live but people have won more than once, even with the high odds.
The data only includes the ‘Lotto’ not the other draw types that are available.

## Exectutive Summary

Sadly, but expected, this project cannot predict the numbers of the next upcoming draw. However, with the data, the project provides insight into the most commonly occurring balls, validates the draws mechanism’s integrity and randomness over time. The purpose of this project is to validate the claims that the lottery is random and that there is no pattern associated with the numbers that are drawn. The insight from the data has provided some interesting analysis of the draws.
The K-means clustering model, using decade-based groupings helps segment a pattern of historical draws to enable insights from the balls drawn from the C.3000 draws since 1994. The insights gathered are as follows:
•	Frequency of individual ball (most to least)
•	Common decade-based grouping
•	Silhouette scores
Using this insight, it allows the user to add variables to suit their needs for creating ‘Lucky dip style lines’, such as:
•	No consecutive numbers (1,2,3,4,5,6)
•	No duplicate draws from previous (some draws have shared 5 of 6 numbers but never a perfect match)
•	Specific lines such as most reoccurring number versus the least reoccurring number
•	Names of machines that are used (This is not known pre to selection of numbers)
•	Set of balls (This is not known pre to selection of numbers)
Using this approach, provides a data-led decision making of generating a ‘Lucky dip’ versus a national lottery generated Lucky dip’ purchased at a relator or online.


