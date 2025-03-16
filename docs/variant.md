# **Writing `freyja_variants.nf` Module**

## **Step 1: Writing the `freyja_variants.nf` Module**  

In this step, we will define the `freyja_variants.nf` module, which contains the `FREYJA_VARIANTS` process. This module:

- Takes a **.BAM** file and a **FASTA** file as input.
- Runs the `freyja variants` command to extract **variant** and **depth** information.
- Produces `.variants` and `.depths` files as output.

Use your preferred text editor to edit `freyja_variants.nf` file or run:  

```bash
nano modules/freyja_variants.nf
```

---

Here is the full code for the FREYJA_VARIANTS process:

```nextflow
process FREYJA_VARIANTS {
    
    input:
        path fasta_file
        each path(bam_file)
        
    output:
        path "${bam_basename}.variants", emit: variants
        path "${bam_basename}.depths", emit: depths

    script:
    bam_basename = bam_file.baseName

    """
    freyja variants $bam_file \
        --ref $fasta_file \
        --variants ${bam_basename}.variants \
        --depths ${bam_basename}.depths
    """
}
```

---

## **Breaking it Down step by step**
### **Process Definition**
Every Nextflow process starts with the `process` keyword, followed by a name (written in uppercase).

```nextflow
process FREYJA_VARIANTS { }
```

- Naming convention: The process is named after the tool it runs (FREYJA_VARIANTS).
- The curly braces `{}` enclose the process logic.

---

### **Defining Inputs**
The input section specifies what files the process needs.

```nextflow
    input:
        path fasta_file
        each path(bam_file)
```

- These files will be received from a channel.
- `path fasta_file` → The reference genome file (shared across samples).
- `each path(bam_file)` → Represents a BAM file containing aligned sequencing reads.
- The [`each`](https://www.nextflow.io/docs/latest/process.html#input-repeaters-each) keyword ensures that the process runs individually for each BAM file using the same reference file.

---

### **Defining Outputs**
The output section declares the files the process will generate.

```nextflow
    output:
        path "${bam_basename}.variants", emit: variants
        path "${bam_basename}.depths", emit: depths
```

- `${bam_basename}.variants` → Contains detected genetic variants.
- `${bam_basename}.depths` → Stores sequencing depth information.
- [`emit`](https://www.nextflow.io/docs/latest/process.html#naming-outputs) labels (`variants` and `depths`) allow other processes to reference these outputs.

---

### **Writing the Command (Script Section)**
This is where the actual Freyja command is executed.

```nextflow
    script:
    bam_basename = bam_file.baseName

    """
    freyja variants $bam_file \
        --ref $fasta_file \
        --variants ${bam_basename}.variants \
        --depths ${bam_basename}.depths
    """
```

- `bam_basename` = `bam_file.simpleName` → Extracts the filename (without extension) to create meaningful output names.
- `$bam_file` and `$fasta_file` → Access input variables.
- `${variant_file}.variants` and `${depth_file}.depths` → Define output filenames.
- Triple quotes (""") allow multi-line commands for better readability.

---

!!! note
    To access variables in a nextflow process, use `$variable_name`.<br>
    To add suffixes or prefixes, enclose the variable in `{}` → `${depth_file}.depths`.<br>

Now, save your changes to the freyja_variants.nf module!

---