# Project - Record Linkage Amazon

## Contents
* [Overview](#overview)
* [Background](#background)
    * [Datasets](#datasets)
    * [Preprocessing](#preprocessing)
* [Exploratory Data Analysis](#exploratory-data-analysis)
* [Building Model](#building-model)
* [Conclusion](#conclusion)

## Overview
Record linkage is becoming increasingly important in statistical and academic research. This technique seek to find links from multiple files that can increase the efficiency of data collection and enrich information by linking with another sources. In this project, 

* Using blocking algorithm to improve the computational time.
* Using machine learning model as baseline models to detect records.
* Using deep learning architecture to outperform the result.

## Background
Entity resolution is a information integration problem caused by identifying and linking different information sources. It is known as record linkage and deduplication ([Li & G 2013](https://www.sciencedirect.com/book/9780124047020/intelligent-systems-for-security-informatics)). The record linkage is a procedure to find links from multiple files that represent the same entity or identify in a single dataset ([Yancey 2004](https://www.semanticscholar.org/paper/Improving-EM-Algorithm-Estimates-for-Record-Linkage-Yancey/0143d09b47cc852df754ae4098723ba88d0293d0)). In computer science, record linkage is also known as data matching and this technique is becoming more and more common in statistical and academic research such as E-Commerce, health research and crime detection. 

Motivated by this, we want to build a link between Google and Amazon products datasets that compare shopping platforms to link products from multiple online shops. It can allow customers to see all offers from same products across different online shops. We use binary classifier to classify record pairs into matches and nonmatches, explore different methods to classify candidate record pairs and find a suitable model for datasets.

## Exploratory Data Analysis
### Datasets
In this report, we have two datasets one is from Amazon and one from Google. Five rows from each training dataset have been included in Figure 1 and Figure 2. Both of datasets are stored in many different formats that shows in Table 1. We can notice that date type of price in Google is object instead of float and there are missing values in some attributes in both datasets.

<img src="/image/amazon.JPG" width="800"/> 

<em>Figure 1: The product dataset for Amazon.</em>

<img src="/image/google.JPG" width="820"/> 

<em>Figure 2: The product dataset for Google.</em>

<table>
<tr><th>Amazon dataset </th><th>Google dataset</th></tr>
<tr><td>
  
| Column | Non-Null Count | Dtype |
|--|--|--|
| id | 1113 non-null | object |
| title | 1113 non-null | object |
| description | 1017 non-null | object |
| manufacturer | 1113 non-null | object |
| price | 1113 non-null | float64 |

</td><td>

| Column | Non-Null Count | Dtype |
|--|--|--|
| id | 2588 non-null | object |
| name | 2588 non-null | object |
| description | 2422 non-null | object |
| manufacturer | 192 non-null | object |
| price | 2588 non-null | object |

</td></tr> </table>

<em>Table 1: The attribute for datasets of Amazon and Google.</em>

### Preprocessing
In practice, many datasets contain noisy, inconsistent and missing data which may influence the result of analysis ([Christen 2012](https://www.springer.com/gp/book/9783642311635)). The conversion of dataset before analyzing is called preprocessing or data preparation. By doing this process, we can increase the usability of dataset and enrich the data quality. Int his project, we use some techniques and employ those in the following analysis.

1. Missing Values:
Records are incomplete that means some information is available. In record linkage, it is common to left the missing values instead of using the imputation technique ([Christen 2012](https://www.springer.com/gp/book/9783642311635)). Missing values also play an important role in classification method. In that way, we will fill in space into every missing values in both of datasets.

2.





## Building Model

## Conclusion
