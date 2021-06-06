---
title: Windows Subsystem for Linux (WSL) behind Proxy
author: Michael
type: post
date: 2017-12-13T11:41:50+00:00
url: /windows-subsystem-linux-behind-proxy/
featured_image: /wp-content/uploads/2017/12/pexels-photo-577585.jpeg
classic-editor-remember:
  - classic-editor
categories:
  - Programming
  - System Administration
tags:
  - linux
  - vscode
  - wsl

---
Recently I came accross the issue of wanting to install apt packages in WSL behind a corporate proxy. Plus I wanted to update my yarn package by using &#8220;curl -o- -L https://yarnpkg.com/install.sh | bash&#8221; which also needs to go through the proxy.

The solution is the same as if we want to set the proxy in a standard Ubuntu. So simply create a proxy.conf inside the apt config folder as follows.

<pre><span>vi /etc/apt/apt.conf.d/proxy.conf
# add the following line (press i to insert and escape followed by :x to save)
Acquire::http::Proxy "<a href="http://myproxy:myproxyport/" rel="nofollow">http://username:password@myproxy:myproxyport</a>";
</span></pre>

Aditionally we need to set the proxy for curl. For that we create or modify an user specific <span>~/.curlrc file in our homefolder.</span>

<pre>cd ~/
vi <span>.curlrc
# insert the following line
<code>proxy = &lt;proxy_host&gt;:&lt;proxy_port&gt;</code></span></pre>

Thats it. You are now using apt and curl through your corporate proxy.