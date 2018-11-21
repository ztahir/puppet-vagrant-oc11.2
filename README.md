## Oracle Commerce VM + Managed Environments - Vagrant + Puppet

## Supported Environments

- MacOSX
- Windows

## Dependencies

- biemond/orawls = 1.0.41
- biemond/orautils = 0.3.1
- adrien/filemapper = 1.1.3
- reidmv/yamlfile = 0.2.0
- fiddyspence/sleep = 1.2.0
- puppetlabs/stdlib = 4.4.0
- hajee/easy_type = 0.13.3
- hajee/oracle  = 0.5.0

## Pre-requisites

- A machine with atleast 16 GB RAM, as the VM would need atleast 8 GB allocated.
- The VM is designed to expand dynamically upto 60 GB - so its better to have atleast 75 GB of free space on your host machine

## Features

- Build an Oracle Commerce 11.2 Oracle Linux 6.6 based VM from Ground up using Vagrant + Puppet Modules/Manifests. 
- The same puppet configs can be used to configure and manage your managed environments - Dev/Test/Acceptance/Production
- Puppet Manifests for installing the following are packed in this project - JDK, Gradle, ATG, Endeca, Weblogic, Oracle XE, SQLDeveloper, Eclipse 
- Puppet hiera configs available for 
  - Creating 4 database schemas on Oracle XE - atg_core, atg_ca, atg_cata and atg_catb
  - Installing and Configuring Weblogic AdminServer and NodeManager
  - Creating 2 managed weblogic nodes - Storefront (Live/Production) and Management (CA/BCC)
  - Configuring Datasources and targeting them to servers - ATGCoreDS, ATGCataDS, ATGCatbDS, ATGCaDS

## Needed Software Installables

- Software installables to be made available in the /Software mount point - folder corresponding to /Users/Naga/Downloads/Commerce11.2  in the host machine (refer to **vagrant_config.tmp.yaml**)

| # | Software Name | Installable |
| --- | :----------- | :---------- |
| 1 | JDK | jdk-8u65-linux-x64.gz |
| 2 | Gradle | gradle-2.14.1-all.zip |
| 3 | ATG 11.2 | V78217-01.zip |
| 4 | Endeca CAS 11.2 | V78204-01.zip |
| 5 | Endeca Tools & Frameworks 11.2 | V78229-01.zip |
| 6 | Endeca MDEX 6.5.2 | V78211-01.zip |
| 7 | Endeca Platform Service 11.2 | V78226-01.zip |
| 8 | Eclipse Mars | eclipse-jee-mars-2-linux-gtk-x86_64.tar.gz |
| 9 | Oracle XE 11gR2 | oracle-xe-11.2.0-1.0.x86_64.rpm.zip |
| 10 | SQL Developer 4.0.3.16| sqldeveloper-4.1.3.20.78-1.noarch.rpm |
| 11 | Oracle Weblogic 12c | wls_121300.jar |
| 12 | Oracle JDBC Driver | ojdbc6.jar |
| 13 | ATG DAS Protocol.jar | protocol.jar |

## Steps to set up and kickstart the Virtual Machine

- Download and install Oracle VirtualBox (latest version should be fine)
- Download and install Vagrant (latest version should be fine)
- Download all the necessary software (To Be Installed - see table above) and place it in a folder in your host machine. 
- Download the base box (an Oracle Enterprise Linux 6.6 OS) for Vagrant manually from [here](https://www.dropbox.com/s/f5jk8tym60efisp/oel66.box?dl=0)(if not done already) and add it to vagrant boxes list using the following command
```
vagrant box add --name <<name>> <<path to the box file>>
```
- Make a copy of the [vagrant_config.tmp.yaml ](./vagrant_config.tmp.yaml) to create a vagrant_config.yaml ( This file is not checkedin to avoid merge issues - the tmp is only a reference file, the Vagrant config is looking for a file named vagrant_config.yaml ) and edit it according to your setup / needs
- Start the VM by running the following command from Terminal or Command prompt, this will try and import the base box and run provision to install the software needed - You can decide and update what to install by updating the classes section in [common.yaml](./hieradata/nodes/local/common.yaml)
```
vagrant up
```

## Whats in the box ?

- The vagrant box (oel66.box) comes with git and puppet preinstalled.
- Its configured to have a disk that cab expan upto 60GB, which should be sufficient for most of the development purposes.

## Planned for future

- Support for JBoss EAP
- Installing Commerce Reference Store 11.2
- Installing Commerce Store Accelerator 11.2

## References / Appendix

- Want to know more about **Vagrant**? Please read about vagrant [here](https://www.vagrantup.com/)
- Want to know more about **Puppet**, Please read about what puppet has to offer [here](https://puppetlabs.com/)
- Want to know more about **VirtualBox**, Please read the documentation [here](https://www.virtualbox.org/)

## Issues / Feedback

- Please feel free to raise any issues that you find [here](https://github.com/nagaseshadri/puppet-vagrant-oc11.2/issues/new), I will try and look at it ASAP
- Please provide your valuable feedback / improvements by writing to me at the email provided above, you can also write me if you need help with setting up your managed environment using the same configs, I am happy to help wherever needed.
