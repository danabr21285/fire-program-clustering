# 🔍 FIRE Program Hierarchical Clustering Analysis

This project applies **hierarchical clustering** in R to analyze student profiles in the FIRE (Prematriculation) program. The goal is to identify patterns and subgroupings based on key indicators such as first-generation status, GPA, MCAT, and eventual COMLEX outcomes.

---

## 🎯 Objectives

- Cluster FIRE program students using binary academic and background variables
- Visualize student groupings via dendrograms
- Compare cluster-level outcomes and support needs
- Inform targeted intervention or resource planning for at-risk students

---

## 🛠️ Tools & Packages

- **Language**: R
- **Libraries**:
  - `tidyverse`
  - `cluster`
  - `fpc`
  - `factoextra`
  - `dendextend`
  - `janitor`
- **Distance Metric**: Manhattan
- **Linkage Method**: Average linkage
- **Visualization**: Colored dendrograms

---

## 📁 Dataset Features (binary variables used)

- `First.Gen` — First-generation college student  
- `HS.50..or.less.go.to.College` — High school population stats  
- `Received.GED`, `HPSA.Area` — Background risk markers  
- `MCAT.500`, `UG.Sci.Major`, `UG.SCI.GPA...3.4` — Academic readiness
- `Non.Traditional.25.`, `Out.of.UG.2.Years` — Non-traditional status
- `FIREParticipant`, `From.a.family.that.Received.Public.Assistance`
- `COMLEX` — Outcome (pass/fail)

---

## 🧠 Method Summary

1. Filtered dataset to include 13 relevant binary variables
2. Converted all categorical outcomes to 0/1
3. Calculated **Manhattan distance**
4. Applied hierarchical clustering using **average linkage**
5. Plotted and saved colored dendrograms using `dendextend`
6. Formed 3–4 clusters with `cutree`
7. Merged cluster labels into original dataset
8. Analyzed proportions by cluster using `tabyl()` and `adorn_percentages()`

---

## 📊 Sample Outputs

- 📌 Clustered dendrogram of all FIRE students  
- 📌 Frequency breakdowns of each variable by cluster  
- 📌 COMLEX pass rates by cluster

---

## 📦 Reproducible Steps (In R)

```r
# Load required packages
library(tidyverse)
library(cluster)
library(fpc)
library(factoextra)
library(dendextend)
library(janitor)

# Load your data
FIREdf <- read.csv("FIRE1.csv")

# Select binary features
bindf <- FIREdf[c(3,4,5,6,7,8,11,13,15,17,19,20,21)]

# Convert outcomes to binary (e.g., COMLEX P/F → 1/0)
bindf$COMLEX <- ifelse(FIREdf$COMLEX == "P", 1, ifelse(FIREdf$COMLEX == "F", 0, NA))

# Compute distance and cluster
match_dist <- dist(bindf, method="manhattan")
cl_match_avg <- hclust(match_dist, method="average")

# Visualize dendrogram
dend <- as.dendrogram(cl_match_avg)
dend_colored <- color_branches(dend, k = 3)
plot(dend_colored, main = "FIRE Student Clusters")
```

## 💡 Key Insights

- Several clusters aligned with **COMLEX risk and socioeconomic markers**
- First-gen, non-traditional, and GED students grouped together with distinct academic profiles
- Students with higher UG science GPA and MCAT ≥ 500 appeared clustered with better performance

---

## 📁 Files Included

- `fire_clustering.R` – Full analysis script
- `FIRE1.csv` – *(Not included — simulated or redacted data recommended)*
- `FIRE Project(Clustering Analyses).pptx` – Final presentation summarizing the full clustering analysis (K-means + hierarchical)
---

## 🔗 Related Work

- [COMLEX Question Generator](https://github.com/danabr21285/comlex-question-generator)
- [Admissions Dashboard](https://github.com/danabr21285/admissions-dashboard)

---

## 👩‍🏫 Author

**Dana Brooks**  
Executive Director of Admissions | Data & EdTech Advocate  
📧 danatallent@yahoo.com 
🔗 www.linkedin.com/in/dana-tallent-brooks-a15977a0 

---

> *“Clustering isn’t about separating students — it’s about seeing who needs to be brought closer to support.”*
