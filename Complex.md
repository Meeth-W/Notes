# DMBI Practical Implementation and Notes (Advanced)

This document contains sophisticated, production-ready Python code for the Data Mining and Business Intelligence (DMBI) practical experiments, along with code explanations and a comprehensive list of potential Viva questions.

---

## Experiment 1: To Study and Explore ETL Tools (Implementing Basic ETL in Python)

### Code Implementation
```python
import pandas as pd
import logging
from typing import Dict, Any

logging.basicConfig(level=logging.INFO, format='%(levelname)s: %(message)s')

class SimpleETL:
    def __init__(self, data_source: Dict[str, Any]):
        self.raw_data = data_source
        self.df: pd.DataFrame = None

    def extract(self) -> 'SimpleETL':
        logging.info("Extracting data from source...")
        self.df = pd.DataFrame(self.raw_data)
        return self

    def transform(self) -> 'SimpleETL':
        logging.info("Applying transformation pipeline...")
        self.df = (
            self.df
            .assign(
                Salary=lambda x: x['Salary'].fillna(x['Salary'].mean()),
                Department=lambda x: x['Department'].fillna('Unknown')
            )
            .query("Salary >= 55000")
            .reset_index(drop=True)
        )
        return self

    def load(self, destination: str) -> None:
        logging.info(f"Loading transformed data to {destination}...")
        # self.df.to_csv(destination, index=False)
        print(self.df)

if __name__ == "__main__":
    source_data = {
        'EmployeeID': [101, 102, 103, 104, 105],
        'Name': ['Alice', 'Bob', 'Charlie', 'David', 'Eve'],
        'Salary': [50000, None, 60000, 75000, 50000],
        'Department': ['HR', 'IT', 'IT', 'HR', None]
    }
    etl_pipeline = SimpleETL(source_data)
    etl_pipeline.extract().transform().load('transformed_employees.csv')
```

### Code Explanation
- **Extract**: We load raw data using a pandas DataFrame (this simulates extracting from a source database or CSV). The object-oriented approach encapsulates state.
- **Transform**: We handle missing values (`fillna`), perform basic calculations (finding the mean), and filter the dataset based on a condition (Salary >= 55000). The `.assign` and `.query` methods offer a clean, functional style.
- **Load**: We prepare the final cleaned dataframe to be exported or loaded into a target Data Warehouse (simulated via `to_csv`).

---

## Experiment 2: Data Exploration in Python (Creating Box Plot and 5-Number Summary)

### Code Implementation
```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
from scipy import stats

np.random.seed(42)
df = pd.DataFrame({
    'Scores': np.random.normal(loc=70, scale=15, size=100)
})

# Advanced Descriptive Statistics
summary = df['Scores'].describe(percentiles=[.05, .25, .50, .75, .95]).to_frame().T
skewness = stats.skew(df['Scores'])
kurtosis = stats.kurtosis(df['Scores'])
print("--- Statistical Summary ---")
print(summary.assign(Skewness=skewness, Kurtosis=kurtosis).T)

# Complex Visualization: Combined KDE and Box Plot
fig, (ax_box, ax_kde) = plt.subplots(2, sharex=True, gridspec_kw={"height_ratios": (.15, .85)}, figsize=(10, 6))

sns.boxplot(x=df['Scores'], ax=ax_box, color="lightblue", fliersize=5)
sns.histplot(df['Scores'], ax=ax_kde, kde=True, stat="density", color="steelblue", bins=15)
ax_kde.axvline(df['Scores'].mean(), color='r', linestyle='--', label=f'Mean: {df["Scores"].mean():.2f}')
ax_kde.axvline(df['Scores'].median(), color='g', linestyle='-', label=f'Median: {df["Scores"].median():.2f}')

ax_box.set(xlabel='')
ax_kde.legend()
sns.despine(ax=ax_box, left=True)
plt.suptitle('Comprehensive Distribution Analysis of Scores', y=0.95)
plt.show()
```

### Code Explanation
- **5-Number Summary**: `pandas.describe()` automatically computes the key descriptive statistics. We extract `min`, `25%` (Q1), `50%` (Median/Q2), `75%` (Q3), and `max`. We also add skewness and kurtosis.
- **Box Plot**: `matplotlib.pyplot.boxplot()` generates a visualization of the 5-number summary, clearly highlighting the median, interquartile range (IQR), and any potential outliers. We use `seaborn` for an elegant subplot combining the boxplot and kernel density estimation.

---

## Experiment 3: Data Preprocessing in Python (Preprocessing and Visualization)

### Code Implementation
```python
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
from sklearn.compose import ColumnTransformer
from sklearn.preprocessing import StandardScaler, OneHotEncoder

df = pd.DataFrame({
    'Age': [25, 45, 30, 50, 35],
    'Salary': [50000, 120000, 60000, 150000, 80000],
    'Department': ['IT', 'HR', 'IT', 'Finance', 'HR'],
    'Purchased': [0, 1, 0, 1, 1]
})

# Define preprocessing steps using ColumnTransformer
numeric_features = ['Age', 'Salary']
categorical_features = ['Department']

preprocessor = ColumnTransformer(
    transformers=[
        ('num', StandardScaler(), numeric_features),
        ('cat', OneHotEncoder(drop='first'), categorical_features)
    ])

# Fit and transform
X_processed = preprocessor.fit_transform(df)
feature_names = (preprocessor.named_transformers_['num'].get_feature_names_out(numeric_features).tolist() +
                 preprocessor.named_transformers_['cat'].get_feature_names_out(categorical_features).tolist())

df_processed = pd.DataFrame(X_processed, columns=feature_names)
df_processed['Purchased'] = df['Purchased']

print("--- Preprocessed Data Pipeline Output ---")
print(df_processed)

# Pairplot visualization
sns.pairplot(df_processed, hue='Purchased', palette='husl', markers=["o", "s"])
plt.suptitle('Feature Relationships post-preprocessing', y=1.02)
plt.show()
```

### Code Explanation
- **Label Encoding**: Machine learning models require numerical inputs, so `LabelEncoder` translates categorical strings ('Yes'/'No') into integers (1/0). Here we use `OneHotEncoder` via `ColumnTransformer` for advanced handling.
- **Scaling**: `MinMaxScaler` transforms features by scaling them to a specific range (default 0 to 1), preventing attributes with large ranges (like Salary) from dominating the model. We used `StandardScaler` for robust standardization.
- **Visualization**: We visualize the scaled data points, using color mapping to distinguish between the classes. `seaborn.pairplot` provides a multi-dimensional view.

---

## Experiment 4: Implement Apriori Algorithm in Python

### Code Implementation
```python
import pandas as pd
from mlxtend.frequent_patterns import apriori, association_rules
from mlxtend.preprocessing import TransactionEncoder

# Raw transaction lists
dataset = [['Milk', 'Bread', 'Eggs'],
           ['Bread', 'Butter'],
           ['Milk', 'Bread', 'Butter', 'Eggs'],
           ['Milk', 'Bread', 'Butter'],
           ['Bread', 'Butter']]

# 1. Transform raw lists into one-hot boolean DataFrame
te = TransactionEncoder()
te_ary = te.fit(dataset).transform(dataset)
df = pd.DataFrame(te_ary, columns=te.columns_)

# 2. Extract Frequent Itemsets
frequent_itemsets = apriori(df, min_support=0.4, use_colnames=True)
frequent_itemsets['length'] = frequent_itemsets['itemsets'].apply(lambda x: len(x))

# 3. Generate Advanced Association Rules
rules = association_rules(frequent_itemsets, metric="lift", min_threshold=1.0)

# Filter for highly confident rules with high lift
strong_rules = rules[(rules['confidence'] >= 0.7) & (rules['lift'] >= 1.2)]
print("--- Strong Association Rules ---")
print(strong_rules[['antecedents', 'consequents', 'support', 'confidence', 'lift']])
```

### Code Explanation
- **Apriori Method**: Calculates the support for individual items and combinations. `min_support=0.4` means an itemset must appear in at least 40% of transactions. We use `TransactionEncoder` for scalable data formatting.
- **Association Rules**: Extracts rules like "If Milk, then Bread" from the frequent itemsets. It filters out rules that do not meet the `min_threshold` for confidence.
- **Metrics**: Outputs support, confidence, and lift (which indicates the strength of the association).

---

## Experiment 5: Implement Naive Bayes Classifier in Python

### Code Implementation
```python
import pandas as pd
from sklearn.model_selection import train_test_split, cross_val_score
from sklearn.naive_bayes import GaussianNB
from sklearn.metrics import classification_report, RocCurveDisplay
from sklearn.preprocessing import QuantileTransformer
from sklearn.pipeline import make_pipeline
import matplotlib.pyplot as plt

df = pd.DataFrame({
    'Age': [22, 25, 47, 52, 46, 56, 31, 28, 35, 40],
    'Salary': [20000, 30000, 150000, 120000, 140000, 180000, 50000, 45000, 60000, 80000],
    'Purchased': [0, 0, 1, 1, 1, 1, 0, 0, 0, 1]
})

X, y = df[['Age', 'Salary']], df['Purchased']
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.3, stratify=y, random_state=42)

# Build a robust pipeline that normalizes data to make it more Gaussian
model = make_pipeline(QuantileTransformer(output_distribution='normal'), GaussianNB())

# Cross-Validation
cv_scores = cross_val_score(model, X, y, cv=3)
print(f"Cross-Validated Accuracy: {cv_scores.mean():.2f} (+/- {cv_scores.std() * 2:.2f})")

# Fit and Evaluate
model.fit(X_train, y_train)
y_pred = model.predict(X_test)

print("\n--- Classification Report ---")
print(classification_report(y_test, y_pred, zero_division=0))

# Plot ROC Curve
RocCurveDisplay.from_estimator(model, X_test, y_test)
plt.title('ROC Curve for Naive Bayes Pipeline')
plt.plot([0, 1], [0, 1], linestyle='--', lw=2, color='r', alpha=.8)
plt.show()
```

### Code Explanation
- **Data Prep**: We define features (`X`) and target variable (`y`), then split the data into training and testing sets. `stratify=y` ensures class balance.
- **Model Training**: We use `GaussianNB`, which assumes the continuous features follow a normal (Gaussian) distribution. It calculates the prior and likelihood probabilities based on Bayes' theorem. We wrap it in a `Pipeline` with `QuantileTransformer`.
- **Evaluation**: We evaluate performance using accuracy and a confusion matrix to see true positives, false positives, etc. A full classification report and ROC curve are plotted.

---

## Experiment 6: Implement Decision Tree Algorithm for Classification Tasks (with Visualization)

### Code Implementation
```python
import pandas as pd
from sklearn.tree import DecisionTreeClassifier, plot_tree
from sklearn.model_selection import GridSearchCV
import matplotlib.pyplot as plt

df = pd.DataFrame({
    'Outlook': [0, 0, 1, 2, 2, 2, 1, 0, 0, 2],
    'Temperature': [2, 2, 2, 1, 0, 0, 0, 1, 0, 1],
    'Play': [0, 0, 1, 1, 1, 0, 1, 0, 1, 1]
})

X, y = df[['Outlook', 'Temperature']], df['Play']

# Hyperparameter Tuning via GridSearchCV
param_grid = {
    'criterion': ['gini', 'entropy'],
    'max_depth': [2, 3, 4, None],
    'min_samples_split': [2, 3]
}
grid_search = GridSearchCV(DecisionTreeClassifier(random_state=42), param_grid, cv=3)
grid_search.fit(X, y)

best_clf = grid_search.best_estimator_
print(f"Best Parameters: {grid_search.best_params_}")

# Feature Importance
importance = pd.Series(best_clf.feature_importances_, index=X.columns)
print(f"\nFeature Importances:\n{importance}")

# Sophisticated Visualization
plt.figure(figsize=(12, 8))
plot_tree(best_clf, feature_names=X.columns, class_names=['No', 'Yes'], 
          filled=True, rounded=True, proportion=True, fontsize=12)
plt.title(f"Optimized Decision Tree (Criterion: {best_clf.criterion})")
plt.show()
```

### Code Explanation
- **Algorithm Initialization**: We use `DecisionTreeClassifier`. `criterion='gini'` splits nodes based on minimizing Gini impurity. Here, we use `GridSearchCV` to automatically find the optimal depth and splitting criteria.
- **Tree Building**: The algorithm inherently performs attribute selection (choosing the attribute that best separates the classes) at each internal node. We also extract feature importances.
- **Visualization**: `plot_tree` creates a graphical representation showing the splitting rules, Gini scores, samples in that node, and the predicted class.

---

## Experiment 7: Implement K-Means Clustering for Unsupervised Learning Task

### Code Implementation
```python
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
from sklearn.cluster import KMeans
from sklearn.preprocessing import StandardScaler
from sklearn.metrics import silhouette_score

np.random.seed(42)
X_raw = np.vstack((np.random.normal(loc=0, scale=1, size=(50, 2)),
                   np.random.normal(loc=5, scale=1, size=(50, 2)),
                   np.random.normal(loc=10, scale=1, size=(50, 2))))

# It's best practice to scale data before distance-based clustering
X = StandardScaler().fit_transform(X_raw)

# Elbow Method to find optimal k
inertias, silhouettes = [], []
k_range = range(2, 8)

for k in k_range:
    kmeans_temp = KMeans(n_clusters=k, random_state=42, n_init=10)
    labels = kmeans_temp.fit_predict(X)
    inertias.append(kmeans_temp.inertia_)
    silhouettes.append(silhouette_score(X, labels))

optimal_k = k_range[np.argmax(silhouettes)]
print(f"Optimal K determined by Silhouette Score: {optimal_k}")

# Final Model
kmeans_final = KMeans(n_clusters=optimal_k, random_state=42, n_init=10).fit(X)

# Visualization Grid
fig, ax = plt.subplots(1, 2, figsize=(14, 5))

# Plot 1: Elbow Curve
ax[0].plot(k_range, inertias, marker='o')
ax[0].set_title('Elbow Method (Inertia)')
ax[0].set_xlabel('Number of Clusters (k)')

# Plot 2: Final Clustering
sns.scatterplot(x=X[:, 0], y=X[:, 1], hue=kmeans_final.labels_, palette='viridis', s=60, ax=ax[1])
ax[1].scatter(kmeans_final.cluster_centers_[:, 0], kmeans_final.cluster_centers_[:, 1], 
              s=200, c='red', marker='*', edgecolor='black', label='Centroids')
ax[1].set_title(f'K-Means Clusters (K={optimal_k})')
ax[1].legend()

plt.tight_layout()
plt.show()
```

### Code Explanation
- **Data Generation**: We create unlabelled 2D data points centered around three distinct locations. Data is subsequently standardized.
- **K-Means Execution**: The algorithm initializes `k=3` centroids, assigns points to the nearest centroid, and iteratively recomputes the centroids until convergence (minimizing Within-Cluster Sum of Squares). We implement the Elbow Method and Silhouette Scoring to algorithmically determine `K`.
- **Plotting**: Data points are colored by their assigned cluster label, and the final centroids are marked with a red 'X'.

---

## Experiment 8: Implement Hierarchical Clustering Algorithm for Unsupervised Learning Tasks

### Code Implementation
```python
import numpy as np
import matplotlib.pyplot as plt
from scipy.cluster.hierarchy import dendrogram, linkage, fcluster
from sklearn.metrics import silhouette_score
import seaborn as sns

X = np.array([[5,3], [10,15], [15,12], [24,10], [30,30], [85,70], [71,80], [60,78], [70,55], [80,91]])

# 1. Compute Linkage Matrix
linked = linkage(X, method='ward', metric='euclidean')

# 2. Extract clusters dynamically based on distance threshold
distance_threshold = 50
cluster_labels = fcluster(linked, distance_threshold, criterion='distance')
sil_score = silhouette_score(X, cluster_labels) if len(np.unique(cluster_labels)) > 1 else 0

print(f"Formed {len(np.unique(cluster_labels))} clusters at distance threshold {distance_threshold}")
print(f"Silhouette Score: {sil_score:.2f}")

# 3. Comprehensive Visualization
fig, (ax1, ax2) = plt.subplots(1, 2, figsize=(15, 6))

# Dendrogram
dendrogram(linked, orientation='top', distance_sort='descending', show_leaf_counts=True, ax=ax1, color_threshold=distance_threshold)
ax1.axhline(y=distance_threshold, c='k', ls='--', label=f'Threshold={distance_threshold}')
ax1.set_title('Hierarchical Clustering Dendrogram')
ax1.set_ylabel('Ward Distance')
ax1.legend()

# Scatter Plot mapping the extracted labels
sns.scatterplot(x=X[:, 0], y=X[:, 1], hue=cluster_labels, palette='tab10', s=100, ax=ax2)
ax2.set_title('2D Representation of Identified Clusters')

plt.tight_layout()
plt.show()
```

### Code Explanation
- **Linkage and Dendrogram**: `linkage` calculates the distances between clusters using Ward's method. The `dendrogram` visualizes the nested tree of clusters and helps determine the optimal number of clusters by finding the largest vertical distance that doesn't intersect a horizontal line.
- **Agglomerative Clustering**: Treats each data point as a singleton cluster and successively merges the closest pairs until `n_clusters=2` is reached. We use `fcluster` to dynamically derive flat clusters from the hierarchical tree based on distance.

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
