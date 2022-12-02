## File Naming Conventions

File names should be specified as a set of key-value pairs (key-value separated by a hyphen), with key-value pairs separated by underscores indicating the subject, session (REQUIRED)
and other OPTIONAL information. An example filenames in an ephys folder structure may be:
some key-value pairs may include task (e.g. XXX), run (XXXX). Finally, the filename
can end with an OPTIONAL suffix that indicates a logical group to which it belongs. For example,
ephys.
In some instances, XXX own file naming convention. in these instances should put
in their own folder with the BIDS specification name. Anything after . is considered an extension (?)

TODO: write in about session, remote from example

```
project
    sub-001
        ses-001
            ephys
                sub-001_retinotopy.af.bin
                sub-001_task-stimdiscrim_run-001_rightmonitor.af.bin
                sub-001_task-stimdiscrim_run-001_lefttmonitor.af.bin
                sub-001_task-stimdiscrim_run-002_rightmonitor.af.bin
                sub-001_task-stimdiscrim_run-002_lefttmonitor.af.bin
            behav
                sub-001_ses-001_task-stimdiscrim_run-001_rightmonitor.mp4
                sub-001_ses-001_task-stimdiscrim_run-001_rightmonitor.mp4
                sub-001_ses-001_task-stimdiscrim_run-001_rightmonitor.mp4
                sub-001_ses-001_task-stimdiscrim_run-001_rightmonitor.mp4
```