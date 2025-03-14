# **Building a Nextflow Pipeline with Freyja**

## **Overview**
In this section, we'll build a **Nextflow pipeline** integrating **Freyja** commands from the previous section. We'll demonstrate how **processes, channels, and operators** work together by using two interconnected modules (processes):

1.  **Variant Extraction Module** – Uses `freyja variants` to identify genetic variants in a sample and generate sequencing depth information from a `.BAM` file.  
2.  **Lineage Analysis Module** – Uses `freyja demix` to analyze the variant and depth data, estimating the relative abundance of different viral lineages.

---

## **Project Structure**
Here's how our pipeline will be structured:
```
training/
│-- main.nf
│-- nextflow.config
|-- modules/
|   ├── freyja_variants.nf 
|   ├── freyja_demax.nf 
│-- data/
│   ├── ref_genome.fasta
│   ├── bam_files/
│   │   ├── sample1.bam
│   │   ├── sample2.bam
│   │   ├── sample3.bam

```

Breaking it Down:

1.  `training/` - Root directory that contains all the files and folders for the Nextflow pipeline.
2.  `main.nf` – The main script that defines how the pipeline runs. It connects different steps and manages data flow.
3.  `nextflow.config` – A settings file where we define parameters like memory, CPU usage, and other execution settings.
4.  `modules` - A folder containing small, reusable nextflow scripts that handle different tasks in the pipeline.
    - `freyja_variants.nf` - Runs freyja variants to extract variant and depth information from BAM files.
    - `freyja_demax.nf` - Runs freyja demix to estimate lineage abundances.
5.  `data/` – This folder holds input files needed for the pipeline, such as sequencing data and sample information.
    - `ref_genome.fasta` – A reference genome file that serves as a guide for analyzing sequencing data.
    - `bam_files/` – A directory containing BAM files, which store aligned sequencing reads.

!!! note
    Each `.BAM` in the `bam_file` folder represents a different sample

---
