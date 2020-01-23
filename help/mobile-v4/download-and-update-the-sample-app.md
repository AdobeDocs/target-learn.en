---
title: Download and Update the We.Travel Sample App
seo-title: Download the sample app and verify the mobile services SDK
description: The We.Travel sample app is pre-implemented with the Adobe Mobile Services SDK v4. You just need to update it so it points to your own Experience Cloud Org and solution accounts.   
seo-description: The We.Travel sample app is pre-implemented with the Adobe Mobile Services SDK v4. You just need to update it so it points to your own Experience Cloud Org and solution accounts.
feature: mobile
kt: 3040
audience: developer
doc-type: tutorial
activity-type: implement
---

# Download and Update the We.Travel Sample App

The We.Travel sample app is pre-implemented with the Adobe Mobile Services SDK v4. You just need to update it so it points to your own Experience Cloud Org and solution accounts.

## Learning Objectives

At the end of this lesson, you will be able to:

* Download and Open the We.Travel sample app in Android Studio
* Verify & Update the Mobile Services SDK Settings for Target

## Download the We.Travel App

* Download the [We.Travel App](https://github.com/adobe-target/sample-app-android/tree/SDKv4)
* Open the app in Android Studio as an existing project
* Run the app in an emulator to confirm that the app builds and you can see the home screen

![Open the app](assets/wetravel_homeScreen.png)

## Verify & Update the Mobile Services SDK Settings for Target

The Adobe Mobile Services SDK has been preinstalled within the We.Travel app [according to the documentation](https://docs.adobe.com/content/help/en/mobile-services/android/getting-started-android/requirements.html). Now you will update the installation to point to your own Target account.

First, obtain your company settings for Adobe Target from the Mobile Services user interface:

1. Log in to the [Adobe Mobile Services interface](https://mobilemarketing.adobe.com)
1. Add a new app to use for this tutorial, using an Analytics report suite with non-production data
1. Add your Target Client Code (you can find it in the Target interface under Setup > Implementation > Edit Settings, next to the Download at.js button)
1. Enable the Visitor ID Service and make sure your Organization is selected in the drop-down
1. Save your changes
1. Scroll to the App SDK Downloads section at the bottom of the page and download the Config File:

![Download the Config File](assets/config_file.jpg)

Replace the ADBMobileConfig.json file in your Android Studio project assets folder (app > src > main > assets).

Now open the ADBMobileConfig.json file and make sure it contains the expected changes such as your Target Client Code and your Analytics details:
![Download the Config File](assets/client_code.jpg)

We will validate the configuration by validating Target requests in the next module.

**[NEXT : "Add Target Requests" >](add-requests.md)**
