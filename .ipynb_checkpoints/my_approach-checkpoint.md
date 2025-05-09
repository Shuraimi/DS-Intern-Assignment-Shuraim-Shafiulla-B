This file contains my approach to tackle this problem. Here I'm predicting the energy consumption of industrial equipment given various features.

First I set up my local environment using conda which contains Python language and libraries such as NumPy, Pandas, Matplotlib, Seaborn, Scikit-learn and many more.
Then created a notebook and structured it in such a way that it gives me a proper flow to follow so that I can cover all the eavaluation criteria properly.

Then *loaded the data, performed some data exploration* such as `.info()`,`.describe()` etc and also *parsed the dates* i.e. the timestamp column. I then checked whether the dataset is sorted or not along the `timestamp` column and it was sorted.

Then I *split the data into train, valid and test sets*. First into 80-20 train and test set and then 80% train into train and valid of 80-20 split and saved the test data.

I then *handled datatypes of columns* because some columns contained float values but still had dtype as object. This was because of some filler values like 'unknown','error','???' and 'check' and then replaced those values by `np.nan` and changed the columns to numeric and then filled the nan values.

Tried to sort the data but data was already sorted so then made a copy of data and performed *feature engineering* by extracting date, month, year etc from the `timestamp` column because this is important for time-series data and then dropped `timestamp` column.

Then began *Exploratory Data Analysis* by calculating correlation matrix and checking it as to how columns are correlated to target and from this I also assumed that both the random variables i.e. `random_variable1` and `random_variable2` are not useful in prediction of the target due to negative correlation.

Then used a scatter plot to explore few numeric columns followed by a few visualisations. Then I plot the heatmap of correlation matrix.

I then *imputed missing values* using `SimpleImputer` using strategy median and I fit_transform on train data. I then brought the values in the `equipment_energy_consumption` in given range of 10-1080 Wh by replacing values <10 with 10 and those >1080 to 1080

Then started *handling outliers* of all columns. I separated the target column because i was handled earlier. I then defined a function to cap_outliers given data and then after capping, I added the target column to the dataframe.

I also defined a *function to preprocess any data* train, valid or test or even new data before giving it to the model. It takes the data file path and imputer except in case of train data.

I then preprocessed valid data in order to evaluate on it when I train a model.

Then began training a model by first splitting into data and labels for train and valid data. Then trained a `RandomForestregressor`, created a function to evaluate it. Tried a few plots to compare train and valid data.

After that as an attempt to improve model's performance, I tried `RandomForestregressor` with different hyperparameters and also tried a few simple models but the score didn't improve and I'm unaware of the reason even after many tries.

Then tried hyperparameter tuning using `GridSearchCV` but that also didn't give me better performance. Then as a last try, trained a `RandomForestregressor` on train and valid data combined and looked at feature importances and then also trained on important features but even that failed.

So this was my approach. I initially began with the goal of cleaning, EDA and stuff then train a model to get a good score but I couldn't do the last part of training(I don't know why it didn't work).