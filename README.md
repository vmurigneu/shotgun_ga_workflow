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

<p align="center"><img src="/images/overview_shotgun.png" alt="Logo" width="45%"></p>

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
 
https://usegalaxy.org.au/u/valentine_murigneux/h/shotgun-workflow-on-forward-reads-for-15-samples 
Shotgun metagenomics workflow for collection: [link](https://usegalaxy.org.au/u/valentine_murigneux/w/shotgun-metagenomics-ga-workflow-for-collection)   

When run in full, the workflow produces the following outputs:

* Output Dataset: Krona pie plot (MetaPhIAn2 taxonomy abundance)
* Output Dataset: Merged MetaPhIAn2 taxonomy abundance table with sample ID
* Output Dataset: Merged table for HUMAnN2 gene families abundance
* Output Dataset: Merged and normalised table for HUMAnN2 gene families abundance
* Output Dataset: Merged, regrouped and normalised table for HUMAnN2 gene families abundance
* Output Dataset: Merged table for HUMAnN2 Pathways and their abundance
* Output Dataset: Merged table for HUMAnN2 Pathways and their coverage
* Output Dataset Collection: MetaPhIAn2 SAM file (one file per sample)
* Output Dataset Collection: MetaPhIAn2 biom file (one file per sample)

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

<p align="center"><img src="/images/create_collection.png" width="95%"></p>

A. Click the checkbox icon. This will reveal checkboxes to the left of all datasets in the history.  
B. In this case we want to select all datasets, so press "Select All" button (alternatively datasets can be filtered as shown here). This will put a check mark into all checkboxes.  
C. Click "For all selected..." button. This will reveal a dropdown.  
D. Since this is not paired-end (or mate-pair) data we will choose to "Build Dataset List". This will open a dataset collection creator interface.  
E. Within the dataset collection creator interface, use the "Name" box to name the collection. "Hide original elements" checkbox ensures that upon creating the collection the original datasets will be hidden from the history as shown in the next figure. Click "Create collection".  
F. A collection named "10 samples" is now added to the history and original datasets are hidden, so that the history only has one item.  
G. Clicking on collection reveals its content.

### 3. Run the shotgun workflow

  Search for the shotgun metagenomics workflow under 'workflow' and run it. 
<p align="center"><img src="/images/run_workflow.png"></p>

<p align="center"><img src="/images/run_workflow_collection.png" width="100%"></p>

---

# Background and Tutorials 



---

# License(s)

---

# Acknowledgements/citations/credits

The workflow implemented here is heavily influenced by the [Analyses of metagenomics data - The global picture tutorial](https://training.galaxyproject.org/training-material/topics/metagenomics/tutorials/general-tutorial/tutorial.html#shotgun-metagenomics-data), section Shotgun metagenomics data.

