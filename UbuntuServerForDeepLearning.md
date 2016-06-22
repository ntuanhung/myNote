This note describes how to install Ubuntu Server OS for Deep Learning with CUDA-cuDNN-theano framework.

I. Prerequisition 
  i.    Ubuntu Server 14.04 64bit
    + System Requirements
      Ubuntu 16.04 LTS Server Edition supports three (3) major architectures: Intel x86, AMD64 and ARM. The table below lists recommended hardware specifications. Depending on your needs, you might manage with less than this. However, most users risk being frustrated if they ignore these suggestions.
      Recommended Minimum Requirements
        Install Type    CPU    RAM         Hard Drive Space 
                                      Base System  All Tasks Installed

      Server (Standard) 1 gigahertz 512 megabytes 1 gigabyte 1.75 gigabytes
      Server (Minimal)  300 megahertz  192 megabytes  700 megabytes 1.4 gigabytes
    
      The Server Edition provides a common base for all sorts of server applications. It is a minimalist design providing a platform for the desired services, such as file/print services, web hosting, email hosting, etc.
    + Server and Desktop Differences
      There are a few differences between the Ubuntu Server Edition and the Ubuntu Desktop Edition. It should be noted that both editions use the same apt repositories, making it just as easy to install a server application on the Desktop Edition as it is on the Server Edition.
      The differences between the two editions are the lack of an X window environment in the Server Edition and the installation process.
      - Kernel Differences:
        Ubuntu version 10.10 and prior, actually had different kernels for the server and desktop editions. Ubuntu no longer has separate -server and -generic kernel flavors. These have been merged into a single -generic kernel flavor to help reduce the maintenance burden over the life of the release.

        When running a 64-bit version of Ubuntu on 64-bit processors you are not limited by memory addressing space.
        
        To see all kernel configuration options you can look through /boot/config-4.4.0-server. Also, Linux Kernel in a Nutshell is a great resource on the options available.
    + Backing Up
    Before installing Ubuntu Server Edition you should make sure all data on the system is backed up. See Backups for backup options.
    If this is not the first time an operating system has been installed on your computer, it is likely you will need to re-partition your disk to make room for Ubuntu.
    Any time you partition your disk, you should be prepared to lose everything on the disk should you make a mistake or something goes wrong during partitioning. The programs used in installation are quite reliable, most have seen years of use, but they also perform destructive actions.
    
  ii.   CUDA Toolkit SDK 8.0RC
  iii.  cuDNN v5 for 8.0RC
  iv.   Theano framework

II. Install Ubuntu Server LTS 14.04 64-bit
  + Download Ubuntu Server 14.04 64-bit .iso file from [http://releases.ubuntu.com/14.04/ubuntu-14.04.4-server-amd64.iso]
  + Burn .iso file into CD/DVD or USB
  + If you want to install Ubuntu side by side Windows
    - Log in to Windows
    - Go to Computer Management (Right click to "My Computer" -> select "Manage")
    - Select Disk Management
    - Select a physic disk and make an empty part (may use Shrink Volume...) from current disk (at least 10GB)
    - Remember this free disk size (VERY IMPORTANT)
  + Put DVD or plug USB into computer and restart
  + At the boot prompt you will be asked to select the language. 
  + From the main boot menu there are some additional options to install Ubuntu Server Edition. 
  You can install a basic Ubuntu Server, check the CD-ROM for defects, check the system's RAM, boot from first hard disk, or rescue a broken system. 
  The rest of this section will cover the basic Ubuntu Server install.
  + The installer asks which language it should use. Afterwards, you are asked to select your location.
  + Next, the installation process begins by asking for your keyboard layout. You can ask the installer to attempt auto-detecting it, or you can select it manually from a list.
  + The installer then discovers your hardware configuration, and configures the network settings using DHCP. If you do not wish to use DHCP at the next screen choose "Go Back", and you have the option to "Configure the network manually".
  + Next, the installer asks for the system's hostname.
  + A new user is set up; this user will have root access through the sudo utility.
  + After the user settings have been completed, you will be asked if you want to encrypt your home directory.
  + Next, the installer asks for the system's Time Zone.
  + You can then choose from several options to configure the hard drive layout. Afterwards you are asked which disk to install to. You may get confirmation prompts before rewriting the partition table or setting up LVM depending on disk layout. If you choose LVM, you will be asked for the size of the root logical volume. For advanced disk options see Advanced Installation.
  + The Ubuntu base system is then installed.
  + The next step in the installation process is to decide how you want to update the system. There are three options:
    - No automatic updates: this requires an administrator to log into the machine and manually install updates.
    - Install security updates automatically: this will install the unattended-upgrades package, which will install security updates without the intervention of an administrator. For more details see Automatic Updates.
    - Manage the system with Landscape: Landscape is a paid service provided by Canonical to help manage your Ubuntu machines. See the Landscape site for details.
  + You now have the option to install, or not install, several package tasks. See Package Tasks for details. Also, there is an option to launch aptitude to choose specific packages to install. For more information see Aptitude.
  + Finally, the last step before rebooting is to set the clock to UTC.


During the Server Edition installation you have the option of installing additional packages from the CD. The packages are grouped by the type of service they provide.
  + DNS server: Selects the BIND DNS server and its documentation.
  + LAMP server: Selects a ready-made Linux/Apache/MySQL/PHP server.
  + Mail server: This task selects a variety of packages useful for a general purpose mail server system.
  + OpenSSH server: Selects packages needed for an OpenSSH server.
  + PostgreSQL database: This task selects client and server packages for the PostgreSQL database.
  + Print server: This task sets up your system to be a print server.
  + Samba File server: This task sets up your system to be a Samba file server, which is especially suitable in networks with both Windows and Linux systems.
  + Tomcat Java server: Installs Apache Tomcat and needed dependencies.
  + Virtual Machine host: Includes packages needed to run KVM virtual machines.
  + Manually select packages: Executes aptitude allowing you to individually select packages.
Installing the package groups is accomplished using the tasksel utility. One of the important differences between Ubuntu (or Debian) and other GNU/Linux distribution is that, when installed, a package is also configured to reasonable defaults, eventually prompting you for additional required information. Likewise, when installing a task, the packages are not only installed, but also configured to provided a fully integrated service.
Once the installation process has finished you can view a list of available tasks by entering the following from a terminal prompt:

tasksel --list-tasks

The output will list tasks from other Ubuntu based distributions such as Kubuntu and Edubuntu. Note that you can also invoke the tasksel command by itself, which will bring up a menu of the different tasks available.
You can view a list of which packages are installed with each task using the --task-packages option. For example, to list the packages installed with the DNS Server task enter the following:

tasksel --task-packages dns-server

The output of the command should list:

bind9-doc 
bind9utils 
bind9

If you did not install one of the tasks during the installation process, but for example you decide to make your new LAMP server a DNS server as well, simply insert the installation CD and from a terminal:

sudo tasksel install dns-server



The recommended way to upgrade a Server Edition installation is to use the do-release-upgrade utility. Part of the update-manager-core package, it does not have any graphical dependencies and is installed by default.
Debian based systems can also be upgraded by using apt dist-upgrade. However, using do-release-upgrade is recommended because it has the ability to handle system configuration changes sometimes needed between releases.
To upgrade to a newer release, from a terminal prompt enter:

do-release-upgrade

It is also possible to use do-release-upgrade to upgrade to a development version of Ubuntu. To accomplish this use the -d switch:

do-release-upgrade -d

Upgrading to a development release is not recommended for production environments.
For further stability of a LTS release there is a slight change in behaviour if you are currently running a LTS version. LTS systems are only automatically considered for an upgrade to the next LTS via do-release-upgrade with the first point release. So for example 14.04 will only upgrade once 16.04.1 is released. If you want to update before, e.g. on a subset of machines to evaluate the LTS upgrade for your setup the same argument as an upgrade to a dev release has to be used via the -d switch.
