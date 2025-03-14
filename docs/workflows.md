# **Understanding Workflows in Nextflow**  

## **What is a Workflow?** 

A [**workflow**](https://www.nextflow.io/docs/latest/workflow.html#workflows) in Nextflow is like a blueprint that defines how **processes, channels, and operators** interact. It controls the flow of data and execution in your pipeline.

Workflows help:

- **Structure pipelines** – Define the execution order of processes.  
- **Reuse code** – Use named workflows multiple times.  
- **Improve readability** – Keep complex pipelines manageable.  

---

## **Types of Workflows**  
There are two types of workflows:  

- **Entry Workflow** – The main workflow that runs when you execute the script.  
- **Named Workflows** – Workflows that can be reused and called from other workflows.

---

## **Entry Workflow (Main Workflow)** 
Every Nextflow script has **one** entry workflow that acts as the starting point of execution.  

**Example:** A simple workflow that adds "world!" to different greetings.  

```nextflow
workflow {
    Channel.of('Bonjour', 'Ciao', 'Hello', 'Hola')
        | map { v -> "$v world!" }
        | view
}
```
 How it works:

- A channel is created with greetings.
- The map operator modifies each greeting by adding "world!".
- The view operator prints the output.

output:
```
Bonjour world!
Ciao world!
Hello world!
Hola world!
```
---

Named Workflows (Reusable Workflows)
A named workflow is a reusable workflow that can be called inside other workflows, making pipelines modular and structured.

Example: Connecting two workflows:

```nextflow
workflow my_workflow {
    foo()
    bar( foo.out.collect() )
}

workflow {
    my_workflow()
}
```

Explanation:

- `my_workflow` is a named workflow that contains two processes:  
        1. `foo()` runs first.  
        2. `bar()` takes the output of `foo()` and processes it.  

- The main workflow (`workflow { my_workflow() }`) calls `my_workflow()`, executing everything in order.  

---

