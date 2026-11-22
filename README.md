# ⚡ Introduction to PySpark

Welcome to the **Introduction to PySpark** repository! This project covers the fundamentals of distributed big data processing using **Apache Spark** with Python (**PySpark**), configured to run seamlessly on **GitHub Codespaces** (Ubuntu Linux cloud environment) without needing a local Virtual Machine.

---

## 📖 Overview

**PySpark** is the Python API for **Apache Spark**, an open-source, distributed computing framework designed for large-scale data processing and analytics. It combines the simplicity and rich ecosystem of Python with the speed and scalability of Spark's in-memory cluster computing engine.

### Key Concepts Covered
* **SparkSession & Architecture:** Understanding the Driver, Executors, and Cluster Manager.
* **Resilient Distributed Datasets (RDDs):** Low-level fault-tolerant distributed collections.
* **DataFrames & Spark SQL:** Structured data manipulation, filtering, aggregations, and SQL queries.
* **Data Ingestion & Export:** Working with CSV, JSON, and Parquet formats.
* **Scalable Pipelines:** Building and running distributed data processing workflows.

---

## ☁️ Environment Setup Guide (GitHub Codespaces)

Instead of running a heavy local Ubuntu VM via VMware and Remote-SSH, this repository uses **GitHub Codespaces**—giving you an instant **Ubuntu Linux** cloud container with **Visual Studio Code** ready out of the box.

### Prerequisites
* A **GitHub** account
* A modern web browser (or local **VS Code** with the *GitHub Codespaces* extension)

---

### Step 1: Launch a GitHub Codespace
1. Navigate to this repository on GitHub.
2. Click the green **`<> Code`** button at the top right.
3. Switch to the **Codespaces** tab and click **`Create codespace on main`**.
4. Wait a few moments while GitHub provisions your Ubuntu cloud environment and opens VS Code.

---

### Step 2: Install Java (OpenJDK)
Apache Spark runs on the Java Virtual Machine (JVM), so Java (JDK 11 or 17) must be installed first.

1. Open the integrated terminal in Codespaces (`Ctrl + ~` or **Terminal > New Terminal**).
2. Update package lists and install **OpenJDK 17**:
   ```bash
   sudo apt update && sudo apt install -y openjdk-17-jdk
   ```

---

### Step 3: Verify Java Installation & Set `JAVA_HOME`
After installing OpenJDK 17, verify that Java is installed properly and configure `JAVA_HOME` so PySpark and Hadoop/Spark binaries can locate it reliably:

1. **Verify the Java installation:**
   ```bash
   java -version
   ```

2. **Set the `JAVA_HOME` environment variable and add Java's `bin` directory to `PATH` (persisted in `~/.bashrc`):**
   ```bash
   echo 'export JAVA_HOME=/usr/lib/jvm/java-17-openjdk-amd64' >> ~/.bashrc
   echo 'export PATH=$JAVA_HOME/bin:$PATH' >> ~/.bashrc
   source ~/.bashrc
   ```

3. **Confirm `JAVA_HOME` is set correctly:**
   ```bash
   echo $JAVA_HOME
   ```

---

### Step 4: Create & Activate the PySpark Virtual Environment
Following best practices for isolated Python environments, create and activate `pyspark-env`:

1. **Create the virtual environment:**
   ```bash
   python3 -m venv ~/pyspark-env
   ```

2. **Activate the virtual environment:**
   ```bash
   source ~/pyspark-env/bin/activate
   ```
   *(Your terminal prompt should now display `(pyspark-env)` at the beginning)*.

---

### Step 5: Install PySpark & Jupyter
With `(pyspark-env)` active, install **PySpark** and **Jupyter/IPython** kernel support:

```bash
pip install --upgrade pip
pip install pyspark jupyter ipykernel
```

*(Optional)* Register the virtual environment as a Jupyter kernel so you can select it directly in VS Code `.ipynb` notebooks:
```bash
python -m ipykernel install --user --name=pyspark-env --display-name "Python (PySpark)"
```

---

### Step 6: Verify the PySpark Installation
1. **Create a test file named `test.py` in your workspace:**
   ```python
   from pyspark.sql import SparkSession

   # Initialize SparkSession in local mode
   spark = SparkSession.builder \
       .appName("PySparkCodespaceIntro") \
       .master("local[*]") \
       .getOrCreate()

   print("Apache Spark Version:", spark.version)

   # Quick DataFrame test
   data = [("Alice", 28), ("Bob", 34), ("Charlie", 25)]
   df = spark.createDataFrame(data, ["Name", "Age"])
   df.show()

   spark.stop()
   ```

2. **Run the script in the terminal:**
   ```bash
   python test.py
   ```
   *(Tip: If using VS Code notebooks or scripts, press `Ctrl + Shift + P` → **Python: Select Interpreter** → choose `~/pyspark-env/bin/python`)*.

---

### Step 7: Stop / Pause Your Codespace
When you finish working, stop your Codespace to conserve your free monthly GitHub Codespaces hours:
1. Click the **`Codespaces`** badge in the bottom-left corner of VS Code.
2. Select **`Stop Current Codespace`** (or stop it from your GitHub Codespaces dashboard).

---

## 📁 Repository Structure

```text
├── notebooks/          # Interactive Jupyter notebooks covering PySpark fundamentals
├── scripts/            # Standalone Python scripts (.py) for Spark jobs
├── datasets/           # Sample datasets used in exercises
└── README.md           # Project overview and Codespaces setup guide
```

---

## 🤝 Contributing
Feel free to fork this repository, open issues, or submit pull requests with additional PySpark examples and exercises.
