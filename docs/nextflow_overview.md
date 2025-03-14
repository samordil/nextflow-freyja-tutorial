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
    echo "Hello, Nextflow!"
    """
}

workflow {
    sayHello()
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
echo "Hello, Nextflow!"
```  

- **Output section (`output: stdout`)**  
Captures the **output of the process**, in this case, the text "Hello, Nextflow!".  
<br>
- **Defining a workflow (`workflow { sayHello() }`)**  
    The **workflow** section calls the `sayHello` process. In larger pipelines, this is where you define how different processes connect.  
---

## **Running your first nextflow script**

Save this script as **`hello.nf`** and run it with:

```bash
nextflow run hello.nf
```

### **Expected Output**
If everything is set up correctly, you should see something like this:

```bash
N E X T F L O W  ~  version X.X.X
Launching `hello.nf` [random_id] - revision X.X.X
Hello, Nextflow!
```

This confirms that **Nextflow is installed and working correctly!**

---