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

The We.Travel sample app is pre-implemented with the Adobe Mobile Services SDK v4. You just need to update it, so that it points to your own Experience Cloud Org and solution accounts.

## Learning Objectives

At the end of this lesson, you will be able to:

* Download and Open the We.Travel sample app in Android Studio
* Verify & Update the Mobile Services SDK Settings for Target

## Download the We.Travel App

* Download the [sample-app-android-SDKv4-Base-Version.zip](https://github.com/adobe-target/sample-app-android/archive/SDKv4-Base-Version.zip)
* Decompress the zip file
* Open the app in Android Studio as an existing project (ignore any errors about "Invalid VCS root mapping")
* Run the app in an emulator to confirm that the app builds and you can see the home screen
* Browse the app and verify that you can complete the booking process (select any payment optin and just hit "Proceed" to skip over the billing screen!)

    ![Open the app](assets/wetravel_homeScreen.png)![Confirmation screen](assets/wetravel_confirmationScreen.png)

## Verify & Update the Mobile Services SDK Settings for Target

The Adobe Mobile Services SDK has been preinstalled within the We.Travel app [according to the documentation](https://docs.adobe.com/content/help/en/mobile-services/android/getting-started-android/requirements.html). Now you will update the installation to point to your own Target account.

First, create a new App in the Mobile Services user interface:

1. Log in to the [Adobe Mobile Services interface](https://mobilemarketing.adobe.com)
1. Go to the Manage Apps and click "Add" to add a new app to use with this tutorial (Manage Apps > Add)
1. Choose an an Analytics report suite with non-production data, give the app a name, select the "Standard" type and click "Save"
1. Once the app has been added, add your Target Client Code on the next screen in the "SDK Target Options" section (you can find your client code in the Target interface under Setup > Implementation > Edit Settings, next to the Download at.js button)
1. The "Request Timeout" setting determines how long the app will wait for the response from the Target server before executing timeout instructions. Just leave the default setting.
1. Enable the "Visitor ID Service" and make sure your Organization is selected in the drop-down
1. Save your changes by clicking the Save button on the top right side of the window (not the one in the "Universal Links and App Links Options" or "Push Services" section)
1. Scroll to the App SDK Downloads section at the bottom of the page and download the Config File:

    ![Download the Config File](assets/config_file.jpg)

1. Replace the ADBMobileConfig.json file in your Android Studio project assets folder (app > src > main > assets).

1. Now open the ADBMobileConfig.json file and make sure it contains the expected changes such as your Target Client Code and your Analytics details:
    ![Download the Config File](assets/client_code.jpg)

If you don't see your settings, please confirm that you clicked the right "Save" button in the Mobile Services interface and copied the file to the correct location.

Congratulations! You've updated the SDK with your Target account details! We will do additional validation of the configuration after we add Target requests in the next lesson.

**[NEXT : "Add Target Requests" >](add-requests.md)**
