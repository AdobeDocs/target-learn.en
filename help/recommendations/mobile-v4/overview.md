---
title: Adobe Target location request scenarios
seo-title: Adobe Target location request scenarios
description: Adobe Target mobile SDK methods can be used to display Target locations in several scenarios.
---

# Adobe Target Location Request Scenarios

The Adobe Mobile Services SDK version 4 provides Adobe Target methods & functionality that enable you customize your mobile app implementation and tailor it for different experiences.

* **Request using a Prefetch "Blocking"**
* **Request using a Live Location**
* **Request Multiple Target Locations in one Call**
* **Requests combining Prefetch & Live Locations**
* **Clearing Prefetched Locations from Cache**

## We.Travel App

This article discusses multiple scenarios using a sample travel app. The app has a search feature that finds available bus routes. The app will be used for demonstration purposes.

* Target locations are prefetched on the home screen, so no Target content appears, but locations are cached in the device behind the scene
* The search results screen loads a Target location and displays banners based off a JSON offer loaded from the Target server. 
![](images/travel_app2.jpg)

## Use a Prefetch "Blocking" Request

Configuring Target methods as prefetch "blocking" requests provides two main benefits:

* The prefetch method call Target in the "background". It caches locations (mboxes) in device memory for quick access later in the session. This avoids excessive requests to the server & results in a faster app experience.
* A "Blocking" request enables Target content to load into the app before other app content is loaded.

In the code examples below, the changes were made to the main activity of the We.Travel app. The result is an app launch with Target prefetching before any other content loads.

A prefetch blocking request can be set up in an Android Activity by moving the app's content layout methods from the onCreate() method to a separate method that Target calls after a location request.

### Code Example:  Move app layout logic to a new method

```java
// Move the setContentView() method (and other app layout logic) from
// onCreate() into a new setUp() function:

private void setUp() {
    setContentView(R.layout.activity_home);
    // add other logic for app setup
}
```

#### Code Example:  Call setUp() AFTER Target callback  

```java
// Add a call to setUp() at the end of the Target location or prefetch call.
// This example loads a prefetch request and then calls setUp():

public void targetPrefetchContent() {
    List<TargetPrefetchObject> prefetchList = new ArrayList<>();
    Map<String, Object> profileParameters;
    profileParameters = new HashMap<String, Object>();
    profileParameters.put("ProfileParam18Sep", "1");
    Map<String, Object> mboxParameters1 = new HashMap<String, Object>();
    mboxParameters1.put("MboxParam18Sep", "1");
    mboxParameters1.put("at_property", "7962ac68-17db-1579-408f-9556feccb477");
    prefetchList.add(Target.createTargetPrefetchObject("mboxTest3", mboxParameters1));
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

## Use a Live Location Request

On the bus results screen, if we wanted to display an offer related to the bus destination, a live location request should be called for that offer instead of a prefetched location. This is because the offer needs to be changed depending on where the user wants to travel to. Prefetched locations could be used with other elements on the screen not related to the destination (like general discounts or promotions). 

### JSON Offers

This demo uses JSON offers to determine which banners to display. In the Target interface, create JSON offers for each experience:

![](images/json_offers.jpg)

#### Code Example

A live location request is called with the **Target.loadRequest()** method. This request below calls the JSON offer, retrieves an ID element from the JSON object, and uses that ID to determine the right assets to display.

```java
// SINGLE MBOX SCENARIO - JSON OFFER
public void targetLoadRequest() {
    Map<String, Object> mboxParam;
    mboxParam = new HashMap<String, Object>();
    mboxParam.put("at_property", "7962ac68-17db-1579-408f-9556feccb477");
    Target.loadRequest("mboxTest3", "----default_mbox----", null, null, mboxParam, new Target.TargetCallback<String>() {
        @Override
        public void call(final String s) {
            SearchBusActivity.this.runOnUiThread(new Runnable() {
                @Override
                public void run() {
                    try {
                        JSONObject obj = new JSONObject(s);
                        banner_id = obj.getInt("id");
                    } catch (
                            Throwable t) {
                        Log.e("My App", "Could not parse malformed JSON: \"" + s + "\"");
                    }

                    setUpSearch();
                    getSearchData();

                }
            });
        }
    });
}

```

In the demo app's getSearchData() method, add the returned banner_id (and the next banner if desired):

```java
// FIND BANNER DETERMINED BY ADOBE TARGET OFFER
searchOffersList.add(offerList.get(banner_id));
searchOffersList.add(offerList.get(banner_id+1));
//searchOffersList.addAll(offerList);
searchOffersAdapter.notifyDataSetChanged();
```

## Request Multiple Target Locations in one Call

To display multiple mboxes on the Bus Results Screen, multiple target locations can be requested in a single call. In this example, we'll display one mbox in the top offer area of the screen, and another mbox just above the bus search results.

Multiple mboxes are built & displayed as follows:

* Create a TargetRequestObject for each location
* Add each TargetRequestObject to an Array
* Add the Array to the **Target.loadRequests()** method and call the locations

### Code Example

Here is an example from the Bus Results activity. The code is called from the activity's onResume() method. Note that the parameters for the createTargetRequestObject() method are in a different order than the targetLoadRequest() method.

```java
// MULTIPLE MBOX SCENARIOS- 2 JSON OFFERS
public void targetLoadRequests() {

// Create Multiple Target Location Requests & send in one loadRequests() call

// 1st Location
Map<String, Object> mboxParam;
mboxParam = new HashMap<String, Object>();
mboxParam.put("at_property", "7962ac68-17db-1579-408f-9556feccb477");
TargetRequestObject request1 = Target.createTargetRequestObject("mboxTest3", "--mboxTest3_default--", mboxParam, null, null, new Target.TargetCallback<String>() {
    @Override
    public void call(final String s) {
        SearchBusActivity.this.runOnUiThread(new Runnable() {
            @Override
            public void run() {
                try {
                    JSONObject obj = new JSONObject(s);
                    banner_id = obj.getInt("id");
                } catch (
                        Throwable t) {
                    Log.e("My App", "Could not parse malformed JSON: \"" + s + "\"");
                }
            }
        });
    }
});

// 2nd Location
TargetRequestObject request2 = Target.createTargetRequestObject("mboxTest4", "--mboxTest4_default--", mboxParam, null, null, new Target.TargetCallback<String>() {
@Override
public void call(final String s) {
    SearchBusActivity.this.runOnUiThread(new Runnable() {
        @Override
        public void run() {
            try {
                // Get JSON Offer name
                JSONObject obj2 = new JSONObject(s);
                String offer2_name = obj2.getString("offer2_name");
                Log.d("Sent:", s);

                // Get 2nd banner based on JSON offer name & display above Bus results
                ImageView target_banner = findViewById(R.id.target_banner);
                int offer2_id = getResources().getIdentifier(offer2_name, "drawable", getPackageName());
                target_banner.setImageResource(offer2_id);
            } catch (
                    Throwable t) {
                Log.e("My App", "Could not parse malformed JSON: \"" + s + "\"");
            }
        }
    });
}
});

// Create Array of both requests
List<TargetRequestObject> locationRequests = new ArrayList<>();
locationRequests.add(request1);
locationRequests.add(request2);

// Send Location Requests
Target.loadRequests(locationRequests, null);
setUpSearch();

}
```

#### Result

2 Target locations are displayed on the screen:

![](images/2mboxes.jpg)

## Combining Prefetch & Live Location Requests

The scenario above (Request Multiple Target Locations in one Call) also demonstrates how to request a prefetched location ("mboxTest3<!---->" was prefetched on the home screen) and a live location request from the server, both in a single call. This can be done with the **Target.loadRequests()** method.

## Clearing Prefetched Locations from Cache

Suppose a special add-on offer was prefetched and cached on the booking > seating screen. A user may revisit that screen later. However, if the user decides to change the bus line during the app session, the prefetched offer should be cleared so a new offer for the new bus line can display. All prefetched locations are cleared with the **Target.clearPrefetchCache()** method.
