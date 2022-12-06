# Project Folder Structure 

Standardized project folders containing raw data are hierarchically structured according to the 
[BIDS standard](https://bids-specification.readthedocs.io/en/stable/02-common-principles.html). For example:

```
└── project/
    ├── rawdata/
    │   └── sub-<label>/
    │       └── ses-<label>/
    │           ├── <datatype_1>/
    │           │   └── raw_data.file
    │           └── <datatype_2>/
    │               └── raw_data.file  
    └── derivatives/
        └── ...
```

The project folder may have any name descriptive of the project (that does not include spaces). Within the 
project folder, data is separated into `rawdata` and `derivatives`. `rawdata` contains the raw
data acquired during data collection. `derivatives` includes any processed data (e.g. ephys preprocessing, 
behavioural movement tracking). The subject / session / datatype folder structure within derivatives should
match the rawdata folder.

Each subject (e.g. mouse, rat) in the project has a dedicated folder in which all data from 
experimental sessions are stored.
In the case of multiple sessions, each session has its own folder where acquired data, belonging to
a dataype (e.g. `ephys, behav, imaging, histology`) are stored.

Subject and session folder names cannot contain spaces and must consist of key-value pairs separated
by underscores, e.g. `sub-001_date-06122022`. 

### subject
The subject level is prefixed with the REQUIRED "sub" key and optional value, e.g. `sub-001`. Only one subject
folder per-subject is permitted, and subject labels must be unique to each subject.

### session
If data for the subject were acquired across multiple sessions,then within the subject 
directory resides subdirectories named with the REQUIRED prefix "ses", e.g. `ses-<label>`. A session represents a recording, 
imaging or behavioural experimental session, and may contain multiple blocks, or runs, of data acquisition.
The session folder will contain the acquired datatypes. Different sessions may have different combinations of datatypes.

### datatype
Datatypes included at the session level are REQUIRED to have one of the following names `ephys, behav, imaging, histology`.
If collected, `ephys, behav, imaging` are REQUIRED to be placed at the session label. 
If collected, `histology` is REQUIRED to be the subject level. 

### Example
A real project folder may look like: 
```
project
  rawdata
    sub-001
      ses-001_date-20220516
        ephys
          recording.bin
          probe.imec0
        behav
          camera_1.wav 
          responses.csv 
  derivatives
    sub-001
        ses-001_date-20220516
          ephys
            spike_sorted_data.mat
          behav
            tracking_results.csv
```
