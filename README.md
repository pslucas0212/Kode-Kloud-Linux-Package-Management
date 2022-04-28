# Kode Cloud Linux Basics: Package Management

[KodeKloud Linux Basics Course Notes Table of Contents](https://github.com/pslucas0212/LinuxBasics)

## Linux Package Management
Debian/Ubuntu
- DPKG/APT
Redhat/Fedora
- RPM

.deb -> debian package manager
.rpm -> Red Hat package manager

Package - a compressed archive that is a set code packages (binaries, files and meta-data) to run software (or an application)

Manifest of a package describe the list of dependencies and minimal versions of supporting package/softare that is required to install softare

Package manage
- insure integreity and authenticy of the padkage
- Simplfy package management - installation, cofnfiguration
- Group packages
- 

Types of package manageer
- DPKG - debian
- APT - new version that frontends DPAK
- APT-GET
- RPM - Red Hat
- Yum - front end for RPM
- DNF - new front end for RPM

#### RPM and YUM

RPM - Red Hat Package Manager
- CentOS, Fedora, Redhat
- .rpm 

RPM has five modes
- installation - $ rpm -ivh telnet.rpm
- uninstalling - $ rpm -e telnet.rpm
- upgrade - $ rpm -Uvh telnet.rpm 
- query - $ fpm -q telnet.rpm
- verify - $ rpm -VF

YUM - YellowDog Update Manager
- Works on RPM base distors
- software repository
- high level package manager - uses RPM under the covers
- Automaticatlly resolves dependencies - which RPM does not

Repoistory information is stored under /etc/yum.repos.d
For Red Hat -> /etc/yum.repos.d/redhat.repo
You may need to create your on repo file /etc/yum.repos.d/nginx.rpm

YUM install example
```
$ yum install httpd
$ yum -y install httpd
```
After checking repository for all code and packages, Yum displays a transcation log.  

```
$ yum repolist
```
To find where a particular app is located
```
$ yum provides scp
```
To remove package run:
```
$ yum remove httpd
```
To update a package
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
