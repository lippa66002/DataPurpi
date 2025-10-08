# 🎵 Popularity & Musical Characteristics of Songs Across Streaming Platforms 

This project investigates how **musical features** (e.g., danceability, energy, valence, tempo) influence **song popularity** across streaming platforms such as Spotify, Apple Music, Deezer, and Shazam.  

We use **Apache Spark** for large-scale processing, **HDFS** for distributed storage, and **MLlib** for predictive modeling and clustering.  
Visualizations and dashboards are built with **Tableau / Plotly / Matplotlib**.  

---

## 📌 Objectives
- Identify which audio features most strongly correlate with popularity.
- Analyze differences across **genres** and **time periods**.
- Predict a track’s popularity from its musical composition.
- Cluster songs into **data-driven groups** (new “genres”) based on audio features.
- Explore artist/album dynamics and collaboration effects.

---

## 🛠️ Tech Stack
- **Storage**: HDFS (or Parquet for Colab runs)  
- **Processing**: Apache Spark (PySpark, Spark SQL, Spark MLlib)  
- **Machine Learning**: Regression, Classification, Clustering (MLlib)  
- **Visualization**: Tableau, Plotly, Matplotlib, Seaborn  
- **Version Control**: GitHub (+ Issues, Projects, Actions)  
- **Optional**: DVC for dataset versioning, Kafka for streaming simulation  

---

## 📂 Repository Structure
```
music-popularity-spark/
├─ data/                 # raw & processed data (ignored in Git)
├─ notebooks/            # Colab/Jupyter notebooks for EDA & prototyping
├─ src/
│  ├─ ingestion.py       # Load dataset (Kaggle → HDFS/Parquet)
│  ├─ preprocessing.py   # Cleaning, scaling, encoding
│  ├─ features.py        # Feature engineering
│  ├─ modeling.py        # MLlib regression/classification pipelines
│  ├─ clustering.py      # KMeans & segmentation
│  ├─ evaluation.py      # Metrics (RMSE, R², Precision/Recall)
│  └─ utils.py           # Helper functions
├─ dashboards/           # Tableau/Plotly dashboards
├─ conf/                 # Config files (YAML for Spark, thresholds, etc.)
├─ tests/                # Unit tests
├─ requirements.txt      # Python dependencies
├─ environment.yml       # (optional, for conda)
├─ dvc.yaml              # (optional, if using DVC for data)
└─ README.md             # Project documentation
```

---

## ⚡ Getting Started

### 1. Clone the repository
```bash
git clone https://github.com/<your-org>/music-popularity-spark.git
cd music-popularity-spark
```

### 2. Dataset (Kaggle)
We use the [Spotify Tracks Dataset](https://www.kaggle.com/datasets/maharshipandya/-spotify-tracks-dataset).  

Download via **Kaggle API**:
```bash
pip install kaggle
kaggle datasets download -d maharshipandya/-spotify-tracks-dataset -p data/
unzip data/*.zip -d data/
```

> ⚠️ The dataset is large → not committed to Git. Use **DVC** or shared storage.

### 3. Run Spark on Colab (quick start)
In a Colab notebook:
```python
!pip -q install pyspark==3.5.1

from pyspark.sql import SparkSession
spark = (SparkSession.builder
         .appName("music-popularity")
         .master("local[*]")
         .config("spark.sql.shuffle.partitions", "8")
         .getOrCreate())

df = spark.read.csv("data/spotify_tracks.csv", header=True, inferSchema=True)
df.printSchema()
```

### 4. Run with HDFS (optional, advanced)
Using Docker (single-node Hadoop + Spark):
```bash
docker-compose up -d
# put data into HDFS
docker exec -it namenode hdfs dfs -mkdir -p /data/raw
docker exec -it namenode hdfs dfs -put data/spotify_tracks.csv /data/raw/
```
Then in Spark:
```python
df = spark.read.csv("hdfs://namenode:9000/data/raw/spotify_tracks.csv", header=True, inferSchema=True)
```

### 5. Run on Databricks (alternative)
- Import CSV into **DBFS**.  
- Use **Repos** to connect GitHub repo.  
- Run Spark SQL + MLlib pipelines in shared workspace.  

---

## 🚀 Project Workflow
1. **Data Ingestion & Cleaning**  
   - Load dataset (CSV → Spark DataFrame).  
   - Handle missing values & outliers.  
   - Normalize numerical features, encode categorical ones.  

2. **Exploratory Data Analysis (EDA)**  
   - Correlations between audio features & popularity.  
   - Temporal analysis (release year, recency).  
   - Genre-level comparisons.  

3. **Modeling (Spark MLlib)**  
   - Regression: predict popularity score.  
   - Classification: predict whether a song enters charts.  
   - Clustering: group songs by musical features.  

4. **Visualization & Insights**  
   - Tableau/Plotly dashboards.  
   - Feature importance plots, cluster profiles, temporal trends.  

---

## 👥 Team Roles
- **Data Lead**: ingestion, DVC, schema management  
- **ML Lead**: regression, classification, feature importance  
- **Platform Lead**: Spark config, Docker/VM/HDFS, CI/CD  
- **Visualization Lead**: dashboards, storytelling, reporting  

---

## ✅ Expected Outcomes
- Key **drivers of popularity** across genres & time.  
- Predictive models for new track popularity.  
- Clusters of songs → new “data-driven genres”.  
- Interactive dashboards for artists, producers, and labels.  

---

## 📌 References
- Kaggle Dataset: [Spotify Tracks](https://www.kaggle.com/datasets/maharshipandya/-spotify-tracks-dataset)  
- Apache Spark MLlib Docs: https://spark.apache.org/docs/latest/ml-guide.html  
- DVC (Data Version Control): https://dvc.org/  
- Databricks Community: https://community.cloud.databricks.com/  

---
