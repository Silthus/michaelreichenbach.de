---
title: 'How-To: Configure Google Chrome Extensions with Windows GPO'
author: Michael Reichenbach
type: post
date: 2019-09-20T19:56:54+00:00
url: /how-to-configure-google-chrome-extensions-with-windows-gpo/
categories:
  - System Administration

---
I recently worked on a project where we needed to create a fully self configuring mounted wall display solution that could be zero touch deployed across the company. You can read more about the full solution in my upcoming blog post.

In this post I will highlight one piece of that solution: the Google Chrome Extension that can be configured with Windows Group Policy (GPO).

## Preparing the Chrome Extension

**[Update 25.01.2020]: The following section is obsolete! There is now a chrome extension that does tab rotation for enterprises with a zero touch approach. You can find it here: <https://github.com/Silthus/chrome-enterprise-tab-rotate>**

Chrome Extensions need a policy schema.json and use the managed storage API for this to work. Unfortunately almost no chrome extension provides this. So I had to implement this myself in an existing open source extension. For the dashboard solution I forked the great <a href="https://github.com/KevinSheedy/chrome-tab-rotate" style="color: #999999;">chrome-tab-rotate extension from KevinSheedy</a> and added the required schema and managed storage API code.

### How to compile the Chrome Extension

You can find my fork here: <a href="https://github.com/Silthus/chrome-tab-rotate" style="color: #999999;">https://github.com/Silthus/chrome-tab-rotate</a>

  1. clone my fork
  2. run npm install and gulp
  3. open your favorite Chromium browser
  4. go to extensions and enable developer mode  
     {{< figure src="chromium_developer_mode.png" caption="Enable the chrome developer mode." >}}
    <span style="color: #999999;"><img loading="lazy" src="https://i1.wp.com/michaelreichenbach.de/wp-content/uploads/2019/09/chromium_developer_mode.png?resize=586%2C211&#038;ssl=1" alt="Shows how to enable chromium developer mode" width="586" height="211" class="size-full wp-image-180 aligncenter" srcset="https://i1.wp.com/michaelreichenbach.de/wp-content/uploads/2019/09/chromium_developer_mode.png?w=586&ssl=1 586w, https://i1.wp.com/michaelreichenbach.de/wp-content/uploads/2019/09/chromium_developer_mode.png?resize=300%2C108&ssl=1 300w" sizes="(max-width: 586px) 100vw, 586px" data-recalc-dims="1" /></span>
  5. <span style="color: #999999;">click on &#8220;Load unpacked&#8221; and select the &#8220;build&#8221; directory</span>

<span style="color: #999999;">The plugin is now loaded and ready to use. The last thing you need is the ID of the plugin. This ID will be different for everyone but will stay the same for subsequent builds. That is, if you use the build.pem created from your first build.<img loading="lazy" src="https://i2.wp.com/michaelreichenbach.de/wp-content/uploads/2019/09/chrome_tab_rotate_id.png?resize=404%2C210&#038;ssl=1" alt="" width="404" height="210" class="size-full wp-image-181 aligncenter" srcset="https://i2.wp.com/michaelreichenbach.de/wp-content/uploads/2019/09/chrome_tab_rotate_id.png?w=404&ssl=1 404w, https://i2.wp.com/michaelreichenbach.de/wp-content/uploads/2019/09/chrome_tab_rotate_id.png?resize=300%2C156&ssl=1 300w" sizes="(max-width: 404px) 100vw, 404px" data-recalc-dims="1" /></span>

<span style="color: #999999;">You can now use the chrome extension and configure it with your registry.</span>

## Configuring the Chrome Extension with GPOs

To make creating the GPO easier, I will first create the matching registry entry and use that inside the GPO.

### Preparing the registry

Start and open the registry as administrator. Navigate to the following registry hive and create all keys that do not exist. Make sure to replace the ID with your own extension ID.

**HKEY\_LOCAL\_MACHINE\SOFTWARE\Policies\Google\Chrome\3rdparty\extensions\_<span style="color: #0000ff;">gfjcoadgcaljefmlmokgadacckjipikb</span>_\policy**

Inside this hive you can start creating items that match the extension policy. Open <chrome://policy> or schema.json to find out what properties your can set. In my case I wanted to set the **source** and **url** parameter. With those parameters the plugin will automatically load my config at startup.

<img loading="lazy" src="https://i1.wp.com/michaelreichenbach.de/wp-content/uploads/2019/09/chrome_tab_rotate_registry.png?resize=750%2C327&#038;ssl=1" alt="Shows the configured registry" width="750" height="327" class="size-large wp-image-182 aligncenter" srcset="https://i1.wp.com/michaelreichenbach.de/wp-content/uploads/2019/09/chrome_tab_rotate_registry.png?resize=1024%2C446&ssl=1 1024w, https://i1.wp.com/michaelreichenbach.de/wp-content/uploads/2019/09/chrome_tab_rotate_registry.png?resize=300%2C131&ssl=1 300w, https://i1.wp.com/michaelreichenbach.de/wp-content/uploads/2019/09/chrome_tab_rotate_registry.png?resize=768%2C334&ssl=1 768w, https://i1.wp.com/michaelreichenbach.de/wp-content/uploads/2019/09/chrome_tab_rotate_registry.png?w=1162&ssl=1 1162w" sizes="(max-width: 750px) 100vw, 750px" data-recalc-dims="1" /> 

### Creating the GPO

Open gpmc.msc go to **Computer <span></span>****Configuration**<span> -> </span>**Preferences**<span> -> </span>**Windows Settings**<span> -> </span>**Registry**<span> and select </span>**New**<span> -> </span>**Registry Wizard<span> </span>**<span>in the context menu.</span>

<img loading="lazy" src="https://i0.wp.com/michaelreichenbach.de/wp-content/uploads/2019/09/gpp-registry-wizard.jpg?resize=750%2C528&#038;ssl=1" alt="Registry wizard context menu" width="750" height="528" class="aligncenter size-full wp-image-184" srcset="https://i0.wp.com/michaelreichenbach.de/wp-content/uploads/2019/09/gpp-registry-wizard.jpg?w=800&ssl=1 800w, https://i0.wp.com/michaelreichenbach.de/wp-content/uploads/2019/09/gpp-registry-wizard.jpg?resize=300%2C211&ssl=1 300w, https://i0.wp.com/michaelreichenbach.de/wp-content/uploads/2019/09/gpp-registry-wizard.jpg?resize=768%2C540&ssl=1 768w" sizes="(max-width: 750px) 100vw, 750px" data-recalc-dims="1" /> 

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