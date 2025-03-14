# **Writing Nextflow Modules for Freyja**

## **Overview**
Now that we have created **Nextflow processes**, it's time to organize them using **modules**.  

## **What is a Module?**
A **module** in Nextflow is simply a **separate file** that contains a **process**.  
This makes the pipeline **organized** and allows us to **reuse** processes easily.  

For example:  
Instead of writing a long `main.nf` script, we put each **process in its own module**.  
This helps keep the pipeline **clean** and **modular**.  

---

## **Creating Nextflow Modules**
We will create **two modules**, each containing one Nextflow process:

1. **`freyja_variants.nf` Module** – Contains the `FREYJA_VARIANTS` process, which extracts sequencing depth and variant data from a `.BAM` file.  
2. **`freyja_demix.nf` Module** – Contains the `FREYJA_DEMIX` process, which estimates the relative abundance of viral lineages from the extracted data.  

!!! tip
    **Naming Nextflow Processes**  

    It's **common practice** (but not mandatory) to name Nextflow processes in **capital letters** and include the tool's name.  

    This improves **readability** and makes it **easier to understand** what each process does.  

    Example:  
    ```nextflow
    process FREYJA_VARIANTS { ... }  // Runs freyja variants  
    process FREYJA_DEMIX { ... }     // Runs freyja demix  
    ``` 
---