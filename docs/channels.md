# **Understanding Channels in Nextflow**  

## **What Are Channels?**  
In nextflow, [**channels**](https://www.nextflow.io/docs/latest/channel.html) are the main way data moves between processes.  
They act as **data streams**, passing files, variables, or other values between processes.  

Think of channels as **conveyor belts** that move data from one process to another. 

---

## **Types of Channels** 
Channels in Nextflow are one-directional and can be either:

- **Value Channel** – Hold a single value (e.g., a number or string).
- **Queue Channel** – Hold multiple values and behave like a stream.

---

## **Creating Channels**  
Channels can be created using built-in [**factory methods**](https://www.nextflow.io/docs/latest/channel.html#channel-factories) like ``Channel.of()``, `Channel.from()`, `Channel.fromPath()` and `Channel.value()`.  

---

### **Example 1**: Creating a simple channel
```nextflow
sample_ch = Channel.of("sample1.fastq", "sample2.fastq", "sample3.fastq")
```
What this does:

- Creates a channel containing paths to three FastQ file and assigns them to `sample_ch` varible.
- The `sample_ch` can now be passed as input to a process

---

### **Example 2**: Creating a channel from files
```nextflow
fastq_file_ch = Channel.fromPath("data/*.fastq")
```
This will create a channel that holds all FASTQ files in the data/ directory.

---

### How Channels Work in a Pipeline:
- Channels **send** data to a process as input.
- A process **modifies** the data and sends it to an **output channel**.
- The **output channel** can then be used by another process.
