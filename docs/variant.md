# **Writing freyja_variants.nf Module**

## **Step 1: Writing the `freyja_variants.nf` Module**  

The **`freyja_variants.nf` module** contains the `FREYJA_VARIANTS` process. This process will:  

- Take a **.BAM** file and **FASTA** fileS as input.  
- Run `freyja variants` to extract **variant** and **depth** information.  
- Produce `.depths` and `.variants` files as output.  
 
Use your preferred text editor or run:  

```bash
nano modules/freyja_variants.nf
```

Here is the full code for the FREYJA_VARIANTS process:

```nextflow
process FREYJA_VARIANTS {
    
    input:
        path fasta_file
        each path(bam_file)
        
    output:
        path "${bam_basename}.variant", emit: variant
        path "${bam_basename}.depths", emit: depths

    script:
    bam_basename = bam_file.simpleName

        """
        freyja variants $bam_file \
            --ref $fasta_file \
            --variants ${bam_basename}.variant \
            --depths ${bam_basename}.depths
        """
}
```

## **Breaking it Down step by step**
### **Process Definition**
Every Nextflow process starts with the `process` keyword, followed by a name (written in uppercase).

```nextflow
process FREYJA_VARIANTS { }
```

- Naming convention: Tool name in uppercase (e.g. `FREYJA_VARIANTS`).
- The curly braces `{}` enclose the process logic.

### **Defining Inputs**
The input section specifies what files the process needs.

```nextflow
    input:
        path bam_file
        path fasta_file
```

- path each `bam_file` → The BAM file (aligned sequencing reads). The each keyword ensures that the process runs separately for each BAM file in the input channel.
- path `fasta_file` → The reference genome.
- These files will be received from a channel.

### **Defining Outputs**
The output section declares the files the process will generate.

```nextflow
    output:
        path "${variant_file}.variant"
        path "${depth_file}.depths"
```

- `${variant_file}.variant` → Stores variant information.
- `${depth_file}.depths` → Stores sequencing depth.
- `${}` syntax allows dynamic filenames based on variable names.

### **Writing the Command (Script Section)**
This is where the actual Freyja command is executed.

```nextflow
    script:
        """
        freyja variants $bam_file \
            --ref $fasta_file \
            --variants ${bam_basename}.variant \
            --depths ${bam_basename}.depths
        """
```

- `$bam_file` and `$fasta_file` → Access input variables.
- `${variant_file}.variant` and `${depth_file}.depths` → Define output filenames.
- Triple quotes (""") allow multi-line commands for better readability.

!!! note
    To access variables in a process, use `$variable_name`.<br>
    To add suffixes or prefixes, enclose the variable in `{}` → `${depth_file}.depths`.<br>

Now save the changes you have made to the `freyja_variants.nf` module.

---