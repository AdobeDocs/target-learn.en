---
title: Add Parameters to the Requests
description: In this lesson we will validate Adobe lifecycle metrics and add custom parameters to the prefetch request. The lifecycle metrics and custom parameters will be used for creating audiences that determine new and returning users. We will also enhance the third location request (found on the thank you screen) with parameters that will be used to determine the user's trip origin & x`destination so we can later serve an offer based on those parameters.

feature: mobile
kt: 3040
audience: developer
doc-type: tutorial
activity-type: implement
---

# Add Parameters to the Requests

In this lesson we will add and validate Adobe lifecycle metrics and custom parameters the Target requests added in the previous lesson. The lifecycle metrics and custom parameters will be used for creating audiences that determine new and returning users.

## Learning Objectives

At the end of this lesson, you will be able to:

* **Add and Validate the Adobe Lifecycle Metrics Request (used for creating audiences later)**
* **Add Parameters to the Prefetch Request (used for creating audiences later)**
* **Add Parameters to the Live Location (used for creating audiences later)**
* **Validate the Parameters for Both Requests**

## Add the Lifecycle Parameters

The Config.collectLifecycleData function found in the onResume() function enables the [Adobe mobile lifecycle metrics](https://docs.adobe.com/content/help/en/mobile-services/android/metrics.html). This request adds parameters to location requests, including the prefetch request. We'll build audiences in the next lesson using data that the lifecycle request provides.

To enable lifecycle metrics, add the Config.collectLifecycleData to the onResume() function in your HomeActivity:
![Lifecycle Request](assets/lifecycle_code.jpg)

### Validate the Lifecycle Parameters for the Prefetch Request

Run the Emulator and use Logcat to validate the lifecycle parameters. Filter for "prefetch" to find the prefetch response and look for the new parameters:
![Lifecycle Validation](assets/lifecycle_validation.jpg)

## Add the at_property Parameter to the Prefetch Request

Adobe Target Properties are defined in the Target interface and are used to establish boundaries for personalizing apps and websites. The at_property parameter identifies the specific property where your offers and activities are accessed and maintained. We'll add a property to the prefetch and live location requests.

>!NOTE You may or may not see the Properties options in the Target interface, depending on your license. If you don't have these options, just skip ahead to the next section of this lesson.

You can retrieve your at_property value in the Target interface under Setup > Properties.  Hover over the property, select the code snippet icon and copy the at_property value:
![Copy at_property](assets/at_property_interface.jpg)

Add it as a parameter for each location in the prefetch request like this:
![Add at_property parameter](assets/params_at_property.jpg)
Here is the updated code for the targetPrefetchContent() function:

```java
public void targetPrefetchContent() {
        List<TargetPrefetchObject> prefetchList = new ArrayList<>();

        Map<String, Object> params1;
        params1 = new HashMap<String, Object>();
        params1.put("at_property", "your at_property value goes here");

        prefetchList.add(Target.createTargetPrefetchObject(Constant.wetravel_engage_home, params1));
        prefetchList.add(Target.createTargetPrefetchObject(Constant.wetravel_engage_search, params1));
        Target.TargetCallback<Boolean> prefetchStatusCallback = new Target.TargetCallback<Boolean>() {
            @Override
            public void call(final Boolean status) {
                HomeActivity.this.runOnUiThread(new Runnable() {
                    @Override
                    public void run() {
                        String cachingStatus = status ? "YES" : "NO";
                        System.out.println("Received Response from prefetch : " + cachingStatus);
                        engageMessage();
                        setUp();

                    }
                });
            }};
        Target.prefetchContent(prefetchList, null, prefetchStatusCallback);
    }
```

### Note About Parameters

<!--Show in general how to add other parameters (locationParams & profileParams) -->
For future projects, you may want to implement additional parameters. The createTargetPrefetchObject() method allows three types of parameters: locationParams, orderParams, and productParams. Here is the syntax for the createTargetPrefetchObject() method:

```java
public static TargetPrefetchObject createTargetPrefetchObject(
final String locationName,
final Map<String, Object> locationParams)
final Map<String, Object> orderParams,
final Map<String, Object> productParams)
```

Also note that different location parameters can be added to each location in the prefetch request. For example, you could create another Map called param2, put a new parameter in it, then set param2 in one location and param1 with the other location in the createTargetPrefetchObject function. Here's an example:

```java
public static TargetPrefetchObject createTargetPrefetchObject(
prefetchList.add(Target.createTargetPrefetchObject(location1_name, params1);
prefetchList.add(Target.createTargetPrefetchObject(location2_name, params2);
```

## Validate the at_property Parameter in the Prefetch Request

Now run the emulator and use Logcat to verify that the at_property is showing on the prefetch request and response for both locations:
![Validate the at_property parameter](assets/parameters_at_property_validation.jpg)

## Add Custom Parameters to the Live Location Request

The third location (wetravel_context_dest) was already loaded in real-time and validated in the previous lesson, so it's ready to display an offer. This location will display a relevant banner offer on the final confirmation screen when a user books a trip. Before we move on to build the offer, we need the at_property and two custom location parameters for this request to identify the trip source and destination. In the next lesson, we'll use these parameter values to build personalized offers. Add the following parameters to the targetLoadRequest() function in the ThankYouActivity controller:
![Add Parameters to the Live Location Request](assets/parameters_live_location.jpg)
Here is the updated code for the targetLoadRequest() function:

```java
public void targetLoadRequest(final ArrayList<Recommandation> recommandations) {
    Map<String, Object> locationParams = new HashMap<>();
    locationParams.put("at_property","add your at_property value here");
    locationParams.put("locationSrc", (""+Utility.getInSharedPreference(ThankYouActivity.this,Constant.departure,"")));
    locationParams.put("locationDest", (""+Utility.getInSharedPreference(ThankYouActivity.this,Constant.destination,"")));

    Target.loadRequest(Constant.wetravel_context_dest, "", null, null, locationParams, new Target.TargetCallback<String>() {
        @Override
        public void call(final String response) {
        try {
            runOnUiThread(new Runnable() {
                @Override
                public void run() {
                    AppDialogs.dialogLoaderHide();
                    filterRecommendationBasedOnOffer(recommandations, response);
                    recommandationbAdapter.notifyDataSetChanged();
                }
            });
        } catch (Exception e) {
            e.printStackTrace();
        }
        }
    });
    Target.clearPrefetchCache();
}
```

### Validate the Custom Parameters in the Live Location Request

Run the emulator and open Logcat. Filter for one of the parameters to verify that the request contains the needed parameters:
![Validate the Custom Parameters in the Live Location Request](assets/parameters_live_location_validation.jpg)

## About Order Confirmation Parameters

Although not used in this demo project, order details will need to be tracked in a live app so Target can use order details as metrics/dimensions. To add order parameters (along with location & profile parameters), use this syntax with the Target.loadRequest() method:

```java
Map<String, Object> profileParams = new HashMap<String, Object>();
profileParams.put("profile-parameter-key", "profile-parameter-value");

Map<String, Object> orderParams = new HashMap<String, Object>();
orderParams.put("order-parameter-key", "order-parameter-value");

Map<String, Object> locationParams = new HashMap<String, Object>();
locationParams.put("mbox-parameter-key", "mbox-parameter-value");

Target.loadRequest("locationName", "defaultContent", profileParams, orderParams, locationParams, new TargetCallback<String>() {
    @Override
    public void call (String item) {
       Log.d("Target Content", item);
    }
});
```

## About Analytics for Target (A4T)

Adobe Analytics can be configured as the reporting source for Target. This allows all metrics/dimensions collected by the Target SDK to be viewed in Adobe Analytics. See the [A4T Overview](https://docs.adobe.com/content/help/en/target/using/integrate/a4t/a4t.html) for more details.

## Conclusion

Nice work! Now that parameters are in place, we're ready to use those parameters to create audiences and offers in Adobe Target.

<!--Add this style for CTA on all pages-->
**[NEXT : "Create Audiences and Offers" >](create-audiences-and-offers.md)**
<!--Rename segments to audiences in file & titles-->