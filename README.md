Shotgun metagenomics Galaxy Australia Workflows DRAFT
===========

  - [Analysis overview](#analysis-overview)
  - [Example output](#example-output)
  - [User guide](#user-guide)
      + [Running a single sample workflow](#running-a-single-sample-workflow)
      + [Running a multi sample experiment](#running-a-multi-sample-experiment)
      + [Next steps](#next-steps)
  - [Background and Tutorials](#background-and-tutorials)
  - [Licence(s)](#licences)
  - [Acknowledgements/citations/credits](#acknowledgementscitationscredits)

---

---

# User guide
## Running a multi sample experiment


1. Upload the raw datasets (fastq files) in a Galaxy history

2. Create a dataset collection containing the fastq files. 

The goal of a collection is to process all the samples at once.  

![](./creating_list.pdf)
Figure 1. Creating a list (collection). \
A. Click the checkbox icon. This will reveal checkboxes to the left of all datasets in the history.  
B. In this case we want to select all datasets, so press "All" button (alternatively datasets can be filtered as shown here). This will put a check mark into all checkboxes.  
C. Click "For all selected..." button. This will reveal a dropdown.  
D. Since this is not paired-end (or mate-pair) data we will choose to "Build Dataset List". This will open a dataset collection creator interface.  
E. Within the dataset collection creator interface use the "Name" box to name the collection. "Hide original elements" checkbox ensures that upon creating the collection the original datasets will be hidden from the history as shown in the next figure. Click "Create list".  
F. A collection named "patients" is now added to the history and original datasets are hidden, so that the history only has one item.  
G. Clicking on collection reveals its content.


---

# Acknowledgements/citations/credits

The workflow implemented here is heavily influenced by the [Analyses of metagenomics data - The global picture tutorial](https://training.galaxyproject.org/training-material/topics/metagenomics/tutorials/general-tutorial/tutorial.html#shotgun-metagenomics-data), section Shotgun metagenomics data.

