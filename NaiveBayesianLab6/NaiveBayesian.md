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
         Outlook Temperature Humidity  Windy PlayTennis
    0     Sunny         Hot     High  False         No
    1     Sunny         Hot     High   True         No
    2  Overcast         Hot     High  False        Yes
    3     Rainy        Mild     High  False        Yes
    4     Rainy        Cool   Normal  False        Yes
    


```python
# obtain train data and train output
X = data.iloc[:, :-1]
print("\nThe First 5 values of the train data is\n", X.head())
```

    
    The First 5 values of the train data is
         Outlook Temperature Humidity  Windy
    0     Sunny         Hot     High  False
    1     Sunny         Hot     High   True
    2  Overcast         Hot     High  False
    3     Rainy        Mild     High  False
    4     Rainy        Cool   Normal  False
    


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
    0        2            1         0      0
    1        2            1         0      1
    2        0            1         0      0
    3        1            2         0      0
    4        1            0         1      0
    


```python
le_PlayTennis = LabelEncoder()
y = le_PlayTennis.fit_transform(y)
print("\nNow the Train output is\n",y)
```

    
    Now the Train output is
     [0 0 1 1 1]
    


```python
from sklearn.model_selection import train_test_split
X_train, X_test, y_train, y_test = train_test_split(X,y, test_size = 0.20)

classifier = GaussianNB()
classifier.fit(X_train, y_train)

from sklearn.metrics import accuracy_score
print("Accuracy is:", accuracy_score(classifier.predict(X_test), y_test))
```

    Accuracy is: 1.0
    
