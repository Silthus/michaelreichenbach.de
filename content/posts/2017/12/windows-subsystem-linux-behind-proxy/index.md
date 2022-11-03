---
title: Windows Subsystem for Linux (WSL) behind Proxy
date: 2017-12-13
url: /posts/windows-subsystem-linux-behind-proxy/
categories:
  - Programming
  - System Administration
  - Windows
tags:
  - linux
  - vscode
  - wsl
  - wsl2
  - windows
---
## Windows Subsystem for Linux (WSL) behind Proxy

Recently I came accross the issue of wanting to install apt packages in WSL behind a corporate proxy. Plus I wanted to update my yarn package by using `curl -o- -L https://yarnpkg.com/install.sh | bash` which also needs to go through the proxy.

The solution is the same as if we want to set the proxy in a standard Ubuntu. So simply create a proxy.conf inside the apt config folder as follows.

```bash
vi /etc/apt/apt.conf.d/proxy.conf
```

```conf
# add the following line (press i to insert and escape followed by :x to save)
Acquire::http::Proxy http://username:password@myproxy:myproxyport;
```

Aditionally we need to set the proxy for curl. For that we create or modify an user specific `~/.curlrc` file in our homefolder.

```bash
vi ~/.curlrc
```

```bash
# insert the following line
proxy = <proxy_host>:<proxy_port>;
# for example
# proxy = my-proxy:8080
```

Thats it. You are now using apt and curl through your corporate proxy.
