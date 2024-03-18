# NVMe-HOMA
This is a repo which stores the diff files that we can apply to kernel tree 6.5-rc1 to get a working version of NVMe-HOMA. While developing an initial version it is easier for me to keep it as a diff file.
Once I am done working on this full time, I will make a kernel module that can be simply installed into your kernel.


# Installation Instructions

1. Download and compile the net-dev linux kernel branch on the 6.5-rc1 branch.
2. Download a Homa Kernel Module that can run on kernel version 6.5-rc1
3. Apply the host and target diffs to the respective machines.
4. If you try compiling the kernel modules after this you will notice that in each Makefile you will have to change the path to your Homa Kernel Module source code
5. Once you do this everything should compile fine.
6. Install the Homa Kernel Module
7. You might have to change your homa parameters based on your machine. For setups on a VM I recommend:
```
sysctl net.homa.gro_policy=0
sysctl net.homa.gso_force_software=1
```
8. Install the nvmet-tcp and nvme-tcp kernel modules
9. On the target machine you can create your nvmet-tcp port by running this [script](https://github.com/sulaimansuhas/nvmescripts/blob/master/target_script.sh). This is the same process of setting up nvme-tcp, it works because right now nvme-homa has been created by hacking the nvme-tcp code!
10. After this the nvme-connect command should work (as of the last iteration of this diff file we only support 1 io queue so please set `-i 1` as a parameter. [This script](https://github.com/sulaimansuhas/nvmescripts/blob/master/host_quick_setup.sh) should be helpful to you.

That is all for the setup, if you need debug information you can run modules with dyndbg on:
```
insmod nvme-tcp.ko dyndbg
```
**warning** this prints a lot of output to kernel console. This will greatly reduce performance, and will fill up log files very quickly.

If you are still facing any issues with the installation please feel free to contact me!
