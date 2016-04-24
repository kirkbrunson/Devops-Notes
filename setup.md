For the projects in this course, you'll need to install some software onto your computer:

- VirtualBox
- Vagrant
- Git and ssh
- Packer


**Git**
If you don't already have Git installed, [download Git from git-scm.com](https://git-scm.com/downloads). Install the version for your operating system.
On Windows, Git will provide you with a Unix-style terminal and shell (Git Bash).

(On Mac or Linux systems you can use the regular terminal program.)
You will need Git to install the configuration for the VM. If you'd like to learn more about Git, [take a look at our course about Git and Github](http://www.udacity.com/course/ud775).


**VirtualBox:**
VirtualBox is the software that actually runs the VM. [You can download it from virtualbox.org](https://www.virtualbox.org/wiki/Downloads). Install the platform package for your operating system. You do not need the extension pack or the SDK. You do not need to launch VirtualBox after installing it.

Ubuntu 14.04 Note: If you are running Ubuntu 14.04, install VirtualBox using the Ubuntu Software Center, not the virtualbox.org web site. Due to a [reported bug](http://ubuntuforums.org/showthread.php?t=2227131), installing VirtualBox from the site may uninstall other software you need.


**Vagrant:**
Vagrant is the software that configures the VM and lets you share files between your host computer and the VM's filesystem. [You can download it from vagrantup.com](https://www.vagrantup.com/downloads.html). Install the version for your operating system.

Windows Note: The Installer may ask you to grant network permissions to Vagrant or make a firewall exception. Be sure to allow this.


**Packer:**
Packer is used to build golden images for various build targets that range from VMs to cload providers such as Google Compute Engine, AWS, Digital Ocean, and Microsoft Azure.

[Download it](https://www.packer.io/downloads.html) and [follow the installation instructions](https://www.packer.io/intro/getting-started/setup.html) for your platform.


**Set up:**
Use Git to fetch the app configuration

Windows: Use the Git Bash program (installed with Git) to get a Unix-style terminal.
Other systems: Use your favorite terminal program.

From the terminal, run:
```
git clone http://github.com/udacity/devops-intro-project devops
```

This will give you a directory named devops.