# Metasploitable3

Metasploitable3 is a VM that is built from the ground up with a large amount of security vulnerabilities. It is intended to be used as a target for testing exploits with [metasploit](https://github.com/rapid7/metasploit-framework).

Metasploitable3 is released under a BSD-style license. See COPYING for more details.

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
* [VirtualBox](https://www.virtualbox.org/wiki/Downloads)
* Internet connection

To build automatically:

1. On Linux/OSX run `./build.sh windows2008` to build the Windows box or `./build.sh ubuntu1404` to build the Linux box. On Windows, run `build_win2008.ps1` in a powershell terminal to build the Windows box.
2. If the command completes successfully, run `vagrant up`. On Windows, if the script failed try to build manually.
3. When this process completes, you should be able to open the VM within VirtualBox and login. The default credentials are U: `vagrant` and P: `vagrant`.

To build manually:

1. Clone this repo and navigate to the main directory.
2. Build the base VM image by running `packer build --only=<provider>-iso .\packer\templates\windows_2008_r2.json` where `<provider>` is your preferred virtualization platform. Currently `virtualbox` and `vmware` providers are supported. This will take a while the first time you run it since it has to download the OS installation ISO. Windows Defender might detect a virus, just allow the file(s) to stay- but try not to run it.
3. After the base Vagrant box is created you need to add it to your Vagrant environment. This can be done with the command `vagrant box add windows_2008_r2_<provider>.box --name=metasploitable3.` Note: the .box file might include a version number- go into the .\packer\builds directory and check the file name and input it where `windows_2008_r2_<provider>.box` is in the command
4. Use `vagrant plugin install vagrant-reload` to install the reload vagrant provisioner if you haven't already.
5. To start the VM, run the command `vagrant up`. This will start up the VM and run all of the installation and configuration scripts necessary to set everything up. This takes about 10 minutes.
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
