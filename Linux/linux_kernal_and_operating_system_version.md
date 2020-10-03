## lsb_release

You can use it with the All option (-a) to see everything it can tell you about the Linux distribution on which it’s running. To do so, type the following command:

`lsb_release -a`

## /etc/os-release File

/etc/os-release file contains useful information about your Linux system

`cat /etc/os-release`

## hostnamectl

The hostnamectl command will display useful information about which Linux is running on the target computer. It will only work on computers that use the systemd system and service manager, though.

`hostnamectl`

## uname

uname command to find out which version of the kernel it’s running. Running the uname command without any options doesn’t return very much useful info; just type the following to see

`uname`

## dmesg

dmesg command allows you to see messages in the kernel messaging ring-buffer. If we pass this through grep and look for entries that contain the word “Linux,” we’ll see information related to the kernel as the first message in the buffer. Type the following to do this

`sudo dmesg | grep Linux`
