# Behaviour

## SLEAP

### Pip install fails for SLEAP on Windows 10
SLEAP lists several [installation methods](https://sleap.ai/develop/installation.html#installation-methods). People have reported problems with the `pip install` method on windows. The `conda` method - `conda create -y -n sleap -c sleap -c nvidia -c conda-forge sleap=1.2.8` - works well on Linux and Windows (as of October 2022). For ARM64 silicon Macs, follow the [M1-specific installation instructions](https://sleap.ai/develop/installation.html#m1-macs).
