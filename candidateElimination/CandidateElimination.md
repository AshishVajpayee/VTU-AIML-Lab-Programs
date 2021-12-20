### For a given set of training data examples stored in a .CSV file, implement and demonstrate the Candidate-Elimination algorithm to output a description of the set of all hypotheses consistent with the training examples.

<p> Lab Program 3 AIML</p>



```python
import csv
 
with open("trainingexample.csv") as f:
    csv_file = csv.reader(f)
    data = list(csv_file)
    
    s = data[1][:-1]
    g = [['?' for i in range(len(s))] for j in range(len(s))]
 
    for i in data:
        if i[-1] == "Yes":
            for j in range(len(s)):
                if i[j] != s[j]:
                    s[j] = '?'
                    g[j][j] = '?'
 
        elif i[-1] == "No":
            for j in range(len(s)):
                if i[j] != s[j]:
                    g[j][j] = s[j]
                else:
                    g[j][j] = "?"
        print("\nSteps of Candidate Elimination Algorithm", data.index(i)+1)
        print(s)
        print(g)
    gh = []
    for i in g:
        for j in i:
            if j != '?':
                gh.append(i)
                break
    print("\nFinal specific hypothesis:\n", s)
    print("\nFinal general hypothesis:\n", gh)
```

    
    Steps of Candidate Elimination Algorithm 1
    ['Sunny', 'Warm', '?', 'Strong', 'Warm', 'Same']
    [['?', '?', '?', '?', '?', '?'], ['?', '?', '?', '?', '?', '?'], ['?', '?', '?', '?', '?', '?'], ['?', '?', '?', '?', '?', '?'], ['?', '?', '?', '?', '?', '?'], ['?', '?', '?', '?', '?', '?']]
    
    Steps of Candidate Elimination Algorithm 2
    ['Sunny', 'Warm', '?', 'Strong', 'Warm', 'Same']
    [['?', '?', '?', '?', '?', '?'], ['?', '?', '?', '?', '?', '?'], ['?', '?', '?', '?', '?', '?'], ['?', '?', '?', '?', '?', '?'], ['?', '?', '?', '?', '?', '?'], ['?', '?', '?', '?', '?', '?']]
    
    Steps of Candidate Elimination Algorithm 3
    ['Sunny', 'Warm', '?', 'Strong', 'Warm', 'Same']
    [['Sunny', '?', '?', '?', '?', '?'], ['?', 'Warm', '?', '?', '?', '?'], ['?', '?', '?', '?', '?', '?'], ['?', '?', '?', '?', '?', '?'], ['?', '?', '?', '?', '?', '?'], ['?', '?', '?', '?', '?', 'Same']]
    
    Steps of Candidate Elimination Algorithm 4
    ['Sunny', 'Warm', '?', 'Strong', '?', '?']
    [['Sunny', '?', '?', '?', '?', '?'], ['?', 'Warm', '?', '?', '?', '?'], ['?', '?', '?', '?', '?', '?'], ['?', '?', '?', '?', '?', '?'], ['?', '?', '?', '?', '?', '?'], ['?', '?', '?', '?', '?', '?']]
    
    Final specific hypothesis:
     ['Sunny', 'Warm', '?', 'Strong', '?', '?']
    
    Final general hypothesis:
     [['Sunny', '?', '?', '?', '?', '?'], ['?', 'Warm', '?', '?', '?', '?']]
    


```python

```
