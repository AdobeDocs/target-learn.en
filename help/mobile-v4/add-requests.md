---
title: Add Adobe Target Requests
seo-title: Add Adobe Target Requests
description: The Adobe Mobile Services SDK (v4) provides Adobe Target methods & functionality that enable you to personalize your app with different experiences for different users.   
seo-description: The Adobe Mobile Services SDK (v4) provides Adobe Target methods & functionality that enable you to personalize your app with different experiences for different users.
feature: mobile
kt: kt-3040
audience: developer
doc-type: tutorial
activity-type: implement
---

# Add Adobe Target Requests

The Adobe Mobile Services SDK (v4) provides Adobe Target methods & functionality that enable you to personalize your app with different experiences for different users.

In this lesson, you will prepare the We.Travel app for personalization by implementing multiple Target requests.

## Prerequisites

Be sure to [download and update the We.Travel app](download-and-update-the-sample-app.md).

## Learning Objectives

At the end of this lesson, you will be able to:

* **Cache Multiple Target Locations Using a Batch Prefetch Request**
* **Load Prefetched Target Locations**
* **Load a Target Location in Real-Time (non-prefetched)**
* **Clear Prefetched Locations from Cache**
* **Validate Prefetched Locations & a Live Location in Android Studio**

## Terminology

Below is some of key Target terminology that we will be using in this tutorial.

* **Request:**  a network request to the Adobe Target servers
* **Location:**  a placeholder for Target offers
* **Offer:**  a snippet of code, defined in the Target user interface (or with API), which is delivered in the response. Usually JSON when Target is used in native mobile apps.
* **Batch Request:**  a single request that includes multiple locations
* **Prefetch Request:**  a single request that retrieves offers and caches them into memory for future use in the app
* **Batch Prefetch Request:**  a single request that prefetches offers for multiple locations
* **Audience:**  a group of visitors defined in the Target interface or shared to Target from other Adobe applications (e.g. “iPhone X visitors”, “visitors in the California”, “First App Open”
* **Activity:**  a Target construct, defined in the Target user interface (or with API) which links locations, offers and Audiences to create a personalized experience.

## Add a Batch Prefetch Request

Our first scenario on We.Travel is a batch prefetch request with two Target locations to the Home Screen. In a later lesson, we'll configure offers for these locations that display messages to help guide new users through the booking process. For now, we'll use the locations as placeholders for the offers.

A prefetch request fetches Target locations as minimally as possible by caching Adobe Target server responses. A batch prefetch request retrieves and caches multiple locations. All prefetched locations are cached on the device for future use in the user session. By prefetching multiple locations on the Home Screen, we can retrieve offers for later use as the user navigates through the app. Refer to the [prefetch documentation](https://docs.adobe.com/content/help/en/mobile-services/android/target-android/c-mob-target-prefetch-android.html) for more details on prefetch methods.

We'll start with the HomeActivity controller (the Home Screen's source code), which is located under app > main > java > com.wetravel > Controller. We'll add the two code blocks shown in red:

![HomeActivity Prefetch Code](assets/homeactivity.jpg)

Scroll down to the end of the HomeActivity's code and add the code provided below after the setHeader() function:

```java
@Override
protected void onResume() {
    super.onResume();
    Config.collectLifecycleData(this);
    targetPrefetchContent();
}

public void targetPrefetchContent() {
    List<TargetPrefetchObject> prefetchList = new ArrayList<>();
    prefetchList.add(Target.createTargetPrefetchObject(Constant.wetravel_engage_home, null));
    prefetchList.add(Target.createTargetPrefetchObject(Constant.wetravel_engage_search, null));
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
    Target.prefetchContent(prefetchList, null, prefetchStatusCallback);
}
```

### Batch Prefetch Request Code Explanation

| Code | Description |
|--- |--- |
| Config.collectLifecycleData(this) | Enables collection of [mobile lifecycle metrics](https://docs.adobe.com/content/help/en/mobile-services/android/metrics.html). We will use lifecycle metrics in the next lesson. |
| targetPrefetchContent() | Retrieves and caches two Target locations. The first time a request is sent, the Target Server will create a location name which we will use later in the Target interface. |
| Constant.wetravel\_engage\_home | Prefetched Target location which will later be loaded & display its offer content on the Home Screen |
| Constant.wetravel\_engage\_search | Prefetched Target location which will later be loaded & display its offer content on the Search Results Screen. Since this is a second location in the prefetch, this prefetch request is called a "prefetch batch request". |
| setUp() | Renders the app's home screen after the Target offers are prefetched |

### About Asynchronous vs. Synchronous

In this scenario, the prefetch request runs synchronously as a blocking call, just before the app's home screen renders. Note how setUp() is called after the prefetch request. This can be beneficial in many scenarios because it ensures that Target offers are available before the app's screen renders. To allow the requests load asynchronously (in the background), just call setUp() within the onCreate() function instead.

### Validate the Batch Prefetch Request

Open the Android Emulator in Android Studio. The following examples use the Pixel 2 on Android Q (version 9+, API level 29). The prefetch response should read "prefetch response received":

When the Home screen renders, the prefetch request should be loaded. With Logcat, filter for "Target" to see the request & response:

![Validate the requests on the Home Screen](assets/prefetch_validation.jpg)

If you are not seeing a successful response, verify settings in the ADBMobileConfig.json file and code syntax in the HomeActivity file.

Two locations are now cached to the device. The location names are also created on the Target server which will make them visible in the Target interface.

## Add a Real-time Request

Our next scenario is to load a live location placeholder on the Thank You screen. The request that we add here will serve an offer that depends on the user's trip destination, so this will need to be a real-time location. Target needs to determine the right offer at the time of the booking. A prefetched cached offer won't work here, since we wouldn't know the user's destination before they had selected it.

Now let's add a real-time location placeholder on the Thank You screen. In the ThankYouActivity file, we'll add the code shown in red:

![Add a Real-time location on the Thank You Screen](assets/thankyou.jpg)

Scroll to the end of the ThankYouActivity file and add this code below as shown above:

```java
// Add this line to the getRecommandations() function:
targetLoadRequest(recommandation.recommandations);

// Add this code block after the filterRecommendationBasedOnOffer() function:
public void targetLoadRequest(final ArrayList<Recommandation> recommandations) {
    Target.loadRequest(Constant.wetravel_context_dest, "", null, null, null, new Target.TargetCallback<String>() {
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
}

```

### targetLoadRequest() Code Explanation

| Code | Description |
|--- |--- |
| targetLoadRequest() | This function fires Target.loadRequest() which loads & displays the wetravel\_context\_dest location |
| Constant.wetravel\_context\_dest | This is the location that will display offers to the user (we'll configure the offer content in a later lesson) |

### Validate the Real-time Request

Open the Android Emulator and go through all the steps to book a trip: Home > Bus Search Results > Seat Selection, Payment Options (any payment option with blank data will work).

On the final Thank You screen, watch Logcat for the response. The response should read "Default content was returned for "wetravel\_context\_dest":

![Add a Real-Time location on the Thank You Screen](assets/thankyou_validation.jpg)

## Clearing Prefetched Locations from Cache

There may be situations where prefetched locations need to be cleared during a session. For example, when a booking occurs, it makes sense to clear the cached locations since the user is now "engaged" and understands the booking process. If they book another trip during their session, they won't need the original locations on the home screen & search results screen to guide their booking. It would make more sense to clear the locations from cache and prefetch new locations for perhaps a discounted second booking or another relevant scenario. Logic could be added to the home screen & search results screen to prefetch new locations if a booking has taken place during the session.

For this example, we'll just clear prefetched locations for the session when a booking takes place. This is done by calling the Target.clearPrefetchCache() function. Set the function inside the targetLoadRequest() function as shown below:

![Clear Prefetched Locations from Cache](assets/clearPrefetch.jpg)

Congratulations! Your app now has the framework for personalization. In the next lesson, you'll be adding parameters to these locations. This will enhance the locations and provide more data-driven insights to optimize the app.

**[NEXT : "Add Parameters" >](add-parameters.md)**
