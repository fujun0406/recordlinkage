# Project - Record Linkage Amazon

## Contents
* [Overview](#overview)
* [Background](#background)
* [Exploratory Data Analysis](#exploratory-data-analysis)
    * [Datasets](#datasets)
    * [Preprocessing](#preprocessing)
    * [Feature Vectors](#feature-vectors)
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

2. Cleaning Dataset:
Cleaning and removing unwanted texts, whitespace or brackets may increase your record linkage accuracy. In this step, we will clean string or numerical information for both dataset excluded the column of id. This process involves the removal of special characters, convert upper characters to lower characters and remove stopwords such as ”the”, ”on”, ”is” etc. We also remove morphological affixes from words and leave only the word stem. By using this way, it will reduce of record complexity and help to detect the matching. Furthermore, we will change data type of price in Google to float and change the column name to be consistent.

3. Blocking: 
Blocking is a linking method which can enhance computation efficiency. This technique in some way remove all record pairs that are not good candidates for linking ([Newcombe et al.1959](https://science.sciencemag.org/content/130/3381/954)). In this project, we employ sorted neighbourhood blocking algorithm that is not sensitive to misspell issue.

4. Comparing Information:
After reducing complexity of datasets, we use the class recordlinkage.Compare() in Python compute the similarity between two strings. In this project, we use Jaro-Winkler method to compare string and Gaussian algorithm to comapre the numerical information. Then, we can get feature vectors.

### Feature Vectors
All pairs records is 2880444 (= 1113 × 2588) since the number of record in Amazon dataset is 1113 and 2588 in Goggle dataset. There are 2879378 negative samples and 1066 positive samples. By using sorted neighbourhood blocking algorithm, we can create blocking record pairs and utilize title as sorting key. It shows that there are 203087 blocking record pairs having 202564 negatives and 523 positives (Figure 3) that is unbalanced dataset. 

<img src="/image/is_duplicate.jpg" width="500"/> 

<em>Figure 3: The distribution of blocking samples.</em>
## Building Model

## Conclusion
