# **Writing Nextflow Modules for Freyja**

## **Overview**
Now that we’ve created **Nextflow processes**, let's organize them using **modules**.  

### **What is a Module?**
A **module** in Nextflow is simply a **separate file** that contains a **process**.  
Using modules helps to:

- **Keep the pipeline organized** – Each process has its own file.  
- **Improve reusability** – We can use the same process in different workflows.  
- **Make debugging easier** – If something goes wrong, it's easier to find the issue.  

Instead of putting everything in one big `main.nf` file, we separate each process into its own module.  

---

## **Creating Nextflow Modules**
We will create **two modules**, each containing one Nextflow process:

| **Module**                | **Process Name**       | **Function** |
|---------------------------|-----------------------|--------------|
| `freyja_variants.nf`      | `FREYJA_VARIANTS`     | Extracts sequencing depth and variant data from a `.BAM` file.  |
| `freyja_demix.nf`         | `FREYJA_DEMIX`        | Analyzes variants to estimate the relative abundance of viral lineages. |

---

## **Why Use Separate Module Files?**
Imagine writing everything inside `main.nf`, it would become messy and hard to manage.  

By separating each process into its own file, we get:

- **Better readability** – Each module handles one specific task.  
- **Easier maintenance** – If we need to update one process, we modify only that module.  
- **Reusability** – The same module can be used in different pipelines.

---
!!! note  
    **Naming conventions for Nextflow modules** 

    While not mandatory, it's common practice to:  
    - Name **modules** after the tool they run (e.g., `freyja_variants.nf` for `freyja variants`).  
    - Use **UPPERCASE** for process names to make them easily recognizable.  

    Example:  
    - `freyja_variants.nf` → `FREYJA_VARIANTS`  
    - `freyja_demix.nf` → `FREYJA_DEMIX`  

    This improves readability and makes it clear what each module does.  

Now that we understand why we use modules, let’s start writing them!  

---
