# Project Proposal: Team 38
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
    1. Imputation: We will use scikit-learn’s SimpleImputer for missing values (mode for categorical, mean/median for numerical) and KNNImputer for non-random missing data.
2. Time Series Aggregation: For accelerometer data, we will apply sliding window aggregation using pandas or tsfresh and Fourier Transforms (FFT) to capture periodic patterns.
3. Normalization: We will standardize features using scikit-learn’s StandardScaler to ensure consistent scaling.
4. Handling Missing Labels:
    1. Approaches include deletion (if minimal impact), imputation (pseudo-labeling), data augmentation, re-weighting for class imbalance, and semi-supervised learning.

### ML Algorithms

1. K-Means Clustering (Unsupervised):
    1. K-Means will be used to cluster and assign pseudo-labels to unlabeled data based on feature similarity. We’ll assess cluster quality using the silhouette coefficient.
    2. Class: KMeans from scikit-learn.
2. Random Forest Classifier (Supervised):
    1. Random Forest will be employed for its robustness in handling missing data and continuous features.
    2. Class: RandomForestClassifier from scikit-learn.
3. Logistic Regression (Supervised):
    1. Logistic Regression will provide a baseline for binary classification, particularly suited to our labeled data subset.
    2. Class: LogisticRegression from scikit-learn.

## Results/Discussion

1. **Accuracy, Precision, Recall, F1-score:** We aim for 80-90% accuracy in our classification model to effectively identify individuals at risk of PIU, minimizing false positives and negatives, especially in our random forest implementation.
2. **Quadratic Weighted Kappa (QWK):** For evaluating the agreement between predicted and actual SII scores, a high score will indicate that the model is robust and reliable in predicting PIU severity.
3. **Silhouette coefficient:** Assesses label imputation accuracy, especially for unsupervised methods (K-means clustering).

We aim to accurately predict the SII and identify early signs of PIU using physical activity and related data, enabling timely interventions promoting healthier habits.We expect high prediction accuracy (measured by QWK) and will identify key factors contributing to PIU, such as physical activity, age, and gender.

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
| Data Sourcing and Cleaning | Pennon | 10/5/2024 | 10/10/2024 | 5   |
| Model Selection | Annabelle | 10/10/2024 | 10/12/2024 | 2   |
| Data Pre-Processing | Tony | 10/12/2024 | 10/18/2024 | 6   |
| Model Coding | Alex | 10/18/2024 | 10/28/2024 | 10  |
| Results Evaluation and Analysis | Rohan | 10/28/2024 | 11/2/2024 | 4   |
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
| Rohan Karthik | Results Discussion, Editing    |
| Alex Latz | Methods, Editing, GitHub Pages    |
| Anthony Nguyen |  Introduction, Video Proposal, Editing   |
| Pennon Shue | Results Metrics, Video Proposal, Gantt Chart  |
| Annabelle Xie | Problem Definition, References |
