---
title: About disks and VHDs for Microsoft Azure Linux VMs | Microsoft Docs
description: Learn about the basics of disks and VHDs for Linux virtual machines in Azure.
services: storage
documentationcenter: ''
author: robinsh
manager: timlt
editor: tysonn
tags: azure-resource-manager,azure-service-management

ms.assetid: 7be8dd52-98f7-4187-9b78-55197915bc9b
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/09/2017
ms.author: robinsh

---
# About disks and VHDs for Azure Linux VMs
Just like any other computer, virtual machines in Azure use disks as a place to store an operating system, applications, and data. All Azure virtual machines have at least two disks – a Linux operating system disk and a temporary disk. The operating system disk is created from an image, and both the operating system disk and the image are actually virtual hard disks (VHDs) stored in an Azure storage account. Virtual machines also can have one or more data disks, that are also stored as VHDs. 

In this article, we will talk about the different uses for the disks, and then discuss the different types of disks you can create and use. This article is also available for [Windows virtual machines](storage-about-disks-and-vhds-windows.md).

[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-both-include.md)]

## Disks used by VMs

Let's take a look at how the disks are used by the VMs.

## Operating system disk
Every virtual machine has one attached operating system disk. It’s registered as a SATA drive and is labeled /dev/sda by default. This disk has a maximum capacity of 1023 gigabytes (GB). 

## Temporary disk
The temporary disk is automatically created for you. On Linux virtual machines, the disk is typically /dev/sdb and is formatted and mounted to /mnt/resource by the Azure Linux Agent.

The size of the temporary disk varies, based on the size of the virtual machine. For more information, see [Sizes for Linux virtual machines](../virtual-machines/virtual-machines-linux-sizes.md).

> [!WARNING]
> Don’t store data on the temporary disk. It provides temporary storage for applications and processes and is intended to only store data such as page or swap files. 
> 

For more information on how Azure uses the temporary disk, see [Understanding the temporary drive on Microsoft Azure Virtual Machines](https://blogs.msdn.microsoft.com/mast/2013/12/06/understanding-the-temporary-drive-on-windows-azure-virtual-machines/)

## Data disk
A data disk is a VHD that’s attached to a virtual machine to store application data, or other data you need to keep. Data disks are registered as SCSI drives and are labeled with a letter that you choose. Each data disk has a maximum capacity of 1023 GB. The size of the virtual machine determines how many data disks you can attach to it and the type of storage you can use to host the disks.

> [!NOTE]
> For more details about virtual machines capacities, see [Sizes for Linux virtual machines](../virtual-machines/virtual-machines-linux-sizes.md).
> 

Azure creates an operating system disk when you create a virtual machine from an image. If you use an image that includes data disks, Azure also creates the data disks when it creates the virtual machine. Otherwise, you add data disks after you create the virtual machine.

You can add data disks to a virtual machine at any time, by **attaching** the disk to the virtual machine. You can use a VHD that you’ve uploaded or copied to your storage account, or one that Azure creates for you. Attaching a data disk associates the VHD file with the VM, by placing a ‘lease’ on the VHD so it can’t be deleted from storage while it’s still attached.

[!INCLUDE [storage-about-vhds-and-disks-windows-and-linux](../../includes/storage-about-vhds-and-disks-windows-and-linux.md)]

## Troubleshooting
[!INCLUDE [virtual-machines-linux-lunzero](../../includes/virtual-machines-linux-lunzero.md)]

## Next steps
* [Attach a disk](../virtual-machines/virtual-machines-linux-add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) to add additional storage for your VM.
* [Configure software RAID](../virtual-machines/virtual-machines-linux-configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for redundancy.
* [Capture a Linux virtual machine](../virtual-machines/virtual-machines-linux-classic-capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json) so you can quickly deploy additional VMs.

