# DMBI Practical Implementation and Notes

This document contains basic, functional Python code for the Data Mining and Business Intelligence (DMBI) practical experiments, along with code explanations and a comprehensive list of potential Viva questions.

---

## Experiment 1: To Study and Explore ETL Tools (Implementing Basic ETL in Python)

### Code Implementation
```python
import pandas as pd

# 1. EXTRACT: Read data from a source (e.g., a CSV file or dictionary)
data = {
    'EmployeeID': [101, 102, 103, 104, 105],
    'Name': ['Alice', 'Bob', 'Charlie', 'David', 'Eve'],
    'Salary': [50000, None, 60000, 75000, 50000],
    'Department': ['HR', 'IT', 'IT', 'HR', None]
}
df = pd.DataFrame(data)
print("--- Extracted Data ---")
print(df)

# 2. TRANSFORM: Clean and format the data
# Fill missing salaries with the average salary
avg_salary = df['Salary'].mean()
df['Salary'] = df['Salary'].fillna(avg_salary)

# Fill missing department with a default value
df['Department'] = df['Department'].fillna('Unknown')

# Filter out employees with salary less than 55000
df_transformed = df[df['Salary'] >= 55000]

print("\n--- Transformed Data ---")
print(df_transformed)

# 3. LOAD: Save the transformed data to a new destination (e.g., a new CSV)
# df_transformed.to_csv('transformed_employees.csv', index=False)
print("\nData successfully loaded to destination.")
```

### Code Explanation
- **Extract**: We load raw data using a pandas DataFrame (this simulates extracting from a source database or CSV).
- **Transform**: We handle missing values (`fillna`), perform basic calculations (finding the mean), and filter the dataset based on a condition (Salary >= 55000).
- **Load**: We prepare the final cleaned dataframe to be exported or loaded into a target Data Warehouse (simulated via `to_csv`).

---

## Experiment 2: Data Exploration in Python (Creating Box Plot and 5-Number Summary)

### Code Implementation
```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt

# Generate sample data
np.random.seed(42)
data = pd.DataFrame({
    'Scores': np.random.normal(loc=70, scale=15, size=100)
})

# 5-Number Summary using describe()
# This includes Min, 25% (Q1), 50% (Median), 75% (Q3), and Max
summary = data['Scores'].describe()[['min', '25%', '50%', '75%', 'max']]
print("--- 5-Number Summary ---")
print(summary)

# Creating a Box Plot
plt.figure(figsize=(8, 5))
plt.boxplot(data['Scores'], vert=False, patch_artist=True)
plt.title('Box Plot of Scores')
plt.xlabel('Scores')
plt.grid(axis='x', linestyle='--', alpha=0.7)
plt.show()
```

### Code Explanation
- **5-Number Summary**: `pandas.describe()` automatically computes the key descriptive statistics. We extract `min`, `25%` (Q1), `50%` (Median/Q2), `75%` (Q3), and `max`.
- **Box Plot**: `matplotlib.pyplot.boxplot()` generates a visualization of the 5-number summary, clearly highlighting the median, interquartile range (IQR), and any potential outliers.

---

## Experiment 3: Data Preprocessing in Python (Preprocessing and Visualization)

### Code Implementation
```python
import pandas as pd
import matplotlib.pyplot as plt
from sklearn.preprocessing import MinMaxScaler, LabelEncoder

# Sample Data with categorical and unscaled numerical data
df = pd.DataFrame({
    'Age': [25, 45, 30, 50, 35],
    'Salary': [50000, 120000, 60000, 150000, 80000],
    'Purchased': ['No', 'Yes', 'No', 'Yes', 'Yes']
})

print("--- Original Data ---")
print(df)

# 1. Label Encoding (converting categorical 'Purchased' to numeric)
le = LabelEncoder()
df['Purchased_Encoded'] = le.fit_transform(df['Purchased'])

# 2. Min-Max Scaling (Normalizing Age and Salary)
scaler = MinMaxScaler()
df[['Age_Scaled', 'Salary_Scaled']] = scaler.fit_transform(df[['Age', 'Salary']])

print("\n--- Preprocessed Data ---")
print(df[['Age_Scaled', 'Salary_Scaled', 'Purchased_Encoded']])

# 3. Visualization (Scatter Plot of Scaled Data)
plt.figure(figsize=(6, 4))
scatter = plt.scatter(df['Age_Scaled'], df['Salary_Scaled'], c=df['Purchased_Encoded'], cmap='bwr')
plt.title('Scaled Age vs Scaled Salary')
plt.xlabel('Scaled Age (0 to 1)')
plt.ylabel('Scaled Salary (0 to 1)')
plt.colorbar(scatter, label='Purchased (0=No, 1=Yes)')
plt.show()
```

### Code Explanation
- **Label Encoding**: Machine learning models require numerical inputs, so `LabelEncoder` translates categorical strings ('Yes'/'No') into integers (1/0).
- **Scaling**: `MinMaxScaler` transforms features by scaling them to a specific range (default 0 to 1), preventing attributes with large ranges (like Salary) from dominating the model.
- **Visualization**: We visualize the scaled data points, using color mapping to distinguish between the classes.

---

## Experiment 4: Implement Apriori Algorithm in Python

### Code Implementation
```python
import pandas as pd
from mlxtend.frequent_patterns import apriori, association_rules

# Sample transaction data (One-hot encoded)
data = {
    'Milk':  [1, 0, 1, 1, 0],
    'Bread': [1, 1, 1, 1, 1],
    'Butter':[0, 1, 0, 1, 1],
    'Eggs':  [1, 0, 1, 0, 0]
}
df = pd.DataFrame(data)

# Find frequent itemsets with minimum support of 0.4 (40%)
frequent_itemsets = apriori(df, min_support=0.4, use_colnames=True)
print("--- Frequent Itemsets ---")
print(frequent_itemsets)

# Generate association rules with minimum confidence of 0.7 (70%)
rules = association_rules(frequent_itemsets, metric="confidence", min_threshold=0.7)
print("\n--- Association Rules ---")
print(rules[['antecedents', 'consequents', 'support', 'confidence', 'lift']])
```

### Code Explanation
- **Apriori Method**: Calculates the support for individual items and combinations. `min_support=0.4` means an itemset must appear in at least 40% of transactions.
- **Association Rules**: Extracts rules like "If Milk, then Bread" from the frequent itemsets. It filters out rules that do not meet the `min_threshold` for confidence.
- **Metrics**: Outputs support, confidence, and lift (which indicates the strength of the association).

---

## Experiment 5: Implement Naive Bayes Classifier in Python

### Code Implementation
```python
import pandas as pd
from sklearn.model_selection import train_test_split
from sklearn.naive_bayes import GaussianNB
from sklearn.metrics import accuracy_score, confusion_matrix

# Dataset: Predicting if a user will buy a product based on Age and EstimatedSalary
data = {
    'Age': [22, 25, 47, 52, 46, 56, 31, 28, 35, 40],
    'Salary': [20000, 30000, 150000, 120000, 140000, 180000, 50000, 45000, 60000, 80000],
    'Purchased': [0, 0, 1, 1, 1, 1, 0, 0, 0, 1]
}
df = pd.DataFrame(data)

X = df[['Age', 'Salary']]
y = df['Purchased']

# Train-Test Split (70% train, 30% test)
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.3, random_state=42)

# Train Gaussian Naive Bayes model
classifier = GaussianNB()
classifier.fit(X_train, y_train)

# Predictions
y_pred = classifier.predict(X_test)

# Evaluation
print("Accuracy:", accuracy_score(y_test, y_pred))
print("Confusion Matrix:\n", confusion_matrix(y_test, y_pred))
```

### Code Explanation
- **Data Prep**: We define features (`X`) and target variable (`y`), then split the data into training and testing sets.
- **Model Training**: We use `GaussianNB`, which assumes the continuous features follow a normal (Gaussian) distribution. It calculates the prior and likelihood probabilities based on Bayes' theorem.
- **Evaluation**: We evaluate performance using accuracy and a confusion matrix to see true positives, false positives, etc.

---

## Experiment 6: Implement Decision Tree Algorithm for Classification Tasks (with Visualization)

### Code Implementation
```python
import pandas as pd
from sklearn.tree import DecisionTreeClassifier, plot_tree
import matplotlib.pyplot as plt

# Dataset: Weather conditions to play tennis
data = {
    'Outlook': [0, 0, 1, 2, 2, 2, 1, 0, 0, 2], # 0:Sunny, 1:Overcast, 2:Rain
    'Temperature': [2, 2, 2, 1, 0, 0, 0, 1, 0, 1], # 2:Hot, 1:Mild, 0:Cool
    'Play': [0, 0, 1, 1, 1, 0, 1, 0, 1, 1] # 0:No, 1:Yes
}
df = pd.DataFrame(data)

X = df[['Outlook', 'Temperature']]
y = df['Play']

# Train Decision Tree using Gini Index (CART algorithm)
clf = DecisionTreeClassifier(criterion='gini', max_depth=3, random_state=0)
clf.fit(X, y)

# Visualization
plt.figure(figsize=(10, 6))
plot_tree(clf, feature_names=['Outlook', 'Temperature'], class_names=['No', 'Yes'], filled=True, rounded=True)
plt.title("Decision Tree Visualization")
plt.show()
```

### Code Explanation
- **Algorithm Initialization**: We use `DecisionTreeClassifier`. `criterion='gini'` splits nodes based on minimizing Gini impurity.
- **Tree Building**: The algorithm inherently performs attribute selection (choosing the attribute that best separates the classes) at each internal node.
- **Visualization**: `plot_tree` creates a graphical representation showing the splitting rules, Gini scores, samples in that node, and the predicted class.

---

## Experiment 7: Implement K-Means Clustering for Unsupervised Learning Task

### Code Implementation
```python
import numpy as np
import matplotlib.pyplot as plt
from sklearn.cluster import KMeans

# Generate random clustered data
np.random.seed(42)
X = np.vstack((np.random.normal(loc=0, scale=1, size=(50, 2)),
               np.random.normal(loc=5, scale=1, size=(50, 2)),
               np.random.normal(loc=10, scale=1, size=(50, 2))))

# Apply K-Means
kmeans = KMeans(n_clusters=3, random_state=42, n_init=10)
y_kmeans = kmeans.fit_predict(X)

# Visualization
plt.figure(figsize=(8, 5))
plt.scatter(X[:, 0], X[:, 1], c=y_kmeans, cmap='viridis', s=40, label='Data Points')
plt.scatter(kmeans.cluster_centers_[:, 0], kmeans.cluster_centers_[:, 1], 
            s=150, c='red', marker='X', label='Centroids')
plt.title('K-Means Clustering (K=3)')
plt.legend()
plt.show()
```

### Code Explanation
- **Data Generation**: We create unlabelled 2D data points centered around three distinct locations.
- **K-Means Execution**: The algorithm initializes `k=3` centroids, assigns points to the nearest centroid, and iteratively recomputes the centroids until convergence (minimizing Within-Cluster Sum of Squares).
- **Plotting**: Data points are colored by their assigned cluster label, and the final centroids are marked with a red 'X'.

---

## Experiment 8: Implement Hierarchical Clustering Algorithm for Unsupervised Learning Tasks

### Code Implementation
```python
import numpy as np
import matplotlib.pyplot as plt
from scipy.cluster.hierarchy import dendrogram, linkage
from sklearn.cluster import AgglomerativeClustering

# Sample Data
X = np.array([[5,3], [10,15], [15,12], [24,10], [30,30], [85,70], [71,80], [60,78], [70,55], [80,91]])

# 1. Create and plot the Dendrogram
linked = linkage(X, method='ward') # Ward's method minimizes variance

plt.figure(figsize=(8, 5))
dendrogram(linked, orientation='top', distance_sort='descending', show_leaf_counts=True)
plt.title('Hierarchical Clustering Dendrogram')
plt.xlabel('Data Index')
plt.ylabel('Distance')
plt.show()

# 2. Perform Agglomerative Clustering (Bottom-Up)
cluster = AgglomerativeClustering(n_clusters=2, metric='euclidean', linkage='ward')
cluster_labels = cluster.fit_predict(X)
print("Assigned Clusters:", cluster_labels)
```

### Code Explanation
- **Linkage and Dendrogram**: `linkage` calculates the distances between clusters using Ward's method. The `dendrogram` visualizes the nested tree of clusters and helps determine the optimal number of clusters by finding the largest vertical distance that doesn't intersect a horizontal line.
- **Agglomerative Clustering**: Treats each data point as a singleton cluster and successively merges the closest pairs until `n_clusters=2` is reached.

---

## Experiment 9: Demonstrate Algorithms Using WEKA Open Source Tool

**WEKA** (Waikato Environment for Knowledge Analysis) is a GUI-based Java software for data mining.

### Steps to Assess Performances in WEKA:
1. **Load Data**: Open the `WEKA Explorer`. Click `Open file...` under the Preprocess tab to load an `.arff` or `.csv` dataset (e.g., weather.nominal.arff).
2. **Association Mining (Apriori)**:
   - Go to the **Associate** tab.
   - Choose `Apriori` as the algorithm.
   - Adjust parameters (like `lowerBoundMinSupport` or `minMetric`).
   - Click **Start**. Analyze the discovered rules in the output panel.
3. **Classification (Decision Tree / Naive Bayes)**:
   - Go to the **Classify** tab.
   - Choose a classifier (e.g., `trees -> J48` for C4.5 Decision Tree, or `bayes -> NaiveBayes`).
   - Select Test Options (e.g., 10-fold cross-validation).
   - Click **Start**. Review the Accuracy, Precision, Recall, and Confusion Matrix in the results window.
4. **Clustering (K-Means)**:
   - Go to the **Cluster** tab.
   - Choose `SimpleKMeans`.
   - Click the parameters box to set `numClusters` (e.g., 3).
   - Click **Start**. Evaluate the Sum of Squared Errors (SSE) and cluster assignments in the output.

---

## Experiment 10: Detailed Case Study on any one BI Tool (Tableau)

### Case Study: Data Visualization and Dashboarding with Tableau

**Introduction:**
Tableau is a powerful and rapidly growing data visualization tool used in the Business Intelligence Industry. It helps in simplifying raw data into an easily understandable format (dashboards and worksheets). 

**Key Features:**
1. **Data Blending & Connection**: Connects to varied data sources (SQL databases, cloud spreadsheets, flat files) simultaneously.
2. **Real-time Analysis**: Allows for live connections to dynamic data sources.
3. **No-Code Interface**: Features a drag-and-drop interface, enabling users to build complex graphs, maps, and dashboards without programming knowledge.

**BI Workflow using Tableau:**
1. **Data Connection**: The user connects Tableau to an enterprise Data Warehouse (e.g., Snowflake, AWS Redshift).
2. **Data Preparation**: Utilizing Tableau Prep, the user cleans and transforms the data (joins, unions, filtering).
3. **Exploratory Data Analysis**: The user drags dimensions (categorical data) and measures (numerical data) to rows and columns to discover trends.
4. **Dashboard Creation**: Individual worksheets (charts) are combined into a centralized interactive dashboard. Filters are applied globally so users can slice and dice data across all charts simultaneously.
5. **Publishing**: The dashboard is published to Tableau Server/Online for stakeholders to make data-driven decisions.

**Conclusion:**
Tableau bridges the gap between complex data warehouses and business stakeholders, acting as the final "Knowledge Presentation" layer in the KDD process.

---

## Viva Questions (Based on DMBI Concepts)

1. **What is the difference between Data Mining and KDD?**
   *Data Mining is actually one specific step in the larger Knowledge Discovery in Databases (KDD) process. KDD involves cleaning, integration, selection, transformation, data mining, pattern evaluation, and knowledge presentation.*

2. **Differentiate between OLTP and OLAP.**
   *OLTP (Online Transaction Processing) is for day-to-day operations, normalized, and optimized for quick updates. OLAP (Online Analytical Processing) is for decision support, historical, de-normalized (star/snowflake schemas), and optimized for complex read queries.*

3. **What are the common OLAP operations?**
   *Roll-up (aggregating data), Drill-down (getting finer details), Slice (fixing one dimension), Dice (fixing multiple dimensions), and Pivot (rotating the axes).*

4. **Why is data preprocessing important? What are its steps?**
   *Real-world data is dirty (noisy, incomplete, inconsistent). Garbage in, garbage out. The steps are Data Cleaning, Integration, Reduction, and Transformation.*

5. **Explain the Apriori Property.**
   *If an itemset is infrequent, all of its supersets must also be infrequent. This property is used to reduce the search space and prune candidate itemsets.*

6. **Why can confidence alone be misleading in Association Rules?**
   *Confidence ignores the base probability (support) of the consequent. A high confidence might just be because the consequent is extremely popular. We should use Lift to check if the items are actually dependent.*

7. **How does Naive Bayes work and why is it "Naive"?**
   *It calculates probabilities using Bayes' Theorem. It is "naive" because it makes the strong assumption that all predictor attributes are completely independent of each other given the class label.*

8. **What is the difference between Information Gain and Gini Index?**
   *Both are attribute selection measures for Decision Trees. Information Gain (ID3) is based on entropy and favors attributes with many values. Gini Index (CART) measures impurity and uses strictly binary splits.*

9. **Differentiate between Classification and Clustering.**
   *Classification is supervised learning where we predict predefined categorical class labels using training data. Clustering is unsupervised learning where we group unlabelled data based on similarity.*

10. **Explain K-Means vs K-Medoids.**
    *K-Means uses the mean of the points in a cluster as the centroid, which is sensitive to outliers. K-Medoids uses an actual data point (the medoid) as the representative, making it more robust to outliers.*

11. **What is the difference between Agglomerative and Divisive clustering?**
    *Agglomerative is bottom-up (start with singletons, merge). Divisive is top-down (start with one large cluster, split).*

12. **What is DBSCAN and what are its main parameters?**
    *DBSCAN is a density-based clustering algorithm that groups dense regions and marks sparse regions as noise. Its parameters are $\epsilon$ (Epsilon, the radius) and MinPts (minimum points required in the radius).*

13. **What is a Decision Support System (DSS)?**
    *An interactive system that helps managers make semi-structured or unstructured decisions, utilizing data, models, and knowledge bases.*

14. **What are the key components of Business Intelligence (BI)?**
    *Data Sources, ETL processes, Data Warehouse, OLAP engines, Data Mining, and Reporting/Visualization tools (Dashboards).*
