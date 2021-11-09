#### Attention

This SDK is intended for OpenWrt Chaos Calmer.

Correct assembly is possible on a 64-bit operating system architecture.

#### Build Process
It is recommended to install the necessary packages on your computer before use:
> :$ **sudo apt-get install subversion git g++ libncurses5-dev zlib1g-dev gawk libssl-dev unzip build-essential**

An example of the helloworld service daemon build and user-activated program helloworld_oneshot:
1. Download the archive with SDK OpenWrt-SDK-mxs_gcc-4.8-linaro_uClibc-0.9.33.2_eabi.Linux-x86_64.tar.bz2
2. Unpack the archive with the command:
    > :$ **bzcat OpenWrt-SDK-mxs_gcc-4.8-linaro_uClibc-0.9.33.2_eabi.Linux-x86_64.tar.bz2 | tar -xvf -**

3. Go to directory SDK:
    > :$ **cd OpenWrt-SDK-mxs_gcc-4.8-linaro_uClibc-0.9.33.2_eabi.Linux-x86_64/**

4. Create a directory for your package, for example:
    > :$ **mkdir -p package/helloworld**

5. Place the source code files in the directory (located in the attached archive helloworld.tar)
6. With command make menuconfig go to the menu, choose Ulilities and checkbox helloworld
7. Build the package:
    > :$ **make V=s**

8. Compiled for OpenWrt applications can be found under the path:
    > build_dir/target-arm_arm926ej-s_uClibc-0.9.33.2_eabi/helloworld

9. The ready-to-install package helloworld_123-321_mxs.ipk is located in the directory:
    > bin/mxs/packages/base

10. Then copy our package to a device with OpenWrt, for example, via SCP:
    > :$ **scp bin/mxs/packages/base/helloworld_123-321_mxs.ipk root@192.168.88.1:/tmp/**

11. On a device with OpenWrt, install our package:
    > root@GTR30:/# **opkg install /tmp/helloworld_123-321_mxs.ipk**

12. Try it:

    > \# helloworld_oneshot
    > 
    > root@GTR30:/# **helloworld_oneshot**
    > 
    > helloworld: Hi! This is oneshot HELLO
    > 
    > \# Start the helloworld daemon:
    > 
    > root@GTR30:/# **/etc/init.d/helloworld start**
    > 
    > \# The daemon's activity can be monitored by the command
    > 
    > root@GTR30:/# **logread -f | grep helloworld**
    > 
    > \# The helloworld daemon can be stopped in the same way as starting it:
    > 
    > root@GTR30:/# **/etc/init.d/helloworld stop**
    > 
    > \#  If rebooting, everything remains, as configured


#### Troubleshooting 
As a rule, most of the problems during the build's assembly (something is missing, new packages are not detected, etc.)
are caused either by errors in the code, or by lack of necessary packages on your PC (for example, with Ubuntu)
If problem occurs, try:
> :$ make distclean && make menuconfig
