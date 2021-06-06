---
title: 'How-To: Extend windows partition blocked by recovery partition'
author: Michael
type: post
date: 2018-01-29T08:13:39+00:00
url: /how-to-extend-windows-partition-blocked-by-recovery-partition/
featured_image: /wp-content/uploads/2018/01/night-computer-hdd-hard-drive.jpg
hestia_layout_select:
  - default
classic-editor-remember:
  - classic-editor
categories:
  - System Administration
tags:
  - diskpart
  - dism
  - powershell
  - windows
  - winpe

---
When you are working with Visual Machines (VMs) and fixed hard disks it can happen that you run out of space. In such cases it comes in handy that you can simply extend the existing virtual hard disk. Since Windows Server 2012R2 and Windows 8.1 this is even [possible while the VM is running][1]. After extending the VHDX you just need to go into Disk Management and expand your partition. That&#8217;s the theory at least. However in a non lab environment things might look a little different.

<div id="attachment_105" style="width: 1617px" class="wp-caption aligncenter">
  <img aria-describedby="caption-attachment-105" loading="lazy" src="https://i1.wp.com/michaelreichenbach.de/wp-content/uploads/2018/01/move_recovery_1.png?resize=750%2C189&#038;ssl=1" alt="" width="750" height="189" class="wp-image-105 size-full" srcset="https://i1.wp.com/michaelreichenbach.de/wp-content/uploads/2018/01/move_recovery_1.png?w=1607&ssl=1 1607w, https://i1.wp.com/michaelreichenbach.de/wp-content/uploads/2018/01/move_recovery_1.png?resize=300%2C76&ssl=1 300w, https://i1.wp.com/michaelreichenbach.de/wp-content/uploads/2018/01/move_recovery_1.png?resize=768%2C194&ssl=1 768w, https://i1.wp.com/michaelreichenbach.de/wp-content/uploads/2018/01/move_recovery_1.png?resize=1024%2C258&ssl=1 1024w, https://i1.wp.com/michaelreichenbach.de/wp-content/uploads/2018/01/move_recovery_1.png?w=1500&ssl=1 1500w" sizes="(max-width: 750px) 100vw, 750px" data-recalc-dims="1" /></p> 
  
  <p id="caption-attachment-105" class="wp-caption-text">
    Primary Partition blocked by Recovery Partition
  </p>
</div>

# Primary Partition blocked by Recovery Partition

More often than not, the partition you want to extend is blocked by a &#8220;Recovery Partition&#8221;. Blocked because you can only extend your existing partition with unallocated space directly to the right of the partition you want to extend. In our case there is a recovery partition in between and therefor the primary partition (C:) cannot be extended. This happens because Windows 10 creates the recovery partition after your primary partition so it can easily be extended.

## Windows Partition Layout

The [Windows 10 UEFI parition layout][2] looks like the following. First comes a System Partition containing the master boot record (MBR). Without the system parition you will not be able to start Windows. Follwing the system partition you have the Microsoft Reserved Parition (MSR) that manages the partitions itself. Then you have your primary Windows parition followed by the recovery parition containing tools and data to recover your Windows installation in case of failures.

<div id="attachment_106" style="width: 730px" class="wp-caption aligncenter">
  <img aria-describedby="caption-attachment-106" loading="lazy" src="https://i1.wp.com/michaelreichenbach.de/wp-content/uploads/2018/01/dep-win10-partitions-uefi.png?resize=720%2C89&#038;ssl=1" alt="" width="720" height="89" class="wp-image-106 size-full" srcset="https://i1.wp.com/michaelreichenbach.de/wp-content/uploads/2018/01/dep-win10-partitions-uefi.png?w=720&ssl=1 720w, https://i1.wp.com/michaelreichenbach.de/wp-content/uploads/2018/01/dep-win10-partitions-uefi.png?resize=300%2C37&ssl=1 300w" sizes="(max-width: 720px) 100vw, 720px" data-recalc-dims="1" /></p> 
  
  <p id="caption-attachment-106" class="wp-caption-text">
    Windows 10 UEFI Paritions
  </p>
</div>

&nbsp;

## Deleting the Recovery Partition

We can now go ahead and delete the recovery partition to make room for our primary Windows Partition. You can delete the recovery parition with **DISKPART** using the following commands from an admin commandline.

<pre>C:\Windows\System32\&gt; DISKPART

Microsoft DiskPart version 10.0.14393.0
Copyright (C) 1999-2013 Microsoft Corporation.

DISKPART&gt; rescan

Please wait while DiskPart scans your configuration...

DiskPart has finished scanning your configuration.

DISKPART&gt; list disk

 Disk ### Status Size Free Dyn Gpt
 -------- ------------- ------- ------- --- ---
 Disk 0 Online 300 GB 0 B *

DISKPART&gt; select disk 0

Disk 0 is now the selected disk.

DISKPART&gt; list part

 Partition ### Type Size Offset
 ------------- ---------------- ------- -------
 Partition 1 Recovery 300 MB 1024 KB
 Partition 2 System 500 MB 301 MB
 Partition 3 Reserved 128 MB 801 MB
 Partition 4 Primary 298 GB 929 MB
 Partition 5 Recovery 451 MB 299 GB

DISKPART&gt; select part 5

Partition 5 is now the selected partition.

DISKPART&gt; delete partition override

DiskPart successfully deleted the selected partition.</pre>

We can now go ahead and extend our Windows Parition to consume the free space. You should however leave about 500MB room so we can recreate our recovery parition.

<div id="attachment_107" style="width: 1640px" class="wp-caption aligncenter">
  <img aria-describedby="caption-attachment-107" loading="lazy" src="https://i0.wp.com/michaelreichenbach.de/wp-content/uploads/2018/01/expand_recovery.png?resize=750%2C170&#038;ssl=1" alt="" width="750" height="170" class="wp-image-107 size-full" srcset="https://i0.wp.com/michaelreichenbach.de/wp-content/uploads/2018/01/expand_recovery.png?w=1630&ssl=1 1630w, https://i0.wp.com/michaelreichenbach.de/wp-content/uploads/2018/01/expand_recovery.png?resize=300%2C68&ssl=1 300w, https://i0.wp.com/michaelreichenbach.de/wp-content/uploads/2018/01/expand_recovery.png?resize=768%2C174&ssl=1 768w, https://i0.wp.com/michaelreichenbach.de/wp-content/uploads/2018/01/expand_recovery.png?resize=1024%2C232&ssl=1 1024w, https://i0.wp.com/michaelreichenbach.de/wp-content/uploads/2018/01/expand_recovery.png?w=1500&ssl=1 1500w" sizes="(max-width: 750px) 100vw, 750px" data-recalc-dims="1" /></p> 
  
  <p id="caption-attachment-107" class="wp-caption-text">
    Expanded Windows Partition
  </p>
</div>

# Recreating the Recovery Partition

If you do not need your recovery environment you can stop here and enjoy your new disk space. However I highly recommend recreating the just deleted recovery enviroment. That way in case of a system failure you can easly troubleshoot and restore your system. To create a new recovery partition we first must format the remaining 500MB free space accordingly. Windows recognizes the recovery partition by the static unique id _de94bba4-06d1-4d40-a16a-bfd50179d6ac_ and the GPT attribute bit _0x8000000000000001_.

<pre>DISKPART&gt; create part primary

DiskPart succeeded in creating the specified partition.

DISKPART&gt; format quick fs=ntfs label="Recovery tools"

100 percent completed

DiskPart successfully formatted the volume.

DISKPART&gt; assign letter="R"

DiskPart successfully assigned the drive letter or mount point.

DISKPART&gt; set id="de94bba4-06d1-4d40-a16a-bfd50179d6ac"

DiskPart successfully set the partition ID.

DISKPART&gt; gpt attributes=0x8000000000000001

DiskPart successfully assigned the attributes to the selected GPT partition.

DISKPART&gt; list volume
DISKPART&gt; exit</pre>

We now have a partition that can host the [Windows Recovery Environment][3] (WinRE). In the next step we are going to extract the WinRE from the Windows Installation media and copy it to the just created volume.

## Extrating the Windows Recovery Environment (WinRE)

Download the .ISO image for your version of Windows our insert your installation disk and mount it by right clicking the image. We are now going to mount the installation files and [copy the winre.wim file from Windows PE][4]. Open an admin powershell and enter the following commands.

<pre>PS C:\Windows\System32&gt; md C:\WinPE

PS C:\Windows\System32&gt; md C:\WinPE\mount

# Copy install.wim from the mounted installation media
PS C:\Windows\System32&gt; copy D:\sources\install.wim C:\WinPE\

# Mount the image in readonly mode
PS C:\Windows\System32&gt; dism /mount-wim /wimfile:C:\WinPE\install.wim /index:1 /mountdir:C:\WinPE\mount /readonly

# Extract the Windows Recovery Environment
PS C:\Windows\System32&gt; copy C:\WinPE\mount\Windows\System32\Recovery\Winre.wim C:\WinPE\

# Unmount the image
PS C:\Windows\System32&gt; dism /unmount-wim /mountdir:c:\WinPE\mount /discard</pre>

## Installing the Windows Recovery Enviroment (WinRE)

Now that we have the WinRE image we can install it in our new recovery volume (R:). We are going to copy the image and then tell Windows were to find it.

<pre>PS C:\Windows\System32&gt; md R:\Recovery\WindowsRE

PS C:\Windows\System32&gt; copy C:\WinPE\Winre.wim R:\Recovery\WindowsRE\

# Register the recovery image 
PS C:\Windows\System32&gt; C:\Windows\System32\reagentc /setreimage /path R:\Recovery\WindowsRE /target C:\Windows
Directory set to: \\?\GLOBALROOT\device\harddisk0\partition5\Recovery\WindowsRE

REAGENTC.EXE: Operation Successful.</pre>

Thats it. We are all done and you can now use your recovery enviroment as before.

 [1]: https://blogs.msdn.microsoft.com/virtual_pc_guy/2014/01/28/online-vhdx-resize-in-windows-server-2012-r2-windows-8-1/
 [2]: https://docs.microsoft.com/en-us/windows-hardware/manufacture/desktop/configure-uefigpt-based-hard-drive-partitions
 [3]: https://docs.microsoft.com/en-us/windows-hardware/manufacture/desktop/windows-recovery-environment--windows-re--technical-reference
 [4]: https://docs.microsoft.com/en-us/windows-hardware/manufacture/desktop/capture-and-apply-windows-system-and-recovery-partitions