# **Introduction to nextflow**

[Nextflow](https://www.nextflow.io/docs/latest/overview.html) is a **workflow management system** designed to build and run computational pipelines. It is widely used in bioinformatics, data science, and HPC (High-Performance Computing).

## **Why use nextflow?**
Nextflow makes workflows:

- **Reproducible** – Ensures pipelines run the same way on different systems.  
- **Scalable** – Works on laptops, HPC clusters, and cloud environments.  
- **Modular** – Pipelines are broken into reusable processes (modules).  
- **Parallelized** – Automatically runs tasks in parallel when possible.  

---

## **Nextflow script basics**

A Nextflow pipeline is written in **nextflow DSL2 (Domain-Specific Language 2)**. Let's look at a simple example:

### **Example: Hello World in Nextflow**
```nextflow
#!/usr/bin/env nextflow     

nextflow.enable.dsl=2

process sayHello {
    output:
    stdout

    script:
    """
    echo "Hello, World!"
    """
}

workflow {
    sayHello().view()
}
```

### **Breaking it down:**

- **`#!/usr/bin/env nextflow`**  
This tells the system to use **Nextflow** to execute the script.  
<br>
- **`nextflow.enable.dsl=2`**  
Enables **Nextflow DSL2**, which is the latest and most flexible version.  
<br>
- **Defining a process (`process sayHello { ... }`)**  
A process is a unit of execution. In this case, it runs a small shell command.  
<br>
- The **script section** contains the actual command:
```bash
echo "Hello, World!"
```  

- **Output section (`output: stdout`)**  
Captures the **output of the process**, in this case, the text "Hello, World!".  
<br>
- **Defining a workflow:** 
```bash
workflow { 
    sayHello().view() 
}
```
The **workflow** section defines how processes run. In larger pipelines, this is where you define how different processes connect. Here, it calls `sayHello()` process and `.view()` displays its output to the terminal.

---

## **Running your first nextflow script**

Save this script as **`hello.nf`** and run it with:

```bash
nextflow run hello.nf
```

### **Expected Output**
If everything is set up correctly, you should see something like this:

```bash
 N E X T F L O W   ~  version 24.10.5

Launching `hello.nf` [drunk_gates] DSL2 - revision: c2fd982266

executor >  local (1)
[d4/99ae5a] sayHello | 1 of 1 ✔
Hello, World!
```

This confirms that the sayHello process ran successfully once (1 of 1 ✔).

---