# How to contribute to this website

## Website structure
The website is structured in sections, each one corresponding to a different experimental __modality__, and sub-sections, each corresponding to a different `tool`.

Examples of `tools` that belong in each __modality:__
* __Behaviour:__ `SLEAP`, `DeepLabCut`
* __Electrophysiology:__  `Kilosort`, `Phy`, `SpikeInterface`
* __Imaging:__ `Suite2p`, `CaImAn`
* __Histology:__ `AllenSDK`, `brainreg`, `cellfinder`
* __Programming:__ `Spyder`, `Jupyter`, `VSCode`, `Shell`
  
Each __modality__ is represented by a homonymous markdown file, e.g. `docs/source/Behaviour.md`.
* The H1 heading of each markdown file is the title of the section
* The H2 headings are `tool`-specific sub-sections.
* The H3 headings should provide a succinct description of an issue with a particular `tool`
* The text below the corresponding H3 headings should elaborate on the issue and provide a solution.

A dummy example is given below:
```md
# Behaviour

## SLEAP

### SLEAP is slow on Sundays
On Sundays you should be pre-occupied with sleeping, **NOT** SLEAPing.
```
  
## Editing the website
* Clone the GitHub repository, and create your `new_branch`.
* Edit the website and commit your changes to the `new_branch`.
* Push the `new_branch` to GitHub and create a pull request. This will automatically trigger a [GitHub Action](https://github.com/ammaraskar/sphinx-action) that checks if the website still builds correctly.
* If the checks pass, assign someone to review your changes. 
* When the reviewer merges your changes into the `main` branch, a different [GitHub Action](https://github.com/peaceiris/actions-gh-pages) will be triggered, which will build the website and publish it to the `gh-pages` branch.
* The website should be available at [troubleshooting.neuroinformatics.dev](https://troubleshooting.neuroinformatics.dev)

> **_TIP:_**
> 
> If you wish to view the website locally, before you push it, you can do so by running the following commands from the root of the repository:
> 
> `pip install -r docs/requirements.txt`
> 
> `sphinx-build docs/source docs/build`
> 
> You can view the local build at `docs/build/index.html`