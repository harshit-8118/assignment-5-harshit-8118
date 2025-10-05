# DA5401 Assignment 5: Visualizing Data Veracity Challenges in Multi-Label Classification

**Student Name:** Harshit Shukla  
**Roll Number:** DA25S003  

---

## 1. Objective

This assignment explores how **non-linear dimensionality reduction techniques** can help in understanding challenges within **multi-label classification** problems, particularly focusing on **data veracity** issues such as noisy labels, outliers, and hard-to-learn samples.  
The analysis is based on the **Yeast dataset**, a biological dataset frequently used to study gene function prediction.

The main goal is to apply and compare **t-SNE** and **Isomap** to visualize complex high-dimensional gene expression data and interpret what these visualizations reveal about the dataset’s manifold structure and classification challenges.

---

## 2. Methodology

The analysis was conducted in three main parts:

### **Part A: Preprocessing and Setup**
- Loaded the **Yeast dataset** containing 103 features and 14 functional categories.  
- Created a simplified **categorical target variable** for visualization by selecting:
  - Two most frequent single-label classes.  
  - One most frequent multi-label combination.  
  - Grouped all others under “Other”.  
- Standardized features using **z-score normalization** to ensure distance-based methods like t-SNE and Isomap perform correctly.

### **Part B: t-SNE and Veracity Inspection**
- Applied **t-Distributed Stochastic Neighbor Embedding (t-SNE)** on the scaled feature space.
- Tested multiple perplexity values (`5, 15, 30, 50, 80`) to evaluate trade-offs between local and global structure preservation.
- Final perplexity chosen: **50**, as it provided the best balance between local cluster cohesion and global separation.
- Analyzed the resulting embedding to identify:
  - **Noisy/Ambiguous labels:** overlapping clusters of different colors.
  - **Outliers:** isolated or sparsely connected points.
  - **Hard-to-learn samples:** mixed-color regions indicating class ambiguity.

### **Part C: Isomap and Manifold Learning**
- Applied **Isomap** with varying neighborhood sizes (`n_neighbors = 5, 10, 15`).
- Compared results with t-SNE using quantitative metrics:
  - **Trustworthiness (local preservation):** t-SNE = 0.9316, Isomap = 0.7216  
  - **Distance correlation (global preservation):** t-SNE = 0.4087, Isomap = 0.4739
- Observed that t-SNE captured fine-grained local clusters, while Isomap revealed smoother global relationships, indicating a **moderately curved manifold**.

---

## 3. File Structure

The submission is organized as follows. For a complete evaluation, all files listed below are essential.

```
.
├── Assignment_5.ipynb      # The Jupyter Notebook with all code, analysis, and explanations.
└── README.md               # This documentation file.
```


---

## 4. How to Run the Analysis

1. Open `Assignment_5.ipynb` in **Jupyter Notebook** or **VS Code (Python environment)**.  
2. Ensure the following Python libraries are installed:
   - `numpy`, `pandas`, `matplotlib`, `seaborn`
   - `scikit-learn`, `scipy`, `umap-learn`
3. Run all cells sequentially.  
   The notebook is self-contained and automatically performs:
   - Data preprocessing
   - Embedding computation (t-SNE, Isomap)
   - Visual analysis and quantitative comparison

---

## 5. Key Findings and Recommendations

- The **t-SNE** visualization effectively revealed **local clusters**, making it ideal for detecting **noisy and ambiguous samples**.  
- The **Isomap** embedding provided better insight into **global manifold geometry**, showing that the data lies on a **nonlinear, moderately curved manifold**.
- The curvature and overlap of class regions indicate why **linear classifiers** would struggle on this dataset.
- For better model performance:
  - Use **nonlinear classifiers** such as kernel SVM or neural networks.
  - Consider **manifold-aware approaches** (e.g., UMAP or supervised embeddings).
  - Explore **metric learning** or **representation learning** to adapt to manifold complexity.
