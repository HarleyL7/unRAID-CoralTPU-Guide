# unRAID-CoralTPU-Guide w/ CodeProject.AI
This guide is compiled from multiple sites and with the help of multiple sources. When setting up my Google Coral TPU, I spent a good amount of time searching for how to all across the internet. 

# Hardware Installation

* USB Accelerator - https://coral.ai/products/accelerator/
* M.2 Accelerator B+M key - https://coral.ai/products/m2-accelerator-bm/
* M.2 Accelerator with Dual Edge TPU - https://coral.ai/products/m2-accelerator-dual-edgetpu/

If using the M.2 Accelerator with Dual Edge TPU you might have to use adapters to make it work with your system. These are located here:
* https://www.makerfabs.com/dual-edge-tpu-adapter.html
* https://www.makerfabs.com/dual-edge-tpu-adapter-m2-2280-b-m-key.html

Simply install the TPU in your system and boot up your unRAID server.

# unRAID Coral Drivers Installation

First you must make sure you have the community applications installed. This can be done by going here: https://forums.unraid.net/topic/38582-plug-in-community-applications/

Go to the APPs tab:

![APPs](APPs.png)

In the search bar type: coral accelerator module drivers

![search](search.JPG)

Once installed, you can go to SETTINGS > CORAL DRIVER and if unRAID can see your TPU then you will see something like this:

![driver](driver.JPG)

# CodeProject.AI Docker Install

Go back to the APPS TAB in unRAID and search for Codeproject

![cpai](cpai.JPG)

Click on it and press install. It will take you to a page that looks like this:

We need to pass through our Coral TPU - Click "Add another Path, Port Variable, Label or Device"

![docker](docker.PNG)

Change Config Type to "Device"

![config](config.PNG)

For Value:
* USB - /dev/bus/usb
* M.2 - /dev/apex_0
* Dueal Edge TPU - /dev/apex_0

Press ADD
Then press APPLY
It will pull the image and run the docker run command and you should have an output similiar to this: 
![cmdexec](cmdexec.PNG)

# CodeProject.AI Coral Module Installation

This is where a lot of issues arrive and this will probably be updated with new releases of CPAI. The module does not like to be installed. There are other work arounds, but the one that worked for me was to stop all ObjectDetection modules, Uninstall Coral Module, and re-install Coral Module until it worked via watching in the system log tab. If there are any "pip" error messages then try and reinstall until sucessful. Credit for this work around goes to PeteUK on the codeproject discusions. 
This will most likely change once CPAI is updated.

The PIP errors will look something like this: 

![error](error.PNG)

Turn off all Object Detection Modules

![off](off.PNG)

Uninstall Coral Module

![uninstall](uninstall.PNG)

Go back to "Install Modules" and re-install Coral Module. Make sure to watch the server log to see if it worked without any PIP errors. 

This is what a bad install looks like

![badinstall](badinstall.PNG)

And this is what a good install looks like

![goodinstall](goodinstall.PNG)

Once we acheive a good install, we can move on. Head back to Status Tab and enable the ObjectDetection(Coral)

Now you should see this "Edge TPU detected" in the log and at the bottom "CPU" should have changed to "GPU(TPU)

![detect](detect.PNG)

# Summary

This should get you started and fully installed. Issues I have noticed so far in my limited testing. The last step of re-installing multiple times (Average of three for me) seems to be required on every restart. This is problematic and this is a known issue on the CodeProject Discussions. Hopefully it will be fixed asap. I will be looking into the other work arounds mentioned on the discussion. If they work, I will add them here.


