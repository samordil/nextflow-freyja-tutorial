# **Exercise: Extending the Pipeline with Freyja Aggregate & Plot**  

Now that you've successfully run **Freyja Variants** and **Freyja Demix**, it's time to extend the pipeline further!  

In this exercise, you will:  

1. Create two **Nextflow modules** for: 

      - [`freyja aggregate`](https://andersen-lab.github.io/Freyja/src/usage/aggregate.html#freyja-aggregate) (to merge results).  
      - [`freyja plot`](https://andersen-lab.github.io/Freyja/src/usage/plot.html#freyja-plot) (to visualize the data).  

2. Integrate them into your **existing pipeline**.  
3. Run the full pipeline from start to finish.  

---

## **Step 1: Setting Up the Modules**  

Navigate to your **modules directory** where you previously created Nextflow modules.  
Create **two new Nextflow modules**:  

   - One for **aggregating the results** using `freyja aggregate`.  
   - Another for **generating a plot** using `freyja plot`.  

!!! hint
    Each module should follow the same structure as `FREYJA_VARIANTS` and `FREYJA_DEMIX`, with proper **input, output, and script sections**.
 
---

## **Step 2: Writing the Freyja Aggregate Module**  

Your first task is to write a **Nextflow module** that:

- Takes the output from **Freyja Demix** as input.  
- Runs the `freyja aggregate` command to **merge** the results.  
- Produces a **single output file** containing aggregated lineage data.  

!!! tip
    **Think About:**  
      
    - What **input** will this module need?  
    - What **output** should it generate?  
    - How will you ensure it runs correctly within Nextflow?  


---

## **Step 3: Writing the Freyja Plot Module**  

Next, create a **module** that:

- Takes the **aggregated file** as input.  
- Runs `freyja plot` to create a **visualization**.  
- Saves the output as a **PNG image**.  

!!! tip
      **Consider:** 
      
      - How will you pass the **correct file** to this module?  
      - What should be the **expected output file**?  
      - Do you need any **additional parameters** for the plot?  

---

## **Step 4: Integrating with the Existing Pipeline**  

Now, **modify your workflow** in `main.nf` to include the new processes.  

**Steps to Follow:**

- Make sure `FREYJA_VARIANTS` and `FREYJA_DEMIX` **run first** as before.  
- After `FREYJA_DEMIX`, add your `FREYJA_AGGREGATE` module.  
- Finally, use `FREYJA_PLOT` to process the aggregated data.  

!!! tip
      - Use `.out` to connect processes correctly.  
      - Ensure each process **emits** meaningful outputs.  
      - Test each step separately before running the full pipeline.  

---

## **Step 5: Running and Validating Your Pipeline**  

Run the updated pipeline using:  

```bash
nextflow run main.nf
```

---
