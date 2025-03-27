# **Running and Testing the Nextflow Pipeline**

## **Overview**
Now that we've set up our **Nextflow pipeline**, it's time to **run it** and see if everything works!  
In this section, we will:  

- Run the pipeline step by step.  
- Check that our processes execute correctly.  
- Troubleshoot any potential errors.  

---

## **Step 1: Running the Pipeline**
From your terminal run:  

```nextflow
nextflow run main.nf
```

Nextflow will execute the pipeline and display progress messages:

```
 N E X T F L O W   ~  version 24.10.5

Launching `main.nf` [nasty_gautier] DSL2 - revision: 43eb342fc2

executor >  local (6)
[c0/b014cd] FREYJA_VARIANTS (3) [100%] 3 of 3 ✔
[7e/b05de0] FREYJA_DEMIX (2)    [100%] 3 of 3 ✔

```
If you see ✔ for all processes, congratulations—your pipeline ran successfully!

Let's break down what each part means:

- `N E X T F L O W ~ version 24.10.5` → Confirms the Nextflow version you're using.

---

- `Launching main.nf [nasty_gautier] DSL2 - revision: 43eb342fc2` → Shows that Nextflow is running main.nf using DSL2.

---

- `executor > local (6)` → Tells you that Nextflow is running processes on your local machine. The number (6) indicates the total number of tasks executed.

---

- `[c0/b014cd] FREYJA_VARIANTS (3) [100%] 3 of 3 ✔` → Process Execution Progress. The FREYJA_VARIANTS process completed all 3 tasks successfully.  
    - `[c0/b014cd]` → Unique task ID, useful for locating outputs in the `work/` directory.  
    - `FREYJA_VARIANTS` → The process name being executed.  
    - `(3)` → The last task label that was run. Since there are 3 samples, Nextflow runs 3 parallel tasks.  

---

- `[7e/b05de0] FREYJA_DEMIX (2) [100%] 3 of 3 ✔` → Similar to FREYJA_VARIANTS, this line confirms that the FREYJA_DEMIX process also completed all tasks successfully.

---

## **Step 2: Checking Output Files**
After the pipeline finishes running, you can check the generated output files. These files will be stored in the work/ directory and the specified output paths.

### **Viewing Process Output**
To check the output of a specific process, first, copy its unique task ID and use the ls command. For example:

```bash
ls work/c0/b014cd
```

Press the Tab key to auto-complete the path, then press Enter. You should see output similar to this for one of the FREYJA_DEMIX tasks:

```cpp
variant.tsv  data
```

If you want to view the contents of a file, use the less command instead of ls:

```bash
less work/c0/b014cd/variant.tsv
```

This will display the contents of the file, for example:

```
	sample.variants.tsv
summarized	[('Other', 0.9999999999188374)]
lineages	B.1.160.22
abundances	1.00000000
resid	4.696910204950047
coverage	10.597598903120089
```

Now, let’s move on to organizing the output files from different processes and using custom parameters to refine our pipeline.

---