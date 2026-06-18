# Lab 2: Predictive Analytics with Machine Learning

**Duration:** 2 weeks [18 Jun – 25 Jun, 2026]
**Due Date:** 25th June, 2026
**Format:** Jupyter Notebook / Google Colab
**Grading:** This is a graded lab.

**Description:** You will run a complete machine-learning workflow on two real tabular datasets,
covering both supervised and unsupervised learning. Using NumPy, Pandas, and scikit-learn you will
load and explore the data, clean and preprocess it, engineer features, split it into
train/validation/test sets, train models, check for overfitting, and discover hidden structure
with K-Means clustering.

**Topics Covered:** Supervised learning (regression & classification), unsupervised learning
(clustering), feature engineering, train/validation/test splits, model evaluation, overfitting.

---

## Lab Setup

1. Create a public repository called `lab-2-predictive-analytics` on GitHub/GitLab.
2. Clone it to your machine (or link it to Google Colab).
3. Create the notebook `lab_2_predictive_analytics.ipynb` inside the repo (a scaffolded template is provided).

### Local setup

```bash
python -m venv .venv
source .venv/bin/activate        # Windows: .venv\Scripts\activate
pip install -r requirements.txt
jupyter lab
```

`requirements.txt`:

```
numpy
pandas
scikit-learn
matplotlib
seaborn
```

### Google Colab setup

Open a new Colab notebook, rename it `lab_2_predictive_analytics.ipynb`, and run the cells
directly. The datasets load straight from their URLs, so no Drive mount is required.

---

## The Datasets

| # | Task | Dataset | Type | Target |
|---|------|---------|------|--------|
| 1 | Regression | NYC Yellow Taxi trips | Supervised | `tip_amount` (continuous) |
| 2 | Multi-class classification | Obesity-level prediction | Supervised | `NObeyesdad` (7 classes) |
| 3 | Clustering (K-Means) | Obesity features (labels hidden) | Unsupervised | discover groups |

- Taxi: `https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/pu9kbeSaAtRZ7RxdJKX9_A/yellow-tripdata.csv`
- Obesity: `https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/GkDzb7bWrtvGXdPOfk6CIg/Obesity-level-prediction-dataset.csv`

---

## Tasks

**Section 1 — Regression (Taxi):** load & explore, preprocess + feature-engineer, split into
train/validation/test, train a regressor, and evaluate RMSE/R² on all three splits to diagnose
overfitting.

**Section 2 — Classification (Obesity):** load & explore (check class balance), encode and scale,
make a *stratified* train/validation/test split, train a multi-class classifier, and evaluate
accuracy/macro-F1 plus a confusion matrix to diagnose overfitting.

**Section 3 — Clustering (Obesity, unsupervised):** drop the labels, choose `k` with the Elbow /
silhouette method, fit K-Means, visualise the clusters (two features or PCA), and compare the
clusters against the true obesity levels with a crosstab.

**Section 4 — Reflection:** short written answers comparing the three tasks.

Each section ends with a **Student Reasoning** box that must be completed — reasoning is graded.

---

## Submission Instructions

1. Restart & Run All so every cell executes top-to-bottom with no errors.
2. Fill in every Student Reasoning box and the Section 4 reflection.
3. Ensure plots are visible in the saved notebook.
4. Commit and push the notebook to your `lab-2-predictive-analytics` repository.
5. Submit the repository link to the course portal.

### Grading (100 pts)

| Area | Pts |
|------|-----|
| Section 1 — Regression | 30 |
| Section 2 — Classification | 30 |
| Section 3 — K-Means clustering | 20 |
| Reasoning boxes & reflection | 15 |
| Reproducibility (clean run, `random_state`, tidy code) | 5 |
