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

# Adobe Target Mobile Implementation

## Overview

Implementing Target Mobile on your Android™ application needn't be a complicated or lengthy effort. This walkthrough will demonstrate the steps and thought processes behind this powerful implementation.

The walkthrough covers a comprehensive mobile Target implementation, showcasing different Target scenarios and customizations. The step-by-step exercise and foundational information will help you implement Target Mobile and understand its value.  A demo Android app is provided for you to complete the walkthrough, so you can learn the underlying techniques in a safe environment- Download the [We.Travel App here](https://github.com/Adobe-Marketing-Cloud/busbooking-mobileapps).  After successful completion, you should be ready to work through your own use cases and start implementing within your Android app!

After completing this walkthrough you will be able to:

* Validate the [Adobe Mobile Services SDK](https://docs.adobe.com/content/help/en/mobile-services/android/getting-started-android/requirements.html) setup
* Setup Target calls in the following Scenarios:
  * Global Pre-Fetch of all Targeted content
  * Blocking call (Runs before App display)
  * Non-Blocking call (Runs in the background)
  * Real-Time (non-caching)
  * Cache Busting Re-Fetch
* Work with Run-Time & Mobile specific Parameters
* Feature Flagging (Using Target to roll out new features)
* Personalizing Layouts & Offers
  * Including Geolocation
* Target Recommendations

## Prerequisites

With this walkthrough, it is assumed that you have an Adobe Id and the required Target permissions to complete the exercises. If not, you may need to reach out to your Experience Cloud Administrator to request access.

* For Target, you must have approver-level access to the Adobe Target interface
* Know your Adobe Client ID to direct Target calls to your own account

### Tools

* Download and Install [Android Studio](https://developer.android.com/studio/install)
* Download the [We.Travel App](https://github.com/Adobe-Marketing-Cloud/busbooking-mobileapps)

It is also assumed that you are familiar with Android development in Java.  You will get more out of this walkthrough if you can comfortably read and understand code.

The foundational step of the Adobe Target implementation, the mobile SDK, has been preinstalled within this demo app.  But before proceeding in setting up the Global mbox, let's verify the SDK implementation steps.

## Verify the SDK Implementation

The foundational step of the Adobe Target implementation, the Adobe Mobile Services SDK, has been preinstalled within the We.Travel app.  But before proceeding with setting up our initial Target call, let's verify the SDK implementation steps.

* Download and add the [Adobe Mobile Services SDK](https://docs.adobe.com/content/help/en/mobile-services/android/getting-started-android/requirements.html) to your project
* Add the ADBMobileConfig.json file to the assets folder in your project
* Verify that that ADBMobileConfig.json file has the target.clientCode value set to the correct value for your implementation
* Verify that the correct [Target Classes & Methods](https://docs.adobe.com/content/help/en/mobile-services/android/target-android/c-target-methods.html) are implemented with the correct Target location names (previously known as mboxes)

## Implement a Global Pre-Fetch Location

A prefetchContent location uses the Android Mobile SDKs to fetch offer content as few times as possible by caching the server responses. Creating a prefetch request with an array of locations can be configured to call the Target server and retrieve content for many locations at once.  All content will be retrieved and cached, and will then be retrievable from the cache by all future calls for this content for the specified location names.  Additional location names can be added to this array, as appropriate, to support the increased scope and sophistication of the install.

Additional details - [Prefetch offer content in Android](https://docs.adobe.com/content/help/en/mobile-services/android/target-android/c-mob-target-prefetch-android.html)

### prefetchContent() Code

Here is the syntax of the Target.prefetchContent() Java request to be installed:

```java
public void targetPrefetchContent() {
    List<TargetPrefetchObject> prefetchList = new ArrayList<>();
    Map<String, Object> profileParameters;
    profileParameters = new HashMap<String, Object>();
    profileParameters.put("ProfileParam18Sep", "1");
    Map<String, Object> travelParameters1 = new HashMap<String, Object>();
    travelParameters1.put("travelParam18Sep", "1");
    travelParameters1.put("at_property", "7962ac68-17db-1579-408f-9556feccb477");
    prefetchList.add(Target.createTargetPrefetchObject("travelTest3", travelParameters1));
    Target.TargetCallback<Boolean> prefetchStatusCallback = new Target.TargetCallback<Boolean>() {
        @Override
        public void call(final Boolean status) {
            HomeActivity.this.runOnUiThread(new Runnable() {
                @Override
                public void run() {
                    String cachingStatus = status ? "YES" : "NO";
                    System.out.println("Received Response from prefetch : " + cachingStatus);
                    setUp();
                }
            });
        }};
    Target.prefetchContent(prefetchList, profileParameters, prefetchStatusCallback);
}
```

## How to Validate Adobe Target (SDK v4) for your mobile app

Now that the SDK is implemented and our initial globalprefetch location call has been setup, let's validate the requests & responses from the Adobe Target Servers.  The Adobe Target SDK can be validated on your mobile app by using an Android Emulator & reviewing verbose logging in your Android IDE environment. This article demonstrates how to use the Android Studio IDE to debug Target server calls for the Adobe Mobile Services SDK version 4.  

### Validate with an Emulator

Android Studio's Android Emulator & Logcat feature can be used to validate requests & responses from the Adobe Target servers. If you're using a different IDE such as Eclipse, logging should follow a similar process. Importing your own Android app into Android Studio to use the Logcat feature will allow the same validation.  

#### Debug Requests & Responses with Logcat

* In Android Studio, select the Logcat console (View > Tool Windows > Logcat OR select the Logcat tab @ the bottom of the screen)
* On the Logcat filter bar, select "Verbose" and set the filter keyword to "adbmobile" (note: if the filter menu doesn't show, try setting the console to a floating window: Window > Active Tool Window > Floating Mode)
* Run the Android Emulator and look for the Target request and response. "Response received" indicates that the server connection and response was successful:

![Finding the request in Logcat](  assets/logcat_example.jpg)  

* Remove the "adbmobile" filter and note any connection errors. Most errors are likely caused from incorrect request syntax or configuration. Proxy settings in the Emulator settings can also cause connection errors.  

#### Verify the Target Activity in the UI

If an Activity is already created in the Target UI, the location requested in the Target SDK call (if successful) can be seen in the location drop-down menu under Activities > (Select Activity Name) > Edit Activity > Experiences:

If no Activity has not yet created, create a new one:

* Select Activities > Create Activity
* Select the Activity Type (such as A/B Test)
* Select Mobile App
* Select "Form" as the Experience Composer
* Select the Workspace & Property
* The location drop-down on a selected Experience shows the locations that are registered:

![Locations will show in interface dropdowns in the Form Composer](  assets/target_location_dropdown2.jpg)

### Response Details Example

Here are the details of the response from the Logcat console (expanded JSON view for readability):

```java
{
"requestId":"4988228c-8430-4e33-b3ca-37ce82e3a90c",
"client":"ecserverside",
"id":
  {
  "tntId":"111568817282645-907045.28_29",
  "marketingCloudVisitorId":"34552764763276759957814173181896264559"
  },
"edgeHost":"mboxedge28.tt.omtrdc.net",
"contentAsJson":false,
"prefetchResponses":
  [{
  "mbox":"travelTest3",
  "parameters":  
    {
    "a.ltv.amount":"0",
    "MboxParam18Sep":"1",
    "at_property":"7962ac68-17db-1579-408f-9556feccb477"
    },
  "content":"{\"id\":\"1\",\"bannersToDisplay\":\"blue_green\"}",
  "eventTokens":["iuniIAuYUHON1jhC+7UzfmqipfsIHvVzTQxHolz2IpSCnQ9Y9OaLL2gsdrWQTvE54PwSz67rmXWmSnkXpSSS2Q=="],
  "clientSideAnalyticsLoggingPayload":{"pe":"tnt","tnta":"308228:0:0|2"}
  }]
}
```

The main key/value pairs to validate and check for accuracy are listed below:

| Key | Value |
|--- |--- |
| client | your Adobe Target clientCode value - unique to your environment  |
| tntId | primary identifier in Target for an individual user |
| prefetchResponses | for prefetch requests: this object list locations (mboxes) that are prefetched and cached into device memory and any profile parameters included in the request |
| at_property | the Target property from which mboxes (locations) are served. This value is found in the Target interface under Setup > Properties > (select the property of the offer) > (code box) |
| mbox | the location identifier used in Activities in Adobe Target  |
| content | for prefetch requests:  content delivered to the specified mbox |

#### JSON Offers: Common Errors

For JSON Offers:  If the request appears to be sending properly, but continues to return default content, check all the parameters in the Target.loadRequest call. If the "targetParameters" value is empty for a JSON offer request, default content will be returned:

![Default content returned in the response](  assets/error1.jpg)

To correct this, make sure the at_property is defined and set in the loadRequest. This ensures the offer is being served from the correct Target property.

![Make sure the at_property parameter is defined if using workspaces](  assets/mboxparam1.jpg)

The correct Target property is found in the target property is found in the Target interface under Setup > Properties > select the property of the offer.

#### JSON Offer Conversion

The Target.loadRequest method returns an offer in String format. If you're displaying a JSON offer, it needs to be converted from String to JSON after a response is returned in order to parse or reference items within the JSON object.
