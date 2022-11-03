---
title: RoboCopy the better XCopy – Parsing error logs
date: 2018-03-12
url: /posts/robocopy-the-better-xcopy-parsing-error-logs/
categories:
  - System Administration
tags:
  - powershell
  - robocopy
  - windows
  - xcopy
  - tools
---
A few weeks ago I wrote about [using XCopy to copy files and folder structures including their NTFS Permissions][1]. Recently I came to the point where I wanted to see all errors and their related files, so I could fix messed up NTFS permissions. With XCopy however parsing the log is pretty much impossible. Also Microsoft suggests using RoboCopy as a sucessor to XCopy. And thats what I did.

## Using RoboCopy like XCopy

In my other blog post I meantioned that I wanted to copy all folders and files including their NTFS permissions and ignore errors on the way. You can do the same thing with **RoboCopy** and it is a lot faster.

To achieve the same result you can use the following command to keep directories in sync.

```powershell
ROBOCOPY S:\Source_Dir D:\Destination_Dir /MIR /SECFIX /COPYALL /R:0 /W:0 /LOG:"C:\Logs\example_$(get-date -f "yyyy-MM-dd_hh-mm-ss").log" /TEE
```

Okay let's go over the switches line by line.

| Parameter | Description |
| --------- | ----------- |
| /MIR | Mirrors the source to the destination dir copying all files and folders, including empty ones. |
| /SECFIX | Fixes security permissions on already copied files (you can leave this out if you want) |
| /COPYALL | Copies all files attributes including NTFS permissions. |
| /R:0 | Number of times to retry copying a failed file. |
| /W:0 | Wait time between retries. Defaults to 30 seconds. |
| /LOG:file | Logs output into the givenfile. |
| /TEE | Logs output to console and logfile. |

You can always see a full list of switches with `/?`.

## Parsing RoboCopy error log

With RoboCopy we now get parseable log files and can use this nifty [script from the Technet Gallery][2] to extract all failed files from the logs.

{{< gist Silthus a54f82aa0036b74b6f588fdcedad3e5e >}}

&nbsp;

 [1]: /xcopy-files-keeping-ntfs-permissions-ignoring-errors/
 [2]: https://gallery.technet.microsoft.com/scriptcenter/Powershell-script-to-parse-a1bc8a92