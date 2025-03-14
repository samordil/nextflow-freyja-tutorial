# **Understanding Operators in Nextflow** 

## **What Are Operators?**  
[**Operators**](https://www.nextflow.io/docs/latest/reference/operator.html#operators) in Nextflow allow you to **manipulate** and **transform** data as it flows through channels.
They help modify, filter, and combine data before passing it to a process.  

---

## **Commonly Used Operators**  

| Operator | Description | Example |
|----------|-------------|---------|
| `map` | Transforms each element in a channel | Convert file names to uppercase |
| `filter` | Selects elements that match a condition | Keep only `.txt` files |
| `collect` | Gathers all elements into a single list | Collect all sample names |
| `flatten` | Flattens nested lists into a single list | Convert list of lists into one |
| `groupTuple` | Groups data into pairs | Pair samples with metadata |

---

## **Example 1**: Using `map` to transform data 
The **`map`** operator applies a function to every element in a channel.  

```nextflow
Channel.from("sample1.txt", "sample2.txt", "sample3.txt")
    | map { it.toUpperCase() }
    | view()
```
Output:
```
SAMPLE1.TXT  
SAMPLE2.TXT  
SAMPLE3.TXT  
```
---

## **Example 2**: Using `filter` to select data
The `filter` operator removes unwanted elements based on a condition.
```nextflow
Channel.from("data1.txt", "image.png", "data2.txt")
    | filter { it.endsWith('.txt') }
    | view()
```
Output:
```
data1.txt  
data2.txt  

```
---

## **Example 3**: Using `groupTuple` to Organize Data
The `groupTuple` operator groups elements into structured tuples.
```nextflow
Channel.from(["A", "B", "C"], [1, 2, 3])
    | groupTuple()
    | view()
```
Output:
```
[A, 1]  
[B, 2]  
[C, 3]  
```
---

!!! note
    In Nextflow, you can connect channels and operators using the [pipe (`|`)](https://www.nextflow.io/docs/latest/workflow.html#pipe) symbol.  
    The [`view`](https://www.nextflow.io/docs/latest/reference/operator.html#view) operator is one example of an operator that processes and displays data in a pipeline.
    
---
