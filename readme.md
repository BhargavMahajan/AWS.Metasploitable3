# Metasploitable3

[![Build Status](https://travis-ci.org/jocic/AWS.Metasploitable3.svg?branch=master)](https://travis-ci.org/jocic/AWS.Metasploitable3) [![Coverage Status](https://coveralls.io/repos/github/jocic/AWS.Metasploitable3/badge.svg?branch=master)](https://coveralls.io/github/jocic/AWS.Metasploitable3?branch=master) [![Codacy Badge](https://api.codacy.com/project/badge/Grade/23fa45c3ca674a449331462fc24a435a)](https://www.codacy.com/app/jocic/AWS.Metasploitable3?utm_source=github.com&amp;utm_medium=referral&amp;utm_content=jocic/AWS.Metasploitable3&amp;utm_campaign=Badge_Grade)

Metasploitable3 is a VM that is built from the ground up with a large amount of security vulnerabilities. It is intended to be used as a target for testing exploits. This project is, as you can expect a fork of the original [Metasploitable3](https://github.com/rapid7/metasploitable3) and is intended solely for deploying Metasploitable on AWS.

Metasploitable3 is released under a BSD-style license. See COPYING for more details.

[![Buy Me Coffee](other/assets/buy-me-coffee.png)](https://www.paypal.me/DjordjeJocic)

**Song of the project:** [Grailknights - Pumping Iron Power](https://www.youtube.com/watch?v=qnzurkSGBCs)

## Versioning Scheme

I use a 3-digit [Semantic Versioning](https://semver.org/spec/v2.0.0.html) identifier, for example 1.0.2. These digits have the following meaning:

*   The first digit (1) specifies the MAJOR version number.
*   The second digit (0) specifies the MINOR version number.
*   The third digit (2) specifies the PATCH version number.

Complete documentation can be found by following the link above.

## Quick-start

To use the prebuilt images provided at https://app.vagrantup.com/rapid7/ create a new local metasploitable workspace:
```
mkdir metasploitable3-workspace
cd metasploitable3-workspace
curl -O https://raw.githubusercontent.com/rapid7/metasploitable3/master/Vagrantfile && vagrant up
```
Or clone this repository and build your own box.

## Building Metasploitable 3
System Requirements:
* OS capable of running all of the required applications listed below
* VT-x/AMD-V Supported Processor recommended
* 65 GB Available space on drive
* 4.5 GB RAM

Requirements:

* [Packer](https://www.packer.io/intro/getting-started/install.html)
* [Vagrant](https://www.vagrantup.com/docs/installation/)
* [Vagrant Reload Plugin](https://github.com/aidanns/vagrant-reload#installation)
* [VirtualBox](https://www.virtualbox.org/wiki/Downloads), libvirt/qemu-kvm, or vmware (paid license required)
* Internet connection

### To build automatically:

1. - On **Linux/OSX** run `./build.sh windows2008` to build the Windows box or `./build.sh ubuntu1404` to build the Linux box. If /tmp is small, use `TMPDIR=/var/tmp ./build.sh ...` to store temporary packer disk images under /var/tmp.
   - On **Windows**, open powershell terminal and run `.\build.ps1 windows2008` to build the Windows box or `.\build.ps1 ubuntu1404` to build the Linux box. If no option is passed to the script i.e. `.\build.ps1`, then both the boxes are built.
2. If both the boxes were successfully built, run `vagrant up` to start both. To start any one VM, you can use:
    - `vagrant up ub1404` : to start the Linux box
    - `vagrant up win2k8` : to start the Windows box
3. When this process completes, you should be able to open the VM within VirtualBox and login. The default credentials are U: `vagrant` and P: `vagrant`.

### To build manually:

1. Clone this repo and navigate to the main directory.
2. Build the base VM image by running `packer build --only=<provider> ./packer/templates/windows_2008_r2.json` where `<provider>` is your preferred virtualization platform. Currently `virtualbox-iso`, `qemu`, and `vmware-iso` providers are supported. This will take a while the first time you run it since it has to download the OS installation ISO.
3. After the base Vagrant box is created you need to add it to your Vagrant environment. This can be done with the command `vagrant box add packer/builds/windows_2008_r2_*_0.1.0.box --name=metasploitable3-win2k8`.
4. Use `vagrant plugin install vagrant-reload` to install the reload vagrant provisioner if you haven't already.
5. To start the VM, run the command `vagrant up win2k8`. This will start up the VM and run all of the installation and configuration scripts necessary to set everything up. This takes about 10 minutes.
6. Once this process completes, you can open up the VM within VirtualBox and login. The default credentials are U: vagrant and P: vagrant.

Videos:

Thanks to [Jeremy](https://twitter.com/webpwnized), you can also follow the steps in these videos to set up Metasploitable3:

https://www.youtube.com/playlist?list=PLZOToVAK85MpnjpcVtNMwmCxMZRFaY6mT

## Vulnerabilities
* [See the wiki page](https://github.com/rapid7/metasploitable3/wiki/Vulnerabilities)

## More Information
The wiki has a lot more detail and serves as the main source of documentation. Please [check it out](https://github.com/rapid7/metasploitable3/wiki/).

## Acknowledgements
The Windows portion of this project was based off of GitHub user [joefitzgerald's](https://github.com/joefitzgerald) [packer-windows](https://github.com/joefitzgerald/packer-windows) project.
The Packer templates, original Vagrantfile, and installation answer files were used as the base template and built upon for the needs of this project.

## Contribution

Please review the following documents if you are planning to contribute to the project:

*   [Contributor Covenant Code of Conduct](code-of-conduct.md)
*   [Contribution Guidelines](contributing.md)
*   [License](license.md)
