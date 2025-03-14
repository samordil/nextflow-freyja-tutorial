# **Writing Nextflow Processes for Freyja**

## **Overview**
In this section, we will define **Nextflow processes** (modules) to run Freyja commands within the pipeline.  
A **process** in Nextflow represents a computational step that takes input, performs an operation, and produces output.  

We'll define two modules:  

1. **Variant Extraction module** (`FREYJA_VARIANT`) – Extracts sequencing depth and variant data from a BAM file.  
2. **Lineage Analysis Module** (`FREYJA_DEMIX`) – Estimates the relative abundance of viral lineages from the extracted data.  

---

## **Step 1: Understanding Nextflow Processes**
A Nextflow **process** has three main components:  

- **Input**: Defines the data needed for execution.  
- **Output**: Specifies the files generated.  
- **Script**: Contains the command(s) to be executed.  

Each process runs in isolation, meaning they can execute in parallel if resources allow.  

---

## **Step 2: Writing the Variant Extraction Process**
Let's create the first process, which runs `freyja variants`.  

### **1. Create the File**
Run this command to create the script inside the **modules/** directory:

```bash
touch modules/freyja_variants.nf
```