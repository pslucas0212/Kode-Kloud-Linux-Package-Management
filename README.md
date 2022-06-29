# Kode Cloud Linux Basics: Package Management

[KodeKloud Linux Basics Course Notes Table of Contents](https://github.com/pslucas0212/LinuxBasics)

Hunders of Linux distributions available.  One way to categorize Linux OSes is by the package manager they use.  

## Linux Package Management
- Debian including Debian, Ubuntu, Minut Linux, etc use DPKG and APT use DPKG for Package management are Debian distributions
- Redhat/Fedora/CentOS/AlmaLinux/Rocky/OEL and RHEL derived Linux distos use RPM and Yum for package management and are known as an RPM distribution       

.deb -> debian package manager  
.rpm -> Red Hat package manager

Package - A package is a compressed archive that is a set of all code packages for a Linux distribution which includes the software binaries, configuration files and meta-data to run the Operating system and software (or an applications).

Each Linux distribution may run different tools, kernel and libraries and have different dependencies.  Each Linux OS may run differently.  Each package includes a manifest which lists the correct pakage and those package dependencies to need to run that particular Linux OS.  And each package dependcy may package dependcies of its own.

Manifest of a package describe the list of dependencies and minimal versions of supporting package/softare that is required to install softare

Package manager is:
- Software in a linux system that provides a consistent and automated process for installing, configuring, upgrading and removeing packages from the OS 
- insure integreity and authenticy of the padkage by verifying digital certificates and checksums.  To make sure the package is download from a trusted sourced and is safe to install
- Simplfy package management proces - Provide querying options for installation, cofnfiguration and updates
- Group packages by function
- Manageing dependcies for all packages installed have all the packages needed to run a particular packages

Types of package manageer for Linux systems
- DPKG - base package manager for debian
- APT - new version that frontends DPKG for debian - Ubuntu, Mint, etc.
- APT-GET - traditional frontend for DKPG systems
- RPM - Base package manage for Red Hat Linux distros
- Yum - front end for the RPM system found in Red Hat distor Systems
- DNF - new more feature rich front end for RPM

###  Working with RPM and YUM

RPM - Stands for Red Hat Package Manager
- Used with CentOS, Fedora, Red Hat Enterprise Linux (Alma and Rocky)
- most common extension - .rpm 

RPM has five basic modes of operation: Installation, Uninstall, Upgrade, Query, Verifying

- installation: -i install, -v verbose pritnting details output of command
```
$ rpm -ivh telnet.rpm
```
- uninstalling -e uninstall
```
$ rpm -e telnet.rpm
```
- upgrade -U for Upgrade
```
$ rpm -Uvh telnet.rpm 
```
- RPM database stores information about all RPM packages installed on the system.  Stored in the /var/lib/rpm directory and keeps track of installed packages and their history on your system
- query database to get information about the installed package.  
```
$ fpm -q telnet.rpm
```
- verify - verify compares information from installed packages with the original packages.  Good to make sure the package is installed from a trusted source
```
$ rpm -VF
```
- RPM does not resolve dependecies on its own.  That's why we use YUM

YUM - YellowDog Update Modifier - free open source base package manager for RPM base linux systems
- Works on RPM base distros
- software repository - repository collection of packages and provides package dependcy management /etc/yum.repos.d. Repositories have a .repos extension
- high level package manager - Under the hood Yum uses RPM under the covers
- Automaticatlly resolves dependencies and can install any RPM packages and dependecies which RPM does not

Repoistory information is stored under /etc/yum.repos.d
For Red Hat -> /etc/yum.repos.d/redhat.repo
You may need to create your on repo file /etc/yum.repos.d/nginx.rpm

YUM depends on software repositories which act as a wharehouse with hundres to thousands of packages.  These can be installed locally or accessed remotely accessed via ftp, http or https.  Information about repository is stored in a files under /etc/yum.repos.d   
Under the hood YUM uses RPM
For Redhat OS you would find a file /etc/yum.repos.d/redhat.repo this repository file points to the orricial Red hat Repos.   
You can add additional repos in the /etc/yum.repos.d if you need newer versions of the code.  In case you don't want to make use of the repo.  The official repo may not have the latest version of the repo you want to install or may not have the software that you would want to install.  

Yum sequence of installation
1. Yum first runs a transcation check.  If the package is not installed in the system, YUM checks for availabliity of installation package and it checks to see if any of the dependcies are already installed on the system or needs to be upgraded
2. Next YUM displays a transcation summary and prompts the user to continuer or stop.  Type Y to continue or add -y to the command
3. Next YUM downloads packages to install on the system


YUM install example. 
```
$ yum install httpd
$ yum -y install httpd
```
After checking repository for all code and packages, Yum displays a transcation log.  

Yum Commands
```
$ yum repolist

Not root, Subscription Management repositories not updated

This system is not registered with an entitlement server. You can use subscription-manager to register.

repo id                          repo name
rhel-8-for-x86_64-appstream-rpms Red Hat Enterprise Linux 8 for x86_64 - AppStream (RPMs)
rhel-8-for-x8
```

To find where a particular app is located and the package
```
$ yum provides scp
```
To remove package run:
```
$ yum remove httpd
```
To update a single package, include the package name
```
$ yum update telnet
```
Update all packages
```
$ yum update
```
See YUM man page for the complete list of YUM commands.   


### YUM Lab
- Use an rpm command and find out the exact package name for wget installed in this server
```
rpm -q wget
wget-1.14-18.el7_6.1.x86_64
```
- The package for firefox browser has been downloaded under /home/bob
```
$ rpm -ivh firefox-68.6.0-1.el7.centos.x86_64.rpm 
error: Failed dependencies:
        liberation-fonts-common is needed by firefox-68.6.0-1.el7.centos.x86_64
        liberation-sans-fonts is needed by firefox-68.6.0-1.el7.centos.x86_64
...
$ 
```
This installed failed due to missing dependencies.  
- Install firefox with YUM
```
$ sudo yum install firefox-68.6.0-1.el7.centos.x86_64.rpm 
[sudo] password for bob: 
Loaded plugins: fastestmirror, ovl
Examining firefox-68.6.0-1.el7.centos.x86_64.rpm: firefox-68.6.0-1.el7.centos.x86_64
Marking firefox-68.6.0-1.el7.centos.x86_64.rpm to be installed
Resolving Dependencies
...
Transaction Summary
=======================================================================================================================================
Install  1 Package  (+88 Dependent packages)
Upgrade             (  7 Dependent packages)

Total size: 268 M
Total download size: 38 M
Is this ok [y/d/N]: 
...
Dependency Updated:
  nspr.x86_64 0:4.32.0-1.el7_9                     nss.x86_64 0:3.67.0-4.el7_9               nss-softokn.x86_64 0:3.67.0-3.el7_9      
  nss-softokn-freebl.x86_64 0:3.67.0-3.el7_9       nss-sysinit.x86_64 0:3.67.0-4.el7_9       nss-tools.x86_64 0:3.67.0-4.el7_9        
  nss-util.x86_64 0:3.67.0-1.el7_9                

Complete!
```
- How may software repositories are configured for YUM in this system
```
$ sudo yum reploist
Loaded plugins: fastestmirror, ovl
No such command: reploist. Please use /bin/yum --help
[bob@centos-lab ~]$ sudo yum repolist
Loaded plugins: fastestmirror, ovl
Loading mirror speeds from cached hostfile
 * base: mirror.pit.teraswitch.com
 * extras: mirror.umd.edu
 * updates: mirrors.lug.mtu.edu
repo id                                                        repo name                                                         status
base/7/x86_64                                                  CentOS-7 - Base                                                   10,072
extras/7/x86_64                                                CentOS-7 - Extras                                                    512
updates/7/x86_64                                               CentOS-7 - Updates                                                 3,891
repolist: 14,475
```
- Which package provides tcpdump? 
```
$ sudo yum reploist
Loaded plugins: fastestmirror, ovl
No such command: reploist. Please use /bin/yum --help
[bob@centos-lab ~]$ sudo yum repolist
Loaded plugins: fastestmirror, ovl
Loading mirror speeds from cached hostfile
 * base: mirror.pit.teraswitch.com
 * extras: mirror.umd.edu
 * updates: mirrors.lug.mtu.edu
repo id                                                        repo name                                                         status
base/7/x86_64                                                  CentOS-7 - Base                                                   10,072
extras/7/x86_64                                                CentOS-7 - Extras                                                    512
updates/7/x86_64                                               CentOS-7 - Updates                                                 3,891
repolist: 14,475
[bob@centos-lab ~]$ sudo yum provides tcpdump
Loaded plugins: fastestmirror, ovl
Loading mirror speeds from cached hostfile
 * base: mirror.pit.teraswitch.com
 * extras: mirror.umd.edu
 * updates: mirrors.lug.mtu.edu
14:tcpdump-4.9.2-4.el7_7.1.x86_64 : A network traffic monitoring tool
Repo        : base
```


### DPKG and APT

Debian distros PureOS, Ubuntu, Linux mint, etc.
Debian Package Manager - DPKG - low leve package manager like RPM.  It can be used to install, update, list, status and verify 


- Installation/upgrade  - $ dpkg -i telnet.deb
- uninstalling -  $ dpkg -r telnet.deb
- List -  $ dpkg -l telnet
- Status - check for installation - $ dpkg -s telnet
- Verifying -  $ dpkg -p <path to file>
  
 DPKG does not support package dependencies.  That's why we use higer level managers like APT and APT-GET.  APT and APT-GET do do not depend on each other
 
  APT - Advanced Pagkacge Manager
  
  APT acts as a front end manager depends on the DKPG utility.  DPKG package Repos list are found in /etc/apt/sources.list. Repos can be on disk or remote
  
  APT commands
  Refresh the repositories and downloads a list of all packages
  ```
  $ apt update
  ```
  Upgrade
  ```
  $ apt upgread
  ```
  Add repos opens /etc/apt/sources.list in vi for manual udpate.
  ```
  $ apt edit-sources
  ```
  Install package
  ```
  $ apt install telnet
  ```
  Remove package
  ```
  $ apt remove telnet
  ```
  Search 
  ```
  $ apt search telent
  ```
  List all available packages
  ```
  $ apt list
  ```
  
  #### APT vs APT-GET
  APT is more user frienldy then apt-get.  All the latest debian distros include APT
  
  Installation output is easier to read with just enough information.  APT-GET does not provide as user friendly outptu
  
  Eassier to search
  ```
  $ apt search telnet
  ```
 Cannot search for a package with atp-get.  You must use apt-cachce search and it the results are less useful. 
