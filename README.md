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
1) Install ubuntu following this [guide](https://itsfoss.com/install-ubuntu-1404-dual-boot-mode-windows-8-81-uefi/)
    - Note that when installing, don't check downloading the third party software because it will install the wrong NVIDIA driver.
2) If ubuntu cannot be booted up, try following [Black/purple screen after you boot Ubuntu for the first time](https://askubuntu.com/questions/162075/my-computer-boots-to-a-black-screen-what-options-do-i-have-to-fix-it)
3) After booting up, one will see the screen with bad resolution. That's normal because the graphic driver has not yet been installed. Try following [4. Install Official Nvidia Driver](https://www.itzgeek.com/post/how-to-install-nvidia-drivers-on-ubuntu-20-04-ubuntu-18-04.html) and it should work.
    - Note that I tried 1), 2) methods on Ubuntu 18.04 but it ends up cannot be booted. Only the 4) method works.
    - If the resolution went bad again, it maybe because the driver went wrong again. So try step 2) and step 3) again then the problem should solve.

## Ubuntu 18.04 starter pack
```bash
# Update the software
sudo apt update && sudo apt upgrade -y

# installing pip
sudo apt install python-pip python3-pip
```
4) To install multiple version of CUDA and CUDNN, follow this [guide](https://towardsdatascience.com/installing-multiple-cuda-cudnn-versions-in-ubuntu-fcb6aa5194e2) 

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
