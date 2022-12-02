## File Naming Conventions

File names should be specified as a set of key-value pairs (key-value separated by a hyphen), 
with key-value pairs separated by underscores indicating the subject, session (REQUIRED)
and other OPTIONAL information. In some instances, acquisition software may output data with its own required file naming convention - 
in these instances should put in their own folder with the BIDS specification name. 


An example filenames in an ephys folder structure may be:
some key-value pairs such as task, run,  (e.g. task-escape, run (run-001). Finally, the filename
can end with an suffix (OPTIONAL) that indicates a logical group to which it belongs. 
Anything after the left-most stop (.) is considered the file extension. 

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
the sub-<label> tag is REQUIRED in file names, but ses-<label> is OPTIONAL. 



