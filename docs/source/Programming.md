# Programming

## Ubuntu

### Distro update error
This is an error that appeared when updating to a new Ubuntu distribution.
Error msg: Software Updater - Not all updates can be installed.   
Solution: `sudo apt-get dist-upgrade`

### Terminal is not opening after installing a new Python version
If you installed a new Python version without the use of `conda`, there might be a mismatch in the python naming in a bin file.   
If it's possible open terminal through vscode or open a virtual terminal (VT) with CTRL + ALT + F3 and run `gnome-ternimal`.
Does it throw a Python error? If yes run `sudo nano /usr/bin/gnome-terminal` and change `#!/usr/bin/python3` to `#!/usr/bin/python3.10` if the version you're currently using is 3.10.  
Exit the VT via CTRL + ALT + F2.

## VSCode
### SSH into an unmanaged machine from remote
> **_Example Usecase:_**  When working from home, connect from you local Mac to the SWC office Linux machine

In your local machine `cd` and ` open .ssh/config` and append the following configurations:
```
Host *
    ServerAliveInterval 60

Host jump-host
    User swcUserID
    HostName ssh.swc.ucl.ac.uk

Host remote-host
    User remoteMachineUsername
    HostName 172.24.243.000
    ProxyCommand ssh -W %h:%p jump-host
```
Make sure to replace `172.24.243.000` with the IP address of your remote machine.
On Ubuntu, you can find the IP address in this way:
* Got to `Settings` then `Network`
* Click on the cogwheel next to your connections (usually `Wired`)
* The `IPv4` is the address you are looking for

If you do not have a config file in your .ssh folder, create one:
```bash
cd .ssh/
touch config
```
Connect to VPN, then use the `Open a remote window` (Remote - SSH extension) tool of vscode and connect to `remote-host`. You will be asked for your SWC and Linux passwords. 