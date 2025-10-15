# 🎵 From Sound to Insight  
### *Scalable Feature Engineering, Popularity Modeling, and Clustering of Spotify Tracks with Apache Spark*

**KTH Royal Institute of Technology – ID2221: Data-Intensive Computing, Fall 2025**

**Authors:**  
Leonardo Liparulo · Emanuele Minotti · Stefano Romano · Giannantonio Sanrocco  
📧 `minotti | sromano | sanrocco | liparulo @kth.se`

---

## 📘 Overview

This project investigates the relationship between musical features and the **popularity of Spotify tracks**, implementing a fully **scalable big data pipeline** using **Hadoop** and **Apache Spark**.  
We designed an **end-to-end distributed workflow** that handles ingestion, preprocessing, modeling, and clustering over a large dataset to demonstrate the principles of **data-intensive computing**.

---

## 🗂️ Dataset

We use the **[Spotify Tracks Dataset](https://www.kaggle.com/datasets/maharshipandya/-spotify-tracks-dataset)** (≈114,000 songs), containing:

- **Identifiers & metadata** (track ID, name, genre)  
- **Compositional features:** tempo, key, mode, duration, time signature  
- **Audio descriptors:** danceability, energy, loudness, valence, acousticness, etc.  
- **Target variable:** popularity (0–100)

---

### 3️⃣ Prepare the Dataset

Download the dataset via [Kaggle](https://www.kaggle.com/datasets/maharshipandya/-spotify-tracks-dataset)  
or manually upload it to your Google Drive, for example under:

```python
data_path = "/content/drive/MyDrive/spotify_dataset.csv"
```

---

### 4️⃣ Execute the Pipeline

Run the notebooks **in sequence** to reproduce the complete data-intensive workflow:

| Notebook | Description |
|-----------|--------------|
| `01_Data_Ingestion.ipynb` | Configure Hadoop HDFS, ingest the raw dataset, and create a bronze Parquet copy |
| `02_Preprocessing.ipynb` | Clean, normalize, and scale the data to generate a silver Parquet dataset |
| `03a_Composition_Popularity_Model.ipynb` | Train Ridge Regression using only compositional (structural) audio attributes |
| `03b_Popularity_Features.ipynb` | Compute feature importances using Lasso Regression and Random Forest |
| `04_Clustering.ipynb` | Apply K-Means clustering, evaluate inertia, and visualize the discovered groups |

All required dependencies (Hadoop, Spark, and Python libraries) are automatically installed when running in Google Colab.  
You can execute the pipeline entirely in the cloud without local setup.

---

## 🧠 Technologies

This project integrates multiple technologies to demonstrate **scalable data processing and machine learning**:

- **Apache Spark (PySpark):** distributed data analytics, MLlib for regression and clustering  
- **Hadoop HDFS:** reliable, scalable file storage for big data workloads  
- **Google Colab + Drive:** lightweight cloud execution environment and persistent storage  
- **Python Libraries:** `pandas`, `numpy`, `matplotlib`, `seaborn`, `pyspark.ml`  
- **File Formats:** CSV (raw), Parquet (bronze/silver datasets)  

---

## 🧩 Project Structure

```bash
├── 01_Data_Ingestion.ipynb
├── 02_Preprocessing.ipynb
├── 03a_Composition_Popularity_Model.ipynb
├── 03b_Popularity_Features.ipynb
├── 04_Clustering.ipynb
│
├── data/
│   └── spotify_dataset.csv
│
├── results/
│   ├── feature_importance.csv
│   ├── clusters_summary.csv
│   └── visualizations/
│
└── README.md
```

**Folders:**
- `data/` → contains the raw Spotify dataset  
- `results/` → stores feature importances, clustering results, and generated plots  
- `.ipynb` notebooks → modular pipeline components, runnable independently or in sequence  

---
