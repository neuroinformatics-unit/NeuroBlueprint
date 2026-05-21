:orphan:
# Metadata

Metadata is additional data that describes the project data itself. Metadata can
be high-level (e.g. a general overview of the study and its purpose) or
low-level (acquisition parameters for extracellular electrophysiology
setup, or microscope).

A number of detailed metadata standards exist, including those from
[BIDS](https://bids-specification.readthedocs.io/en/stable/introduction.html),
[openMINDS](https://github.com/openMetadataInitiative) and
the [Allen Institute for Neural Dynamics](https://github.com/AllenNeuralDynamics/aind-data-schema),
each differing in its structure, level of detail and the datatypes they cover.

Here, we provide a simple metadata organisation scheme that you can use to
get started with adding metadata to your project. You are free to add
metadata fields if you wish, but at the end of this guide we recommend fields
that can go in each section.

Please get in touch if you would like additional keys added to the metadata fields.

## Metadata Organisation Description

At each level of the project, a metadata file can be included that describes that level:

```yaml
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
        │           └── ephys_metadata.yml
        ├── sub-002/
        │   ├── sub-002_metadata.yml
        │   └── ...
        └── ...
```

**``project_metadata.yml``**
- This file contains high-level information about the project, for example its overall purpose,
who is involved in the project. See [project metadata](project-metadata).

**``rawdata_metadata.yml``**
- This file contains information about the data collection, for example the species of animal used
in the project. It may also contain specific sections for datatypes, that apply to all subjects
in the project. For example, if `ephys` data was collected at a sampling rate of 30kHz for each subject,
it may contain an `ephys` section with a `samplingRate` field. See [rawdata metadata](rawdata-metadata).

**``sub-<value>_metadata.yml``**
- This contains information about an individual subject, for example the date of birth,
identifiers, genotype or other key information. See [subject metadata](sub-metadata).

**``ses-<value>_metadata.yml``**
- This file contains information related to the particular experimental session. For example,
the date, additional notes on what happened in the session.  See [session metadata](ses-metadata).

**``<datatype>_metadata.yml``**
- This file can contain metadata specific to the datatype acquisition. See the [datatype keys](datatype-keys)
section for details on keys to include for particular datatypes.

# YAML file format

Metadata files should use the [YAML](https://yaml.org/) file format (`.yml` or `.yaml`).
YAML is a human-readable text format designed to be easy to read and edit.

YAML stores information as **key-value pairs** and uses indentation (spaces) to represent structure.

For example, a simple metadata file may look like:

```yaml
projectName: "Visual Decision Making Study"
species: "Mus musculus"

ephys:
  samplingRate: 30000
  probeType: "Neuropixels 2.0"

experimenters:
  - "Jane Smith"
  - "John Doe"
```

# Inheritance

It may be that a particular metadata entry is the same for all sub-folders in a project.
For example, the sampling rate used for the `ephys` data may be the same across all sessions
in the project.

In this case, we can place the metadata entries for lower levels as keys at a higher level.
For example, if your `ephys` sampling rate for all subjects was `30 kHz`, you could structure
your `rawdata_metadata.yml` file as:

```yaml
SomeKey: someValue
ephys:
    samplingRate: 30000
```

This would then apply to all subjects in the `rawdata` folder.

However, this can be overwritten for particular cases e.g. if due to an error, a different
sampling rate was used in the acquisition. To do this, a metadata file should be included
for the case of interest in the relevant folder. For example, if `sub-005` used a different
sampling rate for all sessions, a `sub-005_metadata.yml` file could be included to overwrite the
information for this particular subject. e.g.

```yaml
samplingRate: 30500
notes: "A mistake was made during acquisition, leading to a sampling rate of 30500 Hz."
```

The folder structure may look like:

```
.
└── my_project/
    └── rawdata/
        ├── rawdata_metadata.yml   # contains the `ephys` entry applying to all subjects
        └── sub-001/
            ├── ses-001/
            │   └── ephys/
            │       ├── ephys_metadata.yml   # contains the overwriting entry
            │       └── ...
            └── ses-002/
                └── ...
```

This was inspired by the similar inheritance principle in [BIDS](https://bids-validator.readthedocs.io/en/stable/validation-model/inheritance-principle.html)

# Recommended Metadata Keys

To ensure alignment across and within projects, we recommend using metadata keys from
a predefined set. Here we use BIDS as an existing source of metadata keys for each section.

Please get in touch if you would like us to add new metadata fields to this list.

(project-metadata)=
## Project Metadata

We use the BIDS `dataset_description.json` fields as a starting point for project-level metadata.

See the full specification for detailed descriptions:
[BIDS Dataset Description Specification](https://bids-specification.readthedocs.io/en/stable/modality-agnostic-files/dataset-description.html#dataset_descriptionjson)

Recommended keys:

```yaml
Name:
BIDSVersion:
DatasetType:
License:
Authors:
Acknowledgements:
HowToAcknowledge:
Funding:
EthicsApprovals:
ReferencesAndLinks:
DatasetDOI:
```

(rawdata-metadata)=
## Rawdata Metadata

This file is primarily intended for metadata that applies across the whole dataset,
including inherited datatype-specific metadata (for example `ephys` acquisition settings).

Example structure:

```yaml
species:
strain:

ephys:
  samplingRate:
  probeType:

behav:
  taskName:
```

(sub-metadata)=
## Sub Metadata

We use the BIDS participant fields as a starting point for subject-level metadata.

See the full specification for detailed descriptions:
[BIDS Participants Specification](https://bids-specification.readthedocs.io/en/stable/modality-agnostic-files/data-summary-files.html)

Recommended keys:

```yaml
subject_id:
age:
sex:
handedness:
species:
strain:
strain_rrid:
genotype:
dateOfBirth:
```

(ses-metadata)=
## Ses Metadata

We use the BIDS session fields as a starting point for session-level metadata.

See the full specification for detailed descriptions:
[BIDS Sessions Specification](https://bids-specification.readthedocs.io/en/stable/modality-agnostic-files/data-summary-files.html#sessions-file)

Recommended keys:

```yaml
session_id:
sessionDate:
age:
weight:
notes:
experimenter:
```

(datatype-keys)=
## Datatype keys

Datatype metadata files contain acquisition-specific metadata for each modality.

(ephys-metadata)=
## `ephys`

We use BIDS electrophysiology metadata fields as a starting point.

See the full specification for detailed descriptions:
[BEP032 Electrophysiology Metadata Specification](https://bep032tools.readthedocs.io/en/latest/)

Recommended keys:

```yaml
samplingRate:
probeType:
manufacturer:
hardwareFilters:
softwareFilters:
electrodeCount:
referenceChannel:
groundChannel:
amplifier:
```

(behav-metadata)=
## `behav`

We use the BIDS behavioural experiment metadata fields as a starting point.

See the full specification for detailed descriptions:
[BIDS Behavioural Experiments Specification](https://bids-specification.readthedocs.io/en/stable/modality-specific-files/behavioral-experiments.html)

Recommended keys:

```yaml
taskName:
taskDescription:
instructions:
stimulusPresentation:
responseDevice:
samplingRate:
softwareName:
softwareVersion:
```

(anat-metadata)=
## `anat`

We use the BIDS microscopy metadata fields as a starting point.

See the full specification for detailed descriptions:
[BIDS Microscopy Specification](https://bids-specification.readthedocs.io/en/stable/modality-specific-files/microscopy.html)

Recommended keys:

```yaml
sampleFixation:
staining:
microscopeManufacturer:
microscopeModel:
objectiveLens:
magnification:
numericalAperture:
immersionMedium:
voxelSize:
imageFormat:
```
