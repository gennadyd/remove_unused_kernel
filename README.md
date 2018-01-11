# remove_unused_kernel

**Configure Unattended Upgrades to Remove Unneeded Kernels Automatically**

Note: The following methods will only remove kernels that are marked as being automatically installed as described above. In Ubuntu 16.04 kernels installed by Software Updater are marked as being automatically installed. In Ubuntu 14.04 only kernels installed by unattended-upgrades are marked as being automatically installed. See bug #1439769 for details. 

Note: This way will not remove all automatically installed old kernel providing packages as fallback versions are kept; the list of kept kernels is maintained and automatically updated in the file /etc/apt/apt.conf.d/01autoremove-kernels as a list of matching regular expressions. The second step is to edit the configuration file /etc/apt/apt.conf.d/50unattended-upgrades to enable automatic removal. It's owned by root, so remember to use sudo!

Option for All Ubuntu Releases
The following setting configures unattended-upgrade to remove unused dependencies after an unattended upgrade.
Make sure /etc/apt/apt.conf.d/50unattended-upgrades contains line
```
Unattended-Upgrade::Remove-Unused-Dependencies "true";
```
and that it is not commented out. Comments start with '//' in this file.
Thereafter unattended-upgrades will remove automatically remove packages providing old kernels as part of unattended upgrade. (It does not purge them, however.) It also removes other unneeded packages, as well.

Option for Ubuntu 16.04 and newer
Unattended-upgrades version 0.90 supports a new configuration variable that makes it possible to automatically remove only packages that become excessive during a run of unattended-upgrades. It is enabled i.e. "true" by default, so make sure /etc/apt/apt.conf.d/50unattended-upgrades does not contain:
```
Unattended-Upgrade::Remove-New-Unused-Dependencies "false"
```
The way this is designed, it is important that you let unattended-upgrades handle installion of security updates. Otherwise unattended-uprades will not remove old kernels and you may have to do some manual removing of kernels.
