---
title: XCopy files keeping NTFS permissions and ignoring errors
date: 2018-02-28
url: /posts/xcopy-files-keeping-ntfs-permissions-ignoring-errors/
categories:
  - System Administration
tags:
  - tools
  - windows
  - ntfs
  - xcopy
---
XCopy is a very useful tool included in all versions of Windows. With XCopy you can copy large amounts of data with ease. Plus it has a switch that lets you copy over the NTFS permissions.

## Creating an initial full copy with XCopy

```powershell
xcopy "C:\Source Folder" "F:\Destination Folder" /X /H /E /V /C
```

## Copy files and folders that changed since initial copy

```powershell
xcopy "C:\Source Folder" "F:\Destination Folder" /X /H /E /V /D /Y /C
```

### Explanation of XCopy switches

| Parameter | Description |
| --------- | ----------- |
| /? | Shows a list of all possible XCopy commands. |
| /X | Copies file audit settings and file ownership and ACL information. |
| /H | Copies hidden and system files. |
| /E | Copies directories and subdirectories, including empty ones. |
| /V | Verifies each new file. |
| /D | Copies files changed on or after the specified date (D:m-d-y). If no date is given, copies only those files whose source time is newer than the destination time. |
| /Y | Suppresses prompting to confirm you want to overwrite an existing destination file. |
| /C | Continues copying even if errors occur. |

The [full XCopy documentation][1] can be found at microsoft.

 [1]: https://docs.microsoft.com/en-us/windows-server/administration/windows-commands/xcopy