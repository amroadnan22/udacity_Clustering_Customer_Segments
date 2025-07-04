# Identify Customer Segments

A complete, end‑to‑end workflow for discovering meaningful clusters in a general‑population demographics dataset using modern Python **(≥ 3.11)**, scikit‑learn, and complementary data‑science libraries. The project walks through data cleaning, feature engineering, dimensionality reduction, clustering, evaluation, and interpretation wrapping everything in reproducible notebooks and scripts.

---

## ✨ Project Highlights

* **Clean, modular code base** with clear separation between data, notebooks, and reusable pipelines.
* **Scalable preprocessing**: automated missing‑value handling and one‑hot/ordinal encoding that adapts to arbitrary tabular inputs.
* **Dimensionality reduction** via PCA to tame high‑dimensional data while preserving > 90 % of variance.
* **Cluster discovery** with K‑Means (elbow & silhouette diagnostics) plus optional Gaussian Mixture & HDBSCAN extensions.
* **Rich visualizations**—elbow curve, silhouette plot, cluster heatmaps, and interactive embeddings.
* **Jupyter + CLI**: run the whole analysis in notebooks or headless via the command line.
* **Reproducible environment**: lockfile for exact package versions and Makefile targets for common tasks.

---

## 🔧 Requirements

| Package      | Tested Version | Notes                               |
| ------------ | -------------- | ----------------------------------- |
| Python       | **3.11**       | ≥ 3.11 recommended; 3.10 also works |
| numpy        | 1.26.x         |                                     |
| pandas       | 2.2.x          |                                     |
| scikit‑learn | 1.5.x          |                                     |
| matplotlib   | 3.9.x          |                                     |
| seaborn      | 0.13.x         | optional, for nicer charts          |
| jupyterlab   | 4.x            | for notebook workflows              |
| joblib       | 1.5.x          | model persistence                   |
| tqdm         | 4.x            | progress bars                       |

Install with **conda** (recommended):

```bash
conda env create -f environment.yml
conda activate customer‑segments
```

—or with **pip**:

```bash
python -m venv .venv
source .venv/bin/activate  # Windows: .venv\Scripts\activate
pip install -r requirements.txt
```

---

## 🚀 Quickstart

1. **Clone** the repo

   ```bash
   git clone https:github.com/amroadnan22/udacity_Clustering_Customer_Segments.git
   cd customer‑segments
   ```
2. **Install** dependencies (see above).
3. **Add data**: place your raw CSV/Parquet files in `data/raw/`. Example dataset schema is documented in `notebooks/01_data_cleaning.ipynb`.
4. **Run the full pipeline** with Make:

   ```bash
   make all        # clean → engineer → pca → cluster → report
   ```

   or open the notebooks sequentially in JupyterLab for an interactive walkthrough.
5. **Inspect results** in `results/` and the final notebook `04_results.ipynb`.

---

## 🧪 Methodology & Code Walkthrough

### 1 ▸ Data Cleaning (`data_prep.py` / `01_data_cleaning.ipynb`)

* **Missing values**: numeric → median impute, categorical → new `"Unknown"` category.
* **Outlier guardrails**: winsorization at the 1st/99th percentiles.
* **Train/test split** by stratified sampling on key demographics.

### 2 ▸ Feature Engineering (`features.py`)

* One‑hot encode nominal vars (drop‑first to avoid collinearity).
* Ordinal‑encode ordered categories.
* Standard‑scale all numeric columns.

### 3 ▸ Dimensionality Reduction (`dimensionality.py`)

* Fit PCA on the training set, retaining components that explain **≥ 90 % variance** (typically 40–50 PCs).
* Save the fitted transformer to `models/pca.joblib`.

### 4 ▸ Clustering (`clustering.py` / `03_clustering.ipynb`)

* Iterate **k = 2…30**; record *inertia* and *silhouette* scores.
* Select optimal **k** via elbow + peak silhouette (defaults to k=6).
* Persist the final `KMeans` model to `models/kmeans_k6.joblib`.

### 5 ▸ Evaluation & Interpretation (`04_results.ipynb`)

* Silhouette plot to visualise cohesion vs. separation.
* PCA 2‑D scatter coloured by cluster label.
* Cluster profiles: feature means ± std vs. population means.

---

## 📊 Example Results

*Silhouette Score:* **0.42** @ k = 6
*Top distinguishing features:* `Age`, `Income`, `Urbanicity`, `FamilyStatus`.

Full discussion and figures are embedded in the results notebook.

---

## 🗺️ Roadmap / Future Work

* AutoML sweep for alternative clustering algorithms (GMM, HDBSCAN, spectral).
* SHAP or permutation importance for deeper feature impact analysis.
* Deploy as a **FastAPI** microservice that returns cluster IDs for incoming records.

---

## 🤝 Contributing

1. Fork the repo & create a feature branch.
2. Run `pre‑commit install` to auto‑format with *ruff* & *black*.
3. Open a pull request describing your changes.

Please adhere to the existing code style and write unit tests for new logic.

---

## 📄 License

Distributed under the **MIT License**. See `LICENSE` for details.

---

## 🙋‍♂️ Contact

**Amro Adnan Badran**
\[amroadnanb@gmail.com](mailto:amroadnanb@gmail.com)
Questions? Ideas? Feel free to open an issue or email me directly.
