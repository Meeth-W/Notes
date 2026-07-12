# DMBI Practical Code Cheat Sheet

A quick reference guide for all the Python implementations in the DMBI practicals.

## 1. ETL (Extract, Transform, Load)
```python
import pandas as pd

# Extract
df = pd.DataFrame({'Name': ['A', 'B', 'C'], 'Salary': [50000, None, 60000]})

# Transform
df['Salary'] = df['Salary'].fillna(df['Salary'].mean())
df_transformed = df[df['Salary'] >= 55000]

# Load
df_transformed.to_csv('output.csv', index=False)
```

## 2. Exploration (5-Number Summary & Box Plot)
```python
import pandas as pd
import matplotlib.pyplot as plt

# 5-Number Summary
summary = df['Scores'].describe()[['min', '25%', '50%', '75%', 'max']]

# Box Plot
plt.boxplot(df['Scores'], vert=False, patch_artist=True)
plt.title('Box Plot'); plt.show()
```

## 3. Preprocessing (Encoding & Scaling)
```python
from sklearn.preprocessing import LabelEncoder, MinMaxScaler

# Label Encoding (Categorical to Numeric)
df['Purchased_Encoded'] = LabelEncoder().fit_transform(df['Purchased'])

# Min-Max Scaling (Normalization 0 to 1)
df[['Age_Scaled', 'Salary_Scaled']] = MinMaxScaler().fit_transform(df[['Age', 'Salary']])
```

## 4. Apriori Algorithm (Association Rules)
```python
from mlxtend.frequent_patterns import apriori, association_rules

# Frequent Itemsets
freq_items = apriori(df, min_support=0.4, use_colnames=True)

# Association Rules
rules = association_rules(freq_items, metric="confidence", min_threshold=0.7)
print(rules[['antecedents', 'consequents', 'support', 'confidence', 'lift']])
```

## 5. Naive Bayes Classifier
```python
from sklearn.model_selection import train_test_split
from sklearn.naive_bayes import GaussianNB
from sklearn.metrics import accuracy_score, confusion_matrix

X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.3, random_state=42)

# Train & Predict
clf = GaussianNB().fit(X_train, y_train)
y_pred = clf.predict(X_test)

# Evaluate
print("Accuracy:", accuracy_score(y_test, y_pred))
print("Confusion Matrix:\n", confusion_matrix(y_test, y_pred))
```

## 6. Decision Tree Classifier
```python
from sklearn.tree import DecisionTreeClassifier, plot_tree
import matplotlib.pyplot as plt

# Train
clf = DecisionTreeClassifier(criterion='gini', max_depth=3).fit(X, y)

# Visualize
plt.figure(figsize=(10, 6))
plot_tree(clf, feature_names=['Outlook', 'Temp'], class_names=['No', 'Yes'], filled=True)
plt.show()
```

## 7. K-Means Clustering
```python
from sklearn.cluster import KMeans
import matplotlib.pyplot as plt

# Train & Predict
kmeans = KMeans(n_clusters=3, random_state=42).fit(X)
y_kmeans = kmeans.predict(X)

# Visualize
plt.scatter(X[:, 0], X[:, 1], c=y_kmeans, cmap='viridis')
plt.scatter(kmeans.cluster_centers_[:, 0], kmeans.cluster_centers_[:, 1], c='red', marker='X')
plt.show()
```

## 8. Hierarchical Clustering
```python
from scipy.cluster.hierarchy import dendrogram, linkage
from sklearn.cluster import AgglomerativeClustering
import matplotlib.pyplot as plt

# 1. Dendrogram
linked = linkage(X, method='ward')
dendrogram(linked)
plt.show()

# 2. Agglomerative Clustering
cluster_labels = AgglomerativeClustering(n_clusters=2, linkage='ward').fit_predict(X)
```
