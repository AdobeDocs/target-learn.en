---
title: How to Validate Adobe Target for your mobile app
seo-title: How to Validate Adobe Target for Your Mobile App
description: The Adobe Target SDK can be validated on your mobile app by debugging Target server calls in an Android Emulator.   
seo-description:
feature: mobile
kt: kt-3040
audience: developer
doc-type: tutorial
activity-type: implement
---

# Download, Validate, and Update the We.Travel Sample App

The We.Travel sample app is pre-implemented is the Adobe Mobile Services SDK v4. You just need to update it so it points to your own Experience Cloud Org and solution accounts.

## Learning Objectives

At the end of this lesson, you will be able to:

* Download and Open the We.Travel sample app in Android Studio
* Update the Target Client Code to use your own Target account
* Add a request to the sample app
* Validate the request using Logcat

## Download the We.Travel App

* Download the [We.Travel App](https://github.com/adobe-target/sample-app-android/tree/SDKv4)

## Verify the SDK Implementation

The Adobe Mobile Services SDK, has been preinstalled within the We.Travel app [according to the documentation](https://docs.adobe.com/content/help/en/mobile-services/android/getting-started-android/requirements.html).  Before proceeding with setting up our initial Target call, let's verify the SDK implementation steps.

* Open Android Studio
* Select "Open an existing Android Studio Project"
  ![NEEDS ALT TEXT](assets/mobile-launch-install-openProject.png)
* Open the build.gradle file at the root of the We.Travel Android folder <!--where to validate the SDK Install. Is it pre-installed at https://github.com/adobe-target/sample-app-android/tree/SDKv4?-->
* Open the ADBMobileConfig.json file in the assets folder of the project
* Update the ADBMobileConfig.json file to you use your own the target.clientCode and otehr account values set to the correct value for your implementation
  ![NEEDS ALT TEXT](assets/insert_screenshot.png)
* Verify that the correct [Target Classes & Methods](https://docs.adobe.com/content/help/en/mobile-services/android/target-android/c-target-methods.html) are implemented with the correct Target location names (previously known as mboxes)<!--how do they do this if no requests have been added yet?-->

[Next "Add Target Requests" >](add-requests.md)
