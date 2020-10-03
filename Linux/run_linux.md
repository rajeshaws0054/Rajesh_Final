
let's run Linux!!

You have some options, so let's go through those. Which operating system are you using right now? If you're using a desktop running Linux of some variety, you're already set and you can skip this section unless you're curious how to get up and running on macOS and Windows.

# Virtualization

We're going to running our Linux through a process call virtualization. We'll be running a virtual machine which is frequently abbreviated as VMs. VMs are an operating system running within another operating system, called the host machine. The host machine will create a virtual environment with virtual acccess to its hardware to the VM. The VM will have no idea that it's not actually running on real hardware; all it can see is the resources that the host is providing it.

So, at this point, I'll be giving you instructions on how to get a VM running on macOS and on Windows. I'll give you several options so you can do what's best fit for you.

I'll recommend most people will want to do Multipass.


# For either macOS or Windows: VirtualBox

Oracle makes a product called [VirtualBox][vb]. VirtualBox is a hosted hypervisor which is another way of saying that this is a program that allows you to run VMs. It can run Windows, Linux, macOS, and many other VMs but today all we care about is Linux. I've been using VirtualBox for years and it's a reliable product. It's not the fastest nor the most feature rich but dammit it works.

What's annoying about going down this path is that you'll need to download VirtualBox and you'll need to download the Ubuntu Server installer as well and go through the whole process. It's possible, it just takes some time. [Here's the link to the Ubuntu installer][ubuntu].

For creating the VM, just create a new Ubuntu 64 bit VM with the all default options. When you go to start it for the first time, it'll ask you to choose a boot media file. Point it at the Ubuntu 18.04 .iso file you downloaded. From here, just follow the instructions to install Ubuntu. Give it a username and password. This doesn't need to be super secure so just it a username and password you can remember. For everything else, just follow the menus and give the default responses. You don't need to connect to GitHub or anything, nor do you need any additional packages installed.

It will ask you to restart after you install so do that. Once done, you should be able to start your VM and log in to your new shell with the username and password you created. At this point, your screen shoud look something like this:

![Screenshot of logged in shell](./images/up-and-running.png)

It bears mentioning that VirtualBox isn't the only option. [VMWare Fusion][vmware] and [Parallels][parallels] (macOS only) are two great options too. They just aren't free.


# Wrap Up

At this point, you should have a shell prompt ready to go so we can continue with the course. This was annoying but necessary! Let's keep going.

[vb]: https://www.virtualbox.org/
[ubuntu]: https://ubuntu.com/download/server

