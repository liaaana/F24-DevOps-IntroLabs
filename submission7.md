# Virtualization Lab
Learned how to deploy a Virtual Machine (VM) using VirtualBox and customize its settings.

## Task 1: VM Deployment
Installed VirtualBox and deployed a new VM using Ubuntu.

### VirtualBox installation

Downloaded VirtialBox of version v7.1.0 from [VirtualBox website]( https://www.virtualbox.org/)

Command to find the version: `virtualbox --help`

### Deployed a Virtual Machine
1) Created a new Virtual Machine (VM) using VirtualBox and chose the Ubuntu operating system.
    Downloaded ISO image from [Ubuntu website](https://ubuntu.com/download)
Used commands to install desktop version:
```
sudo apt update
sudo apt install ubuntu-desktop
sudo reboot
```
2) VM settings. Allocated memory, number of CPU cores, and network configuration.
3) Screenshot of the running VM.
![settings](./img1.png)
![settings](./img2.png)
![settings](./img3.png)
![vm](./img4.png)

## Task 2: System Information Tools
Discovered and used command-line tools to display system information of the VM.

### Processor, RAM, and Network Information
1) Discovered a suitable command-line tool: `inxi`
2) Installed the tool on VM: `sudo apt-get install inxi`
3) Used the tool to display the processor, RAM, and network information of the VM:
![Processor, RAM, and Network Information](./img5.png)

### Operating System Specifications
1) Discovered a suitable command-line tool: `lsb_release`
2) Installed the tool on VM: `sudo apt-get install lsb-release`
3) Used the tool to display the operating system specifications of the VM:
![Processor, RAM, and Network Information](./img6.png)