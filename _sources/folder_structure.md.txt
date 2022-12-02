# Folders structure 
Your project folder containing raw data will be structured in a hierarchical way following BIDS standards:
```
project/
└── subject/
    └── session/
        └── datatype/
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
            ├── my_recording.wav
            ├── spike_sorted_data.mat
            └── notes.yaml
```
## Naming folders

### Project
Can have any name, this should be descriptive of the dataset contained in the folder.

### Subject
Structure: `sub-<participant label>`
One folder per subject in this dataset. Labels should be unique for each subject.
Example: `mouse-01`

### Session
Structure: `ses-<session label>`

In general, a session represents a recording, imaging or behavioural experiment, with a definite kind of techniques involved and a given set of parameters. You might have multiple sessions per subject if you collected data from them on several occasions. 
Example: `ses-01`

### Datatype
Structure: `datatype`
Represents different types of data. Must be one of:
- `ephys`
- `imaging` (microscopy)
- `behaviour`
- `histology`
