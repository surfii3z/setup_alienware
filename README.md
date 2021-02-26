# Alienware M15 R4
NVIDIA RTX 3080

# WINDOWS
1) To install Dual boot Windows and Ubuntu, the sata operation needs to be changed from `RAID ON` to `AHCI`, otherwise, the ubuntu installer cannot see the SSD.
    - Note that by doing so, the OEM Windows, which was installed in `RAID ON` mode would not be able to boot up anymore.
    - Therefore, we need to reinstall it.
    - The alienware updater come with the OEM Windows could be download from [Dell alienware support site](https://www.dell.com/support/home/en-us/product-support/product/alienware-15-r4/drivers) later
2) Reinstall the Windows using some installer, select one SSD and install it.

# Ubuntu
1) Install ubuntu following this [guide](https://itsfoss.com/install-ubuntu-1404-dual-boot-mode-windows-8-81-uefi/)
    - Note that when installing, don't check downloading the third party software because it will install the wrong NVIDIA driver.
2) If ubuntu cannot be booted up, try following [Black/purple screen after you boot Ubuntu for the first time](https://askubuntu.com/questions/162075/my-computer-boots-to-a-black-screen-what-options-do-i-have-to-fix-it)
3) After booting up, one will see the screen with bad resolution. That's normal because the graphic driver has not yet been installed. Try following [4. Install Official Nvidia Driver](https://www.itzgeek.com/post/how-to-install-nvidia-drivers-on-ubuntu-20-04-ubuntu-18-04.html) and it should work.
    - Note that I tried 1), 2) methods on Ubuntu 18.04 but it ends up cannot be booted. Only the 4) method works.

## Ubuntu 18.04 starter pack
```bash
# Update the software
sudo apt update && sudo apt upgrade -y

# installing pip
sudo apt install python-pip python3-pip


```
