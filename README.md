Shotgun metagenomics Galaxy Australia Workflows DRAFT
===========

  - [Analysis overview](#analysis-overview)
  - [Example output](#example-output)
  - [User guide](#user-guide)
      + [Running a multi sample experiment](#running-a-multi-sample-experiment)
  - [Background and Tutorials](#background-and-tutorials)
  - [Licence(s)](#licences)
  - [Acknowledgements/citations/credits](#acknowledgementscitationscredits)

---
This document describes how to use the shotgun metagenomics workflow on Galaxy Australia.

# Analysis overview

The diagram below represents an overview of the shotgun metagenomics pipeline, with the tools used (blue), the databases (orange), and the input and output data (yellow).  

<p align="center"><img src="/images/shotgun_workflow_scheme.png" alt="Logo" width="65%"></p>

The different steps of the pipeline are representing in more details in the Galaxy workflow diagram below. The arrows in orange point to the main results files.

<p align="center"><img src="/images/shotgun_galaxy_workflow_image.png" alt="Logo2" width="95%"></p>


## 1. Extraction of taxonomic information ([MetaPhlAn2](https://huttenhower.sph.harvard.edu/metaphlan2/))

Assignation of taxonomy on the whole sequences using databases with marker genes. MetaPhlAn2 is using a database of ~1M unique clade-specific marker genes (not only the rRNA genes) identified from ~17,000 reference (bacterial, archeal, viral and eukaryotic) genomes.

MetaPhlAn2 generates 3 files:

* A tabular file with the community structure. Each line contains a taxa and its relative abundance found for our sample. The results are visualised with Krona plots.

* A BIOM file with the same information as the previous file but in BIOM format

* A SAM file with the results of the mapping of the sequences on the reference database

## 2. Extraction of functional information ([HUMAnN2](https://huttenhower.sph.harvard.edu/humann2/))

In the shotgun data, we have access to the gene sequences from the full genome. We use that to identify the genes, associate them with a function, build pathways, etc., to investigate the functional part of the community.

HUMAnN2 generates 3 files:

* A file with the abundance of gene families. Gene family abundance is reported in RPK (reads per kilobase) units to normalize for gene length. It reflects the relative gene (or transcript) copy number in the community. The RPKs of reads that map to gene families that lack UniRef90 IDs are captured as UniRef90_unknown, and unmapped read abundances as UNMAPPED. The “UNMAPPED” value is the total number of reads which remain unmapped after both alignment steps (nucleotide and translated search). Since other gene features in the table are quantified in RPK units, “UNMAPPED” can be interpreted as a single unknown gene of length 1 kilobase recruiting all reads that failed to map to known sequences.

* A file with the coverage of pathways. Pathway coverage provides an alternative description of the presence (1) and absence (0) of pathways in a community, independent of their quantitative abundance.

* A file with the abundance of pathways

---

# Example output
 
When run in full, the workflow produces the following outputs:

* Output Dataset: Krona pie plot (MetaPhIAn2 taxonomy abundance)
* Output Dataset: Merged MetaPhIAn2 taxonomy abundance table with sample ID
* Output Dataset: HUMAnN2 merged gene families abundance
* Output Dataset: HUMAnN2 merged pathways coverage
* Output Dataset: HUMAnN2 merged and normalised pathways abundance
* Output Dataset: HUMAnN2 merged and normalised gene families abundance
* Output Dataset: HUMAnN2 regrouped, merged and normalised gene families abundance  

This is an example of Galaxy history containing the results for 15 samples:  
https://usegalaxy.org.au/u/valentine_murigneux/h/shotgun-workflow-forward-reads-15-samples  
and the workflow report:  
https://usegalaxy.org.au/workflows/invocations/report?id=78f98f14bf4a7a20

---

# User guide
## Running a multi sample experiment

### 1. Upload the raw datasets (fastq files) in a Galaxy history

### 2. Create a dataset collection containing the fastq files 
The goal of a collection is to process all the samples at once.  

The workflow will take one fastq file per sample as input.     
* If the dataset are single-end reads, include all the files in the collection
* If the dataset are paired-end reads, only include the forward reads (R1) for each sample

Figure: Creating a collection

<p align="center"><img src="/images/create_collection.png" width="99%"></p>

A. Click the checkbox icon. This will reveal checkboxes to the left of all datasets in the history.  
B. In this case we want to select all datasets, so press "Select All" button (alternatively datasets can be filtered). This will put a check mark into all checkboxes.  
C. Click "All 10 selected..." button. This will reveal a dropdown.  
D. Since this is not paired-end (or mate-pair) data we will choose to "Build Dataset List". This will open a dataset collection creator interface.  
E. Within the dataset collection creator interface, use the "Name" box to name the collection. "Hide original elements" checkbox ensures that upon creating the collection the original datasets will be hidden from the history as shown in the next figure. Click "Create collection".  
F. A collection named "10 samples" is now added to the history and original datasets are hidden, so that the history only has one item.  
G. Clicking on collection reveals its content.

### 3. Run the shotgun workflow

A. Click on "Workflow" in the Galaxy horizontal menu  
B. Search for the shotgun metagenomics workflow called "Analyses of shotgun metagenomics data with MetaPhlAn v2". [Link](https://usegalaxy.org.au/u/valentine_murigneux/w/analyses-of-shotgun-metagenomics-data-with-metaphlan-v2) to the shotgun metagenomics workflow for collection  
C. Click on "Run workflow" (white arrow on the right)  
D. Select the "input fastq collection" to be the collection you just created ("10 samples") from the currenty history.  
E. Click on "Run Workflow" 
  
Figure: Run the workflow

<p align="center"><img src="/images/run_workflow_figure.png" width="99%"></p>

### 4. Once the workflow has completed, open the report
A report will be automatically generated for each invocation of the workflow. The report is located under the menu "User" -> "Workflow Invocations".  
A. Click on "User" in the Galaxy horizontal menu   
B. Click on "Workflow Invocations"  
C. Scroll down and click on the name of the workflow: "Analyses of shotgun metagenomics data (for collection) with subworkflow".  
D. Right Click "View Report" -> Open in a new tab   
E. The main output files are located under the "Workflow Outputs" section.  
* Output Dataset: Krona pie plot (MetaPhIAn2 taxonomy abundance)
* Output Dataset: Merged MetaPhIAn2 taxonomy abundance table with sample ID
* Output Dataset: HUMAnN2 merged gene families abundance
* Output Dataset: HUMAnN2 merged pathways coverage
* Output Dataset: HUMAnN2 merged and normalised pathways abundance
* Output Dataset: HUMAnN2 merged and normalised gene families abundance
* Output Dataset: HUMAnN2 regrouped, merged and normalised gene families abundance  

You can download each output dataset by clicking on the icon "Download Dataset" on the top right corner.  
The "Output Dataset Collections" items contain the output file for each sample separately ().  

Figure: Workflow Report

<p align="center"><img src="/images/workflow_report.png" width="99%"></p>

### 5. Diversity stats (runnning on Galaxy Europe while the tools are not yet available within Galaxy Australia)

In the shotgun analysis history, look for the file named “Metaphlan species output, Alpha/Beta diversity input file”
(item 160 in your history). Download the file by clicking on the icon “Download”.  Optional: Rename the file on your computer. 

Go to Galaxy europe: https://usegalaxy.eu/. Create an account and upload your file by clicking the icon “Upload Data” at the top of the left menu. Select “Choose local files”, select the file on your computer, modify the type to “tabular” before clicking Start then Close once the file is 100% uploaded. 
Run the tools:
* Calculate alpha diversity on each sample in an otu table, using a variety of alpha diversity metrics (alpha_diversity)
  * OTU table: the file you just uploaded “Metaphlan species output, Alpha/Beta diversity input file”
  * Select the diversity metrics to use: for instance
    * chao1 richness estimator 
    * Gini index
    * Shannon entropy of counts 
    * Simpson’s index
      
* Krakentools: calculates beta diversity (Bray-Curtis dissimilarity) from Kraken, Krona and Bracken files 
  * Taxonomy file: the file you just uploaded “Metaphlan species output, Alpha/Beta diversity input file”
  * Specify type of input file(s): single tabular data file

---

# Background and Tutorials 



---

# License(s)

---

# Acknowledgements/citations/credits

The workflow implemented here is heavily influenced by the [Analyses of metagenomics data - The global picture tutorial](https://training.galaxyproject.org/training-material/topics/metagenomics/tutorials/general-tutorial/tutorial.html#shotgun-metagenomics-data), section Shotgun metagenomics data.

