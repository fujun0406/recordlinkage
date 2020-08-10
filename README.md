# Project - Record Linkage Amazon

## Contents
* [Overview](#overview)
* [Background](#background)
* [Exploratory Data Analysis](#exploratory-data-analysis)
    * [Datasets](#datasets)
    * [Preprocessing](#preprocessing)
    * [Feature Vectors](#feature-vectors)
* [Building Model](#building-model)
    * [Training Data](#training-data)
    * [Testing Data](#testing-data)
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

Then, we employ the recordlinkage.Compare class to measure the similarity between both datasets. The similarity distribution of negative and positive records in Figure 4. There are a lot of missing values in manufacturer causing the most of feature vectors of manufacturer are 0. We can see that the pairwise relationships for the dataset in Figure 5 and there is no specific relationship between each variables. 

<img src="/image/similarity_negative.png" width="410"/> <img src="/image/similarity_positive.png" width="410"/> 

<em>Figure 4: The similarity distribution of negative and positive records.</em>

<img src="/image/pairplot.png" width="500"/> 

<em>Figure 5: Pair plot of feature vectors.</em>

## Building Model
We split the dataset into 20 percent as validation dataset, and we standardize features and train our models on 80 percent of the dataset. In this section, we choose decision tree and K-means methods to fit model. Decision trees is supervised learning and this method is to segment the feature space into a number of smaller, simpler, non-overlapping regions and K-means is unsupervised learning and aims to find a set number clusters. Then, we try to use deep learning technique to outperform the result (the model architecture shows in Figure 6).

<img src="/image/deep_learning.JPG" width="300"/> 

<em>Figure 6: Simple Neural network architecture.</em>

### Training Data
The result of validation dataset shows in Table 2. It shows that the accuracy rate for deep learning model is close the decision trees model and precision is 0.0332 which is also lesser than the decision tree model but higher Kmeans. Compared with the recall, the deep learning model is the highest having 0.9495.

| Method | Accuracy | Precision | Avg. Precision | Recall | F1 score |
| ----------- | ----------- | ----------- | ----------- | ----------- | ----------- |
| Decision Tree | 0.9976 | 0.5098 | NA | 0.2626 | 0.3467 |
| K-means (K=2) | 0.8012 | 0.0077 | NA | 0.6364 | 0.0154 |
| Deep Learning | 0.9325 | 0.0332 | 0.3554 | 0.9495 | 0.064 |

<em>Table 2: The performance of models classifiers on the blocking dataset. (optimal threshold for deep learning is 0.448849)</em>

We can check the history of of precision, recall, accuracy and loss plot for training and validation datasets display in Figure 7. That indicate that our deep learning model is enough for convergence. We employ [Youden (1950)](https://pubmed.ncbi.nlm.nih.gov/15405679/) technique to find optimal threshold for deep learning model is 0.448849. More details about precision recall curve and ROC curve show in Figure 8. The ROC curve indicates the distribution of positive and negative class. It shows that two distributions are overlap and AUC is 0.972 which means there is 97.2% chance that model will be able to distinguish between positive class and negative class.

<img src="/image/precision_recall.png" width="600"/> 
<img src="/image/acc_loss.png" width="600"/> 

<em>Figure 7: : Checking training history.</em>

<img src="/image/precicsion_call_plot.png" width="400"/> <img src="/image/roc.png" width="300"/> 

<em>Figure 8: The precision recall curve and ROC curve.</em>

### Testing Data
After building up model, we employ the deep learning model on testing dataset. The testing datasets include the same attributes as training dataset. The all pairs of testing dataset is 159500 (= 250 × 638) since the number of records in Amazon and Goggle testing dataset are 250 and 638 respectively. By using recordlinkage.Compare class, we canmeasure the similarity for all pairs records. The result show in Table 3. The precision recall curve and ROC curve show in Figure 9 and it shows that the performance of data matching is acceptable.

| | Accuracy | Precision | Avg. Precision | Recall | F1 score |
| ----------- | ----------- | ----------- | ----------- | ----------- | ----------- |
| Testing dataset | 0.8267 | 0.0077 | 0.3768 | 0.9103 | 0.0152 |

<em>Figure 3: The performance of testing dataset. (optimal threshold for deep learning is 0.072108)</em>

<img src="/image/testing_AP.png" width="400"/> <img src="/image/testing_roc.png" width="300"/> 

<em>Figure 8: The precision recall curve and ROC curve.</em>

We can get a confusion matrix in Table 4 and Figure 9 and it show that the stability of identifying positive and negative records are quite sensitive.

| | Predicted Negative | Predicted Positive | 
| ----------- | ----------- | ----------- | 
| Actual Negative | 131644 | 27622 | 
| Actual Positive | 21 | 213 | 

<em>Table 4: The confusion matrix for testing dataset.</em>

<img src="/image/testing_cm.png" width="400"/>

<em>Figure 9: The normalized confusion matrix. (each elements are divided the sum of row which is the actual observations)</em>

## Conclusion
To conclude despite the fact that we only use a simple deep learning model in this report, it still provides many information about linking records between Amazon and Google dataset. Compared with K-means and decision tree model, deep learning model gives an outperformed result. But we only try a simple architecture of neural network. As far as for future research, we can try to explore different architectures of deep learning model or other machine learning techniques on datasets. [Christen (2012)](https://ieeexplore.ieee.org/document/5887335) indicates the importance of indexing techniques. We can also explore difference indexing techniques to improve the performance of model.
