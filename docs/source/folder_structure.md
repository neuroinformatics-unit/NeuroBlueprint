# Specification
## Folders structure 
Your project folder containing raw data will be structured in a hierarchical way following BIDS standards:
```
project/
└── subject/
    └── session/
        └── datatype/
            └── run/
                ├── some_raw_data_file
                ├── some_preprocessed_data_file
                └── notes
```

Here is an example:
```
my_project/
└── mouse-01/
    └── ses-01/
        └── ephys/
            └── run-01/
                ├── my_recording.wav
                ├── spike_sorted_data.mat
                └── notes.yaml
```
## Naming convention

### Project
Can have any name, this should be descriptive of the dataset contained in the folder.

### Subject
Structure: `sub-<participant label>`
One folder per subject in this dataset. Labels should be unique for each subject.
Example: `mouse-01`

### Session
Structure: `ses-<session label>`

In general, a session represents a recording session, and subjects will stay in the scanner or under the microsocpe during that session. You might have multiple sessions per subject if you collected data from them on several occasions. If there is only a single session per subject, this level of the hierarchy may be omitted.




A subject can be either a human or an animal. For each subject, multiple experimental session might exists. 
In each session, multiple data types can be collected.
Each data type can be collected multiple times (e.g. multiple runs of the same experiment).
Each run can contain multiple files (e.g. raw data, preprocessed data, notes).
