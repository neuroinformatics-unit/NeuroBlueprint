# NeuroBlueprint

<img src="_static/NeuroBlueprint_logo-light_no-text.png" alt="NeuroBlueprint logo" class="only-light img-responsive"/>
<img src="_static/NeuroBlueprint_logo-dark_no-text.png" alt="NeuroBlueprint logo" class="only-dark img-responsive"/>

**NeuroBlueprint** is a folder structure specification for (systems) neuroscience research projects. It is inspired by,
and based on the [BIDS specification](https://bids-specification.readthedocs.io/en/stable/), widely used in human neuroimaging.

The [NeuroBlueprint specification](specification.md) provides a set of rules and guidelines for project folder organisation,
ensuring consistent data management within and between labs. The focus is on ensuring minimal overhead for researchers.

**NeuroBlueprint** is being developed at the [Sainsbury Wellcome Centre (SWC) for Neural Circuits and Behaviour](https://www.sainsburywellcome.org/)
by members of the [Neuroinformatics Unit (NIU)](https://neuroinformatics.dev/). As such, it prioritizes interoperability with NIU-developed data analysis tools. That said, the specification is designed to be as general as possible, and
should be useful to anyone within the neuroscience field.

To facilitate **NeuroBlueprint**'s pain-free adoption we are also developing
[datashuttle](https://datashuttle.neuroinformatics.dev/)—a tool that integrates
into data acquisition workflows and automates the creation and transfer
of **NeuroBlueprint**-compliant folders.

We (the NIU) welcome feedback and contributions from the wider community and commit to maintaining the specification as a living and evolving document.
Check out the NeuroBlueprint [Zulip chat](https://neuroinformatics.zulipchat.com/#narrow/stream/406000-NeuroBlueprint) or
raise a [GitHub Issue](https://github.com/neuroinformatics-unit/NeuroBlueprint/issues) to get in touch.
We will also collaborate with [ongoing efforts](https://github.com/INCF/neuroscience-data-structure) by the [INCF](https://www.incf.org/)
and [BIDS community](https://bids.neuroimaging.io/) to extend the BIDS specification to non-human animal research.

```{toctree}
:maxdepth: 3
:caption: Contents

specification
community
```

