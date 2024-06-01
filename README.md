# UnRaid-OS-User-Guide

Brief description of your project. What does it do? Why is it useful?

## Table of Contents

- [Installation](#installation)
- [Usage](#usage)
- [Features](#features)
- [Contributing](#contributing)
- [License](#license)
- [Contact](#contact)

## Intro

At its core, Unraid is a hardware-agnostic solution that can turn almost any 64-bit capable system into a NAS. Unraid can manage an array of drives (connected via IDE, SATA, or SAS).

With unRAID , unlike traditional RAID-based technologies, it can scale on-demand by adding more drives without the need to rebalance the existing data. So essectially just pop your system add another hdd or sdd without the need to delete any existing data. 

Before I start here are some basic essential terminology that a user needs to know.

1. Disk array :

2. Cache pool: The cache drive feature of Unraid provides faster data intake.When data is written to a user share that has been configured to use the cache drive, all of that data is initially written directly to the dedicated cache drive. Because this drive is not a part of the array, the write speed is unimpeded by parity updates. Then, a scheduled mover process copies the data from the cache to the array at a time and frequency of your choosing (typically in the middle of the night). Once the mover completes, the space consumed previously on the cache drive is freed up.
[ add pic of Cache pool ]

3. User shares: To simplify manageability, the root user can create shares that allow files written to them to be spread across multiple drives. Each share can be thought of as a top-level folder on a drive. 

4. Parity-Protected Array: The primary purpose of an Unraid array is to manage and protect the data of any group of drives (JBOD) by adding up to two dedicated parity drives. A parity drive provides a way to reconstruct all of the data from a failed drive onto a replacement. The way the process works with a single parity drive is the parity disk and other disks perform a XOR function a bit level. If one disk fails the system performs an XOR function to determine the lost data(the bit) so it can add that data to the new drive that will replace the failed drive. 
[insert picture of single parity drive diagram]


* is a dash

## VMs in unRAID

We will be looking and using 2 shares that unRaid has already provided for us and that is : isos and domains.

When we create a VM it creates a virtual hard disk. And all the virtual hard disks created in unRaid are saved within the domains shares(folder). The isos shares are used to store all install media (eg. Windows11.iso file). 

So first we need to make the isos share available in our network. 

1. click onto isos 
2. Scroll down to export and change to Yes
3. We can add security to the share if we want click apply
4. isos share will be available on our network now 
5. create a new folder for each new type of install ( folder name: Linux )
6. Enable VM Manager by going to settings click on vm manager (make sure HVM and IOMMU are enabled)
7. download lates window virtIO driver git apply and done
8. click vms 
9. If passing through hardware, check the hardware you want to pass-through is in its own iommu group (If i want to run a dedicated GPU look at youtube video linked below)
[VM-GPU-Video]
(https://www.youtube.com/watch?v=RD6OWYJOIzU&list=PLlgoK-okRFaATYcnVdqpDqxoavNVnwMf4&index=7) 
10. install OS . Warning ethernet drivers may have not installed correctly so have to bypass online registration( shift+f10)
11. after logging in go to device manager and install ethernet by selecting the virtio disk and finding the driver (K..->w11 etc.)