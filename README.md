# ML_Feature_Engineering
Predicting Housing Prices with Feature Engineering: A Comprehensive Study

This project explores the impact of feature engineering on model performance in a tabular regression problem using the Ames Housing Dataset. The objective is to evaluate how different machine learning models perform on the dataset, both with and without feature engineering enhancements. We use several regression algorithms, including Linear Regression, Decision Tree, Random Forest, and Support Vector Regressor (SVR), to determine which models benefit most from engineered features.

Abstract

This study evaluates how feature engineering affects model performance in a regression task using the Ames Housing dataset. The dataset consists of 2,930 observations and 81 features, including both numerical and categorical variables. Initially, baseline models (Linear Regression, Decision Tree, Random Forest, and SVR) were trained on minimally processed data. After adding domain-specific features, handling missing values, and applying appropriate scaling, model performance was re-evaluated using RMSE (Root Mean Squared Error).

Key Findings:

Random Forest consistently outperforms other models and benefits the most from feature engineering.

Linear Regression and SVR experienced performance degradation after new features were added, likely due to underfitting in the expanded feature space.

Decision Tree models suffered from overfitting, but pruning using cost-complexity pruning (CCP) helped mitigate this issue.

SVR remained unstable even after hyperparameter tuning.

Background and Motivation

Predicting housing prices is crucial in real estate and investment planning. Given that tabular datasets often contain missing values, mixed data types, and complex interactions between features, feature engineering plays a significant role in enhancing the predictive power of machine learning models. By creating new meaningful features and transforming existing ones, feature engineering can help machine learning models uncover complex relationships within the data.

Problem Statement

This project investigates the following research questions:

How much performance improvement can be achieved through feature engineering?

Which models benefit the most from engineered features?

Which models are most suitable for predicting housing prices in this dataset?

Data Source

The dataset used in this project is the Ames Housing dataset available from the OpenML API.

Data Cleaning Steps

Handling Missing Values:

The Lot_Frontage feature had 0 values, which were replaced with the median of Lot_Frontage for each Neighborhood group. If a group had only one value, the global median was used instead.

Custom Transformer: LotFrontageTransform.

Encoding Categorical Variables:

Ordinal Variables: Ordinal values (qualitative and conditional) were encoded using the OrdinalEncoder with custom orderings defined in the ordinal_columns list.

Nominal Variables: One-hot encoding was applied to nominal variables, with unknown values ignored.

Scaling:

Numerical features were scaled using StandardScaler before applying encoding transformations.

Methodology

Models Used:

Linear Regression

Decision Tree Regressor

Random Forest Regressor

Support Vector Regressor (SVR)

Hyperparameters:

Decision Tree Regressor: The max_depth hyperparameter was set to None by default, which led to overfitting.

SVR: The regularization parameter C was initially set to 1.0, which caused underfitting.

Data Splitting:

The dataset was split using StratifiedShuffleSplit to avoid bias, especially considering the Quality of the house as a target variable.

Model Validation:

5-Fold Cross Validation was used with the cross_val_score method to assess model performance.

Results & Discussion
1. Impact of Feature Engineering:

After adding new features, tree-based models (Random Forest and Decision Tree) showed significant performance improvements.

Linear Regression and SVR experienced reduced performance, likely due to underfitting as the feature space became wider.

2. SVR Model Improvement:

Scaling the numerical features improved the training speed of SVR significantly, from 2 minutes to just 2 milliseconds.

3. Overfitting in Decision Tree:

The Decision Tree Regressor model exhibited strong overfitting due to the absence of depth limitation. By applying Cost-Complexity Pruning (CCP) with ccp_alpha = 7.701, the overfitting issue was resolved, leading to better model performance.

4. SVR Hyperparameter Tuning:

Increasing the C parameter of SVR (from 1.0 to 100) helped alleviate underfitting, resulting in improved performance.

5. Random Forest Performance:

The Random Forest model consistently outperformed other models and showed further improvement with feature engineering.

Hyperparameter tuning with Grid Search revealed that the default hyperparameters worked well without much need for adjustment.

Conclusion

Feature engineering significantly improves performance, especially for tree-based models (Random Forest and Decision Tree). While Linear Regression and SVR models did not benefit as much from additional features, their performance improved with better tuning of hyperparameters and scaling. The Random Forest model, in particular, demonstrated robustness and scalability, making it the best-performing model for this regression task.

Future Work

Investigating the use of more advanced feature selection methods to further enhance model performance.

Experimenting with other regression models, such as Gradient Boosting and XGBoost, for comparison.

Exploring automated machine learning (AutoML) tools for model optimization.
