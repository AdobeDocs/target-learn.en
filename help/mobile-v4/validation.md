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
  ![](assets/mobile-launch-install-openProject.png)
* Open the build.gradle file at the root of the We.Travel Android folder <!--where to validate the SDK Install. Is it pre-installed at https://github.com/adobe-target/sample-app-android/tree/SDKv4?-->
* Open the ADBMobileConfig.json file to the assets folder in your project
* Update the ADBMobileConfig.json file to you use your own the target.clientCode value set to the correct value for your implementation
  ![](assets/insert_screenshot.png)
* Verify that the correct [Target Classes & Methods](https://docs.adobe.com/content/help/en/mobile-services/android/target-android/c-target-methods.html) are implemented with the correct Target location names (previously known as mboxes)<!--how do they do this if no requests have been added yet?-->

## Implement a Global Pre-Fetch Location

<!--Why is this here and not in the lesson to add requests?-->
<!--Where does one add this to the sample app? Any general recommendations about where to put this-->
A prefetchContent location uses the Android Mobile SDKs to fetch offer content as few times as possible by caching the server responses. Creating a prefetch request with an array of locations can be configured to call the Target server and retrieve content for many locations at once.  All content will be retrieved and cached, and will then be retrievable from the cache by all future calls for this content for the specified location names.  Additional location names can be added to this array, as appropriate, to support the increased scope and sophistication of the install.

Additional details - [Prefetch offer content in Android](https://docs.adobe.com/content/help/en/mobile-services/android/target-android/c-mob-target-prefetch-android.html)

### prefetchContent() Code

Here is the syntax of the Target.prefetchContent() Java request to be installed: <!--where should this be added to the sample app? need a screenshot showing the code in context-->
<!--shouldn't this start really simple without any querystring parameters? why is the at_property parameter included? because it is needed for the account Nimit gave them access to? Pare this down-->

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
