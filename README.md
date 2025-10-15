🎵 From Sound to Insight

Scalable Feature Engineering, Popularity Modeling, and Clustering of Spotify Tracks with Apache Spark

Authors:
Leonardo Liparulo · Emanuele Minotti · Stefano Romano · Giannantonio Sanrocco
📧 minotti | sromano | sanrocco | liparulo @kth.se

⸻

📘 Overview

This project investigates the relationship between musical features and the popularity of Spotify tracks, implementing a fully scalable big data pipeline using Hadoop and Apache Spark.
We designed an end-to-end distributed workflow that handles ingestion, preprocessing, modeling, and clustering over a large dataset to demonstrate the principles of data-intensive computing.

⸻

🗂️ Dataset

We use the Spotify Tracks Dataset (≈114,000 songs), containing:
	•	Identifiers & metadata (track ID, name, genre)
	•	Compositional features: tempo, key, mode, duration, time signature
	•	Audio descriptors: danceability, energy, loudness, valence, acousticness, etc.
	•	Target variable: popularity (0–100)

⸻

⚙️ Methodology

1. Data Ingestion
	•	Configured Hadoop 3.3.6 inside Google Colab as a single-node HDFS cluster.
	•	Uploaded raw CSV data to HDFS and exported a bronze Parquet copy to Google Drive for persistence.
	•	Tools: HDFS, PySpark Core, PySpark SQL

2. Data Preprocessing
	•	Scalable cleaning and normalization using distributed DataFrame operations:
	•	Type casting, trimming, deduplication
	•	Missing-value imputation per genre
	•	Outlier capping (IQR)
	•	Feature scaling (Z-score normalization)
	•	Saved processed silver dataset as Parquet for efficient reuse.

3. Feature Importance Analysis
	•	Used Lasso Regression (L1) and Random Forest Regressor to evaluate predictive features for track popularity.
	•	Found that genre, danceability, and energy are dominant predictors.

4. Composition-Only Popularity Modeling
	•	Applied Ridge Regression using only compositional attributes (tempo, key, duration, etc.).
	•	Confirmed low explanatory power — popularity is driven more by perceptual than structural features.

5. Clustering Analysis
	•	Standardized audio features and applied K-Means (k=4), chosen via the elbow method.
	•	Leveraged RDD transformations (map, reduceByKey) for efficient centroid computation.
	•	Identified meaningful clusters representing:
	•	Dance-oriented music
	•	Acoustic/folk tracks
	•	Rap/spoken word
	•	Mainstream pop

⸻

📊 Results
	•	Popularity is largely determined by audio descriptors and categorical attributes.
	•	Random Forest results aligned with correlation analysis.
	•	Clustering revealed coherent genre-based partitions, confirming the value of feature scaling and distributed processing.
	•	End-to-end execution was efficient, reproducible, and fully cloud-based, leveraging Spark’s DAG optimization and HDFS integration.

⸻

🚀 How to Run

This project runs entirely in Google Colab — no local Spark/Hadoop setup required.

1️⃣ Setup

Open Google Colab and upload all notebooks.

2️⃣ Mount Google Drive

from google.colab import drive
drive.mount('/content/drive')

3️⃣ Prepare the Dataset

Download via KaggleHub or manually place it in your Drive:

data_path = "/content/drive/MyDrive/spotify_dataset.csv"

4️⃣ Execute the Pipeline

Run the notebooks in sequence:

Notebook	                              Purpose
01_Data_Ingestion.ipynb	                Configure Hadoop HDFS, ingest dataset, and create bronze Parquet copy
02_Preprocessing.ipynb	                Clean, normalize, and scale data into a silver Parquet dataset
03a_Composition_Popularity_Model.ipynb	Train Ridge Regression on compositional attributes
03b_Popularity_Features.ipynb	          Compute Lasso and Random Forest feature importances
04_Clustering.ipynb	                    Apply K-Means clustering and visualize results

All dependencies install automatically within Colab.

⸻

🧠 Technologies
	•	Apache Spark (PySpark) — distributed computation and MLlib
	•	Hadoop HDFS — scalable storage backend
	•	Google Colab + Drive — cloud execution and persistence
	•	Python libraries: pandas, numpy, matplotlib, pyspark.ml

⸻

🧩 Project Structure

├── 01_Data_Ingestion.ipynb
├── 02_Preprocessing.ipynb
├── 03a_Composition_Popularity_Model.ipynb
├── 03b_Popularity_Features.ipynb
├── 04_Clustering.ipynb
├── data/
│   └── spotify_dataset.csv
├── results/
│   ├── feature_importance.csv
│   ├── clusters_summary.csv
│   └── visualizations/
└── README.md
