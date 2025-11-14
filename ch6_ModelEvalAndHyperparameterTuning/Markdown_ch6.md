# Chapter 6 - Learning Best Practices for Model Evaluation and Hyperparameter Tuning
## Section 1 - Streamlining Workflows with pipelines
*
	Think of pipelines as an estimator wrapper.  In this example, use the pipeline wrapper to scale the data using StandardScalar(), feed that into a PCA dimension reduction
	operator (we set n_components=2) then fit the scaled data using the first 2 principal components to a logistic regression model.
	
## Section 2 - Holdout cross-validation and kfold cross-validation
### Houldout method
*
	Using just a training/test split in a cross-validation method, the test dataset essentially becomes part of the training set so is more likely to overfit the model.
*
	A better approach is to use a train,validation and test/holdout set.  This allows to tune the model using cross-validation on the train/validation sets and evaluate
	model performance on the test/holdout set.  This is a bette approach for model selection.
* 
	Using the test set to evaluate the selected model allows us to obtain a less biased estimate of the models ability to generalize new data.
*
	A disadvantage/tradeoff to this method is the performance estimate may be sensitive to how we split the training/validation set itself.  This is due to how the Model
	estimate/fit varies for different samples/subsets of the training/validation splits themselves (different samples).
	
### kfold cross validation
*
	Kfold cross validation is a more robust approach to the holdout method.  Instead of taking a sample to create our train,validation and test/holdout sets we repeat this
	process into k folds without replacement (using only training/test datasets).  This process being repeated k times yeilds k different models and performance estimates.
*
	After this is done, calculate the average performance of the models based on different,independent test folds to obtain a performance estimate that is less sensitive to how 
	we split the train/validation/test datasets.
*
	Kfold cross-validation is used for model tuning (finding the optimal hyperparamter values).  This is done by evaluating models performance on the test folds.
*
	Once hyperparamater values are optimized, retrain the model on the complete training dataset and evaluate performance on the test set.  
*
	Rationale behind using a single training set is we are only interested in the final model, so it is ok to evaluate final hyperparameters on the test set.  ALSO, models
	usually provide better fit on more training data examples so having the larger training set usually produces better results.
*
	Usually best to use 10 folds when doing kfold cross-validation.  This offeres the best compromise between bias and variance(high variance means its overfit).
	Datasets low in sample size usually do better with more fold.  If there is a lot of data available, less fold may be fine (this also decreases runtime).
*
	In the case of uneven labels (classification outcomes), use stratified kfold to keep the label proportions preserved.
### Learning Curves
*
	See notes in the .ipynb file under the learning curve plot
	
### Validation Curves
*
	Can help address under or overfitting by adjusting the C parameter for a logistic regression model (example of a parameter that can change).
*
	See additional notes in the validation curve plot section of the notebook
### Fine Tuning ML models via grid search
*
	There are 2 types of parameters in ML. 1) parameters that are learned from the training data (like weights/coefficients) and 2) parameters of the algorithm(hyperparameters)
*
	In a grid search, we optimize a given model types hyperparameters, not just a single parameter like C in the Validation Curve example above.
	
### Fine Tuning ML models via Randomized search	
*
	Similar to grid search but insead of searching based off of a discrete list of values like grid search does, uses these lists with distributions to sample from (using these values as potential hyperparameters)
*
	Using the randomized search ensures there are a sufficient number of trials of different hyperparamters when tuning a model.

### Plotting the different folds onto a ROC/AUC curve
*
	Takeaway here is to notice the difference in the AUC curve for the different folds.  This suggests a certain degree of variance between the different folds.
*
	Having a difference in different folds means there will be variations in model fit depending on how the train/test data itself is split. 
	This would be important to note, especially in the case where different observations are collected over a period of time (data drift)

### Imbalanced Datasets
*
	ML algorithms optimize toward a reward or loss function, so the decision rule is likely going to be bias towards the majority class.

*
	One way to deal with this is to adjust the penalty for wrong directions in the minority class.  Do this in sklearn by adjusting class_weight = 'balanced', which is implemented for most classifiers.
*
	Another approach is to upsample the minority or downsample the majority classifiers.  There are tradeoffs to each method and when evaluating, try different approaches to see which method gives the best model fit.
	

