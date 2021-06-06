---
title: XCopy files keeping NTFS permissions and ignoring errors
author: Michael
type: post
date: 2018-02-28T13:26:17+00:00
url: /xcopy-files-keeping-ntfs-permissions-ignoring-errors/
featured_image: /wp-content/uploads/2018/02/pexels-photo-117729.jpeg
hestia_layout_select:
  - default
categories:
  - System Administration

---
XCopy is a very useful tool included in all versions of Windows. With XCopy you can copy large amounts of data with ease. Plus it has a switch that lets you copy over the NTFS permissions.

## Creating an initial full copy with XCopy

<pre><span class="crayon-r">xcopy</span><span class="crayon-h"> </span><span class="crayon-s">"C:\Source Folder"</span><span class="crayon-h"> </span><span class="crayon-s">"F:\Destination Folder"</span><span class="crayon-h"> </span><span class="crayon-o">/</span><span>X <span class="crayon-o">/</span>H<span class="crayon-h"> </span><span class="crayon-o">/</span>E </span><span class="crayon-o">/</span><span>V /C
</span></pre>

## <span>Copy files and folders that changed since initial copy</span>

<pre><span class="crayon-r">xcopy</span><span class="crayon-h"> </span><span class="crayon-s">"C:\Source Folder"</span><span class="crayon-h"> <span class="crayon-s">"F:\Destination Folder" <span class="crayon-o">/</span><span>X</span> <span class="crayon-o">/</span><span>H </span></span></span><span class="crayon-h"><span class="crayon-o">/</span><span>E</span> <span class="crayon-o">/</span><span>V</span> <span class="crayon-o">/</span><span>D</span> <span class="crayon-o">/</span><span>Y </span></span><span>/C
</span></pre>

### <span>Explanation of XCopy switches</span><span class="crayon-h"></span>

<span>/? – Shows a list of all possible XCopy commands.<br /> /X – Copies file audit settings and file ownership and ACL information.</span>  
<span>/H – Copies hidden and system files.</span>  
<span>/E – Copies directories and subdirectories, including empty ones.</span>  
<span>/V – Verifies each new file.<br /> </span><span>/D – Copies files changed on or after the specified date (D:m-d-y). If no date is given, copies only those files whose source time is newer than the destination time.</span>  
<span>/Y – Suppresses prompting to confirm you want to overwrite an existing destination file.<br /> /C – Continues copying even if errors occur.<br /> </span>

&nbsp;

The [full XCopy documentation][1] can be found at microsoft.

 [1]: https://docs.microsoft.com/en-us/windows-server/administration/windows-commands/xcopy