# ML_Feature_Engineering
#Abstract 
This project evaluates how feature engineering influences model performance on a 
tabular regression problem using the Ames Housing dataset. The dataset contains 2,930 
observations and 81 features, including both numerical and categorical variables. Initially, 
baseline models (Linear Regression, Decision Tree, Random Forest, and SVR) were 
trained on minimally processed data. Afterward, several new domain-related features 
were added, missing values were handled, and proper scaling was applied to relevant 
models. Model performance was compared using RMSE metrics. Results show that 
Random Forest consistently performs best among all models and benefits the most from 
feature engineering. Linear Regression and SVR demonstrate reduced performance after 
adding new features, likely due to underfitting in the expanded feature space. Decision 
Tree suffers from strong overfitting, while SVR remains unstable even after 
hyperparameter tuning. Decison Tree pruned with cost coplexity pruning alpha 7.701 did 
not overfit the data. Overall, feature engineering significantly improves tree-based models 
but does not enhance linear or kernel-based models. Recommendations for future work 
and improvements conclude the report. 
#Background and Motivation 
Predicting housing prices is an important task in real estate, investment planning, 
and 
property assessment. Tabular datasets often include complex interactions, missing values, 
and mixed feature types. Feature engineering—creating new meaningful variables and 
transforming existing ones—can enhance the ability of machine learning models to learn 
these relationships. 
#Problem Statement 
This project aims to systematically compare baseline machine learning models with 
improved versions enhanced through feature engineering. Specifically, the research tasks: 
1. How much performance improvement can be achieved through feature 
engineering? 
2. Which models benefit most from engineered features? 
3. Which methods are most suitable for this dataset? 
#Data source 
Ames dataset from openml api 
#Data cleaning steps 
1- there was no null values but there were 0 values in Lot_Frontage, 
they were replaced with median values of Lot_Frontage features grouped by 
Neighborhood feature, 
and if ther were no median for that group(one value) they vere replaced by global 
medina of Lot_Frontage. 
Done by creating custom transformer LotFrontageTransform 
2 - Ordinal values(qualitive and conditional) were encoded by OrdinalEncoder 
with orders provided in "ordianl_columns" list 
3 - nominal values were encoded by OneHotEncoder and unkonw values were 
İgnored 
4 - StandardScaler transformer were applyed to numerical values before 
encoding categorical values 
Methodology 
1 - 4 models were used LinearRegression, DecisionTreeRegressor, 
RandomForest and SVR(suppoer vector machine regressor) 
2 - DecisonTreeRegressor max_depth hyperparameter were set by default to 
None which ment than were no limit to depth(cause of overfitting) 
3 - SVR had default paramter C set to 1.0 which is high regularization which is 
why it was performing poor becuase of underfitting 
4 - dataset was split by StratifidShuffleSplit which prevent from bias(in our case 
for quality of house)
5 - validation was done by 5 fold crossvalidation with cross_val_score
#Results & Discussion 
1 - After adding new features tree based models improved in performance while linear 
and svr got worse probably becuase of data space got wieder and model underfit
2 - After scaling numerical values SVR became much faster to train(from 2 minutes to 2 
ms)  
3 - From how tigh Decison Tree fits the data and how it performes we can deduce that 
model overfits which is expected for this dataset and not setting max depth
4 - To solve the problem of decision tree overfitting we used CCP(cost complexity 
prunning and got ccp_alpha=7.701 hyperparameter which is how much to penalize the 
number of leafs) which made model perform better and not overfit anymore.
5 - By increasing "C" hyperparamter of SVR which by default was 1.0 which is high 
regularization to 100 it performedd better 6 - Random Forest performed the best from the 
get go and got better after adding new features. Hyperparameter tunning whith grid search 
showed that default hyperparametes were good enough.
