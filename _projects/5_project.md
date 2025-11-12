---
layout: page
title: Boston MBTA Bus Equity & Reliability (CS506 Final Project)
description: Clustering MBTA bus routes to analyze reliability and equity using ridership, arrival–departure, and 2024 survey data.
img: assets/img/mbta-bus.jpg   # preview image on the projects grid
importance: 5
category: work
links:
  - name: code
    url: https://github.com/Chava-Sai/Boston-Bus-Equity-CS506-Final-Project
  - name: dataset
    url: https://www.kaggle.com/datasets/manaswiyadamreddy/boston-mbta-bus-equity-and-reliability-dataset/data
  - name: presentation
    url: https://youtu.be/rE_8_-GRwgw
---

## Overview
This project investigates **equity and reliability** of the **Boston MBTA bus system**, combining multiple datasets—**arrival–departure times**, **ridership**, and the **2024 passenger survey**—to explore relationships between service reliability and demographic factors.  
The study uses clustering techniques to group routes with similar operational profiles and assess whether service disparities correlate with rider demographics.

![BU Spark!](https://img.shields.io/badge/BU%20Spark!-Project-red.svg)

---

## Dataset & Setup
### Data Sources
- **Arrival–Departure Data** — schedule adherence, earliness, lateness, and headway.  
- **Ridership Data** — stop-level boardings, alightings, and passenger load across seasons.  
- **Passenger Survey Data** — 2024 MBTA System-Wide Survey with demographic attributes.  

### Project Structure
After downloading the cleaned data from Kaggle, place files under:

Boston-Bus-Equity-CS506-Final-Project/
├── data_cleaned_capped/
│   ├── arrival_departure.parquet
│   ├── ridership.csv
│   └── survey.csv
├── notebooks/clustering/
│   ├── clustering.ipynb
│   └── hierarchical_clustering.ipynb
└── README.md

### Run the Analysis
All clustering and visualizations are implemented in the notebooks inside  
`notebooks/clustering/`.

---

## Preliminary Visualizations

### Top Routes by Record Count
![Top Routes](https://github.com/user-attachments/assets/47cd60f9-591a-40cd-b0af-c6a89612070d)

### Headway & Arrival Delay Distributions
![Headway Delay](https://github.com/user-attachments/assets/7a125b48-9923-490a-97b9-437e101cb0da)

### Top Bus Routes by Late Arrival Rate
![Late Routes](https://github.com/user-attachments/assets/25f3bc3d-4365-44cb-b4d9-c89c935a3f16)

### Most-Late Routes (Latest Year)
![Most Late](https://github.com/user-attachments/assets/4613c31a-e987-41d8-896c-01c4262fc094)

### Late-Rate Trends (Top 5 Worst Routes)
![Trend](https://github.com/user-attachments/assets/f423f38d-ca4f-42b1-8781-344b16f400fa)

### Lateness Heatmap (Worst 20 Routes)
![Heatmap](https://github.com/user-attachments/assets/13cccbd7-9bd6-4fa7-ad54-be0c847176a6)

---

## Data Processing

### 1. Data Loading
Used `pandas` and `pyarrow` to handle large MBTA datasets (up to 30M rows each).  
Each dataset was verified for column types and consistency of identifiers.

### 2. Route ID Normalization
Route formats such as `"01"`, `"1-0-0"`, `"34E"` were standardized into a single normalized route column (`route_id_norm`).

### 3. Multi-Route Expansion
Survey entries like `"114&116&117"` were split into multiple rows to properly map demographic data to routes.

### 4. Dataset Filtering
Filtered to keep only routes present in **all three** datasets (ridership, arrival–departure, survey).

### 5. Efficient Indexing
Used NumPy boolean masks for slicing instead of Pandas indexing to avoid Arrow crashes.

### 6. Final Cleaned Outputs
All processed data stored in `data_cleaned_capped/`:
- `arrival_departure.parquet`  
- `ridership.csv`  
- `survey.csv`

---

## Modeling Methodology

### Feature Construction
Constructed route-level feature vectors including:
- Mean and median **boardings**, **alightings**, and **load**
- Mean & SD of **headway**
- **On-time performance rate** (±60 sec window)
- Total **unique stops** per route

### Standardization
Applied z-score normalization using `StandardScaler` for all numeric features.

### Clustering
Two clustering approaches were applied:

#### K-Means Clustering
- Optimal **K = 3** chosen based on silhouette scores (range = 2–8).  
- Each route assigned to one of 3 clusters.

#### Hierarchical Clustering
- **Ward linkage** method visualized via dendrogram.  
- **4 clusters** chosen after dendrogram inspection.

![Silhouette vs K](https://github.com/user-attachments/assets/e54b226d-b0cc-4fc8-8c55-2e75f1d6e807)
![K-Means PCA](https://github.com/user-attachments/assets/5befc26d-9a0d-40f3-9fbb-e8e6b4cc0cf4)
![Dendrogram](https://github.com/user-attachments/assets/db004e42-19bd-4797-a75c-32e8fe97a581)
![Hierarchical PCA](https://github.com/user-attachments/assets/dfc062ae-dbd2-4e3c-8475-95fc31c2a671)

---

## Demographic Correlation Analysis

Survey data was reshaped into long-form route–category format.  
Weighted proportions of **income** and **ethnicity** were computed per cluster.

### Income Distribution (K-Means)
![Income KMeans](https://github.com/user-attachments/assets/bedf63c8-8b48-4a68-a76f-2f339bf15ca3)

### Ethnicity Distribution (K-Means)
![Ethnicity KMeans](https://github.com/user-attachments/assets/073c28fd-0141-4d1f-954b-7e7a86bf03a5)

### Income Distribution (Hierarchical)
![Income Hierarchical](https://github.com/user-attachments/assets/00a73f29-4dad-4b70-a6d4-91a6edb5548b)

### Ethnicity Distribution (Hierarchical)
![Ethnicity Hierarchical](https://github.com/user-attachments/assets/08041fef-5666-4da6-b634-58ed6c2bddb8)

---

## Findings

- **Cluster 1:** High ridership, short headways — dense, high-frequency urban routes.  
- **Cluster 2:** Moderate ridership and balanced headways — regular city routes.  
- **Cluster 3:** Long headways, low ridership — suburban or low-demand routes.  
- **Cluster 4 (Hierarchical only):** Transitional routes with moderate variability.

### Key Observation
Demographic proportions were similar across clusters, indicating **no strong inequities** based solely on operational performance.

---

## Future Work
- Integrate **temporal reliability** (weekday vs weekend trends).  
- Include **stop-level metrics** like missed trips and headway variability.  
- Test **DBSCAN/HDBSCAN** or **GMM** for more flexible cluster shapes.  
- Combine MBTA operational data with **census-level socioeconomic features** for deeper equity analysis.

---

**Repository:** [github.com/Chava-Sai/Boston-Bus-Equity-CS506-Final-Project](https://github.com/Chava-Sai/Boston-Bus-Equity-CS506-Final-Project)  
**Dataset:** [Kaggle – Boston MBTA Bus Equity Dataset](https://www.kaggle.com/datasets/manaswiyadamreddy/boston-mbta-bus-equity-and-reliability-dataset/data)  
**Presentation:** [YouTube Video](https://youtu.be/rE_8_-GRwgw)