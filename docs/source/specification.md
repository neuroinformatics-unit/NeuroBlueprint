# Specification

## Project Folder Structure 

Standardized project folders containing raw data are hierarchically structured according to the 
[BIDS standard](https://bids-specification.readthedocs.io/en/stable/02-common-principles.html). 

Following the BIDS specification, we mark specifications as *required*, *recommended* and *optional*.

For example:

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
data acquired during data collection. `derivatives` includes any processed data (e.g. spike sorting or pose estimation). 
The subject / session / datatype folder structure within derivatives should
match the rawdata folder whenever possible.

Each subject (e.g. mouse, rat) in the project has a dedicated folder in which all data from 
experimental sessions are stored.
In the case of multiple sessions, each session has its own folder where acquired data, belonging to
a dataype (e.g. `ephys, behav, funcimg, histology`) are stored.

Subject and session folder names cannot contain spaces and must consist of key-value pairs separated
by underscores, e.g. `sub-001_id-5645332`. 

### Subject
The subject level is prefixed with the *required* "sub" key - value pair, e.g. `sub-001`. Only one subject
folder per-subject is permitted, and subject labels must be unique to each subject. *optional* key - value pairs 
can be added after sub-<label> (e.g. `sub-001_id-5645332`).

### Session
Within the subject directory reside session subdirectories named with the *required* prefix "ses", e.g. `ses-<label>`. A session represents a recording, 
functional imaging or behavioural experimental session, and may contain multiple blocks, or runs, of data acquisition.
Different sessions may have different combinations of datatypes. *optional* key - value pairs can be added after ses-<label>
(e.g. `ses-001_date-220516`).

### Datatype
Datatypes are *required* to have one of the following names `ephys, behav, funcimg, histology`.
If collected, `ephys, behav, funcimg` are *required* to be placed at the session level. 
If collected, `histology` is *required* to be at subject level. 

### Example
A real project folder may look like: 
```
└── project/
    ├── rawdata/
    │   └── sub-001/
    │       ├── ses-001_id-5645332/
    │       │   ├── ephys/
    │       │   │   ├── recording.bin
    │       │   │   └── probe.imec0
    │       │   └── behav/
    │       │       ├── camera_1.wav 
    │       │       └── responses.csv 
    │       └── histology/
    │           └── brain_image.tiff
    └── derivatives/
        └── sub-001/
            ├── ses-001_id-5645332/
            │   ├── ephys/
            │   │   └── spike_sorted_data.mat
            │   └── behav/
            │       └── tracking_results.csv
            └── histology/
                └── cell_counts.csv
```

## File Naming Conventions

File names are *required* to be formatted as set of key-value pairs ending with an *optional* suffix and *required* file extension (e.g. `ses-001_date-20220516_retinotopy.ap.bin`). 

Key-value pairs are separated by underscores while the key and values 
separated by hypens (e.g. `sub-001_key1-value1_key2-value2.csv`). Key-value pairs other than the *required* `sub` or `ses` are *optional* and can contain 
additional information. These might include the task name, or run number e.g. `sub-001_task-escape_run-001.csv`

The filename may also end in an *optional* suffix, indicating a logical grouping to which it belongs (e.g. `sub-001_run-001_retinotopy.csv`). 
Anything after the left-most stop (`.`) is considered the file extension. 

If acquisition software outputs data with its own mandatory file naming convention, such are *required* 
to be placed in a folder with the BIDS specification name.

e.g.
```
└── my_project/
    └── rawdata/
        └── sub-001/
            └── ses-001/
                └── behav/
                    └── sub-001_task-discrimination_video/
                        ├── required-software-output-name-3453234.mp4
                        └── required-software-output-name-3453234.mp4
```


### Example Project Structure
```
└── project/
    └── sub-001/
        └── ses-001/
            ├── ephys/
            │   ├── sub-001_probe.imec0
            │   ├── sub-001_retinotopy.af.bin
            │   ├── sub-001_task-discrim_monitor-right_run-001.ap.bin
            │   ├── sub-001_task-discrim_monitor-left_run-001.ap.bin
            │   └── sub-001_task-discrim_monitor-left_run-002.ap.bin
            └── behav/
                ├── sub-001_task-discrim_monitor-right_run-001.mp4
                ├── sub-001_task-discrim_monitor-left_run-001.mp4
                └── sub-001_task-discrim_monitor-right_run-002.mp4
```

