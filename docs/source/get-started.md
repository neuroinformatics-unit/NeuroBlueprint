# Get Started

Getting started with data standardisation can feel overwhelming at first.
Although the benefits of standardising data are significant, learning a new
folder structure takes time and can initially introduce friction.

This section introduces tools that automate data standardisation
with **NeuroBlueprint**, helping make it easier to create, manage, and work with standardised projects.

## Tools

(datashuttle-section)=
### datashuttle

datashuttle is a tool for automating the creation of **NeuroBlueprint** folder structures.
It also provides convenient features for transferring data between machines and validating **NeuroBlueprint** datasets.

datashuttle can be used through either a graphical user interface or a Python API.
The GUI makes it easy to get started with the **NeuroBlueprint** folder structure and quickly create a new project.
I
```{image} /_static/datashuttle-demo-dark.gif
:class: only-dark
:alt: Datashuttle usage GIF
:align: center
:width: 700px
```
```{image} /_static/datashuttle-demo-light.gif
:class: only-light
:alt: Datashuttle usage GIF
:align: center
:width: 700px
```

### Community tools

Community members have also developed tools to support the **NeuroBlueprint** ecosystem,
aimed at simplifying managing standardised projected.


#### metadata manager

[**NeuroBlueprint**-metadata](https://github.com/barnabasberes/NeuroBlueprint-metadata)
is a command-line tool that helps create and manage metadata.yaml files for NeuroBlueprint projects.
It can generate template metadata files throughout a project hierarchy, providing placeholders for
project, subject, session, and datatype-level information. Metadata can then be added to these files
and conveniently inspected from the command line, including resolved metadata for a given session.

### Bonsai extension

Bonsai -> NB converter? Just following up

## Examples

## Validating projects are in NeuroBLueprint style for a labs repository

datashuttle can validate **NeuroBlueprint** folder structures automatically through its Python API.
For example, labs can run scheduled scripts to validate all projects on a weekly basis, helping ensure
that datasets remain organised according to the **NeuroBlueprint** specification.

Check out the code [here](https://datashuttle.neuroinformatics.dev/latest/pages/examples/lab-project-checker.html).

## Searching a repository of NB-formatted projects

When projects follow the **NeuroBlueprint** structure, it becomes easier to search across
datasets using project metadata, such as keywords or abstracts.

The example Python script below searches a collection of project folders, loads each project’s
metadata, and compares its keywords against a user-defined search term.
It uses the [RapidFuzz](https://rapidfuzz.github.io/RapidFuzz/Installation.html) library to
identify close matches between search terms and project keywords.


```python
from pathlib import Path
import yaml
from rapidfuzz import fuzz

SEARCH_KEYWORDS = "visual decision making"
path_to_projects = Path("/path/to_lab_projects")

matching_projects = []
for project_folder in path_to_projects.glob("*"):

    metadata_file = project_folder / "metadata.yaml"

    with open(metadata_file, "r") as f:
        metadata = yaml.safe_load(f) or {}

    project = metadata["project"]

    keywords = project["keywords"]
    format_keywords = " ".join([*keywords])

    score = fuzz.token_set_ratio(SEARCH_KEYWORDS, format_keywords)

    if score >= 80:
        matching_projects.append(project_folder)
```
