---
title: Workaround for TCS has stopped working with HP Loadrunner TruClientIE
author: Michael
type: post
date: 2017-11-16T13:52:47+00:00
url: /tcs-stoped-working-hp-loadrunner-trueclientie/
featured_image: /wp-content/uploads/2017/11/tcs_stopped-300x145-1.png
categories:
  - System Administration
tags:
  - HP Loadrunner

---
When using HP Loadrunner 12 and above with TruClientIE there is a known issue that the TCS process stops working after a couple of minutes.

<div id="attachment_7" class="wp-caption aligncenter">
  <p>
    <img loading="lazy" src="https://i1.wp.com/michaelreichenbach.de/wp-content/uploads/2017/11/tcs_stopped-300x145-1-300x145.png?resize=300%2C145&#038;ssl=1" alt="" width="300" height="145" class="aligncenter wp-image-33 size-medium" srcset="https://i0.wp.com/michaelreichenbach.de/wp-content/uploads/2017/11/tcs_stopped-300x145-1.png?resize=300%2C145&ssl=1 300w, https://i0.wp.com/michaelreichenbach.de/wp-content/uploads/2017/11/tcs_stopped-300x145-1.png?w=517&ssl=1 517w" sizes="(max-width: 300px) 100vw, 300px" data-recalc-dims="1" />
  </p>
</div>

Running a normal scenario with 10 VUsers will cause the scenario to fail after about 20 to 30 minutes, because there will be no more virtual users left to run the scenario.

While this problem is still existent in HP Loadrunner 12.01 as of 04.12.2014 there is a workaround to allow the execution of scenarios that need to run stable and without crashing after about 20 minutes.

The workaround consist out of two things. The first is to create a “**Goal oriented**<span> </span>**scenario**” instead of a “Manual scenario”.

<div id="attachment_8" class="wp-caption aligncenter">
  <div id="attachment_26" style="width: 310px" class="wp-caption aligncenter">
    <img aria-describedby="caption-attachment-26" loading="lazy" class="wp-image-26 size-medium" src="https://i1.wp.com/michaelreichenbach.de/wp-content/uploads/2017/11/new_scenario-300x132-300x132.png?resize=300%2C132&#038;ssl=1" alt="" width="300" height="132" data-recalc-dims="1" /></p> 
    
    <p id="caption-attachment-26" class="wp-caption-text">
      Creating a goal oriented scenario
    </p>
  </div>
</div>

Go to the scenario settings (Edit Scenario Goal) and choose the<span> </span>**Goal Type**<span> </span>“Virtual Users”. Now define the<span> </span>**amount of VUsers**<span> </span>you need for your performance test and the<span> </span>**runtime**<span> </span>of your scenario.  
You can also specify the interval and amount of VUsers that will be initialized when the scenario starts.

<div id="attachment_9" class="wp-caption aligncenter">
  <div id="attachment_27" style="width: 310px" class="wp-caption aligncenter">
    <img aria-describedby="caption-attachment-27" loading="lazy" class="wp-image-27 size-medium" src="https://i0.wp.com/michaelreichenbach.de/wp-content/uploads/2017/11/scenario_settings_1-300x244-300x244.png?resize=300%2C244&#038;ssl=1" alt="" width="300" height="244" data-recalc-dims="1" /></p> 
    
    <p id="caption-attachment-27" class="wp-caption-text">
      Defining the duration of the scenario
    </p>
  </div>
</div>

<div id="attachment_10" class="wp-caption aligncenter">
  <div id="attachment_30" style="width: 310px" class="wp-caption aligncenter">
    <img aria-describedby="caption-attachment-30" loading="lazy" src="https://i2.wp.com/michaelreichenbach.de/wp-content/uploads/2017/11/scenario_settings_2-300x244-1-300x244.png?resize=300%2C244&#038;ssl=1" alt="Setting the startup interval of the VUsers" width="300" height="244" class="wp-image-30 size-medium" data-recalc-dims="1" /></p> 
    
    <p id="caption-attachment-30" class="wp-caption-text">
      Setting the startup interval of the VUsers
    </p>
  </div>
</div>

Here the scenario will run for<span> </span>**30 minutes**<span> </span>with a total of<span> </span>**10 VUsers**, starting<span> </span>**2 VUsers every 10 seconds**.

Now when you start the scenario and a VUsers fails with the<span> </span>**TCS has stopped working**error message a new VUser will take its place.  
However you will still have to click aways the Windows Error message dialog box or otherwise the process won’t be stopped and no new VUser will be initiated.

To work around this we are going to supress the Windows Error Notifications by modifying the<span> </span>**Local Group Policy Settings**. Go to start and type in<span> </span>**gpedit.msc**<span> </span>to open the Local Group Policy Settings.

Now inside the Local Group Policy Settings go to:

Computer Configuration<span> </span>**->**<span> </span>Administrative Templates<span> </span>**->**<span> </span>Windows Components<span> </span>**-> Windows Error Reporting**

Set “**Prevent display of the user interface for critical errors”**<span> </span>to<span> </span>**Enabled**.

<div id="attachment_11" class="wp-caption aligncenter">
  <div id="attachment_31" style="width: 310px" class="wp-caption aligncenter">
    <img aria-describedby="caption-attachment-31" loading="lazy" src="https://i0.wp.com/michaelreichenbach.de/wp-content/uploads/2017/11/gpo-300x275-1-300x275.png?resize=300%2C275&#038;ssl=1" alt="Disabling the display of error notifications" width="300" height="275" class="wp-image-31 size-medium" data-recalc-dims="1" /></p> 
    
    <p id="caption-attachment-31" class="wp-caption-text">
      Disabling the display of error notifications
    </p>
  </div>
</div>

Now when you start the scenario it will run for the complete duration without showing the<span> </span>**TCS has stopped working notification**<span> </span>and will recover the crashed VUsers automatically.

Happy load testing<span> </span><img src="https://i0.wp.com/web.archive.org/web/20150801190955im_/http://michaeldoering.com/wp-includes/images/smilies/icon_smile.gif?w=750&#038;ssl=1" alt=":)" class="wp-smiley" data-recalc-dims="1" />