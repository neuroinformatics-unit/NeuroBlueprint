# SWC BIDS

This repository contains our suggestions on how to organise your data and related files. It is inspired by BIDS, but it is not a formal extension of BIDS.

BIDS is a standard for organizing and describing neuroimaging and behavioural data. 
It is developed and maintained by the [BIDS community](https://bids.neuroimaging.io/). It defines a way to structure your data and metadata within a hierarchy of folders and filenames. It also defines a set of metadata fields that are common to many neuroimaging experiments. We want to expand this standard to include electrophysiology and behavioural experiments and adapt it to the needs of SWC.
 
## SWC BIDS - The SWC Folder Organisation Specification based on BIDS

A standardised folder structure used by researchers across neuroscience projects makes data organisation, analysis and collaboration easier. 
This page will outline the folder structure and file naming standardards recommended at the SWC, based on the BIDS format. The BIDS format
is a project structure specification widely used in human research with ongoing initatives to extend this to animal research.

The BIDS specification is very developed and in it's entirely rather detailed and long. Here in the first instance we aim to provide
a brief subset of this specification aimed at introducing a standardised project folder structure across the SWC with minimal overhead
for researchers. Future tools created by the neuroinformatics-unit for convenient, standardized data analysis pipelines will be build 
to interopate seamlessly with this folder structure.

The Specification

Following the BIDS specification, we //tag specifications as //check REQUIRED, RECOMMENDED and OPTIONAL. At it's heard, the BIDS
specification is a simple file structure to use when organisaing your raw experimental data. Below is an example project with
arbitary data XXX:

└── project_name/
    └── raw_data/
        ├── sub-001/
        │   └── ses-001/
        │       ├── ephys/
        │       └── behav/
        │   └── histology/
        └── sub-002/
            └── ses-001/
                ├── behav/
                └── imaging/
            └── ses-002/
                └── behav/
            └── histology/

here 'sub' refers to subject (any experimental subject or participant, typically, in the SWC case a mouse or rat)
