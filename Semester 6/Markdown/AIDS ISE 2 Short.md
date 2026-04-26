---

# **AIDS ISE 2 — Short Revision Notes (Exam Focussed)**

> **Note:** This document has been heavily consolidated to cover **exclusively** the topics requested within the 2-Mark and 5-Mark question bank syllabus. Irrelevant portions have been pruned for optimized study targeting.

---

# **Module 4: Data Visualization**

## **Data Visualization Overview *(Targeted by Mod 4: Q1, Q5, Q6)***
- **Definition:** The graphical representation of information using visual elements (charts, maps) to intuitively expose trends, patterns, and outliers.
- **Primary Objective:** To translate complex data into a visual context for rapid human understanding.
- **Importance in AI/DS:** Critical for EDA (spotting anomalies), feature selection (correlation checking), and interpreting complex model outputs (like Confusion Matrices).
- **Common Techniques:** Scatter Plots, Boxplots, Bar Charts.
- **Limitation:** Can be highly misleading or biased if scaled improperly (e.g., truncating axes).

## **Benefits & Decision Making *(Targeted by Mod 4: Q2, Q7)***
- **Accelerated Insights:** Human brains process visuals much faster than text.
- **Pattern & Trend Recognition:** Line charts reveal cyclical patterns; scatter plots with regression lines reveal directional trends.
- **Model Performance Analysis:** ROC curves and Confusion Matrices visually summarize classification errors instantly.
- **Support for Decision Making:** Highlights clear correlations, guiding executives to make data-backed strategic choices instead of relying on intuition.

## **Specific Visualization Techniques *(Targeted by Mod 4: Q3, Q4)***
- **Histogram:** Best for **Continuous Numerical Data**. Groups data into bins to visualize frequency distribution, spread, and skewness.
- **Countplot:** Best for **Categorical Data**. Displays the exact frequency of observations in categorical bins via bars. Essential in EDA for identifying dataset class imbalances.

## **Developing an EDA Strategy *(Targeted by Mod 4: Q8)***
*Strategy for Customer Purchase Data:*
1. **Data Cleaning:** Use Missingno matrices to visualize NaNs.
2. **Univariate Analysis:** Histograms for age distribution; Countplots for gender demographics.
3. **Bivariate Analysis:** Scatter plots mapping Age vs Spending to detect behavioral clusters.
4. **Anomaly Detection:** Boxplots to identify extreme outliers that could skew ML models.
5. **Correlation:** Heatmaps to identify multi-collinearity between numerical features.

---

# **Module 5: Problem Solving in AI**

## **Problem Formulations *(Targeted by Mod 5: Q1, Q2, Q8, Q9, Q13)***
- **8-Puzzle Problem:**
  - *State Space:* 3x3 grid configuration. Initial state is scrambled; goal is ordered.
  - *Operators:* Move Blank (Up, Down, Left, Right).
  - *Representation Impact:* Representing as a 1D array requires complex modular arithmetic. A 2D array or bit-string drastically reduces memory, exponentially improving search speed.
- **8-Queens Problem:**
  - *Constraints:* No two queens share a row, column, or diagonal.
  - *Backtracking vs Brute Force:* Brute force evaluates all $64^8$ combinations at the end. Backtracking checks constraints *during* placement. If invalid, it prunes the branch immediately, saving massive computational time.
- **Travelling Salesman Problem (TSP):**
  - *Formulation:* Visit all cities exactly once, return to start, with minimum cost.
  - *Limitations:* Exact methods (Brute force $O(n!)$) suffer from combinatorial explosion, making them impossible for large numbers of cities.

## **Uninformed Search Methods *(Targeted by Mod 5: Q3, Q4, Q10, Q11)***
- **Breadth-First Search (BFS):**
  - *Mechanism:* Uses a FIFO Queue. Expands level-by-level radially.
  - *Optimality:* Mathematically guarantees the shortest optimal path in unweighted graphs because it strictly checks all paths of length $N$ before $N+1$.
- **Depth-First Search (DFS):**
  - *Mechanism:* Uses a LIFO Stack. Dives deeply down a single branch before backtracking.
  - *Failures:* 
    - Fails to find optimal solutions because it ignores path cost (finds a deep path before checking shallow alternatives).
    - Fails completeness in infinite trees (dives infinitely without backtracking).

## **Informed & Local Search Methods *(Targeted by Mod 5: Q5, Q6, Q12, Q14)***
- **A* Search Algorithm:**
  - *Evaluation:* $f(n) = g(n) + h(n)$ [Past cost + Heuristic guess].
  - *Heuristics:* If $h(n)$ is admissible (never over underestimates distance), A* guarantees finding the optimal path efficiently.
- **Hill Climbing Algorithm:**
  - *Mechanism:* Iteratively moves to the neighboring state with the highest value.
  - *Local Optima:* Gets permanently stuck on a peak that is lower than the global maximum because it cannot backtrack.
  - *Plateau:* A flat landscape with no gradient, causing directionless random wandering.

## **Genetic Algorithms *(Targeted by Mod 5: Q7)***
- **Fitness Function:** Evaluates and scores how close a given "chromosome" is to the optimal solution. Ensures only the "fittest" solutions are selected to pass their traits to the next generation, driving evolution.

---

# **Module 6: Sustainable Agriculture and Food Systems**

## **Sustainable Agriculture *(Targeted by Mod 6: Q1, Q2, Q8, Q9)***
- **Definition:** Meeting society's current food needs without compromising future generations' ability to do the same.
- **Objectives & Dimensions:**
  - *Environmental:* Preserving biodiversity, water conservation.
  - *Economic:* Ensuring farm profitability and viability.
  - *Social:* Fair labor practices and equity.
- **Role in Food Security:** Sustainable farming preserves soil/water, guaranteeing the **Stability** and **Long-term Availability** of global food resources.
- **Precision Farming:** Uses IoT sensors, GPS, and drones to apply water/chemicals *only* where needed, maximizing yield and minimizing environmental waste.

## **Food Systems *(Targeted by Mod 6: Q3, Q10, Q11, Q12)***
- **Concept & Components:** Encompasses all processes feeding a population.
  - *Components:* Production -> Processing -> Distribution -> Retail -> Consumption -> Waste.
  - *Interdependence:* A logistics failure (truck strike) immediately causes retail shortages and massive production waste (rotting crops).
- **Global vs Local Food Systems:**
  - *Global:* Highly efficient, massive yield, cheap food. Highly unsustainable, complex supply chains, massive transport emissions.
  - *Local:* Highly sustainable, short supply chains, low emissions. Lower efficiency and yield, struggling to feed mega-cities alone.

## **Challenges & Data-Driven Solutions *(Targeted by Mod 6: Q4, Q5, Q6, Q7, Q13)***
- **Challenges of a Growing Population:**
  - *Climate Change:* Extreme weather directly destroys crop yields.
  - *Water Scarcity:* Agriculture drains 70% of freshwater.
  - *Food Wastage:* 30% of food rots due to poor logistics.
- **Data-Driven Opportunities:**
  - *Decision Making:* IoT soil moisture data combined with ML predicts exact harvesting windows and disease outbreaks.
  - *Logistics & Waste:* Predictive analytics perfectly match supply to demand to stop overstocking. Route optimization algorithms map the fastest paths for cold-chain trucks, minimizing transit spoilage.

---
> **End of Revised Targeted Notes**
