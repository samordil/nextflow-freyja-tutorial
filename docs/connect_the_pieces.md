# **Connecting the Pieces: Channels, Modules, and Workflow**

## **Overview**
Now that we’ve created the Nextflow processes (modules) for Freyja, it’s time to bring everything together!  
In this step, we will:  

- Define **channels** to provide input data to our processes.  
- Import the two **modules** (`freyja_variants.nf` and `freyja_demix.nf`).  
- Create a **workflow** that runs the processes in the correct order.  

## **Step 1: Creating input channels**

We need to define two **input channels**:  
1. **`bamFile_ch`** – This channel collects all **`.BAM`** files from the `data/bam_files/` folder.  
2. **`refSeq_ch`** – This channel collects the **`.FASTA`** reference genome from the `data/` folder.  

Open the `main.nf` file and add the following:

```nextflow
#!/usr/bin/env nextflow

nextflow.enable.dsl=2

// Define channels to provide input data
bamFile_ch = Channel.fromPath("data/bam_files/*.bam") // Collects all .BAM files
refSeq_ch = Channel.fromPath("data/*.fasta")          // Collects the reference genome
```

- Here, we are using channel factory [`Channel.fromPath()`](https://www.nextflow.io/docs/latest/channel.html#channel-factories)` to create channnel and assign it to a variable:
- `Channel.fromPath("data/bam_files/*.bam")` → Looks for all `.BAM` files in `data/bam_files/`.
- `Channel.fromPath("data/*.fasta")` → Looks for the reference genome `.FASTA` file inside `data/`.

---

## **Step 2: Importing the Modules into `main.nf`**
Now that we have our input channels, we need to import the Freyja modules so we can use them inside `main.nf`.

Why do we need to import modules?

Modules are stored in separate `.nf` files, so we must tell Nextflow where to find them.
The [`include`](https://www.nextflow.io/docs/latest/reference/syntax.html#include) command makes the processes available in `main.nf`.

Add these imports to `main.nf`

```nextflow
// Import the two modules into main.nf
include { FREYJA_VARIANTS } from './modules/freyja_variants.nf'
include { FREYJA_DEMIX } from './modules/freyja_demix.nf
```

- `include { FREYJA_VARIANTS } from './modules/freyja_variants.nf'` → This imports the `FREYJA_VARIANTS` process from `freyja_variants.nf`.
- `include { FREYJA_DEMIX } from './modules/freyja_demix.nf'` → This imports the `FREYJA_DEMIX` process from `freyja_demix.nf`.

Now, Nextflow knows where to find our process definitions.

---

## **Step 3: Creating the Workflow**

Let’s now define the workflow, which serves as the entry point of our pipeline. It controls the execution order of processes and passes input between them.

Add this to `main.nf` file:

```nextflow
// Define the workflow (entry point of our pipeline)
workflow {
    // Run the first process (FREYJA_VARIANTS) and pass it the input channels
    FREYJA_VARIANTS(refSeq_ch, bamFile_ch)

    // Run the second process (FREYJA_DEMIX) and pass it the output from the first process
    FREYJA_DEMIX(FREYJA_VARIANTS.out.variants, FREYJA_VARIANTS.out.depths)
}
```

The first process, `FREYJA_VARIANTS`, runs first:

- It takes a `.FASTA` reference genome file from the `refSeq_ch` channel and `.BAM` files from the `bamFile_ch` channel as input.
- It emits variant and depth channels, which contain the output files from the `FREYJA_VARIANTS` process.

The second process, `FREYJA_DEMIX`, runs next:

- It takes the variant and depth channels from the first process as input.
- It produces a channel containing a `.tsv` file with estimated lineage abundances as output.

---

Here is how your final main.nf file should look:

```nextflow
#!/usr/bin/env nextflow

nextflow.enable.dsl=2

// Define channels to provide input data
bamFile_ch = Channel.fromPath("data/bam_files/*.bam") // Collects all .BAM files
refSeq_ch = Channel.fromPath("data/*.fasta")          // Collects the reference genome

// Import the two modules into main.nf
include { FREYJA_VARIANTS } from './modules/freyja_variants.nf'
include { FREYJA_DEMIX } from './modules/freyja_demix.nf'

// Define the workflow (entry point of our pipeline)
workflow {
    // Run the first process (FREYJA_VARIANTS) and pass it the input channels
    FREYJA_VARIANTS(refSeq_ch, bamFile_ch)

    // Run the second process (FREYJA_DEMIX) and pass it the output from the first process
    FREYJA_DEMIX(FREYJA_VARIANTS.out.variants, FREYJA_VARIANTS.out.depth)
}
```

Next, we will run the pipeline and test if everything works correctly!

---