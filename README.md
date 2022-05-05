# Kode Cloud Linux Basics: Package Management

[KodeKloud Linux Basics Course Notes Table of Contents](https://github.com/pslucas0212/LinuxBasics)

## Linux Package Management
- Debian including Debian, Ubuntu, Minut Linux, etc use DPKG and APT use DPKG for Package management are Debian distributions
- Redhat/Fedora and RHEL derived Linux distos use RPM for package management and are known as an RPM distribution       

.deb -> debian package manager
.rpm -> Red Hat package manager

Package - A package is a compressed archive that is a set of all code packages for a Linux distribution which includes the software binaries, configuration files and meta-data to run software (or an application.

Each Linux distribution may run different tools, kernel and libraries and have different dependencies.  Each package includes a manifest.  And each package dependcy may package dependcies of its own.

Manifest of a package describe the list of dependencies and minimal versions of supporting package/softare that is required to install softare

Package manager is r
- Software in a linux system that provides a consistent and automated process for installing, configuring, upgrading and removeing packages from the OS 
- insure integreity and authenticy of the padkage by verifying digital certificates and checksums
- Simplfy package management proces - Provide querying options for installation, cofnfiguration and update
- Group packages
- Manageing dependcies for all packages installed

Types of package manageer
- DPKG - base package manager for debian
- APT - new version that frontends DPKG
- APT-GET - traditional frontend for DKPG systems
- RPM - Base package manage for Red Hat Linux distros
- Yum - front end for the RPM system found in RPM Systems
- DNF - new more feature reich front end for RPM

#### Working withRPM and YUM

RPM - Stands for Red Hat Package Manager
- Used with CentOS, Fedora, Redhat Enterprise Linux (Alma and Rocky)
- most common extension - .rpm 

RPM has five modes: Installation, Uninstall, Upgrade, Quer, Verifying
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
- query.  RPM database stores information about all RPM packages installed on the system.  Stored in the /var/lib/rpm directory and keeps track of installed packages and their history on your system
```
$ fpm -q telnet.rpm
```
- verify - verify compares installed packages with original packages
```
$ rpm -VF
```
- RPM does not resolve dependecies on its own.  

YUM - YellowDog Update Modifier - free open source base package manager for RPM base linux systems
- Works on RPM base distros
- software repository - repository collection of packages and package dependcy manage /etc/yum.repos.d
- high level package manager - Under the hood Yum uses RPM under the covers
- Automaticatlly resolves dependencies and can install any RPM packages and dependecies which RPM does not

Repoistory information is stored under /etc/yum.repos.d
For Red Hat -> /etc/yum.repos.d/redhat.repo
You may need to create your on repo file /etc/yum.repos.d/nginx.rpm

YUM depends on software repositories which act like a whares with hundres to thousands of packages.  These can be installed locally or accessed remotely.  Information about repository is stored in a files under /etc/yum.repos.d   
For Redhat OS you would find a file /etc/yum.repos.d/redhat.repo this repository file points to the Red hat Repos.   
You can add additional repos in the /etc/yum.repos.d if you need newer versions of the code.    

Yum sequence of installation
1. Yum first runs a transcation check.  If not installed in system checks for availabliity of installation package and it checks to see if any of the dependcies are already installed on the system.
2. It displays a transcation summary and prompts the user to continuer or stop
3. It then downloads packages to install on the system


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
To find where a particular app is located
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

#### DPKG and APT

Debian distros PureOS, Ubuntu
Debian Package Manager - DPKG - low lever package manager like RPM

- Installation/upgrade  - $ dpkg -i telnet.deb
- uninstalling -  $ dpkg -r telnet.deb
- List -  $ dpkg -l telnet
- Status - $ dpkg -s telnet
- Verifying -  $ dpkg -p <path to file>
  
 DPKG does not support depencies and we use APT and APT-GET
 
  APT - Advanced Pagkacge Manager
  
  APT - acts as a front end manager depending on DPKG and software repositories.  Repos list are found in /etc/apt/sources.list
  
  APT commands
  Refresh repo
  ```
  $ apt update
  ```
  Upgrade
  ```
  $ apt udpate
  ```
  Add repos
  ```
  $ apt edit-sources
  ```
  Install package
  ```
  $ apt install telnet
  ```
  Uninstall package
  ```
  $ apt remove telnet
  ```
  List 
  ```
  $ apt search telent
  ```
  
  #### APT vs APT-GET
  APT is more user frienldy then apt-get
  
  Installation output is easier to read
  
  Eassier to search
  ```
  $ apt search telnet
  ```
