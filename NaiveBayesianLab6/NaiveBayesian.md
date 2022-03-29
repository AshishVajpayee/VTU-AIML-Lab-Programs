### Naive Bayesian Classifier

#### Lab 6: Write a Program to implement the naive bayesian classifier for a sample training data set stored as a .CSV file. Compute the accuracy of the classifier few test data sets.


```python
# import necessary libraries
import pandas as pd
from sklearn import tree
from sklearn.preprocessing import LabelEncoder
from sklearn.naive_bayes import GaussianNB

# Load Data from CSV
data = pd.read_csv('tennisdata.csv')
print("The first 5 Values of data is :\n", data.head())
```

    The first 5 Values of data is :
         Outlook Temperature Humidity   Windy PlayTennis
    0     Sunny         Hot     High    Weak         No
    1     Sunny         Hot     High  Strong         No
    2  Overcast         Hot     High    Weak        Yes
    3      Rain        Mild     High    Weak        Yes
    4      Rain        Cool   Normal    Weak        Yes
    


```python
# obtain train data and train output
X = data.iloc[:, :-1]
print("\nThe First 5 values of the train data is\n", X.head())
```

    
    The First 5 values of the train data is
         Outlook Temperature Humidity   Windy
    0     Sunny         Hot     High    Weak
    1     Sunny         Hot     High  Strong
    2  Overcast         Hot     High    Weak
    3      Rain        Mild     High    Weak
    4      Rain        Cool   Normal    Weak
    


```python
y = data.iloc[:, -1]
print("\nThe First 5 values of train output is\n", y.head())
```

    
    The First 5 values of train output is
     0     No
    1     No
    2    Yes
    3    Yes
    4    Yes
    Name: PlayTennis, dtype: object
    


```python
# convert them in numbers
le_outlook = LabelEncoder()
X.Outlook = le_outlook.fit_transform(X.Outlook)

le_Temperature = LabelEncoder()
X.Temperature = le_Temperature.fit_transform(X.Temperature)

le_Humidity = LabelEncoder()
X.Humidity = le_Humidity.fit_transform(X.Humidity)

le_Windy = LabelEncoder()
X.Windy = le_Windy.fit_transform(X.Windy)

print("\nNow the Train output is\n", X.head())
```

    
    Now the Train output is
        Outlook  Temperature  Humidity  Windy
    0        2            1         0      1
    1        2            1         0      0
    2        0            1         0      1
    3        1            2         0      1
    4        1            0         1      1
    

    C:\Users\Ashishvajpayee\AppData\Local\Programs\Python\Python310\lib\site-packages\pandas\core\generic.py:5516: SettingWithCopyWarning: 
    A value is trying to be set on a copy of a slice from a DataFrame.
    Try using .loc[row_indexer,col_indexer] = value instead
    
    See the caveats in the documentation: https://pandas.pydata.org/pandas-docs/stable/user_guide/indexing.html#returning-a-view-versus-a-copy
      self[name] = value
    


```python
le_PlayTennis = LabelEncoder()
y = le_PlayTennis.fit_transform(y)
print("\nNow the Train output is\n",y)
```

    
    Now the Train output is
     [0 0 1 1 1 0 1 0 1 1 1 1 1 0]
    


```python
from sklearn.model_selection import train_test_split
X_train, X_test, y_train, y_test = train_test_split(X,y, test_size = 0.20)

classifier = GaussianNB()
classifier.fit(X_train, y_train)

from sklearn.metrics import accuracy_score
print("Accuracy is:", accuracy_score(classifier.predict(X_test), y_test))
```

    Accuracy is: 0.3333333333333333
    
