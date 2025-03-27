# **Setting Up Nextflow and Freyja**

Before we start building workflows, let’s set up our environment by installing [Nextflow](https://www.nextflow.io/docs/latest/overview.html) and [Freyja](https://andersen-lab.github.io/Freyja/index.html#).

## **Prerequisites**
make sure you have:

- A **Linux or macOS** system (Windows users can use WSL, a Linux environment for Windows).
- **Conda**, a tool that makes managing software and dependencies easy, should be installed. If you don’t have it yet, follow the official [installation guide](https://docs.conda.io/projects/conda/en/latest/user-guide/install/index.html).

---

### **Step 1: Installing Nextflow and Freyja via Conda**

Once Conda is set up, create a new environment named training-tutorial with Python 3.10 by running:

```bash
conda create -n training-tutorial python=3.10 -y
```

---

### **Step 2: Activate the Environment**

Before installing software, activate your new environment:
```bash
conda activate training-tutorial
```

---

### **Step 3: Install nextflow**

Nextflow is a tool for managing workflows. Install it by running:

```bash
conda install bioconda::nextflow -y
```

---

### **Step 4: Install freyja**

Freyja is used for lineage analysis. Install it with:

```bash
conda install bioconda::freyja -y
```

---

### **Step 5: Install pyarrow (a required dependency)**

Freyja needs pyarrow to work properly. Install it using:

```bash
conda install anaconda::pyarrow -y
```

---

### **Step 6: Verify installation**

Once installed, check if everything is working by running:

```bash
nextflow -version
```

output:
```
      N E X T F L O W
      version 24.10.5 build 5935
      created 04-03-2025 17:55 UTC (20:55 EAST)
      cite doi:10.1038/nbt.3820
      http://nextflow.io
```

---

```bash
freyja --version
```
output:
```
freyja, version 1.5.3
```

If these commands display version information, your setup is complete!

---