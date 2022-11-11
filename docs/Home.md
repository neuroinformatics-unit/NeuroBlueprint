# Overview
Welcome to the __Neuroinformatics Unit troubleshooting wiki__!
Here we will keep track of software issues and how to solve them. It could be problems that we encounter during our work, or questions that are frequently asked by other researchers. If you troubleshoot an issue for yourself or someone else, remember to document it here!

# Sections
Use the side-bar navigation menu to easily jump between sections
* [Imaging](Imaging): e.g. brainglobe, 2-photon calcium imaging
* [Electrophysiology](Electrophysiology): e.g. SpikeInterface, SpikeGLX, Phy
* [Behaviour](Behaviour): e.g. DeepLabCut, SLEAP
* [Programming](Programming): general issues with python, conda, etc.

# How to contribute
1. Clone the wiki `git clone https://github.com/neuroinformatics-unit/troubleshooting.wiki.git`
2. Make your edits, commit, and push them. You may create branches when working on wikis, but only changes pushed to the default branch will be made live and available to the readers.
3. Add your entries to the appropriate section file from above. The filename determines the title of the wiki page, and the file extension determines how your wiki content is rendered (for now markdown is used, but other formats are possible)
4. Create H2 headings for specific tools (e.g. `## SLEAP`), H3 headings for a category of issues with a specific tool (e.g. `### Installation issues`), and bullet points for individual issues (e.g. `* pip install fails for SLEAP on Windows 10`)