# The specification

:::{note}
We mark specifications with italicised *keywords* that should be interpreted as described by the [Network Working Group](https://www.ietf.org/rfc/rfc2119.txt). In decreasing order of requirement, these are: *must* {octicon}`alert;1em;sd-text-danger`, *should* {octicon}`info;1em;sd-text-warning`, and *may* {octicon}`check-circle;1em;sd-text-success`.
:::

## Project Folder Structure 

Standardized project folders contain data that are hierarchically structured according to the [BIDS standard](https://bids-specification.readthedocs.io/en/stable/02-common-principles.html).

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

### Basic principles

* The project folder *may* have any name descriptive of the project, but it *must* be without spaces.

* Within the project folder, data *must* be separated into `rawdata` and `derivatives`. 

  * `rawdata`: coming out of the data acquisition system (e.g. binary files, tiffs, videos files). 

  * `derivatives`: any processed data that is derived from `rawdata` (e.g. spike sorting or pose estimation).

* Data within the `rawdata` folder *must* be hierarchically structured into `subject/session/datatype` levels. Each level *must* contain at least one folder corresponding to the next (lower) level.

* The `subject/session/datatype` folder structure within `derivatives` *should*
match that of `rawdata` whenever possible.

* `subject` and `session` folder names *must* consist of key-value pairs separated by underscores, withous spaces e.g. `sub-001_id-5645332`.

* `datatype` folder names *must* be one of the following : `ephys`, `behav`, `funcimg`, `histology`.

* If collected, `ephys`, `behav`, `funcimg` *must* be placed under the `session` level. If collected, `histology` *must* be placed under the `subject` level. 

Below we describe each level of the `rawdata` folder hierarchy in more detail.

### Subject

* Subject-level folders *must* be prefixed with a key-value pair that is unique for each subject. The key *must* be "sub" and the value *must* be numerical, e.g. `sub-001`. 
* Subjects *should* be assigned ascending numerical labels as they are added to the project. The labels *should* be prefixed with an arbitrary number of 0s for consistent indentation, e.g. `sub-001`, `sub-002`, `sub-003`.
* Each subject *must* have exactly one subject-level folder. 
* Additional key-value pairs with alphanumerical labels *may* be appended after the "sub" key-value pair. For example, animal IDs (e.g. from the animal facility) can be added as follows: `sub-001_id-5645332`. The keys *should* be consistent across subjects.

:::{hint}
* valid: `sub-02`, `sub-001_id-5645332_sex-F`
* invalid: `mouse-01`, `sub-001_female`, `sub-B`
:::

### Session

* Session-level folders *must* be prefixed with a key-value pair that is unique for each session. The key *must* be "ses" and the value *must* be numerical, e.g. `ses-01`. 
* Sessions *should* be assigned ascending numerical labels as they are added to the project. The labels *should* be prefixed with an arbitrary number of 0s for consistent indentation, e.g. `ses-01`, `ses-02`, `ses-03`.
* Each session *must* have exactly one session-level folder. 
* Additional key-value pairs with alphanumerical labels *may* be appended after the "ses" key-value pair. For example, dates can be added as follows: `ses-001_date-20230310`. The keys *should* be consistent across subjects.
* If a date field is added, it *should* be in the format `YYYYMMDD`.
* Different sessions *may* contain different combinations of datatypes.

:::{hint}
* valid: `ses-02`, `ses-2_date-20230204`
* invalid: `sex-F_ses-01`, `session2`, `ses-A`
:::

### Datatype

The following datatypes are supported:

* `ephys`: electrophysiology data (e.g. Neuropixel probes, tetrodes, etc.)
* `behav`: behavioral data (video and audio files, response logs, etc.)
* `funcimg`: functional imaging data (e.g. calcium imaging, voltage imaging, etc.)
* `histology`: anatomical data (e.g. serial-2-photon images, histology slides, etc.)

:::{note}
Unlike the first three `datatypes` that belong at the `session` level, `histology` belongs at the `subject` level.
:::

### Example project folder
A real project folder might look like:

```
└── project/
    ├── rawdata/
    │   └── sub-001_id-5645332/
    │       ├── ses-01_date-20230310/
    │       │   ├── ephys/
    │       │   │   ├── sub-001_ses-01_recording.bin
    │       │   │   └── sub-001_ses-01_probe.imec0
    │       │   └── behav/
    │       │       ├── sub-001_ses-01_camera1.wav 
    │       │       └── sub-001_ses-01_responses.csv 
    │       └── histology/
    │           └── brain_image.tiff
    └── derivatives/
        └── sub-001_id-5645332/
            ├── ses-01_date-20230310/
            │   ├── ephys/
            │   │   └── sub-001_ses-01_spike-sorted-data.npy
            │   └── behav/
            │       └── sub-001_ses-01_tracking-results.csv
            └── histology/
                └── sub-001_ses-01_cell-counts.csv
```

## File Naming Conventions

`SWC-Bluprint` does not impose any absolute requirements on file names. That said, below we provide some recommendations for file names, based on the [BIDS specification](https://bids-specification.readthedocs.io/en/stable/02-common-principles.html#filenames).

:::{admonition} What makes a good file name?
:class: tip
* be nice to humans -> readable and descriptive
* be nice to computers -> parseable and consistent (e.g. use `key1-value1_key2-value2` convention)
* use alphanumeric characters `Aa-Zz, 0-9`, dashes `-`, underscores `_`
* avoid spaces and special characters
* use appropriate extensions for each file type (e.g. `.csv`, `.avi`, `.tiff`)
* don't rely on capitalization to distinguish files (some operating systems are case-insensitive)
:::

* File names *should* be formatted as series of key-value pairs, followed by an *optional* suffix, and ending with a file extension (e.g `sub-001_ses-001_date-20220516_retinotopy.bin`). 

* Key-value pairs should be separated by underscores while the keys and values are
separated by hyphens (e.g. `sub-001_ses-001_key1-value1_key2-value2.csv`).
* It is *recommended* to include the `sub` and `ses` keys. This may seem redundant (given that the file is already in a subject or session folder), but it makes is easier to identify the file if it is moved out of its original folder.
* Additional information, such as the task name, or run number, *may* be included as further key-value pairs, e.g. `sub-001_ses-001_task-escape_run-001.csv`
* Anything after the left-most stop (`.`) is considered the file extension.
* The filename can include an *optional* suffix, between the last key-value pair and the file extension. You *may* use the suffix to indicate a logical grouping to which the file belongs, e.g. `sub-001_ses-001_run-001_retinotopy.ap.csv`
* If using a suffix, you *should not* include `-` or `_`within it, to avoid confusion with key-value pairs. You *may* use CamelCase to separate words for readability, e.g. `sub-001_ses-001_task-Ymaze_TopCamera.avi`.
* If the acquisition software outputs data with its own mandatory file naming convention, these *should* be placed under a folder that follows the `SWC-Blueprint` naming conventions. You *may* use the suffix to indicate the software that generated the data, e.g:

```
└── my_project/
    └── rawdata/
        └── sub-001/
            └── ses-001/
                └── behav/
                    └── sub-001_ses-001_task-discrimination_software/
                        ├── required-software-output-name-3453234.mp4
                        └── required-software-output-name-3453235.mp4
```


### Example project with file names
```
└── project/
    └── rawdata/
        └── sub-001/
            └── ses-01/
                ├── ephys/
                │   ├── sub-001_ses-01_probe.imec0
                │   ├── sub-001_ses-01_retinotopy.af.bin
                │   ├── sub-001_ses-01_task-discrim_monitor-right_run-001.ap.bin
                │   ├── sub-001_ses-01_task-discrim_monitor-left_run-001.ap.bin
                │   └── sub-001_ses-01_task-discrim_monitor-left_run-002.ap.bin
                └── behav/
                    ├── sub-001_ses-01_task-discrim_monitor-right_run-001.mp4
                    ├── sub-001_ses-01_task-discrim_monitor-left_run-001.mp4
                    └── sub-001_ses-01_task-discrim_monitor-right_run-002.mp4
```

