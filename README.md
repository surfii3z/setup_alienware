# Alienware M15 R4
NVIDIA RTX 3080

# WINDOWS
1) To install Dual boot Windows and Ubuntu, the sata operation needs to be changed from `RAID ON` to `AHCI`, otherwise, the ubuntu installer cannot see the SSD.
    - Note that by doing so, the OEM Windows, which was installed in `RAID ON` mode would not be able to boot up anymore.
    - Therefore, we need to reinstall it.
    - The alienware updater come with the OEM Windows could be download from [Dell alienware support site](https://www.dell.com/support/home/en-us/product-support/product/alienware-15-r4/drivers) later.
2) First at the booting, press `F2` to go into `BIOS`.
3) Then go to `Advances -> SATA Operation`, change from `RAID ON` to `AHCI`.
    - It will ask something, just choose `YES`.
4) Reinstall the Windows using some installer, select one SSD and install it.
    - I select `drive 0`, for example.

# Ubuntu
1) [Ubuntu Installation] Install ubuntu following this [guide](https://itsfoss.com/install-ubuntu-1404-dual-boot-mode-windows-8-81-uefi/)
    - Note that when installing, don't check downloading the third party software because it will install the wrong NVIDIA driver.
2) [Boot-up issue] If ubuntu cannot be booted up, try following [Black/purple screen after you boot Ubuntu for the first time](https://askubuntu.com/questions/162075/my-computer-boots-to-a-black-screen-what-options-do-i-have-to-fix-it) section.
3) [Ethernet Driver] check the hardware driver following, as we might need to update linux kernal to use the driver for hardware (e.g. ubuntu 18.04 LTS comes with kernal 5.4 which doesn't have driver for ethernet card of alienware m15 r4)
    `https://linux-hardware.org/?view=howto`
    - I installed linux kernal 5.8 using this [link](https://ubuntuhandbook.org/index.php/2020/08/install-linux-kernel-5-8-ubuntu/)
4) [NVIDIA Driver] After booting up, one will see the screen with bad resolution. That's normal because the graphic driver has not yet been installed. Try following [4. Install Official Nvidia Driver](https://www.itzgeek.com/post/how-to-install-nvidia-drivers-on-ubuntu-20-04-ubuntu-18-04.html) and it should work.
    - Note that I tried 1), 2) methods on Ubuntu 18.04 but it ends up cannot be booted. Only the 4) method works.
    - If the resolution went bad again, it maybe because the driver went wrong again. So try step 2) and step 3) again then the problem should solve.

5) [Update Ubuntu] Ubuntu 18.04 starter pack
```bash
# Update the software
sudo apt update && sudo apt upgrade -y

# installing pip
sudo apt install python-pip python3-pip
```
6) [CUDA and CuDNN] To install multiple version of CUDA and CUDNN, follow this [guide](https://towardsdatascience.com/installing-multiple-cuda-cudnn-versions-in-ubuntu-fcb6aa5194e2) 
    - HOWEVER, in the last step DON'T DO
 
    ```bash
    sudo apt install cuda   # DON'T do this, because it will break the driver
    ```

    - DO this
    
    ```bash
    sudo apt install cudatoolkit-M-m    # M is major version, m is minor version
    ```

# Performance
1) Tried with [packnet_sfm_ros](https://github.com/surfii3z/packnet_sfm_ros)
```
DGX-station @ Tesla V100
    work at 12 Hz
    work at 16 Hz (with TensorRT)

Alienware M15 R3(?) @ RTX 3080
    work at 10.5 Hz
```

# ISSUES
1) Compilation with `CUDA_ARCH_BIN`, ref: [link](https://arnon.dk/matching-sm-architectures-arch-and-gencode-for-various-nvidia-cards/).
```
RTX 3080 (laptop) has CUDA_ARCH_BIN 8.6 (?) which is only supported from CUDA 11.1
```
This will be the problem when we want to compile OpenCV with CUDA => We need CUDA 11.1.

2) Ethernet Controller doesn't have driver in linux kernel < 5.8 ([How](https://ubuntuhandbook.org/index.php/2020/08/install-linux-kernel-5-8-ubuntu/) to update kernel to 5.8)
    - If you use the following command
    ```bash
    lshw -c network
    ```
    It will show something like
    ```
      *-network UNCLAIMED            
       description: Ethernet interface
       ...
    ```
    
    - check the hardware driver following
    `https://linux-hardware.org/?view=howto`
