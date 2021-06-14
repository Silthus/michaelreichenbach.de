---
title: 'How-To: Configure Google Chrome Extensions with Windows GPO'
author: silthus
type: post
date: 2019-09-20T19:56:54+00:00
url: /how-to-configure-google-chrome-extensions-with-windows-gpo/
categories:
  - System Administration
page:
  theme: full
toc:
  enable: true
resources:
- name: featured-image
  src: banner.jpg

---
I recently worked on a project where we needed to create a fully self configuring mounted wall display solution that could be zero touch deployed across the company. You can read more about the full solution in my upcoming blog post.

In this post I will highlight one piece of that solution: the Google Chrome Extension that can be configured with Windows Group Policy (GPO).

## Update 25.01.2020

The following section is obsolete! There is now a chrome extension that does tab rotation for enterprises with a zero touch approach. You can find it here: [Silthus/chrome-enterprise-tab-rotate][5]

## Preparing the Chrome Extension

Chrome Extensions need a policy schema.json and use the managed storage API for this to work. Unfortunately almost no chrome extension provides this. So I had to implement this myself in an existing open source extension. For the dashboard solution I forked the great [chrome-tab-rotate extension from KevinSheedy][4] and added the required schema and managed storage API code.

### How to compile the Chrome Extension

You can find my fork here: [Silthus/chrome-tab-rotate][1]

  1. clone my fork
  2. run npm install and gulp
  3. open your favorite Chromium browser
  4. go to extensions and enable developer mode  
     {{< figure src="chromium_developer_mode.png" caption="Enable the chrome developer mode." >}}
  5. click on &#8220;Load unpacked&#8221; and select the &#8220;build&#8221; directory

The plugin is now loaded and ready to use. The last thing you need is the ID of the plugin. This ID will be different for everyone but will stay the same for subsequent builds. That is, if you use the build.pem created from your first build.

{{< figure src="chrome_tab_rotate_id.png" >}}

You can now use the chrome extension and configure it with your registry.

## Configuring the Chrome Extension with GPOs

To make creating the GPO easier, I will first create the matching registry entry and use that inside the GPO.

### Preparing the registry

Start and open the registry as administrator. Navigate to the following registry hive and create all keys that do not exist. Make sure to replace the ID with your own extension ID.

```text
HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Google\Chrome\3rdparty\extensions\gfjcoadgcaljefmlmokgadacckjipikb_\policy
```

Inside this hive you can start creating items that match the extension policy. Open <chrome://policy> or schema.json to find out what properties your can set. In my case I wanted to set the **source** and **url** parameter. With those parameters the plugin will automatically load my config at startup.

{{< figure src="chrome_tab_rotate_registry.png" class="wide-width" >}}

### Creating the GPO

Open `gpmc.msc` go to **Computer** -> **Configuration** -> **Preferences** -> **Windows Settings** -> **Registry** and select **New** -> **Registry Wizard** in the context menu.

{{< figure src="gpp-registry-wizard.jpg" class="wide-width" >}}

Now choose the items created earlier and load them into the GPO.

## What&#8217;s next?

Now you might be wondering how you will get the custom compiled extension onto your clients? Don&#8217;t worry, I got you covered in my next blog post where I will explain how to host and deploy custom extensions without uploading them to the store.

Additional resources:

* [chrome-tab-rotate fork source code][1]
* [Chromium documentation about policies][2]
* [Great article about creating registry items in GPOs][3]

 [1]: https://github.com/Silthus/chrome-tab-rotate
 [2]: https://www.chromium.org/administrators/configuring-policy-for-extensions
 [3]: http://woshub.com/how-to-create-modify-and-delete-registry-keys-using-gpo/
 [4]: https://github.com/KevinSheedy/chrome-tab-rotate
 [5]: https://github.com/Silthus/chrome-enterprise-tab-rotate