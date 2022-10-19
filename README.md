# Brain_Cancer_ML

#### Purpose: 

The intent of this project is not only to examine how well three python classifiers (DecisionTreeClassifier, LogisticRegressor, and RandomForestClassifier) perform, but to understand which one performs best and why. To do this, each classifier will be employed on a dataset containing gene expression levels of patients. These expression levels come from number of patients diagnosed with brain cancer. 
#### Significance: 

One goal of the this project is to create a model with accurate performance, however, there is significance beyond measuring accuracy. Every cancer is different on a genetic level. Consequently, each cancer is unique and require varying treatment strategies and techniques. Therefore, creating a model to asses which type of cancer is present and which genes lead to that type of cancer is wildly important in terms of treatment success. 
#### Research Question:

This project seeks to answer two research questions:
- How accurately do DecisionTreeClassifier, LogisticRegressor, and RandomForestClassifier predict cancer type?
- How do the feature importances of the best performing model line up with the significant genes evaluated in the data exploration?
#### Dataset:

The dataset was downloaded from Kaggle. It contains samples of 130 patients of which roughly 90% have some type of brain cancer. This information is contained in the ‘type’ variable, which has categorical values of either Ependymoma, Glioblastoma, Medulloblastoma, Pilocytic Astrocytoma, Normal (non-cancerous). The dataset also contains expression levels of 54,675 genes. These values are all non-negative. For each of the models, the output variable will be the cancer type, while the input variable will be the expression levels of the genes. 

#### Data Preprocessing:

Thankfully, the dataset used in this project was extremely clean and contained no errors or missing values. The only preparation necessary for the models was scaling. A MinMaxScaler() was used in order to maintain the positive values of gene expression. The data was split using a 60/40 split, in order to maintain a large enough testing set (see code snippet 1.1). 
#### Exploratory Data Analysis:

Exploration of this dataset was rather unique. First, the distribution of the output variable was examined (see figure 1.1). The counts were not entirely equal, but seemed to be normally distributed. For exploring the input variable, rather than using all 50,00+ genes, only “Gene’s of Interest” were explored. For each cancer type, the expression levels of each gene was compared its expression levels in the remaining cancer types using a t-test. If the t-test had a value below 0.0001 and the means of expression levels differed by 7.5 times the standard deviation, that gene was considered to be a “Gene of Interest” (see code snippet 1.2). From this process, 17 genes were selected. These genes were visualized by cancer type via box plot and histogram (see figures 1.2 and 1.3). The correlations of these genes were also plotted (see figure 1.4). The box plot and distributions suggested that Ependymoma was to be most unique from all types in terms gene expression. However there were a number of genes where all four cancer types differed from normal tissue. There also seemed to be some genes that were highly correlated. This is to be expected seeing that genes relate in function and interact with one another.  

#### Model Building and Evaluation
Each model was built with the training sets and a random state of 42. The max_iter of the LogisticRegressor was set to 500 to ensure convergence (see code snippet 2.1 and figure 2.1 for model building and accuracy). Since the RandomForestClassifier performed the best, this model was used in a GridSearch (see code snippet 2.2 for grid_params). The best model increased the overall accuracy by ~2% (see code snippet 2.3 and figure 2.2 for accuracy). See table 1.1 for a comparison table of of each model. 

#### Conclusion
After model building and tuning, the models seemed to perform well. The worst model (Decision Tree) still performed fairly well and had an accuracy rating of over 88%. The best model (Random Forest) had an accuracy of 94%. In terms of its feature importances, only two of the genes (1569186_at, 220156_at) in the RandomForest model matched with the “Genes of Interest” found in the EDA (see figure 3.1 for feature importances). This project proved Random Forest, once again, to be the best classifier. Random Forest often performs extremely well due to the number of trees it creates. Because of its constant success, it should be recommended as the classifier to use in cases when accuracy is highly important. 
