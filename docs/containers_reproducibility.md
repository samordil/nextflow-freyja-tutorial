# **Containers & Reproducibility in Nextflow**  

## **Overview**
Reproducibility is a **key challenge** in bioinformatics workflows. Different environments may have different software versions, leading to inconsistent results.  

To solve this, **Nextflow supports containers** like:

- **[Docker](https://docs.docker.com/get-started/)** – A widely used containerization tool.  
- **[Singularity](https://docs.sylabs.io/guides/3.0/user-guide/quick_start.html)** – Preferred for **HPC (high-performance computing)** environments.  
- **[Conda](https://docs.conda.io/projects/conda/en/latest/user-guide/getting-started.html)** – A package manager for dependency management.  

Using containers ensures that your pipeline runs identically on any system!

---

## **Why Use Containers?**
- **Avoids dependency issues** – No need to manually install software.  
- **Ensures reproducibility** – The same environment every time.  
- **Easy to share** – Just send your containerized pipeline to collaborators.  
- **Compatible with HPC clusters** – Works with Singularity and Conda.  

---

### **Using Docker with Nextflow**

Docker packages everything needed for your pipeline into an isolated environment.  

#### **Step 1: Install Docker**
Follow the official guide: [Docker Installation](https://docs.docker.com/get-docker/)  

#### **Step 2: Define a Docker Image in `nextflow.config`**

```nextflow
process {
    container 'freyja:latest'
}
```

This tells Nextflow to use the freyja Docker image when running processes.

### **Step 3: Run Your Pipeline with Docker**

```bash
nextflow run main.nf -with-docker
```

Nextflow will automatically pull the container and run everything inside it!

---

### **Using Singularity for HPC Clusters**

If your system doesn’t support Docker (e.g., on HPC clusters), use Singularity instead.

### **Step 1: Install Singularity**
Follow the official guide: Singularity Installation

### **Step 2: Use Singularity in nextflow.config**

```nextflow
process {
    container 'docker://freyja:latest'
}
```
Singularity can pull and use Docker images, making it HPC-compatible.

### **Step 3: Run Your Pipeline with Singularity**

```bash
nextflow run main.nf -with-singularity
```
This runs your pipeline inside a secure Singularity container!

---

## **Using Conda for Dependency Management**
If you can’t use Docker or Singularity, use Conda to install packages locally.

### **Step 1: Define Conda Dependencies in nextflow.config**

```nextflow
process {
    conda 'bioconda::freyja'
}
```

### **Step 2: Run Your Pipeline with Conda**

```bash
nextflow run main.nf -with-conda
```

Nextflow will automatically create a Conda environment for each process!

---