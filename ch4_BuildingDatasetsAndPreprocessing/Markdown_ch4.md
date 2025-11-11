# Chapter 4 - Building Datasets and Preprocessing
## Section 1 - Dealing with missing data and encoding methods
*
	Examples showing how to count the number of NA or Null values per column
	shows how to eliminate rows/columns that have NA values.  Usually not recommended, as you could potentially lose a lot of data
	Mean imputation using SimpleImputer
	Categorical encoding methods for class features, including ordinal coding using dictionaries.
	One hot methods using pandas get_dummies() function.
## Section 2 - Train/Test splits and scaling methods
*
	It is important to scale features as most ML algorithms will be attempting to optimize weights according to large errors that large scale variables will have
	Scaling methods include MinMaxScaler and StandardScaler in sklearn.
	MinMaxScaling most often refers to normalization and rescales features in a range from 0 to 1
	Standardization centers feature columns with a mean 0 and std dev of 1 so features have a standard normal distribution. However, if there is skewness in the original data, this does NOT transform the data to a normal distribution.
## Section 3 - Selecting Meaningful features
*
	Goes over l1 vs l2 regularization methods (penalties) and changing the C parameter for lr models to change the regularization effect.
	l1 regularization forces features that are not as meaningful to a 0 coefficeint
	l2 (the default in sklearn) tries to force all coefficients to 0 (small coefficients but none are truly 0).  This maintains all features that are fitted to the model.
	function that loops through the different values of C and plots the weights of the coefficients for a range of C values
## Section 4 - SBS (Sequential Backward Selection and KNN classifier method for feature selection (feature importance)
