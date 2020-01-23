---
title: Create Audiences and Offers in Adobe Target
seo-title: Create Audiences and Offers in Adobe Target
description: In this lesson, we'll build audiences and offers in Adobe Target for the three locations we implemented in the previous lessons. These will be used to display personalized experiences in the next lesson.   
seo-description: In this lesson, we'll build audiences and offers in Adobe Target for the three locations we implemented in the previous lessons. These will be used to display personalized experiences in the next lesson.
feature: mobile
kt: 3040
audience: developer
doc-type: tutorial
activity-type: implement
---

# Create Audiences and Offers in Adobe Target

In this lesson, we'll go into the Target interface and build audiences and offers for the three locations we implemented in the previous lessons. 

## Learning Objectives

At the end of this lesson, you will be able to:

* **Create Audiences in Adobe Target**
* **Create Offers in Adobe Target for Each Location in your App**

More specifically, in this lesson we will be creating the following audiences and offers for the locations we created earlier. We want to use the Home and Search screens to help app users book their trips, and we want to use the Thank You screen to display some relevant promotions based on the user's destination. Here is a table representing what we will be building in this lesson:

| Location | Audience | Offer |
| --- | --- | --- |
| wetravel_engage_home | New Users  | "Select your Origin & Destination to search for available bus routes" |
| wetravel_engage_search | New Users | "Use filters to narrow down your search results" |
| wetravel_engage_home | Returning Users (after 30+ days) | "Welcome back! Use promo code BACK30 during checkout to get a 10% discount." |
| wetravel_engage_search | Returning Users (after 30+ days) | default content |
| wetravel_context_dest | Destination: San Diego | "DJ" |
| wetravel_context_dest | Destination: Los Angeles | "Universal" |

## Create Audiences

 In Adobe Target, select Audiences > Create Audience and add a rule for new users:

### Create an Audience for New Users

![Create a New User Audience](assets/audience_new_mobile_app_users.jpg)

### Create an Audience for Returning Users

Now create an audience for users who return after 30+ days:

![Create a Returning User Audience](assets/audience_returning_mobile_app_users.jpg)

>!NOTE: All Lifecycle metrics and dimensions collected in the Target mobile SDK are prepended with "a" (a.DaysSinceFirstUse, a.DaySinceLastUse, etc.) and are available in the . These variables are available to use in Audiences.

Next we will create a few audiences for some of the destinations offered by the We.Travel app. In the last lesson we passed the destination as a location parameter in the wetravel_context_dest location request. That parameter is available in the Custom Parameters option

### Create an Audience for Users Booking a Trip to San Diego

![Create "San Diego" Audience](assets/audience_locationDest_san_diego.jpg)

### Create an Audience for Users Booking a Trip to Los Angeles

![Create "Los Angeles" Audience](assets/audience_locationDest_los_angeles.jpg)

## Create Offers

Now, let's create offers to display these messages. As a reminder, offers are snippets of code/content, which are delivered in the Target response. They are most often created in the Target user interface, but can also be created via API or using the Experience Fragments integration with Adobe Experience Manager. In mobile apps, JSON offers are common. For this demo, we'll be using "HTML offers", which can be used to deliver any plain text content into the app.

First, let's create offers for the messages to New Users. In the Target interface, select Offers > Create HTML Offer:

![Create Offer](assets/create_offers.jpg)

Now add each offer:

### Create Offer for New Users

![Create "new users" offer for home screen](assets/offer_home.jpg)

### Create Offer for Returning Users

![Create "new users" offer for search screen](assets/offer_search.jpg)

Now let's create the one offer for returning users (the second offer will be default content, which will display as nothing):

![Create "returning users" offer for home screen](assets/offer_returning_users.jpg)


When the "Universal" value is returned to the app, a banner for Universal Studios will display. When "DJ" is returned, a banner for "Rock Night with DJ SAM" will display. The idea is to display relevant recommendations based on destination after a booking. Let's first create two custom audiences in the Target interface:

Now we'll create HTML offers for these messages. In the Target UI, create two offers:

### Create Offer for Users going to San Diego

![Create "San Diego" Offer](assets/offer_san_diego.jpg)

### Create Offer for Users going to Los Angeles

![Create "Los Angeles" Offer](assets/offer_los_angeles.jpg)

>Note: Our demo app contains custom logic that captures the destination value from the user's input. The logic then checks that value against the Target response and determines which banner to display. You may need to use similar logic in your own app in specific user scenarios.

## Conclusion

Now that Audiences and Offers are in place, we're ready to view the final experience. In the next lesson, we'll build activities and walk through the experience in the app.

**[NEXT : "Personalize Layouts" >](personalize-layouts.md)**
