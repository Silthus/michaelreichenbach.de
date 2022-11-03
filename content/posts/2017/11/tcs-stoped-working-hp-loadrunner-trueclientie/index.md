---
title: Workaround for TCS has stopped working with HP Loadrunner TruClientIE
date: 2017-11-16
url: /posts/tcs-stoped-working-hp-loadrunner-trueclientie/
featured_image: banner.png
categories:
  - System Administration
tags:
  - HP Loadrunner
cover:
  image: banner.png
---
When using HP Loadrunner 12 and above with TruClientIE there is a known issue that the TCS process stops working after a couple of minutes.

{{< figure src="banner.png" >}}

Running a normal scenario with 10 VUsers will cause the scenario to fail after about 20 to 30 minutes, because there will be no more virtual users left to run the scenario.

While this problem is still existent in HP Loadrunner 12.01 as of 04.12.2014 there is a workaround to allow the execution of scenarios that need to run stable and without crashing after about 20 minutes.

The workaround consist out of two things. The first is to create a “**Goal oriented** -> **Scenario**” instead of a “Manual scenario”.

{{< figure src="new_scenario-300x132.png" caption="Creating a goal oriented scenario." >}}

Go to the scenario settings (Edit Scenario Goal) and choose the**Goal Type** “Virtual Users”. Now define the **amount of VUsers** you need for your performance test and the **runtime** of your scenario.  
You can also specify the interval and amount of VUsers that will be initialized when the scenario starts.

{{< figure src="scenario_settings_1-300x244.png" caption="Defining the duration of the scenario." >}}

{{< figure src="scenario_settings_2-300x244-1.png" caption="Setting the startup interval of the VUsers." >}}

Here the scenario will run for **30 minutes** with a total of **10 VUsers**, starting **2 VUsers every 10 seconds**.

Now when you start the scenario and a VUsers fails with the **TCS has stopped working**error message a new VUser will take its place.  
However you will still have to click aways the Windows Error message dialog box or otherwise the process won’t be stopped and no new VUser will be initiated.

To work around this we are going to supress the Windows Error Notifications by modifying the **Local Group Policy Settings**. Go to start and type in **gpedit.msc** to open the Local Group Policy Settings.

Now inside the Local Group Policy Settings go to:

Computer Configuration **->** Administrative Templates **->** Windows Components **-> Windows Error Reporting**

Set “**Prevent display of the user interface for critical errors”** to **Enabled**.

{{< figure src="gpo-300x275-1.png" caption="Disabling the display of error notifications." >}}

Now when you start the scenario it will run for the complete duration without showing the **TCS has stopped working notification** and will recover the crashed VUsers automatically.

Happy load testing :)
