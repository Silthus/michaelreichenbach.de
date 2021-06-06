---
title: RoboCopy the better XCopy – Parsing error logs
author: Michael
type: post
date: 2018-03-12T09:16:16+00:00
url: /robocopy-the-better-xcopy-parsing-error-logs/
featured_image: /wp-content/uploads/2018/01/night-computer-hdd-hard-drive.jpg
hestia_layout_select:
  - default
categories:
  - System Administration
tags:
  - powershell
  - robocopy
  - windows
  - xcopy

---
A few weeks ago I wrote about [using XCopy to copy files and folder structures including their NTFS Permissions][1]. Recently I came to the point where I wanted to see all errors and their related files, so I could fix messed up NTFS permissions. With XCopy however parsing the log is pretty much impossible. Also Microsoft suggests using RoboCopy as a sucessor to XCopy. And thats what I did.

# Using RoboCopy like XCopy

In my other blog post I meantioned that I wanted to copy all folders and files including their NTFS permissions and ignore errors on the way. You can do the same thing with RoboCopy&#8230; and it is a lot faster.

To achieve the same result you can use the following command to keep directories in sync.

<pre>ROBOCOPY S:\Source_Dir D:\Destination_Dir /MIR /SECFIX /COPYALL /R:0 /W:0 /LOG:"C:\Logs\example_$(get-date -f "yyyy-MM-dd_hh-mm-ss").log" /TEE</pre>

Okay let&#8217;s go over the switches line by line.

/MIR &#8211; Mirrors the source to the destination dir copying all files and folders, including empty ones.  
/SECFIX &#8211; Fixes security permissions on already copied files (you can leave this out if you want)  
/COPYALL &#8211; Copies all files attributes including NTFS permissions.  
/R:0 &#8211; Number of times to retry copying a failed file.  
/W:0 &#8211; Wait time between retries. Defaults to 30 seconds.  
/LOG:file &#8211; Logs output into the givenfile.  
/TEE &#8211; Logs output to console and logfile.

You can always see a full list of switches with /?.system

# Parsing RoboCopy error log

With RoboCopy we now get parseable log files and can use this nifty [script from the Technet Gallery][2] to extract all failed files from the logs.

<div class="oembed-gist">
  <noscript>
    View the code on <a href="https://gist.github.com/Silthus/a54f82aa0036b74b6f588fdcedad3e5e">Gist</a>.
  </noscript>
</div>

&nbsp;

 [1]: https://michaelreichenbach.de/xcopy-files-keeping-ntfs-permissions-ignoring-errors/
 [2]: https://gallery.technet.microsoft.com/scriptcenter/Powershell-script-to-parse-a1bc8a92