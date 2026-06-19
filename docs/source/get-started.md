# Get Started

(some introduction)

## Tools

(datashuttle-section)=
### datashuttle

Getting started with NeuroBlueprint, we have introduced a very nice tool called datashuttle. Datashuttle provides a
graphical user interface or Python API to create, validate and transfer NeuroBlueprint-organised folders.

datashuttle makes getting started with NB folder structure very easy - check out the installation and get
started and you can quickly create a new project through the GUI:

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

(some more stuff on transfer)

### Community tools

Other community members have developed tools, for example checkout
[NeuroBlueprint-metadata](https://github.com/barnabasberes/NeuroBlueprint-metadata) that helps set up
metadata files to implement the NeuroBlueprint specification.

Bonsai -> NB converter? Just following up

## Examples

## Validating projects are in NeuroBLueprint style for a labs repository

datashuttle helps validate NeuroBlueprint folder structures automatically through a
Python API. Users are using regular scripts to run weekly validation of all
projects in the lab, to ensure they are maintained in NeuroBlueprint format.
Check out the code [here](https://datashuttle.neuroinformatics.dev/latest/pages/examples/lab-project-checker.html).

## Searching a repository of NB-formatted projects

When all your projects a neuroblueprint-formatted, it becomes easy to search
across projects for keywords or abstract.

This script searches a list of folders, lodas the metadata and matches
keywords to user-defined search. It uses the [rapidfuzz](https://rapidfuzz.github.io/RapidFuzz/Installation.html)
library that matches words that are close:

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
