---
title: Download and Update the We.Travel Sample App
seo-title: Download the sample app and verify the mobile services SDK
description: The We.Travel sample app is pre-implemented with the Adobe Mobile Services SDK v4. You just need to update it so it points to your own Experience Cloud Org and solution accounts.   
seo-description: The We.Travel sample app is pre-implemented with the Adobe Mobile Services SDK v4. You just need to update it so it points to your own Experience Cloud Org and solution accounts.
feature: mobile
kt: kt-3040
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

## Verify & Update the Mobile Services SDK Settings for Target

The Adobe Mobile Services SDK has been preinstalled within the We.Travel app [according to the documentation](https://docs.adobe.com/content/help/en/mobile-services/android/getting-started-android/requirements.html).

First, make sure the SDK is configured properly with your company settings for Adobe Target in Android Studio:

1. Log in to the [Adobe Mobile Services interface](https://mobilemarketing.adobe.com)
2. Add a new app (if not already done)
3. Add your Target Client Code (you can find it in the Target interface under Setup > Implementation > Edit Settings (next to the Download at.js button)
4. Select the new app from the top left drop-down
5. Select "Manage App Settings" (or gear icon)
6. Scroll to the bottom and download the Config File:

![Download the Config File](assets/config_file.jpg)

Add (or replace) the ADBMobileConfig.json file in your Android Studio project assets folder (app > src > main > assets).

Now open the ADBMobileConfig.json file and make sure your "Client Code" is added. If it's not already added, you can find it in the Target interface under Setup > Implementation > Edit Settings (next to the Download at.js button).
![Download the Config File](assets/client_code.jpg)

## Import Target Classes

The remaining lessons will use Adobe Target Java classes and functions for personalization. Import the Target classes at the top of the HomeActivity as shown in red below:

![Import the Target Classes](assets/import.jpg)

We will validate the configuration by validating Target requests in the next module.

### [NEXT : "Add Target Requests" >](add-requests.md)
