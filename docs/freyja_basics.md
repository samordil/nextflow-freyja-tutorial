# **Introduction to Freyja**
 
[Freyja](https://andersen-lab.github.io/Freyja/index.html#) is a tool for **analyzing SARS-CoV-2 sequencing data**. It helps identify **viral lineages** and estimate their **relative abundances** by processing variant data from sequencing reads. It is typically used after primer trimming and variant calling.

## **Why Use Freyja?**

- **Accurate Variant Analysis** – Identifies SARS-CoV-2 variants in sequencing data.  
- **Computationally Efficient** – Fast processing of large sequencing datasets.  
- **Integrates with Nextflow** – Can be automated in bioinformatics pipelines.  

---

## **Understanding Freyja Commands**
Freyja provides several commands for analyzing sequencing data. In this tutorial, we will focus on three key commands:

- [`freyja variants`](https://andersen-lab.github.io/Freyja/src/usage/variants.html) – This command analyzes a BAM file to identify genetic variants using samtools and iVar
- [`freyja demix`](https://andersen-lab.github.io/Freyja/src/usage/demix.html) – Estimates the relative abundances of viral lineages.

These commands form the foundation of the Nextflow pipeline we will build in the next section.

---

## **Running Freyja Commands**
Now that we understand the key Freyja commands, let's see how they are executed.

### **Running `freyja variants` command**
This command extracts variant and depth information from a sequencing dataset.
```bash
freyja variants sample1.bam \
  --variants sample1_variants.tsv \
  --depths sample1.depths \
  --ref ref_genome.fasta
```
Breakdown:

- ***sample1.bam*** – Input BAM file containing aligned sequencing reads.
- `--variants` ***sample1_variants.tsv*** – Output file storing variant information.
- `--depths` ***sample1.depth*** – Output file storing sequencing depth information.
- `--ref` ***ref_genome.fasta*** – input Reference genome file to align against.

!!! note  
    The `freyja variants` command above takes **2 input files**: a **BAM file** (sequencing data) and a **FASTA file** (reference genome). It produces **2 output files**: a **.depth file** (sequencing depth information) and a **.tsv file** (variant details).
---

### **Running `freyja demix`command**
Once we have the variant and depth files, we can estimate lineage abundances.

```bash
freyja demix sample1_variants.tsv sample1.depth \
--output sample_id.demix.tsv
```
Breakdown:

- ***sample1_variants.tsv*** – Input variant file from freyja variants.
- ***sample1.depth*** – Input depth file from freyja variants.
- `--output` ***sample1_demix.tsv*** – Output file storing detected lineages, their relative abundances, and a summary based on known variant groups. .

!!! note  
    The `freyja demix` command above takes **2 input files**: a **.depth file** (sequencing depth information) and a **.tsv file** (variant details) and generates **1 .tsv output file (relative abundance)**: 

---

Since we've covered two key Freyja commands, we can now integrate them into a Nextflow pipeline to reinforce Nextflow concepts.

---