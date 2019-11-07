---
title: 
description: 
feature: mobile
kt: kt-3040
audience: developer
doc-type: tutorial
activity-type: implement
---

# Personalize Layouts

## Load the First Location on the Home Screen

The first Location will be displayed on the home screen. In the HomeActivity file, we'll add the code shown in red:

![Load the First Location on the Home Screen](assets/home_offer.jpg)

Add the engageMessage() function to the targetPrefetchContent() function as shown above. Add the code below at the end of the file as shown above:

```java
public void engageMessage() {
    Target.loadRequest(Constant.wetravel_engage_home, "", null, null, null,
            new Target.TargetCallback<String>(){
                @Override
                public void call(final String s) {
                    runOnUiThread(new Runnable() {
                        @Override
                        public void run() {
                            System.out.println("Engage Message : " + s);
                            if(s != null && !s.isEmpty()) Utility.showToast(getApplicationContext(), s);
                        }
                    });
                }
            });
}
```

### engageMessage() Code Explanation

| Code | Description |
|--- |--- |
| engageMessage() | This function fires Target.loadRequest() which loads the wetravel\_engage\_home Location |

## Validate the First Location

Now let's make sure the Location is loading correctly. Open the Android Emulator, then open Logcat & filter for "engage". Watch the logs for the response. It should read "Default content was returned for "wetravel_engage_home":

![Validate the Home Screen Location](assets/home_offer_validation.jpg)

If you are not seeing a successful response, verify settings in the ADBMobileConfig.json file and code syntax in the HomeActivity file.

## Load the Second Location on the Search Results Screen

Now we'll load the second Location from cache on the Search Results Screen. We'll add the code blocks in red to the SearchBusActivity file:

![Load the Second Location on the Search Results Screen](assets/searchBusActivity.jpg)

Scroll down to the end of the SearchBusActivity file and add the code below after the setTravelSelectable() function:

```java
@Override
public void onResume() {
    super.onResume();
    engageMessage();
}

public void engageMessage() {
    Target.loadRequest(Constant.wetravel_engage_search, "", null, null, null,
            new Target.TargetCallback<String>(){
                @Override
                public void call(final String s) {
                    runOnUiThread(new Runnable() {
                        @Override
                        public void run() {
                            System.out.println("Engage Message : " + s);
                            if(s != null && !s.isEmpty()) Utility.showToast(getApplicationContext(), s);
                        }
                    });
                }
            });
}
```

## Validate the Second Location

With the Emulator, select a departure & destination on the Home Screen and tap "Find Bus". Watch Logcat for the Target response when the Search Results Screen renders:

![Validate the Offer on the Search Results Screen](assets/prefetch_validation2.jpg)

* The "wetravel\_engage\_search" response should read "Default content was returned for "wetravel\_engage\_search" (default content is returned since this is the first request to the server & there is no offer content configured yet).

If you are not seeing success responses, verify settings in the ADBMobileConfig.json file and code syntax in the SearchBusActivity file.
