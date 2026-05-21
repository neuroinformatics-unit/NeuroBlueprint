:orphan:
# Metadata

[Scientific metadata](https://www.dcc.ac.uk/resources/curation-reference-manual/chapters-production/scientific-metadata)
is additional data that describes the project data itself. **TODO: BETTER MOTIVATION
add a link to what metadata is / why you care and add it to your data etc.**

Metadata can
be high-level (e.g. a general overview of the study and its purpose) or
low-level (acquisition parameters for extracellular electrophysiology
setup, or microscope).

A number of detailed metadata standards exist, including those from
[BIDS](https://bids-specification.readthedocs.io/en/stable/introduction.html),
[openMINDS](https://github.com/openMetadataInitiative) and
the [Allen Institute for Neural Dynamics](https://github.com/AllenNeuralDynamics/aind-data-schema),
each differing in its structure, level of detail and the datatypes they cover.

Here, we provide a simple schema that you can use to
get started with adding metadata to your NeuroBlueprint project. You are free to add
metadata fields if you wish, but at the
[end of this guide](metadata-keys) we recommend fields
that can go in each section.

Please get in touch by raising a
[GitHub Issue](https://github.com/neuroinformatics-unit/NeuroBlueprint/issues)
if you would like additional keys added to the metadata fields.

# YAML file format

Metadata files should use the [YAML](https://yaml.org/) file format (`.yaml` extension).
YAML is a human-readable text format designed to be easy to read and edit.

YAML stores information as **key-value pairs** and uses indentation (spaces) to represent structure.

For example, a simple metadata file might look like:

```yaml
project:
    projectName: "Visual Decision Making Study"
    species: "Mus musculus"
    experimenters:
      - "Jane Smith"
      - "John Doe"

sub:
  genoType: Something TOOOOOOOOOOOOOOOOODOOOOOOOOOOOOOOO

ephys:
  samplingRate: 30000
  probeType: "Neuropixels 2.0"
```

## Metadata Organisation Description

Metadata should be stored in `metadata.yaml` files that can include any of 
these pre-defined sections, which map to NeuroBlueprint folder levels:

- `project`
- `rawdata`
- `sub`
- `ses`
- [Neuroblueprint datatype]() (e.g. `behav`, `ephys`)


For example, a `metadata.yaml` file contents might look like:

```yaml
project:

rawdata:

sub:

ses:

ephys:

behav:
```

To see more information on what information should be
put at each section, see the [metadata keys](metadata-keys) section.

In this case, these entries apply to every dataset in the project. Therefore,
we can place this metadata file at the top-level of the project:

```
└── my_project/
    ├── metadata.yaml
    └── rawdata/
        ├── sub-001/
        │   └── ses-001/
        │       ├── behav/
        │       └── ephys/
        ├── sub-002/
        │   └── ...
        └── ...
```

The location of the folder indicates to which data the metadata belongs to. A metadata
file applies to all levels below it. 

## Inheritance

In some cases, the same metadata might not apply to all datasets within the project.
In this case, a `metadata.yaml` file can be placed at a lower level, overwriting
the metadata fields at a higher level.

For example, let's say that `sub-001`, `ses-002` used a different gain due to an
experimental error. We can put a `metadata.yaml` file in the `sub-001` folder
with the `ephys` entry and `...`. Now, gain at XXX applies to all sessions except for.

```
└── my_project/
    ├── metadata.yaml
    └── rawdata/
        ├── sub-001/
        │   └── ses-001/
        │       ├── behav/
        │       └── ephys/
        ├── sub-002/
        │   └── ...
        └── ...
```

```yaml
ephys:
  xxx
```

This was inspired by the similar inheritance principle in [BIDS](https://bids-validator.readthedocs.io/en/stable/validation-model/inheritance-principle.html)

:::{tip}
When it is possible to put `metadata.yaml` file in multiple places, we recommend placing
the file at the highest possible level. For example, in the example above the ephys
information for `sub-001/ses-001/metadata.yaml` is placed in the equally valid
session folder, rather than in the ephys folder `sub-001/ses-001/ephys/metadata.yaml`.
:::

# Sidecar metadata files 

In some cases it may be required to associate metadata with a specific
data file. In this case, a metadata YAML file that copies the original
filename with the suffix `_metadata` can be instantiated. It should
contain one of the same sections as above (e.g. `sub`, `behav` etc.).
  
:::{warning}

all metadata files must be called metadata.yaml or be
the exact name as an existing file or folder

:::
  
For example, in the `behav` folder you might have multiple
acquisition runs, each with different metadata. 

```
└── my_project/
    ├── metadata.yaml
    └── rawdata/
        └── sub-001/
            └── ses-001/
                └── behav/
                    ├── run-001_camera-top.mp4
                    ├── run-001_camera-top_metadata.yaml
                    ├── run-002_camera-top.mp4
                    └── run-002_camera-top_metadata.yaml
```

metadata.yaml
```yaml
behav:
    cameraSamplingRate: 20Hz
```

run-001_camera-top_metadata.yaml

```yaml
behav:
    cameraSamplingRate: 30Hz
```

run-002_camera-top_metadata.yaml

```yaml
behav:
    cameraSamplingRate: 60Hz
```

Similar to the inheritance principal above, the lower-level metadata
will overwrite any entries at the higher level.

(metadata-keys)=
# Recommended Metadata Keys

To ensure alignment across and within projects, we recommend using metadata keys from
a predefined set. Here we use BIDS as an existing source of metadata keys for each section.

Please get in touch if you would like us to add new metadata fields to this list.
**- examples / suggested keys. A few more sentences about this just to explain our approach. You can put anything in here you like, but good to keep consistent readable
for everyone. if the thing exists already,
then use the BIDS name.**

## Project Metadata

- This file contains high-level information about the project, for example its overall purpose,
who is involved in the project.

We use the BIDS `dataset_description.json` fields as a starting point for project-level metadata.

See the full specification for detailed descriptions:
[BIDS Dataset Description Specification](https://bids-specification.readthedocs.io/en/stable/modality-agnostic-files/dataset-description.html#dataset_descriptionjson).

Recommended keys:

**TODO: check all keys, AI messed this up**
**add actual entries here**.

```yaml
Name:
NeuroBlueprintVersion:
HEDVersion:
DatasetLinks:
DatasetType:
License:
Authors:
Keywords:
Acknowledgements:
HowToAcknowledge:
Funding:
EthicsApprovals:
ReferencesAndLinks:
DatasetDOI:
SourceDatasets: 
```

(rawdata-metadata)=
## Rawdata Metadata

This file contains information about the data collection, for example the species of animal used
in the project. It may also contain specific sections for datatypes, that apply to all subjects
in the project. For example, if `ephys` data was collected at a sampling rate of 30kHz for every subject,
it may contain an `ephys` section with a `samplingRate` field. See [rawdata metadata](rawdata-metadata).


This file is primarily intended for metadata that applies across the whole dataset,
including inherited datatype-specific metadata (for example `ephys` acquisition settings).

Example structure:

```yaml
sub:
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

This metadata file contains information about an individual subject, for example the date of birth,
identifiers, genotype or other key information. Here `<value>` is the subject number, for example `sub-001_metadata.yml`.
See [subject metadata](sub-metadata)

We use the BIDS participant fields as a starting point for subject-level metadata.

See the full specification for detailed descriptions:
[BIDS Participants Specification](https://bids-specification.readthedocs.io/en/stable/modality-agnostic-files/data-summary-files.html).

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

- This file contains information related to the particular experimental session. For example,
the date, additional notes on what happened in the session.
Here `<value>` is the session number, for example `ses-001_metadata.yml`.
See [session metadata](ses-metadata).
- 
We use the BIDS session fields as a starting point for session-level metadata.

See the full specification for detailed descriptions:
[BIDS Sessions Specification](https://bids-specification.readthedocs.io/en/stable/modality-agnostic-files/data-summary-files.html#sessions-file).

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

- This file can contain metadata specific to the datatype acquisition. See the [datatype keys](datatype-keys)
section for details on keys to include for particular datatypes.

Datatype metadata files contain acquisition-specific metadata for each modality.

(ephys-metadata)=
## `ephys`

We use BIDS electrophysiology metadata fields as a starting point.

See the full specification for detailed descriptions:
[BEP032 Electrophysiology Metadata Specification](https://bids.neuroimaging.io/extensions/beps/bep_032.html).

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
[BIDS Behavioural Experiments Specification](https://bids-specification.readthedocs.io/en/stable/modality-specific-files/behavioral-experiments.html).

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
[BIDS Microscopy Specification](https://bids-specification.readthedocs.io/en/stable/modality-specific-files/microscopy.html).

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
