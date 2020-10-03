# Overview
In this article we’re going to introduce virtualization, the various forms of virtualization, terminology, and a high level view of the abstraction that is virtualization. We’ll also be building out a test function for support of virtual machine instructions, followed by defining structures to represent various architectural registers and components. The reason for using structures to represent these things is because it’s common for people to use preprocessor macros, however, I find the abuse of preprocessor macros to be vague, ugly and bad practice overall. Preprocessor macros have their place, and we will use them in our project, but sparingly. All types, flags, bits, etc., will be defined using structures or unions. In the type definition section I’ll discuss a common problem seen among driver developers and encountered by other hypervisor developers. After all type definitions are created we’ll write a quick test to determine if our machine supports VMX and then we’ll close with recommended reading before the big article that is heavy on implementation details.

The recommended reading list is provided at the bottom and I strongly encourage you to read each entry in the list in its entirety, take notes, and connect the dots from the article if something was misunderstood.

Notice: At the time of writing all information has been checked and verified with the sources provided, any additional changes or modifications that may occur at a later date should be forwarded to the author. However, always check the sources should the information in the article be dated.

All development took place on Windows 10 x64 (Version 1803). If you’re on a different version, higher or lower, you may experience issues/conflicts during testing. This is not a guarantee, but a warning that you should – for the sake of correctness – be on the same version of Windows and developing for the same target version.

## Introduction to Intel VT-x
Virtualization is a concept that is decades old, believe it or not. There are countless examples from the early 1960’s, and as of the 21 years ago – VMware made its appearance on the virtualization scene introducing their x86 virtualization software. The timeline is incredible, and while we aren’t going to go into it in this article I’d recommend looking through this timeline of virtualization development to better get a grasp of its progression over the decades. We’re at the pinnacle of virtualization technology and today we begin to take advantage of the decades of hard work and the research of others.

To start let’s discuss the two principal classes of virtual machine software.

 

## Virtual-Machine Monitors (VMM or Hypervisor)
The virtual machine monitor is what is referred to in virtualization software as the host (also known as VMM, or hypervisor). It controls the processors and other platform hardware. It’s an abstraction between the guest environment (guest OS) and the logical processor. A hypervisor is in charge of managing processor resources, system memory, interrupts, and I/O. The hypervisor is a piece of software that gives the impression to the guest environment that they are operating on physical hardware. It’s the technology that allows for multiple operating systems to share a single host platform and its hardware and resources.

There are two types of hypervisors, and as stated in the overview post we’re going to write a Type 2 Hypervisor (also known as a hosted hypervisor.) The other type, which won’t be covered in this series unless doing comparisons, is a Type 1 Hypervisor – otherwise referred to as a native, or baremetal hypervisor. These are incredibly complex and time consuming to write, not to mention the challenge of achieving stability on more than one machine. I’ll provide some information on the two different types below.

## Type 1 Hypervisor (Baremetal/Native)

- Operates directly on hardware of the host, and can monitor operating systems that run above the VMM.
- Can modify boot structures, and CPU features.
- Independent of an operating system.
- Small, compact, with the main task of sharing and resource management for all systems operating above it.
- Used in virtualization products like VMware ESXi Server, Microsoft Hyper-V and Xen Server.

## Type 2 Hypervisor (Hosted)

Installed on an operating system, usually running at the lowest privilege level and supports operating systems above it.
Dependent on host operating system for operations.
Issues on base operating system affect entire system.
To run at the lowest privilege level it is usually written as a device driver that performs virtualization of each processor using kernel provided API.
This is primarily seen in products such as VMware Workstation, Microsoft Virtual PC, Virtual Box, and KVM.


Visual of the Type 2 Hypervisor software stack. Credit: LinuxHub



## Guest Environment (Guest OS or Guest)
Every virtual machine is a guest software environment (Guest OS). It is an operating system and application software executing above a VMM that presents the guest software. Whenever someone refers to something as a VM or virtual machine, they’re talking about the guest environment operating independently of other virtual machines, but using the same interfaces to system resources provided by a physical platform. Those resources include memory, graphics, processor interfaces, and so on. The guest environment, in a well written hypervisor, will be none the wiser about its virtualization status. That is, it should operate the same whether or not it’s running on a VMM.

The caveat with the guest environment is that it executes at a virtually reduced privilege level so that the VMM has control of system resources. Certain operations will trap into the VMM giving it full control of the responses, management of resources, and platform overall.


 
