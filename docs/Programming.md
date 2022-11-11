# Programming
## Ubuntu
Here a list of problems I encountered in Linux and how I was able to fix them.

### Installations
#### Software update error
This is an error that appeared when updating to a new Ubuntu distribution.
Error msg: Software Updater - Not all updates can be installed.   
Solution: `sudo apt-get dist-upgrade`

#### Terminal is not opening after installing a new Python version
If you installed a new Python version without the use of conda, there might be a mismatch in the python naming in a bin file.   
If it's possible open terminal through vscode or use a virtual terminal (VT) with CTRL + ALT + F3 and run `gnome-ternimal`.
Does it throw a Python error? If yes run `sudo nano /usr/bin/gnome-terminal` and change `#!/usr/bin/python3` to `#!/usr/bin/python3.10` if the version you're currently using is 3.10.  
Exit the VT via CTRL + ALT + F2.