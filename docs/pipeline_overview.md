# **Building a Nextflow Pipeline with Freyja**

## **Overview**
In this section, we'll build a **Nextflow pipeline** that integrates **Freyja** commands. This pipeline will have two key steps:

1. **Variant Extraction** – Uses `freyja variants` command to identify mutations and calculate sequencing depth from `.BAM` files.
2. **Lineage Analysis** – Uses `freyja demix` command to estimate the relative abundance of viral lineages.

---

## **Pipeline Structure**
The pipeline follows this directory structure:

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

### **What Each File Does**
| File/Folder         | Description |
|---------------------|-------------|
| `main.nf`          | Defines the **workflow**, linking different processes. |
| `nextflow.config`  | Stores **settings** like memory, CPU, and container options. |
| `modules/`         | Contains **Nextflow modules** for different tasks. |
| `freyja_variants.nf` | Runs `freyja variants` to extract mutations & depth data. |
| `freyja_demix.nf` | Runs `freyja demix` to estimate lineage abundances. |
| `data/`            | Stores input files like `reference genome` and `.BAM` files. |

Now that we understand the pipeline structure, let's set up the project step by step. 

---