# **Setting Up the Project Structure**

Before running our Nextflow pipeline, let's create the necessary files and directories **step by step**.  

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
Next, create the `main.nf` file, which will define the workflow:

```bash
touch main.nf  
```

This script will later contain the workflow definition that links different processes.

---

## **Step 3: Create the Configuration File**
Now, create `nextflow.config`, which will store pipeline settings such as memory, CPU, and execution options.

```bash
touch nextflow.config  
```

---

## **Step 4: Create the Modules Directory**
To organize the pipeline, we'll store different steps as Nextflow modules inside a modules/ directory:

```bash
mkdir modules  
touch modules/freyja_variants.nf  
touch modules/freyja_demix.nf
```
Each of these `.nf` files will contain a Nextflow process for running Freyja commands.

--- 

## **Step 5: Set Up the Data Directory**
Finally, create a data/ folder to store input files:

```bash
mkdir data  
touch data/ref_genome.fasta  
```
Inside bam_files/, add some sample `.BAM` files (or copy real .BAM files here):

```bash
mkdir data/bam_files  
touch data/bam_files/sample1.bam  
touch data/bam_files/sample2.bam  
touch data/bam_files/sample3.bam 
``` 

Now that we’ve set up the project, let's start writing the Nextflow modules!

---