# **Setting Up Nextflow and Freyja**

Before we start building workflows, let’s set up our environment by installing [Nextflow]((https://www.nextflow.io/docs/latest/overview.html)) and [Freyja](https://andersen-lab.github.io/Freyja/index.html#).

## **Prerequisites**
Make sure you have:
- A **Linux or macOS** system (Windows users can use WSL).
- **Java 8 or higher** installed.
- **Python 3** installed.

---

## **Installing Nextflow**

Nextflow requires **Java 8+** and can be installed using the following command:

```bash
curl -s https://get.nextflow.io | bash
chmod +x nextflow
sudo mv nextflow /usr/local/bin
```

To verify installation, run:
```bash
nextflow -version
```

---

## **Installing Freyja**

Freyja requires Python 3 and can be installed via pip:

```bash
pip install freyja
```

To check if Freyja is installed correctly run:
```bash
freyja --help
```
---

## **Alternative installation via conda**

If you prefer using Conda, first ensure it is installed. If not, follow the official [installation guide](https://docs.conda.io/projects/conda/en/latest/user-guide/install/index.html). 

Once Conda is set up, create a new environment named training-tutorial with Python 3.10 by running:

```bash
conda create -n training-tutorial python=3.10
```

Activate the newly created environment:

```bash
conda activate training-tutorial
```

Now, install Nextflow, the workflow manager:

```bash
conda install bioconda::nextflow
```

Then, install Freyja, the tool for lineage analysis:
```bash
conda install bioconda::freyja
```

Once installed, your environment is ready to use!

---