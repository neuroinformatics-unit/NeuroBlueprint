# Metadata

1) introduce
2) explain other approaches
3) explain why we went for this approach?


## Metadata Organisation Description

At each level of the project, a metadata file can be included that describe that level:

```
└── my_project/
    ├── my_project_metadata.yml
    └── rawdata/
        ├── rawdata_metadata.yml
        ├── sub-001/
        │   ├── sub-001_metadata.yml
        │   └── ses-001/
        │       ├── ses-001_metadata.yml
        │       ├── behav/
        │       │   └── behav_metadata.yml
        │       └── ephys/
        │           └── ephya_metadata.yml
        ├── sub-002/
        │   ├── sub-002_metadata.yml
        │   └── ...
        └── ...
```

**``project_metadata.yml``**
- This file contains high-level information about the project, for example it's overall purpose,
who is involved in the project. See [].

**``rawdata_metadata.yml``**
- This file contains information about the data collection, for example XXX. See [].

**``sub-<value>_metadata.yml``**
- This contains information about an individual subject, for example its date of birth,
identifiers, genotype or other key information. See [].

**``ses-<value>_metadata.yml``**
- This file contains information related to the particular experimental session.For example,
the date, notes on what happened in the session, etc. See [].

**``<datatype>_metadata.yml``**
- This file can contain metadata specific to the datatype acquisition. See the [] section
for details on keys to include for particular datatypes.


**Other files and folders**
- In theory, any file or folder in the project can have an associated `_metadata.yml` file.
For example, you may include `events.npy`, `events.bin`, `events.mat` or some other
way of storing event timings in your project, that you would like to describe further (e.g. sampling rate).
In such a case, you can include a side-car metadata file `events_metadata.yml` that includes this information.

# Inheritance

In many cases, metadata entries may be the same for all sub-folders in a project.
For example, the sampling rate of `ephys` may be the same across the project, or the
genotype or species of a mouse line used may be the same.

Note there is no inheritance principle for single-files and folders. We recommend
adding suffixes to filenames and adopting the BIDS inheritance for files in this case.

In this case, we can place the metadata entries for lower-levels as a key in a high level.
For example, if your `ephys` sampling rate for all subjects was `30 kHz`, you could structure
your `rawdata.yml` file as:

```
SomeKey: someValue
ephys:
    samplingRate: 30000
```

This would then apply to all subjects in the folder. `sub-value_metadata.yml` files can
also be included to overwrite this information, or include additional inforatmion that does
not apply to all files. For exampl,e if you have a mouse where for some reason the SamplingRate
was XXX you can overwrite this, you may also want to include a note:

https://bids-validator.readthedocs.io/en/stable/validation-model/inheritance-principle.html
```
samplingRate: 30500
notes: "A mistake was made during acquisition, leading to a sampling rate of 30500 Hz.
```

The folder structure may look like:

```
.
└── my_project/
    └── rawdata  /
        ├── rawdata.yml   # contains the `ephys` entry applying to all subjects
        └── sub-001/
            ├── ses-001/
            │   └── ephys/
            │       ├── ephys.yml   # contains the overwriting entry
            │       └── ...
            └── ses-002/
                └── ...
```


# Recommended Metadata Keys

## Project Metadata

https://bids-specification.readthedocs.io/en/stable/modality-agnostic-files/dataset-description.html#dataset_descriptionjson

## Rawdata Metadata

(I'm not sure we need this)

## Sub Metadata

https://bids-specification.readthedocs.io/en/stable/modality-agnostic-files/data-summary-files.html

## Ses Metadata

https://bids-specification.readthedocs.io/en/stable/modality-agnostic-files/data-summary-files.html#sessions-file

## `ephys`

https://bep032tools.readthedocs.io/en/latest/

## `behav`

https://bids-specification.readthedocs.io/en/stable/modality-specific-files/behavioral-experiments.html

## `anat_metadata`

https://bids-specification.readthedocs.io/en/stable/modality-specific-files/microscopy.html
