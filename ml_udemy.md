
# Udemy machine learning [course](https://www.udemy.com/course/machinelearning/learn/lecture/6682576#overview)

### Section data Pre-processing [link](https://www.udemy.com/course/machinelearning/learn/lecture/6682576#overview)
---

1. `Handle missing data` (library used sklearn=>imputer)
    - replace the values using mean/mode/median value of the column. See example below 💱
    ```python
        from sklearn.preprocessing import Imputer
        imputer = Imputer(missing_values = 'NaN', strategy = 'mean', axis = 0)
        imputer = imputer.fit(X[:,1:3]) #all rows and only missing columns
        #final step
        X[:,1:3] = imputer.transform(X[:,1:3])
    ```

2. `Encode Categorical data to use in a model 🐽` (library used sklearn => LabelEncoder)
    - convert the text data in integer data as ml is all about equations. However, if direct substitution is applied as number, problem arises that model might consider one category as superior to other. Solution 📗 ? `one hot encoding`.
    - `one hot encoding` creates a mapping for each categorical variable assigning one bit for each type. For example, if there are two categories `yes` and `no`, then it can be divided into two different columns where one column is 0 and other is 1 for `yes` and vice versa. So one categorical column will be seperated into `n` columns where n is the type of categories.
    ```python
        from sklearn.preprocessing import OneHotEncoder
        onh = OneHotEncoder(categorical_features = [0]) #where 0 is the categorical column
        X = onh.fit_transform(X).toarray()
    ```

3. `Train and Val and Test split`
4. `Feature scaling` 🍠
    - one feature(like salary) might dominate other feeature (like age) because the values are in the same range or scale. To fix this, we can normalise the values in the whole column using standardisation(`x-mean(x)//sd(x)`) or normalisation `(x-min(x)//max(x)-min(x))`. 
    ```python
    from sklearn.preprocessing import StandardScaler
    X_train = sc_X.fit_transform(X_train)    
    ```
    - Two imp ques: context dependent to feature scale categorical variables.
    - But feature scale on y only if its regression and not classification.

### Section ML Models
---
1. `Linear regression model`
    - $y = b_0 + b_1 * x$    
2. `Multiple linear regression model`
    - $y = b_0 + b_1 * x_1 + b_2 * x_2 + b_3 * x_3 $    
3. `Polynomial regression`
4. `Support vector regression`
5. `Decision tree regression`
6. `Random Forest regression`
7. `Evaluating regression models performance`
8. `Regularization methods`


