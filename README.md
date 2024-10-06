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


