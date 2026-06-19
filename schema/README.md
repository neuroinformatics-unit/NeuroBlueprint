# NeuroBlueprint Metadata Schema

This directory contains YAML schema definitions for NeuroBlueprint metadata files. The schemas describe the allowed top-level sections in a `metadata.yaml` file and the fields available within each section.

## Start here

Open `schema.yaml` first. It is the entry point for the schema and lists the valid top-level sections:

```yaml
sections:
  project: project.yaml
  sub: sub.yaml
  ses: ses.yaml
  ephys: ephys.yaml
  behav: behav.yaml
  anat: anat.yaml
```

Each key under `sections` is a top-level section that can appear in a `metadata.yaml` file. Each value points to the YAML file that defines the fields for that section.

See the metadata specification on the website for full details.
