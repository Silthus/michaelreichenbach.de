---
title: 'Windows Server 2019: How-To run Enable-ClusterStorageSpacesDirect cmdlet'
author: Silthus
type: post
date: 2018-10-22T11:21:10+00:00
url: /windows-server-2019-how-to-run-enable-clusterstoragespacesdirect-cmdlet/
draft: true
categories:
  - System Administration
tags:
  - powershell
  - s2d
  - storage-spaces-direct
  - windows
  - windows-server-2019

---
Microsoft disabled the **Enable-ClusterStorageSpacesDirect** feature in Windows Server 2019. The reason for it is that Microsoft is wating for hardware vendors to certify their hardware for Windows Server 2019. However if you are like me and have hardware that was perfectly fine with Windows Server 2016 you are probably a bit frustrated not being able to run a simple command.

<img loading="lazy" src="https://i2.wp.com/michaelreichenbach.de/wp-content/uploads/2018/10/Enable-ClusterStorageSpacesDirect_Error.png?resize=750%2C289&#038;ssl=1" alt="" width="750" height="289" class="aligncenter size-full wp-image-145" srcset="https://i2.wp.com/michaelreichenbach.de/wp-content/uploads/2018/10/Enable-ClusterStorageSpacesDirect_Error.png?w=842&ssl=1 842w, https://i2.wp.com/michaelreichenbach.de/wp-content/uploads/2018/10/Enable-ClusterStorageSpacesDirect_Error.png?resize=300%2C115&ssl=1 300w, https://i2.wp.com/michaelreichenbach.de/wp-content/uploads/2018/10/Enable-ClusterStorageSpacesDirect_Error.png?resize=768%2C296&ssl=1 768w" sizes="(max-width: 750px) 100vw, 750px" data-recalc-dims="1" /> 

There is a simple registry key you can add to your cluster nodes that will enable you to run the command like you used to.

Microsoft recommends contacting their support, and you should if you are unsure what your are doing or if you are trying to use Storage Spaces Direct (S2D) on a production system.

For the rest, this is the key:

``HKEY\_LOCAL\_MACHINE\SYSTEM\CurrentControlSet\Services\ClusSvc\Parameters\S2D``

Have fun using Storage Spaces Direct with Windows Server 2019.
