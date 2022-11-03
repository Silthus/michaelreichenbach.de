---
title: Getting started with kubectl for Azure AKS on Windows
date: 2017-11-29
url: /posts/getting-started-kubectl-azure-aks-windows/
featured_image: banner.png
categories:
  - System Administration
tags:
  - azure
  - kubernetes
cover:
  image: banner.png
---
In this post you will learn how you can launch the [Kubernetes Web UI Dashboard][1] from you Windows Bash connected to the new [Azure AKS service][2].

## Install the Windows Subsystem for Linux

Before we get started with kubectl, we need to install the &#8220;Windows Subsystem for Linux&#8221;. This will enable us to run a bash shell and connect us to the Azure AKS environment.

To enable the &#8220;Windows Subsystem for Linux&#8221; feature run the following command in an elevated PowerShell and restart your computer if prompted.

```powershell
Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Windows-Subsystem-Linux
```

For details on how to enable the Bash on Windows, follow the [Microsoft Installation Guide][3].

## Install Azure CLI for Bash on Windows

<ol class="lf-text-block lf-block" data-lf-anchor-id="5a2d22b01415efdc7319ccde04e6ed63:0">
  <li>
    Open the Bash shell.
  </li>
  <li>
    Modify your sources list. <pre><code class="lang-bash">&lt;span class="hljs-built_in">echo&lt;/span> &lt;span class="hljs-string">"deb [arch=amd64] https://packages.microsoft.com/repos/azure-cli/ wheezy main"&lt;/span> | \
     sudo tee /etc/apt/sources.list.d/azure-cli.list
</code></pre>
  </li>
  
  <li>
    Run the following sudo commands: <pre><code class="lang-bash">sudo apt-key adv --keyserver packages.microsoft.com --recv-keys 52E16F86FEE04B979B07E28DB02C46DF417A0893
sudo apt-get install apt-transport-https
sudo apt-get update && sudo apt-get install azure-cli
</code></pre>
  </li>
  
  <li>
    Run the CLI from the command prompt with the<span> </span><code>az</code><span> </span>command.
  </li>
</ol>

## Install Kubernetes CLI kubectl

Open Bash for Windows and run the following sudo command.

<pre>sudo az aks install-cli</pre>

After kubectl is installed you need to login into your Azure account and connect  to the correct subscription.

<pre>az login</pre>

List all your Azure subscriptions and connect  to the one holding your AKS cluster.

<pre>az account list -o=table
az account set --subscription="SubName"</pre>

Start the Web UI Admin Dashboard and browse it on http://localhost:8001/

<pre>az aks browse -g MyResourceGroupName -n MyClusterName</pre>

Browse the Web UI Dashboard on http://localhost:8001/.

Happy orchestrating your AKS Kubernetes cluster 🙂

 [1]: https://kubernetes.io/docs/tasks/access-application-cluster/web-ui-dashboard/
 [2]: https://docs.microsoft.com/azure/aks/
 [3]: https://msdn.microsoft.com/commandline/wsl/install_guide
 [4]: https://www.mirenoba.com/2017/11/29/getting-started-kubectl-azure-aks-windows/