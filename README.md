# Netflix-Home-Optimization-Experimental-Analysis

## Executive Summary

In this project, we aimed to minimize the browsing time on Netflix using the following factors: Tile Size, Match Score, Preview Length, and Preview Type. Our experimental journey involved systematically varying these factors to identify their individual and combined effects on browsing time.

After thorough analysis, we discovered that the optimal combination of these factors, leading to the most efficient browsing experience, was [0.2, 75, 75, TT] for Tile Size, Match Score, Preview Length, and Preview Type, respectively.

## Introduction

In the modern world, streaming services like Netflix have revolutionized entertainment, offering an endless amount of content with just a few clicks of a button. However, this abundance of choice can lead to users having trouble making a decision on what to watch, this is known as decision paralysis. Our project aimed to address this issue by optimizing parts of the user interface to minimize browsing time.

To tackle this problem, we used various experimental methods like factorial design, multiple means testing, and visual comparisons, focusing on four key factors: Tile Size, Match Score, Preview Length, and Preview Type. Through hypothesis testing and other analyses, we first identified the statistically significant factors and their interactions. Then we aimed to find the optimal conditions of the four factors using the previous discussed methods in combination with main effect and interaction plots.

## The Experiments

Using the four design factors outlined previously, we aimed to minimize the response variable, average browsing time. 100 observations for each unique condition were collected, which we will be using in our hypothesis testing below.

### First Run
Aimed to determine the significant factors. Through hypothesis testing, we proved that Tile Size and its interactions were statistically insignificant to the model. We also showed that for Preview Type, TT was almost always better than AC in minimizing the average browsing time. We also found a direction towards the most optimal values of Preview Length and Match Score.

### Second Run
With the findings from the first run, we decided to use the default value for Tile Size moving forward. We used partial F-tests in combination with various plots to narrow down the ranges of values for each remaining factor. We found the optimal range to be (70,85) and (60,90) for Match.Score and Prev.Length, respectively.

### Third Run
To narrow down the results from the second run, we investigated the interactions more in-depth and performed more F-tests and pairwise testing. At this stage we also found the optimal value, with 95% confidence.

## First Run

* __Question__: As this is our first run we are interested in getting a sense of where the minimum might lie. Which combination of factors corresponds to the lowest browsing time?

* __Plan__: We start with a wide range for each of Prev.Length and Match.Score. Since we are bound to 10 betas we cannot have too many unique values. Our response variable is Browse.Time and we begin using all 4 design factors Prev.Length, Match.Score, Tile.Size, and Prev.Type.

* __Data__: We started with the following levels for each design factor
Prev.Length = {50, 80, 120}, Match.Score = {50, 70, 100}, Tile.Size = {0.1, 0.5}, Prev.Type = {TT, AC}

* __Analysis__: Using a multiple means approach where 10 unique combinations were tested, based on the initial levels chosen, we found the average browsing time per combination of settings. With the following boxplot we get a sense of the distribution of browsing times for each of the combinations.
* 
![Browse Time Distribution By Group](https://github.com/user-attachments/assets/66bf90de-b6ba-48a1-a4c1-82c6efef1b9e)

From this box-plot we quickly found that Prev.Type AC tends to make browsing times much worse. For further analysis we ran an ANOVA test where,
* Main effects terms are
  * x1,x2 are indicators for Prev.Length (80,120)
  * x3,x4 are indicators for Match.Score (70,100)
  * x5 is an indicator for Tile.Size (0.5)
  * x6 is an indicator for Prev.Type (TT)
 
* The full model equation is the following:

$$
\beta_0 + \beta_1 x_1 + \beta_2 x_2 + \beta_3 x_3 + \beta_4 x_4 + \beta_5 x_1 x_3 + \beta_6 x_1 x_4 + \dots + \beta_{35} x_2 x_4 x_5 x_6
$$

where

$$
\beta_0, \beta_1, \beta_2, \beta_3, \beta_4
$$

are the main effect, Prev.Length, Match.Score, Tile.Size, and Prev.Type.

We proved that Tile.Size is insignificant by comparing the full model (including interactions) vs the full model without Tile.Size (including interactions). This is done with the following hypothesis test:

$$
H_0: \beta_3 = \dots = \beta_{35} = 0, \text{ where all } \beta \text{'s related to Tile.Size are included}, \text{ vs. } H_1: \beta_j \neq 0, \forall \beta_j \text{'s related to Tile.Size}
$$

Using an ANOVA test we get an F-stat of -0.861887, and a P value of 1. Using a significance level of 5%, this p value is too high and therefore we fail to reject the null, indicating that the effect of the coefficients associated with Tile.Size are not significantly different from 0. This allows us to conclude that Tile.Size is not an influential factor in the model and we can move forward without it.

At this stage we also tested the significance of the interaction terms. Using the factorial method and the same full model as the previous test, we compared the full model with the reduced main effects model. This test was done with the following hypothesis:

$$
H_0: \beta_1 = \beta_2 = \beta_3 = \beta_4 = 0 \text{ vs. } H_1: \beta_j \neq 0, \text{ for } j = 1, 2, 3, 4
$$

Using an ANOVA test we get an F-stat of 370.0913 and a P value of 3.7575x10^-161, which is essentially 0. Compared to a significance level of 5% this p value falls within the rejection region and allows us to reject the null hypothesis. Therefore, this test allows us to conclude that there exists at least one, or more than one, significant interaction term. Since there is a presence of a significant interaction effect, it no longer makes sense to discuss the main effects in isolation since this would be ignoring the fact that this effect changes depending on the level of another factor.

This conclusion is also shown in the interaction plots below. Since the lines in all three plots are not parallel we can be sure that the main effect of one factor depends on the levels of another factor. Tile.Size was not considered here since we already proved in the previous test that it is insignificant. Comparing the three plots it seems like the interaction of Prev.Length and Match.Score have the strongest effect on browsing time, since the other two plots are closer to parallel, however this will be further explored in the following experiments.

<img width="1236" alt="Screenshot 2024-10-06 at 3 02 17 PM" src="https://github.com/user-attachments/assets/c1bba29b-9506-4a0c-81f6-c1ae8e3dc985">

From these plots we can also narrow down some of our ranges for the numeric factors. It is evident that a value closer to 80 is best for Prev.Length, value closer to 70 is best for Match.Score, and as shown in the earlier box-plot, Prev.Type of TT is always better than AC. These changes are implemented in the next experiment.

* __Conclusions__: To summarize, in this initial experiment we proved that Tile.Size is insignificant, we found that Prev.Type TT is always better for Browsing Time than AC, and that the optimal values for Prev.Length and Match.Score are closer to 80 and 70, respectively.


## Second Run

* __Question__: We already verified that Prev.Type TT performs better than AC and Tile.Size has no significant effects on determining Browse.Time. In addition, values around 80 for Prev.Length and values around 70 for Match.Score seems to achieve a relatively optimal result. We are interested in narrowing down the ranges for factor Prev.Length and factor Match.Score to find the combination of these four factors to reach the lowest Browse.Time.

* __Plan__: Given Tile.Size is insignificant, we set Tile.Size as default. However, we want to confirm TT Prev.type is better, so we will have only one condition where Prev.Type is set as AC. And we are interested to see whether our determination of ranges for Prev.Length and Prev.Type in the first round is correct.

With the interaction plot of Prev.Length vs. Match Score from the first run , we are interested to see how Browse.Time performs when Prev.Length set in the smaller value range. With the best performance at Prev.Length as 80 in the first run, we set Prev.Length at 30, 45 and 80 in the second run.

Still with the interaction plot above, the pattern for Match.Score is very obvious. Match Score is performing the best around 70. Therefore we can narrow down for Match.Score and make subtle changes around 70. We set Match.Score at 60, 75, 80. In addition, we need to fix the mistake we made in the first run where the three levels in Prev.Length did not match the three levels in Match.Score.

* __Data__: Prev.Length:[30, 45, 80] Match.Score:[60, 75, 80] Tile.Size: 0.2(default) Prev.Type[TT(9),AC(1)]

* __Analysis__: We firstly performed a full linear regression model analysis and observed that all betas are significant in the model. Then we are interested to see the interaction effect by the interaction plot.

<img width="482" alt="Screenshot 2024-10-06 at 3 04 51 PM" src="https://github.com/user-attachments/assets/205d8eb1-4242-4cda-b11c-71e3c53bcdd3">

From this interaction plot between Match.Score and Prev.Length, it is very clear that Browse.Time performs poorly when Prev.Length is at 30 and 45. And Browse.Time is performing the best when Prev.Length at 80 and we probably should explore higher values in Prev.Length. Regarding Match.Score, we confirm that the optimal value for Match.Score is around 80 and there is no big difference between Match.Score 75 and Match.Score.80.

* __Conclusion__: In the second run, we confirm that Match.Score’s optimal value is around 80 and narrow down the range for Prev.Length to be around 80 as well.

## Third Run

* __Question__: In this run we were interested in narrowing the range of Prev.Length and Match.Score on the basis of interaction plots and trends we saw from the second run.

* __Plan__: As we are already getting very low browsing time compared to our first run, in this experiment we wanted to narrow down our range further by choosing the values around the minimum values i.e for both prev length and match score between 50 and 80 that we found in the 2nd run. Also, in this experiment we wanted to verify that this range between 50 and 80 is correct as interaction plot showed in previous run that for one of match score the browsing time decreased with increase in prev length, so we also plan to pass a few combination where value are outside the range of 50 and 80 to confirm if browsing time is minimum in the selected range.

* __Data__: We choose Prev.Length range to be [60,75,80,90] and Match.Score range to be [60,72,75,80] for this experiment, as in the second run we were getting low browsing time with the interactions of Prev.Length at 80 and Match.Score at 75 so we chose these ranges around these two numbers numbers only.

* __Analysis__: With this range we get to see very clear interaction between prev.length and match.score, as match score decreases with increase in preview length the browse time decreases but it was not a very significant decrease. With this range we get a new minimum of Browsing Time at Prev.Length = Match.Score = 75 and Prev.Type = TT.

* __Conclusion__: Now we could try to further close to these values to find a more optimal combination but as the Browsing time is not decreasing by much, this means that we are very close to a global optimum. As such, we can be confident that we have found a global optimum. Below is a table outlining the top 5 final combinations tested and their associated browsing times.

<img width="870" alt="Screenshot 2024-10-06 at 3 06 28 PM" src="https://github.com/user-attachments/assets/01087374-87bf-4778-be8f-1721eb75860c">

## Conclusion

Our systematic exploration of the design space culminated in the discovery of the location and value of the optimum browsing time: [0.2, 75, 75, TT] for Tile Size, Match Score, Preview Length, and Preview Type, respectively. The optimum browsing time was approximately 10.186 minutes with a 95% confidence interval of [10.0077, 10.3643] at this location.

It is important to note, however, that our findings were subject to certain limitations:

* We could have used contour plots in combination with our other plots to get an even more reliable conclusion

* We had a relatively small sample size given we wanted to be as efficient as possible in terms of resources, but a larger sample size would have led to an even more confident conclusion

* Due to the cost of extracting data and running each experiment, there is likely still some distance to the global optimum
