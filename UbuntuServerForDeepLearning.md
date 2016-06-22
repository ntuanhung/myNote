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

$ tasksel --list-tasks

The output will list tasks from other Ubuntu based distributions such as Kubuntu and Edubuntu. Note that you can also invoke the tasksel command by itself, which will bring up a menu of the different tasks available.
You can view a list of which packages are installed with each task using the --task-packages option. For example, to list the packages installed with the DNS Server task enter the following:

$ tasksel --task-packages dns-server

The output of the command should list:

bind9-doc 
bind9utils 
bind9

If you did not install one of the tasks during the installation process, but for example you decide to make your new LAMP server a DNS server as well, simply insert the installation CD and from a terminal:

$ sudo tasksel install dns-server



The recommended way to upgrade a Server Edition installation is to use the do-release-upgrade utility. Part of the update-manager-core package, it does not have any graphical dependencies and is installed by default.
Debian based systems can also be upgraded by using apt dist-upgrade. However, using do-release-upgrade is recommended because it has the ability to handle system configuration changes sometimes needed between releases.
To upgrade to a newer release, from a terminal prompt enter:

$ do-release-upgrade

It is also possible to use do-release-upgrade to upgrade to a development version of Ubuntu. To accomplish this use the -d switch:

$ do-release-upgrade -d

Upgrading to a development release is not recommended for production environments.
For further stability of a LTS release there is a slight change in behaviour if you are currently running a LTS version. LTS systems are only automatically considered for an upgrade to the next LTS via do-release-upgrade with the first point release. So for example 14.04 will only upgrade once 16.04.1 is released. If you want to update before, e.g. on a subset of machines to evaluate the LTS upgrade for your setup the same argument as an upgrade to a dev release has to be used via the -d switch.

Some advanced installation
Please read these site for Software RAID, Logical Volume Manager (LVM), iSCSI [https://help.ubuntu.com/lts/serverguide/advanced-installation.html]
Ubuntu usage
  + Package management [https://help.ubuntu.com/lts/serverguide/package-management.html]
  + More .. [https://help.ubuntu.com/lts/serverguide/index.html]
Problems
  + Kernel Crash Dump [https://help.ubuntu.com/lts/serverguide/kernel-crash-dump.html]
  + Keyboard for Japanese 106 keys [http://www.mazn.net/blog/2014/07/06/1356.html]
    $ dpkg-reconfigure keyboard-configuration
    Select Generic 105-key (Intl) PC → Japanese → Japanese → The default for the keyboard layout → No compose key
  + Editing Local time [http://www.mazn.net/blog/2014/07/06/1356.html]
    $ cp /usr/share/zoneinfo/Asia/Tokyo /etc/localtime
    Verify the local time has been changed to JST
    $ date
    Jul 6 11:34:35 JST 2014
  + Assigning a static IP [http://askubuntu.com/questions/470237/assigning-a-static-ip-to-ubuntu-server-14-04-lts]
    You have to edit /etc/network/interfaces The interface will probably be called eth0. The current entry will look something like
    auto eth0
    iface eth0 inet dhcp
    
    You will need you need to change this to:
    auto eth0
    iface eth0 inet static
      address 165.93.164.185
      netmask 255.255.255.0
      network 10.253.0.0 (sometimes this is not necessary)
      gateway 165.93.164.1
      dns-nameservers 165.93.11.4 (or 8.8.8.8 can be used)

    You will have to change the numbers around depending on you network, but you can find out the information by checking out ipconfig from Windows. Make sure you choose an address outside the address space of the dhcp server.
    Then restart networking if that gives you trouble reboot the machine.
    $ sudo service networking restart
  + SSH accessing [http://askubuntu.com/questions/51925/how-do-i-configure-a-new-ubuntu-installation-to-accept-ssh-connections]
    $ sudo apt-get update
    $ sudo apt-get install openssh-server
    $ sudo ufw allow 22
    Some more about SSH [https://help.ubuntu.com/community/SSH/OpenSSH/InstallingConfiguringTesting]

  + Samba to share files [https://help.ubuntu.com/community/How%20to%20Create%20a%20Network%20Share%20Via%20Samba%20Via%20CLI%20(Command-line%20interface/Linux%20Terminal)%20-%20Uncomplicated,%20Simple%20and%20Brief%20Way!]
    More about sharing between Ubuntu 14.04 and Windows 7
    [http://askubuntu.com/questions/571685/ubuntu-14-04-lts-windows-7-sharing]
  
  + Changing the color for directories with ls in the console [http://askubuntu.com/questions/466198/how-do-i-change-the-color-for-directories-with-ls-in-the-console]
    To change your directory colors, open up your ~/.bashrc file with your editor
    $ nano ~/.bashrc
    and make the following entry at the end of the file:
      LS_COLORS=$LS_COLORS:'di=0;35:' ; export LS_COLORS
    Some nice color choices (in this case 0;35 it is purple) are:
      Blue = 34
      Green = 32
      Light Green = 1;32
      Cyan = 36
      Red = 31
      Purple = 35
      Brown = 33
      Yellow = 1;33
      white = 1;37
      Light Grey = 0;37
      Black = 30
      Dark Grey= 1;30
    The first number is the style (1=bold), followed by a semicolon, and then the actual number of the color, possible styles are:
      0   = default colour
      1   = bold
      4   = underlined
      5   = flashing text
      7   = reverse field
      40  = black background
      41  = red background
      42  = green background
      43  = orange background
      44  = blue background
      45  = purple background
      46  = cyan background
      47  = grey background
      100 = dark grey background
      101 = light red background
      102 = light green background
      103 = yellow background
      104 = light blue background
      105 = light purple background
      106 = turquoise background

    All possible colors:
      31  = red
      32  = green
      33  = orange
      34  = blue
      35  = purple
      36  = cyan
      37  = grey
      90  = dark grey
      91  = light red
      92  = light green
      93  = yellow
      94  = light blue
      95  = light purple
      96  = turquoise
    These can even be combined, so that a parameter like:
      di=1;4;31;42
    in your LS_COLORS variable would make directories appear in bold underlined red text with a green background!
    You can also change other kinds of files when using the ls command by defining each kind with:
      di = directory
      fi = file
      ln = symbolic link
      pi = fifo file
      so = socket file
      bd = block (buffered) special file
      cd = character (unbuffered) special file
      or = symbolic link pointing to a non-existent file (orphan)
      mi = non-existent file pointed to by a symbolic link (visible when you type ls -l)
      ex = file which is executable (ie. has 'x' set in permissions).
      *.rpm = files with the ending .rpm
    
    After you alter your .bashrc file, to put the changes in effect you will have to restart your shell.
    or run $ source ~/.bashrc or you can use the shorter version of the command $ . ~/.bashrc
  
  + Black/purple screen after you boot Ubuntu for the first time [http://askubuntu.com/questions/162075/my-computer-boots-to-a-black-screen-what-options-do-i-have-to-fix-it/162087#162087]
    This usually happens because you have an Nvidia or AMD graphics card, or a laptop with Optimus or switchable/hybrid graphics, and Ubuntu does not have the proprietary drivers installed to allow it to work with these.
    The solution is to boot Ubuntu once in nomodeset mode (your screen may look weird) to bypass the black screen, download and install the drivers, and then reboot to fix it for ever.
    Start your computer, and press the Right Shift when booting up, to get the Grub menu. Use the ← ↑ → ↓ keys to navigate/highlight the entry you want (usually the first one).
    Press 'e' to edit that entry, which will show you the details
    Find the linux entry as shown above, use the ← ↑ → ↓ keys to get to it, and then press the End key to get to that line's end (which may be on the next line!). 
    Enter nomodeset as shown, and press Ctrl+X to boot to where you can successfully install your graphics drivers.

    After go into Ubuntu, do following steps to make 'nomodeset' as default whenever you restart [http://askubuntu.com/questions/38780/how-do-i-set-nomodeset-after-ive-already-installed-ubuntu]
    add this option to /etc/default/grub, firstly:
    $ sudo nano /etc/default/grub
    and then add nomodeset to GRUB_CMDLINE_LINUX_DEFAULT:
      GRUB_DEFAULT=0
      GRUB_HIDDEN_TIMEOUT=0
      GRUB_HIDDEN_TIMEOUT_QUIET=true
      GRUB_TIMEOUT=5
      GRUB_DISTRIBUTOR=`lsb_release -i -s 2> /dev/null || echo Debian`
      GRUB_CMDLINE_LINUX_DEFAULT="quiet splash nomodeset"
      GRUB_CMDLINE_LINUX=""
    And then save by hitting Ctrl+O, then exit nano with Ctrl+X, then simply run:
    $ sudo update-grub
  
  + Unzip file
    $ tar zxvf backups.tgz
    or $ gunzip -c backups.tgz | tar xvf -
    To unpack and put files in a different folder (directory) say /tmp/data, enter:
    $ tar zxvf backups.tgz -C /tmp/data
    $ ls -l /tmp/data
  
    tar command options
    -z : Uncompress the resulting archive with gzip command.
    -x : Extract to disk from the archive.
    -v : Produce verbose output i.e. show progress and file names while extracting files.
    -f backup.tgz : Read the archive from the specified file called backup.tgz.
    -C /tmp/data : Unpack/extract files in /tmp/data instead of the default current directory.

  + Install Dropbox on Ubuntu Server 14.04?
  + Install GitLab?
  + Access Ubuntu Server via SSH from Windows machines [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html]
    - PuTTy = ssh //make ssh connection
    - PSCP = scp //transfer files via ssh connection
  + Change Repository [https://help.ubuntu.com/community/Repositories/CommandLine]
    $ sudo add-apt-repository "deb http://us.archive.ubuntu.com/ubuntu/ saucy universe multiverse"
    $ sudo add-apt-repository "deb http://us.archive.ubuntu.com/ubuntu/ saucy-updates universe multiverse"
    or change file /etc/apt/sources.list
  + 
  
III. CUDA Toolkit SDK 8.0RC [http://developer.download.nvidia.com/compute/cuda/8.0/secure/rc1/docs/sidebar/CUDA_Installation_Guide_Linux.pdf?autho=1466451861_bef16194c32066cd5b60b00e704e8460&file=CUDA_Installation_Guide_Linux.pdf]
  $ sudo dpkg -i cuda-repo-<distro>_<version>_<architecture>.deb
  $ sudo apt-get update
  $ sudo apt-get install cuda
  Post-installation
  The PATH variable needs to include /usr/local/cuda-8.0/bin To add this path to the PATH variable:
  $ export PATH=/usr/local/cuda-8.0/bin${PATH:+:${PATH}}
  In addition, when using the runfile installation method, the LD_LIBRARY_PATH variableneeds to contain /usr/local/cuda-8.0/lib64 on a 64-bit system, or /usr/local/cuda-8.0/lib on a 32-bit system. To change the environment variables for 64-bit operating systems:
  $ export LD_LIBRARY_PATH=/usr/local/cuda-8.0/lib64${LD_LIBRARY_PATH:+:${LD_LIBRARY_PATH}}
  To change the environment variables for 32-bit operating systems:
  $ export LD_LIBRARY_PATH=/usr/local/cuda-8.0/lib${LD_LIBRARY_PATH:+:${LD_LIBRARY_PATH}}
  Note that the above paths change when using a custom install path with the runfile installation method.

  $ cat /proc/driver/nvidia/version
  
  $ cp /usr/local/cuda/bin/cuda-install-samples-8.0.sh ~
  Goto cuda samples directory and compile projects
  $ make
  $ make test
  
  Install the source code for cuda-gdb
  
IV.  cuDNN v5 for 8.0RC
  Download .tar file
  Extract files 
  Copy files into cuda directory in /usr/local/cuda-8.0/include and /usr/local/cuda-8.0/lib64
  
V.   Theano framework
  $ sudo apt-get install python-numpy python-scipy python-dev python-pip python-nose g++ libopenblas-dev git
  $ sudo pip install Theano
