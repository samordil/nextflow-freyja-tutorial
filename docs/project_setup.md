# **Setting Up the Project Structure**

Before writing our Nextflow pipeline, let's first create the necessary files and directories step by step. This will help us organize our project properly.

---

## **Step 1: Create the Main Project Directory**
First, create a new directory for the pipeline and navigate into it:
```bash
mkdir training  
cd training  
```
This will be the root directory where all pipeline files will be stored.

---

## **Step 2: Create the Main Pipeline Script**
The main.nf file defines how the pipeline runs. Create this file:

```bash
touch main.nf  
```
This script will later contain the workflow definition that connects different processes.

## **Step 3: Create the Configuration File**
Next, create nextflow.config, which will store pipeline settings such as memory, CPU usage, and execution options.

```bash
touch nextflow.config  
```

---

## **Step 4: Create the Modules Directory**
To keep our pipeline organized, we'll use Nextflow modules for different steps. Create a `modules/` directory and add the necessary files:

```bash
mkdir modules  
touch modules/freyja_variants.nf  
touch modules/freyja_demix.nf
```

Each of these .nf files will contain a Nextflow process for running Freyja commands.

---

## **Step 5: Set Up the Data Directory**
Now, let's create a folder for input data and add placeholder files.
```bash
mkdir data  
touch data/ref_genome.fasta  
```

Inside `bam_files/`, add some sample .BAM files (or copy your actual BAM files here):

```bash
mkdir data/bam_files  
touch data/bam_files/sample1.bam  
touch data/bam_files/sample2.bam  
touch data/bam_files/sample3.bam  
```

!!! note
    If you already have a `reference genome` and `.BAM` files, copy them into the `data/` folder instead of creating placeholder files.

---