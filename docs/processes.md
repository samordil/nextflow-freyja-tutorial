# **Understanding Processes in Nextflow** 

## **What Are Processes?**  

A [**process**](https://www.nextflow.io/docs/latest/process.html) in Nextflow is a **unit of execution** that:

- Runs a specific command or script.  
- Takes input from a **channel**.  
- Produces an output, which is **sent to a new channel**.  

Processes are **isolated** from each other, often run in **parallel** and communicate only through **channels**.

---


## **Basic structure of a process**  
A **process** follows this structure:  

```nextflow
process NAME {
    input:
    <input definition> // input variable

    output:
    <output definition> // output variable

    script:
    """
    <commands to execute>
    """
}

```

---

Each process has: 

- A **NAME** - name of the process
- An **Input** – data coming from a **channel**.  
- **Execution Block** – Runs the given script/command.  
- **Output** – Sent data to an **output channel**.  

---

### **Example 1**: A simple process
```nextflow
process countBases {
    input:
    path sample_file

    output:
    path "output_file.count"

    script:
    """
    wc -c $sample_file > output_file.count
    """
}
```
Here:

- The process `countBases` defines a variable called `samples_file`, which holds the path to a file received through a `queue channel`.
- It then executes the `wc -c` command in the `script` section to generate the `output_file.count` that is made available through another channel.

---