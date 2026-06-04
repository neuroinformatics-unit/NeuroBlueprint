:orphan:
# Metadata

[Scientific metadata](https://www.dcc.ac.uk/resources/curation-reference-manual/chapters-production/scientific-metadata)
is additional information included with a project that describes the data itself. Adding metadata to your project
makes it easier to understand, reproduce and share the data.

Metadata can be high-level (e.g. a general overview of the study and its purpose) or
low-level (acquisition parameters for extracellular electrophysiology
setup, or microscope).

A number of detailed metadata standards exist, including those from
[BIDS](https://bids-specification.readthedocs.io/en/stable/introduction.html),
[openMINDS](https://github.com/openMetadataInitiative) and
the [Allen Institute for Neural Dynamics](https://github.com/AllenNeuralDynamics/aind-data-schema),
each differing in its structure, level of detail and the datatypes they cover.

Here, we provide a simple schema that you can use to
get started with adding metadata to your **NeuroBlueprint** project. You are free to add
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
    Name: "Visual Decision Making Study"
    Authors:
      - "Jane Smith"
      - "John Doe"

sub:
    Species: "Mus musculus"
    Genotype: "Thy1-GCaMP6s/wt"

ephys:
    SamplingFrequency: 30000
    ManufacturersModelName: "Neuropixels 2.0"
```

# Metadata organisation schema

Metadata should be stored in `metadata.yaml` files that can include any of
these pre-defined sections, which map to **NeuroBlueprint** folder levels:

- `project`
- `sub`
- `ses`
- [**NeuroBlueprint** datatype](https://neuroblueprint.neuroinformatics.dev/latest/specification.html#datatype) (e.g. `behav`, `ephys`)


For example, a `metadata.yaml` file contents might look like:

```yaml
project:
    Name: "Visual Decision Making Study"
    Authors:
      - "Jane Smith"
      - "John Doe"

sub:
    Species: "Mus musculus"
    Strain: "C57BL/6J"
    StrainRrid: "RRID:IMSR_JAX:000664"

ses:
    Experimenter: "Jane Smith"
    Notes: "First recording session"

ephys:
    SamplingFrequency: 30000
    ManufacturersModelName: "Neuropixels 2.0"
    PowerLineFrequency: 50
    RecordingType: "continuous"

behav:
    TaskName: "Visual Decision Making"
    TaskDescription: "Mouse makes decisions based on visual stimuli"
```

For more details on what information should be put in each section,
see the [metadata keys](metadata-keys) section.

The location of the `metadata.yaml` file indicates what data the metadata refers to.

**A metadata file applies to data in all folder levels at or below it.**


In the above example, the entries apply to all data in the project. Therefore,
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

## Inheritance

Sometimes, the same metadata might not apply to all data within the project.
In such cases, a `metadata.yaml` file can be placed at a lower level, overwriting
the metadata fields inherited from higher levels.

For example, let's say that `sub-001/ses-001` used a different sampling frequency,
due to an experimental error. Instead of 30000 Hz, 27000 Hz was used.

We can put a new `metadata.yaml` file in the `sub-001/ses-001` folder
with the `ephys` entry and updated sampling frequency:

```
└── my_project/
    ├── metadata.yaml
    └── rawdata/
        ├── sub-001/
        │   └── ses-001/
        │       ├── metadata.yaml
        │       ├── behav/
        │       └── ephys/
        ├── sub-002/
        │   └── ...
        └── ...
```

with `sub-001/ses-001/metadata.yaml` containing:

```yaml
ephys:
  SamplingFrequency: 27000
```

Now, `SamplingFrequency` at 30000 applies to all sessions except for
`sub-001/ses-001`, which is 27000:

This was inspired by the similar inheritance principle in [BIDS](https://bids-validator.readthedocs.io/en/stable/validation-model/inheritance-principle.html)

:::{tip}
When it is equivalent to put the `metadata.yaml` file at one of multiple folder levels,
we recommend placing the file at the highest possible level.

In the above example, the ephys information for `sub-001/ses-001/metadata.yaml` is placed in the
session folder, rather than the equally valid ephys folder `sub-001/ses-001/ephys/metadata.yaml`.
:::

# Sidecar metadata files

It may be required to associate metadata with a specific data file or folder.
In this case, a metadata YAML file that copies the original
file or folder name with the suffix `_metadata` can be used. These are called 'sidecar' metadata files.

Sidecar metadata files should contain the same sections as above (e.g. `sub`, `behav` etc.).

For example, in the `behav` folder there may be multiple
acquisition runs, with different associated metadata. In this case, a metadata
YAML file that applies specifically to a particular file can be created.

For example, in the project below all videos are assumed to be of the task
`"Visual Decision Making"`. However, imagine for the run `run-002_camera-top.mp4`
a video was taken of a different task.

In this case, we can use inheritance to overwrite the `TaskName` for this particular run
by placing a sidecar metadata file next to the video file of interest:

```
└── my_project/
    ├── metadata.yaml
    └── rawdata/
        └── sub-001/
            └── ses-001/
                └── behav/
                    ├── run-001_camera-top.mp4
                    ├── run-002_camera-top.mp4
                    └── run-002_camera-top_metadata.yaml
```

`/my_project/metadata.yaml`

```yaml
behav:
    TaskName: "Visual Decision Making"
```

`run-002_camera-top_metadata.yaml`

```yaml
behav:
    TaskName: "Visual Decision Making Modified Long"
```

:::{warning}

All metadata files must be called `metadata.yaml` or be
the exact name of an existing file or folder with a `_metadata` suffix.

For example, `my_recording_metadata.yaml` is only valid if there is a file or folder
called `my_recording` (e.g. `my_recording.bin`).

:::

(metadata-keys)=
# Suggested metadata keys

**NeuroBlueprint** does not mandate the use of any specific metadata key-value
pairs. In theory, the structural rules above can be used to document the project
as you wish.

However, we highly recommend using one of the suggested metadata
keys detailed below if it covers the concept you want to document. This helps
ensure that metadata entries are interoperable with your immediate colleagues, and across labs.

For example, if you want to include the species of mice in your project, it
makes sense to use the suggested key `Species` rather than come up with your own key.

If you find that your use case is not covered by a suggested key, please
[get in touch](https://github.com/neuroinformatics-unit/NeuroBlueprint)
and we will be happy to add it to this page.

## `project` metadata

This section contains high-level information about the project, for example the people involved and the project's overall purpose.

For detailed descriptions of the suggested keys, see the
[BIDS Dataset Description Specification](https://bids-specification.readthedocs.io/en/stable/modality-agnostic-files/dataset-description.html#dataset_descriptionjson).

Suggested keys:

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

(sub-metadata)=
## `sub` metadata

This metadata file contains information about experimental subjects,
for example the date of birth, identifiers, strain or genotype.

Suggested key are taken from the
[BIDS Participants Specification](https://bids-specification.readthedocs.io/en/stable/modality-agnostic-files/data-summary-files.html).
Note they are presented as snake_case in the specification, but we recommend PascalCase for consistency with other metadata files.

Suggested keys:

```yaml
SubjectId:
Age:
Sex:
Handedness:
Species:
Strain:
StrainRrid:
Genotype:
DateOfBirth:
```

(ses-metadata)=
## `ses` metadata

This file contains information related to the particular experimental session. For example,
the date, additional notes on what happened in the session.

We use the BIDS session fields as a starting point for session-level metadata.

Suggested key are taken from the
[BIDS Sessions Specification](https://bids-specification.readthedocs.io/en/stable/modality-agnostic-files/data-summary-files.html#sessions-file).
Note they are presented as snake_case in the specification, but we recommend PascalCase for consistency with other metadata files.

Suggested keys:

```yaml
SessionId:
SessionDate:
Age:
Weight:
Notes:
Experimenter:
```

(datatype-keys)=
## Datatype keys

Datatype metadata files contain acquisition-specific metadata for each modality.
**NeuroBlueprint** contains many possible [datatypes](https://neuroblueprint.neuroinformatics.dev/latest/specification.html#datatype)
e.g. `ephys`, `behav`, `funcimg`, `anat`.

Where possible, we recommend using the BIDS keys from relevant Bids Extension Proposals (BEPs).
These are detailed below for `ephys`, `behav` and `anat`.

(ephys-metadata)=
### `ephys`

See the
[BEP032 Electrophysiology Metadata Specification](https://bids.neuroimaging.io/extensions/beps/bep_032.html).
for detailed descriptions.

Suggested keys:

- **Institution Information**
  - `InstitutionName`
  - `InstitutionAddress`
  - `InstitutionalDepartmentName`

- **Setup Information**
  - `PowerLineFrequency`
  - `Manufacturer`
  - `ManufacturersModelName`
  - `ManufacturersModelVersion`
  - `RecordingSetupName`
  - `SamplingFrequency`
  - `DeviceSerialNumber`
  - `SoftwareName`
  - `SoftwareVersions`
  - `RecordingDuration`
  - `RecordingType`
  - `EpochLength`

- **Processing Information**
  - `SoftwareFilters`
  - `HardwareFilters`

- **Pharmaceuticals**
  - `PharmaceuticalName`
  - `PharmaceuticalDoseAmount`
  - `PharmaceuticalDoseUnits`
  - `PharmaceuticalDoseRegimen`
  - `PharmaceuticalDoseTime`

- **Sample**
  - `BodyPart`
  - `BodyPartDetails`
  - `BodyPartDetailsOntology`
  - `SampleEnvironment`
  - `SampleEmbedding`
  - `SliceThickness`
  - `SampleExtractionProtocol`

- **Supplementary**
  - `SupplementarySignals`

- **Task Information**
  - `TaskName`
  - `TaskDescription`
  - `Instructions`
  - `CogAtlasID`
  - `CogPOID`

- **Coordinate System**
  - `MicroephysCoordinateUnits`

(behav-metadata)=
### `behav`

See the
[BIDS Behavioural Experiments Specification](https://bids-specification.readthedocs.io/en/stable/modality-specific-files/behavioral-experiments.html).
for detailed descriptions.

Suggested keys:

**Institution Information**
- `InstitutionName`
- `InstitutionAddress`
- `InstitutionalDepartmentName`
**Task Information**
- `TaskName`
- `Instructions`
- `TaskDescription`
- `CogAtlasID`
- `CogPOID`

(anat-metadata)=
### `anat`

We use the BIDS microscopy metadata fields as a starting point.

See the full specification for detailed descriptions:
[BIDS Microscopy Specification](https://bids-specification.readthedocs.io/en/stable/modality-specific-files/microscopy.html).

Suggested keys:

- **Image Acquisition**
  - `PixelSize`
  - `PixelSizeUnits`
  - `Immersion`
  - `NumericalAperture`
  - `Magnification`
  - `ImageAcquisitionProtocol`
  - `OtherAcquisitionParameters`

- **Sample**
  - `BodyPart`
  - `BodyPartDetails`
  - `BodyPartDetailsOntology`
  - `SampleEnvironment`
  - `SampleEmbedding`
  - `SampleFixation`
  - `SampleStaining`
  - `SamplePrimaryAntibody`
  - `SampleSecondaryAntibody`
  - `SliceThickness`
  - `TissueDeformationScaling`
  - `SampleExtractionProtocol`
  - `SampleExtractionInstitution`

- **Chunk Transformations**
  - `ChunkTransformationMatrix`
  - `ChunkTransformationMatrixAxis`

- **Hardware Information**
  - `Manufacturer`
  - `ManufacturersModelName`
  - `DeviceSerialNumber`
  - `StationName`
  - `SoftwareVersions`

- **Institution Information**
  - `InstitutionName`
  - `InstitutionAddress`
  - `InstitutionalDepartmentName`
