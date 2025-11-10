#  Using Statistical Machine Learning with Apache Spark - *Combined Cycle Power Plant (CCPP) Dataset*

## Overview
This project applies **Apache Spark** and **machine learning** techniques to analyze the **Combined Cycle Power Plant (CCPP)** dataset from the [UCI Machine Learning Repository](https://archive.ics.uci.edu/dataset/294/combined+cycle+power+plant).

The analysis uses both **regression** and **classification** models built in **PySpark MLlib**, executed on a **two-node Spark cluster** to demonstrate distributed data processing and model scalability.

---

## Team Members
| Member | Algorithms Used | Type |
|---------|------------------|------|
| **Member 1 (Power_1)** | Random Forest Regressor + Random Forest Classifier | Regression & Classification |
| **Member 2 (Power_2)** | Linear Regression + Logistic Regression | Regression & Classification |

---

##  Dataset Description
- **Source:** UCI Machine Learning Repository
- **Samples:** 9,568 records
- **Attributes:**
  - `AT` – Ambient Temperature (°C)
  - `V` – Exhaust Vacuum (cm Hg)
  - `AP` – Atmospheric Pressure (mbar)
  - `RH` – Relative Humidity (%)
  - `PE` – Net Electrical Output (MW, target)

Tasks performed:
- **Regression:** Predict `PE` as a continuous variable.
- **Classification:** Predict **High** or **Low** power output (based on median `PE`).

---

## Environment Setup
- **Frameworks:** Apache Spark 3, Hadoop 3
- **Language:** Python (PySpark API)
- **Cluster:** 2 Virtual Machines (Master – `hadoop1`, Worker – `hadoop2`)
- **Java:** OpenJDK 8
- **Libraries:**
  `pyspark.sql`, `pyspark.ml`, `pyspark.ml.feature`, `pyspark.ml.regression`, `pyspark.ml.classification`, `pyspark.ml.evaluation`, `time`

---

##  How to Run

### 1️ Start the Cluster
```bash
start-dfs.sh
start-yarn.sh
/opt/spark/sbin/start-master.sh
/opt/spark/sbin/start-worker.sh spark://hadoop1:7077
```

### 2️ Submit the Jobs
```bash
spark-submit --master spark://hadoop1:7077 "Power predict.py"
spark-submit --master spark://hadoop1:7077 "Power predict 2.py"
```

---

## 📊 Model Results

### **Regression Results**
| Model | RMSE | MAE | R² |
|--------|------:|-----:|----:|
| Linear Regression (Power_2) | 3.481 | 2.662 | 0.956 |
| Random Forest Regressor (Power_1) | 3.481 | 2.662 | 0.956 |

> Both regression models performed equally well, confirming that the dataset’s relationship between inputs and power output is linear.

---

### **Classification Results**
| Model | Accuracy | Precision | Recall | AUC | Train Time (s) |
|--------|-----------:|-----------:|-----------:|-----------:|-----------:|
| Logistic Regression (Power_2) | 0.952 | 0.952 | 0.952 | 0.991 | 0.85 |
| Random Forest Classifier (Power_1) | 0.960 | 0.960 | 0.960 | 0.995 | 6.33 |

> Both classifiers performed excellently. Random Forest achieved slightly higher metrics but required more training time.

---

## Challenges
- Configuring Spark–Hadoop across two VMs (SSH and worker setup).
- Environment variable mismatches (`JAVA_HOME`, `SPARK_HOME`).
- Data access issues between HDFS and local storage.
- Occasional Spark shell freezes due to driver communication settings.

---

##  Key Takeaways
- Regression models showed **identical accuracy (R² = 0.956)**, confirming linearity in the dataset.
- **Random Forest** achieved slightly better classification metrics (AUC = 0.995).
- Spark’s distributed framework can efficiently handle big data processing and ML workloads.

---

## References
- Dataset: [UCI Combined Cycle Power Plant](https://archive.ics.uci.edu/dataset/294/combined+cycle+power+plant)
- Tools: Apache Spark, Hadoop, PySpark, Linux
