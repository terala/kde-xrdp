# KDE Plasma over XRDP Setup

Use these scripts to get a usable KDE based development VM with all the
development tools, shells, compilers, editors, etc in a VM, typically 
running on a Windows VM or a Mac.

## Installation Steps

1. Install [VirtualBox](https://virtualbox.org) (on Windows Home) or Enable HyperV on Windows Pro. You can skip this step if you on a mac.

2. Install [Multipass](https://multipass.run). Multipass is a great tool that let you run Ubuntu VMs with ease.
Multipass will use Hyper-V on Windows Pro and the default hypervisor on Macs. On Windows Home, you'd need to setup the driver to use VirtualBox, so multipass will use VirtualBox to create VMs. Use the following command on Windows Home.
```
multipass set local.driver=virtualbox
```
3. Clone this repo
4. Create a new VM using `multipass`. Change the memory and disk settings for your needs. 

```
multipass launch lts -n kde -m 12G -d 50G
```

5. Mount this directory into the VM, so we can run commands in it.
```
multipass mount . lte:/mnt
```

6. Shell into the VM, so we can start configuration.
```
multipass shell lte
```

7. Once in the VM, run the following commands to start the installation. This may take nearly 20min depending on the speed of your internet connection. Once the installation is done, your KDE environment is ready.
```bash
sudo apt update
sudo apt install ansible
cd /mnt
ansible-playbook setup.yml
```

8. To login to your VM, you need to find the IP address of the VM. Running `multipass list` will show a list something similar to this. Take a note of the IP Address.
```
 2020-09-23 08:22:08 ⌚  devbox in ~
± |origin/master U:3 ?:1 ✗| → multipass list
Name                    State             IPv4             Image
primary                 Stopped           --               Ubuntu 20.04 LTS
lte                     Running           10.212.168.161   Ubuntu 20.04 LTS
```

9. Open Remote Desktop Connection or your favourite RDP client and login to the IP address. The username and password are in `setup.yml`, in the `var` section.
    