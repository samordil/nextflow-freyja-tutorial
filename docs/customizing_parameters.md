
#**Customizing Parameters in Nextflow**

## **Overview**
So far, we've hardcoded file paths and settings in our pipeline. This works but isn’t very flexible.  
Now, we’ll make our pipeline more **configurable** by using **parameters**.  

- Define parameters in `nextflow.config`.  
- Use them in `main.nf`.  
- Run the pipeline with custom values.  

---

## **Step 1: Adding Parameters to `nextflow.config`**
Open (or create) the `nextflow.config` file and define parameters:  

```groovy
params {
    bam_dir = 'data/bam_files/'   // Folder with BAM files
    ref_genome = 'data/ref_genome.fasta'  // Reference genome file
    outdir = ${projectDir}/Results
}
```

Why use parameters?

Makes it easy to change input files without editing the script.

Allows users to override values when running the pipeline.

---

## **Step 2: Using Parameters in `main.nf`**
Now, update `main.nf` to use these parameters instead of hardcoded paths.

```nextflow

#!/usr/bin/env nextflow

nextflow.enable.dsl=2

// Define channels using parameters
bamFile_ch = Channel.fromPath("${params.bam_dir}/*.bam")
refSeq_ch = Channel.fromPath(params.ref_genome)

// Import modules
include { FREYJA_VARIANTS } from './modules/freyja_variants.nf'
include { FREYJA_DEMIX } from './modules/freyja_demix.nf'

// Workflow
workflow {
    FREYJA_VARIANTS(refSeq_ch, bamFile_ch)
    FREYJA_DEMIX(FREYJA_VARIANTS.out.variants, FREYJA_VARIANTS.out.depth)
}
```

What changed?

- Instead of hardcoded paths (data/bam_files/*.bam), we use params.bam_dir.
- Instead of data/ref_genome.fasta, we use params.ref_genome.

Now, we can easily update file paths by changing nextflow.config.


---

## **Step 3: Overriding Parameters at Runtime**
Instead of editing nextflow.config, we can pass parameters when running the pipeline.

For example:

```bash
nextflow run main.nf --bam_dir my_data/bams --ref_genome my_data/genome.fasta --outdir my_results
```
What happens here?

- `--bam_dir` overrides the default `params.bam_dir`.

- `--ref_genome` replaces `params.ref_genome`.

This makes the pipeline more dynamic and reusable across different datasets.

---

## **Step 4: Checking Parameter Values**
If you’re unsure what values are being used, add this to main.nf:

```bash
log.info "Using BAM directory: ${params.bam_dir}"
log.info "Using reference genome: ${params.ref_genome}"
```

Now, when you run the pipeline, it prints:

```bash
N E X T F L O W  ~  version 22.10.1
Using BAM directory: my_data/bams
Using reference genome: my_data/genome.fasta
```

---