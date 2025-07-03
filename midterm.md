# Project Midterm: Team 38
*Annabelle Xie, Alex Latz, Anthony Nguyen, Pennon Shue, Rohan Karthik*
## Introduction/Background

The increase in internet access by adolescents in recent years has led to a significant rise in problematic internet use (PIU): the excessive use of the internet that interferes with daily life. Studies suggest that a Preference for Online Social Interaction (POSI) and those using the internet to regulate emotions can lead to compulsive internet use and negative outcomes \[6\], \[7\], \[5\]. Evidence also shows that poor physical health is associated with excessive screen time \[10\]. However, there is limited attention on physical activity as a PIU predictor.

The Healthy Brain Network has compiled a dataset from roughly 5,000 participants aged 5 to 22, capturing physical activity and internet behavior data. Fitness data includes medical measurements, fitness assessments, bio-electric impedance analysis, and actigraphy series data, while internet usage is measured through usage reports and a parent-child internet addiction test. Each participant has an associated Severity Impairment Index (SII), a standard for measuring problematic internet use.

Dataset:
<https://www.kaggle.com/competitions/child-mind-institute-problematic-internet-use/data>

## Problem Definition

PIU is a growing concern in the digital age and a contributor to mental health issues especially in adolescents whose brains are more vulnerable \[10\], \[8\]. Prolonged PIU habits can exacerbate mental health challenges and disrupt social and emotional learning.

COVID-19 has intensified this issue, with studies showing a sharp rise in PIU symptoms from a pre-pandemic rate of 10-14% to 40% \[2\], \[4\], as children rely more on online platforms for social interaction. Current PIU diagnosis methods require clinical intervention and lack early diagnosis. With PIU now affecting nearly half of adolescents, there’s a critical need for accessible tools to predict PIU risk and promote healthier digital habits \[3\]. This project aims to provide a scalable solution for early intervention in young populations.

## Methods

### Data Preprocessing 

1. Missing Data Handling:
    1. Removal of Features: We decided to remove columns such as identifiers (‘id’), each PCIAT score (‘PCIAT-PCIAT_##’) with the exception of the total PCIAT score, and any seasonal attributes (“Basic_Demos-Enroll_Season”) that don’t contribute to prediction. Additionally, columns with over 45% missing data were removed. This ensures that the model doesn’t attempt to impute excessively incomplete data, which could introduce noise.
    2. Imputation: The ‘KNNImputer’ was chosen due to its ability to fill in missing values based on similarity to closest neighbors. ‘KNNImputer’ uses patterns in the data to provide more accurate estimates, unlike simpler imputation methods that might fill missing values with the mean or median. The labeled data in the training dataset is imputed first, and the patterns are used to fill in missing values for features in the untrained data. A similar imputation process is also done to the test dataset, ensuring that it is consistent with the training data.
2. Handling Imbalanced Data
     1. SMOTE was applied to address class imbalances in the training data, ensuring that underrepresented classes are sufficiently represented. By generating synthetic samples without altering distribution of the majority class or removing any original data points, SMOTE reduces the risk of overfitting and increases generalizability of the model. 

### ML Algorithms

1. K-Means Clustering (Unsupervised):
After generating pseudo-labels with RF, KNN was applied to validate these labels. We used KNN to assign labels by examining labels of nearby samples. We compared the pseudo-labels from RF with those predicted by KNN to assess consistency between models and validate the pseudo-labels. The KNN model was trained on labeled data, using k = 5 as the number of neighbors for majority voting, and data on accuracy, precision, recall, and F1-score metrics were calculated across classes. We chose KNN due to its simplicity and effectiveness in classification based on proximity. Additionally, KNN is flexible in its handling of pseudo-labeled data, which was useful in our scenario of partially missing data.
2. Random Forest Classifier (Supervised):
RF was used to classify labeled data in the training set and to generate pseudo-labels for the unlabeled subset. The labeled subset was used to train an RF classifier. RF is especially useful because it can handle complex patterns and helps interpret the contributions of different features. We chose RF because of its ability to handle complex, non-linear relationships and enhance accuracy and reduce overfitting. Once trained, the RF classifier was used to predict labels (pseudo-labels) for the unlabeled subset, “filling in” the missing labels based on learned patterns. 

## Results/Discussion
### KNN Classifier:
1. Quantitative Metrics:
    1. Labeled Data Only: KNN shows a high accuracy of around 87% when tested on labeled data alone, with strong performance on the majority class (0.0) but weaker on minority classes (class/sii 2.0 and 3.0). Specifically, class 3.0 has a low recall (0.25) and F1-score (0.36), highlighting difficulty in correctly identifying minority classes.
    2. Mixed Pseudo Label/Labeled Data: When including pseudo labeled data in the test set, KNN’s accuracy remains high. However, class 2.0 has an unusually high recall (1.0) but very low precision (0.22), suggesting that KNN may be overfitting to certain patterns in pseudo labeled data.
2. PCA Visualizations:
    1. Labeled Data: The PCA plot shows clusters with overlap, particularly between classes 0.0 and 1.0, indicating that KNN captures some separation but struggles with boundary regions, which affects minority class accuracy.
![PCA of Labeled KNN](/docs/assets/KNN_labeled.png)

    3. Pseudo Labeled Data: The pseudo labeled data visualization shows KNN predicting many samples as class 0.0, consistent with its tendency to rely on majority class predictions.
![PCA of Unlabeled KNN](/docs/assets/KNN_unlabeled.png)

    5. Combined Data: The combined data plot demonstrates that KNN benefits from pseudo labels, capturing additional patterns that improve its performance on a broader dataset.
![PCA of Combined KNN](/docs/assets/KNN_combined.png)
3. After SMOTE: 
    1. For minority classes, precision and recall have improved. However, the F1-score remains lower for this minority class 3.0, indicating there is still room for improvement in capturing the minority classes fully.
    2. The macro average F1-score improved to 0.79, and the weighted average F1-score is now 0.86, showing a more balanced performance across classes.
4. Overall Analysis: KNN performs better on mixed data because of its flexibility with pseudo labels, showing a high accuracy for majority classes. However, it has significant class imbalance issues, particularly in precision and F1-score for minority classes. Though once we applied SMOTE, our results significantly improved the recall and F1-scores for minority classes, particularly on synthetic labels, making the model more reliable for diverse predictions. However, KNN’s reliance on proximity may still lead to some overfitting in regions dominated by the majority class.

### Random Forest Classifier:
1. Quantitative Metrics:
    1. Labeled Data Only: There’s a 87% accuracy on labeled data, with robust performance on class 0.0, where it achieves a precision of 0.92 and recall of 0.95. However, minority classes (class 3.0) show much lower scores (recall of 0.25 and F1-score of 0.36).
    2. Mixed Pseudo Label/Labeled Data: RF performs well on mixed data, with balanced accuracy and strong metrics for the majority class. However, minority classes remain challenging, with poor precision and recall, indicating that the model leans heavily toward the majority class even with pseudo labels.
2. PCA Visualizations:
    1. Labeled Data: The PCA plot shows clear clusters, with some overlap between classes 0.0 and 1.0, but Random Forest provides more distinct separation than KNN, particularly for the majority class.
![PCA of Unlabeled RF](/docs/assets/RF_labeled.png)
    3. Pseudo Labeled Data: The pseudo labeled data plot reveals that Random Forest, like KNN, predicts many samples as class 0.0, indicating a majority class bias.
![PCA of Unlabeled RF](/docs/assets/RF_unlabeled.png)
    5. Combined Data: Random Forest captures more defined clusters compared to KNN, but still has some class imbalance tendencies.
![PCA of Combined RF](/docs/assets/RF_combined.png)
4. After SMOTE: 
    1. Random Forest achieves near-perfect accuracy (100%), with most metrics at or close to 1.0 for all classes. Only sii 3.0, has a recall of 0.80. For minority classes like class 2.0, SMOTE has enhanced performance significantly.
    2. The macro average F1-score is 0.97 and the weighted average F1-score is 1.0 which shows a very balanced pre-processing labeling performance.
5. Overall Analysis: Random Forest performs strongly on labeled data, effectively capturing complex patterns. However, it faces issues with class imbalance, impacting its recall and F1-scores for minority classes. Random Forest’s structured learning approach makes it more consistent on labeled data but less flexible with pseudo labels compared to KNN. Its performance improved dramatically after SMOTE, achieving near-perfect accuracy and robust performance across all classes. One issue to note is that with using pure Random Forest preprocessing, our pseudo labels are most likely being overfitted, as the result metrics are almost all 1.0 across the board. 

## Next Steps:
1. Preprocessing:
    1. Overfitting during pseudo labeling can create overly confident labels that may not generalize well, even with SMOTE balancing the data. In the future, we want to create balanced pseudo labels without overfitting.
    2. Random Forest also runs the risk of overfitting given that accuracy is nearly at 100%. Future work should include cross-validation and testing on unseen data to ensure model robustness.
2. Model: Logistic Regression with Regularization
    1. Logistic Regression is a simple linear model, less likely to overfit, especially when adding ridge regression. L2 regularization will penalize overly complex models and reduce the influence of noisy pseudo labels from the overfit Random Forest.
    2. In addition, Logistic Regression doesn’t require a large amount of data to perform well and is less prone to overfitting than complex models, which would work well for our data set.

**References:**

\[1\] M. A. Moreno, “Problematic internet use among US youth,” Archives of Pediatrics &amp; Adolescent Medicine, vol. 165, no. 9, p. 797, Sep. 2011. doi:10.1001/archpediatrics.2011.58

\[2\] Ł. Tomczyk, M. Szyszka, and L. Stošić, “Problematic internet use among youths,” Education Sciences, vol. 10, no. 6, p. 161, Jun. 2020. doi:10.3390/educsci10060161

\[3\] M. J. Guralnick, “Why early intervention works,” Infants &amp; Young Children, vol. 24, no. 1, pp. 6–28, Jan. 2011. doi:10.1097/iyc.0b013e3182002cfe

\[4\] F. W. Paulus et al., “Problematic internet use among adolescents 18 months after the onset of the COVID-19 pandemic,” Children, vol. 9, no. 11, p. 1724, Nov. 2022. doi:10.3390/children9111724

\[5\] R. LaRose, C. A. Lin, and M. S. Eastin, “Unregulated internet usage: Addiction, habit, or deficient self-regulation?,” Media Psychology, vol. 5, no. 3, pp. 225–253, Aug. 2003. doi:10.1207/s1532785xmep0503_01

\[6\] S. E. Caplan, “Theory and measurement of generalized problematic internet use: A two-step approach,” Computers in Human Behavior, vol. 26, no. 5, pp. 1089–1097, Sep. 2010. doi:10.1016/j.chb.2010.03.012

\[7\] S. E. Caplan, “A social skill account of problematic internet use,” Journal of Communication, vol. 55, no. 4, pp. 721–736, Dec. 2005. doi:10.1111/j.1460-2466.2005.tb03019.x

\[8\] M. M. Spada, “An overview of problematic internet use,” Addictive Behaviors, vol. 39, no. 1, pp. 3–6, Jan. 2014. doi:10.1016/j.addbeh.2013.09.007

\[9\] Published by Ani Petrosyan and A. 19, “Internet and social media users in the world 2024,” Statista,<https://www.statista.com/statistics/617136/digital-population-worldwide/#:~:text=Published%20by%20Ani%20Petrosyan%2C%20Aug,less%20than%20that%20of%20men>

\[10\] A. Restrepo et al., “Problematic internet use in children and adolescents: Associations with psychiatric disorders and impairment,” BMC Psychiatry, vol. 20, no. 1, May 2020. doi:10.1186/s12888-020-02640-x

## Gantt Chart

| **TASK TITLE** | **TASK OWNER** | **START DATE** | **DUE DATE** | **DURATION** |
| --- | --- | --- | --- | --- |
| Project Proposal | All | 10/1/2024 | 10/4/2024 |  3 |
| Introduction & Background | Rohan | 9/27/2024 | 10/4/2024 | 7   |
| Problem Definition | Pennon | 9/27/2024 | 10/4/2024 | 7   |
| Methods | Annabelle | 9/27/2024 | 10/4/2024 | 7   |
| Potential Results & Discussion | Tony | 9/27/2024 | 10/4/2024 | 7   |
| Video Recording | Alex | 9/27/2024 | 10/4/2024 | 7   |
| GitHub Page | Rohan | 9/27/2024 | 10/4/2024 | 7   |
| **Model 1** |     |     |     |     |
| Data Sourcing and Cleaning | Annabelle/Pennon | 10/5/2024 | 10/10/2024 | 5   |
| Model Selection | Tony | 10/10/2024 | 10/12/2024 | 2   |
| Data Pre-Processing | Tony/Alex | 10/12/2024 | 10/18/2024 | 6   |
| Model Coding | Rohan/Alex | 10/18/2024 | 10/28/2024 | 10  |
| Results Evaluation and Analysis | Annabelle/Pennon | 10/28/2024 | 11/2/2024 | 4   |
| Midterm Report | All | 11/2/2024 | 11/8/2024 | 6   |
| **Model 2** |     |     |     |     |
| Data Sourcing and Cleaning | Annabelle | 10/28/2024 | 11/3/2024 | 5   |
| Model Selection | Alex | 11/3/2024 | 11/5/2024 | 2   |
| Data Pre-Processing | Rohan | 11/5/2024 | 11/11/2024 | 6   |
| Model Coding | Tony | 11/11/2024 | 11/21/2024 | 10  |
| Results Evaluation and Analysis | Pennon | 11/21/2024 | 11/25/2024 | 4   |
| **Model 3** |     |     |     |     |
| Data Sourcing and Cleaning | Rohan | 10/28/2024 | 11/3/2024 | 5   |
| Model Selection | Tony | 11/3/2024 | 11/5/2024 | 2   |
| Data Pre-Processing | Pennon | 11/5/2024 | 11/11/2024 | 6   |
| Model Coding | Annabelle | 11/11/2024 | 11/21/2024 | 10  |
| Results Evaluation and Analysis | Alex | 11/21/2024 | 11/25/2024 | 4   |
| **Evaluation** |     |     |     |     |
| Model Comparison | All | 11/25/2024 | 12/3/2024 | 8   |
| Presentation | All | 11/25/2024 | 12/3/2024 | 8   |
| Recording | All | 11/25/2024 | 12/3/2024 | 8   |
| Final Report | All | 11/25/2024 | 12/3/2024 | 8   |

![Gantt Chart](/docs/assets/ganttchart.png)

## Contribution Table

| **Name** | **Proposal Contributions** |
| --- | --- |
| Rohan Karthik | Model Coding, Results/Discussion, Visualizations  |
| Alex Latz | Model Selection, Data Preprocessing, Model Coding  |
| Anthony Nguyen |  Model Selection, Data Preprocessing, GitHub Pages  |
| Pennon Shue | Data Sourcing and Cleaning, Midterm Writeup, Results Evaluation and Analysis  |
| Annabelle Xie | Data Sourcing and Cleaning, Midterm Writeup, Results Evaluation and Analysis |
