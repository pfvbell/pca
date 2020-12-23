# Using PCA with high-demensionality data to predict cancer types

High dimensionality is one aspect of big data. Using a big data set with over 7000 predictors I will build several classification models to distinguish between two related classes of cancer, acute lymphoblastic leukemia (ALL) and acute myeloid leukemia (AML), using gene expression measurements. Each row in this file corresponds to a tumor tissue sample from a patient with one of the two forms of leukemia. 

The first column contains Cancer_type: 0 = ALL class and 1 = AML class
Columns 2-7130 contain expression levels of 7129 genes recorded from each tissue sample
The last column Cancer_subtype additionally distinguishes between two subtypes of ALL, subtype T and subtype B (used in problem 5): 0 = ALL subtype T, 1 = ALL subtype B, 2 = type AML.

## EDA

Data was prepared and scaled using min-max scaling. Below we can see the distribution of the AML and ALL classes across the training set.

![](https://github.com/pfvbell/pca/blob/main/Training%20set%20dist.png)


# Principal Component Analysis

Visualising using PCA allows us to visualise high-dimensional space in low-dimensional space. It would be very difficult to visualise 7129 dimensions, however using PCA we can visualise high-dimensional datasets. This gives a much faster understanding of the nature of the way in which predictors can distinguish between the two classes.

![](https://github.com/pfvbell/pca/blob/main/Visualising%20PCA.png)

We can see that 250 principal components are needed to explain 90% of the variability in the data.

![](https://github.com/pfvbell/pca/blob/main/PCA%20variance.png)

Cycling through different numbers of PCs we see that the accuracy on the testing set improves with an increase in PCAs from 2 to 50, however, decreases with use of 250 PCAs. The training set accuracy also increases with an increased number of PCs from 2 to 50. The training set, however, reaches 100% accuracy with 250 PCs, which suggests overfitting. Subsequently we use cross-validation to pick the best PC number.

#Multi-nomial prediction of cancer type

Cancer sub-type was predicted using a multi-nomial logistic regression. Again, cross-validation was used to explore the best number of PCs. We plot the decision boundaries below for the two final models. The first is a ridge-like regularised model and the second is also a ridge-like regularised model, which also includes an interaction term and quadratic term.

![](https://github.com/pfvbell/pca/blob/main/decision%20boundary.png)

![](https://github.com/pfvbell/pca/blob/main/pca_ridge_quadratic.png)



