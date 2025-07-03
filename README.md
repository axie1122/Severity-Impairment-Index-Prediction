# Machine Learning Project Repository

This repository contains all relevant files and directories for the machine learning project, including data processing, model implementations, and visualizations.

## Directory Structure and File Descriptions

### Directories:
/docs/assets/: Folder to store images for reports

### Files:
/docs/assets/KNN_labeled.png: PCA visualization of the KNN classifier on labeled data, showing clusters with overlap, especially between classes 0.0 and 1.0.

/docs/assets/KNN_unlabeled.png: PCA visualization of the KNN classifier on pseudo-labeled data, showing heavy reliance on the majority class predictions (class 0.0).

/docs/assets/KNN_combined.png: PCA visualization of the KNN classifier on combined labeled and pseudo-labeled data, illustrating improved patterns with additional data.

/docs/assets/RF_labeled.png: PCA visualization of the Random Forest classifier on labeled data, demonstrating more distinct class separations compared to KNN.

/docs/assets/RF_unlabeled.png: PCA visualization of the Random Forest classifier on pseudo-labeled data, showing similar majority class bias as observed in KNN.

/docs/assets/RF_combined.png: PCA visualization of the Random Forest classifier on combined labeled and pseudo-labeled data, showcasing better-defined clusters.

/docs/assets/GMM_labeled.png: PCA visualization of the GMM classifier on labeled data, demonstrating higher performance than RF or KNN on class 3.0.

/docs/assets/True_labeled.png: PCA visualization of the true labeled data

/docs/assets/ganttchart.png: Gantt chart for project management

### Data Files:
/train.csv: The training dataset used for fitting the machine learning models.
/test.csv: The testing dataset used for evaluating the performance of the models.

### Notebooks:
/ML_project.ipynb: The Jupyter notebook containing all data processing steps, machine learning model implementations, performance metrics, and visualizations.

## Summary
This repository contains all necessary resources for replicating the analyses and visualizations presented in the project. The models, including KNN, Random Forest, and GMM classifiers, are evaluated on labeled, pseudo-labeled, and combined datasets, with visualizations and metrics provided in the respective directories and files.
