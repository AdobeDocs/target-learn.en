---
title: Create Audiences and Offers in Adobe Target
description: In this lesson, we build audiences and offers in Adobe Target for the three locations we implemented in the previous lessons. These will be used to display personalized experiences in the next lesson.   
role: Developer
level: Intermediate
topic: Mobile, Personalization
feature: Implement Mobile
doc-type: tutorial
kt: 3040
thumbnail:
exl-id: 4b153e4f-a979-49a8-8c26-f7ac95162a2f
---
# Create Audiences and Offers in Adobe Target

In this lesson, we'll go into the [!DNL Target] interface and build audiences and offers for the three locations we implemented in the previous lessons.

## Learning Objectives

At the end of this lesson, you will be able to:

* Create audiences in Adobe Target
* Create offers in Adobe Target

More specifically, in this lesson we will create audiences and offers needed to accomplish the personalization use cases defined at the beginning of the tutorial. We want to use the Home and Search screens to help app users book their trips, and we want to use the Thank You screen to display some relevant promotions based on the user's destination. Here is a table representing what we will build in this lesson for each location:

| Location | Audience | Offer |
| --- | --- | --- |
| wetravel_engage_home | New Mobile App Users  | "Select your Origin & Destination to search for available bus routes" |
| wetravel_engage_search | New Mobile App Users | "Use filters to narrow down your search results" |
| wetravel_engage_home | Returning Mobile App Users | "Welcome back! Use promo code BACK30 during checkout to get a 10% discount." |
| wetravel_engage_search | Returning Mobile App Users | default content |
| wetravel_context_dest | Destination: San Diego | "DJ" |
| wetravel_context_dest | Destination: Los Angeles | "Universal" |

## Select Your Workspace

If your company uses Properties and Workspaces to establish boundaries for personalizing apps and websites&mdash;and you implemented the at_property parameter in the last lesson&mdash;you should first make sure that you are in the correct Workspace before proceeding with this lesson. If you don't use Properties and Workspaces, just ignore this step. Select the Workspace that you used in the previous lesson to copy the at_property value:

![Workspace Example](assets/workspace.jpg)

## Create Audiences

Now let's create the audiences we will use to personalize the app.

### Create an Audience for New Users

Adobe Target Audiences are used to identify specific groups of visitors. Offers can then be targeted to those specific groups. For the first two locations, we'll use a "New Users" audience:

1. Click **[!UICONTROL Audiences]** in the top navigation.
1. Click the **[!UICONTROL Create Audience]** button.
    ![Create a New User Audience](assets/audience_new_mobile_app_users_1.jpg)

1. Enter **[!UICONTROL New Mobile App Users]** as the audience name.
1. Select **[!UICONTROL Add Rule]**.
1. Select a **[!UICONTROL Custom]** rule.
    ![Create a New User Audience](assets/audience_new_mobile_app_users_2.jpg)

1. Select **[!UICONTROL a.Launches]**.
1. Select **[!UICONTROL is less than]**.
1. Enter **5**.
1. Save the new audience.
    ![Create a New User Audience](assets/audience_new_mobile_app_users_3.jpg)

### Create an Audience for Returning Users

Follow the same steps listed above to create an audience for returning users.

1. Name the audience _Returning Mobile App Users_.
1. Use **[!UICONTROL a.Launches is greater than or equal to 5]** as the custom rule.
1. Save the new audience.

    ![Create a Returning User Audience](assets/audience_returning_mobile_app_users.jpg)

>[!NOTE]
>
>All Lifecycle metrics and dimensions collected in the [!DNL Target] mobile SDK are prepended with "a" (e.g., a.Launches) and are available in the "Custom" option of the drop-down menu and can be used to build audiences.

### Create an Audience for Users Booking a Trip to San Diego

Next we will create a few audiences for some of the destinations offered by the We.Travel app. In the last lesson we passed the destination as a location parameter in the wetravel_context_dest location request. That parameter is available in the "Custom" option of the drop-down menu.

>[!NOTE]
>
>If a parameter you are expecting to see in the Custom dropdown does not appear in the [!DNL Target] interface, double-check that it is indeed being passed in the request. If you have verified that is in the request, but has not lazy-loaded into the [!DNL Target] interface, you can just type the parameter name and hit enter to continue defining your audience

1. Name the audience _Destination: San Diego_.
1. Use a custom rule with this definition: _locationDest contains San Diego_.
1. Save the new audience.

    ![Create "San Diego" Audience](assets/audience_locationDest_san_diego.jpg)

### Create an Audience for Users Booking a Trip to Los Angeles

1. Name the audience _Destination: Los Angeles_
1. Use a custom rule with this definition: _locationDest contains Los Angeles_
1. Save the new audience.

![Create "Los Angeles" Audience](assets/audience_locationDest_los_angeles.jpg)

## Create Offers

Now, let's create offers to display these messages. As a reminder, offers are snippets of code/content, which are delivered in the [!DNL Target] response. They are most often created in the [!DNL Target] user interface, but can also be created via API or using the Experience Fragments integration with Adobe Experience Manager. In mobile apps, JSON offers are common. In this tutorial, we'll be using HTML offers, which can be used to deliver any plaintext content (including JSON) into the app.

### Create the Offer for New Users

First, let's create offers for the messages to New Users:

1. Click **[!UICONTROL Offers]** in the top navigation.
1. Click **[!UICONTROL Create]**.
1. Select **[!UICONTROL HTML Offer]**.

    ![Create Home Offer](assets/offer_home_1.jpg)

1. Name the offer _Home: Engage New Users_.
1. Enter _Select Source and Destination to search for available buses_ as the code.
1. Save the new offer.

    ![Create Home HTML Offer](assets/offer_home_2.jpg)

### Create the Offer for Returning Users

Now let's create the one offer for returning users (the second offer will be default content, which will display as nothing):

1. Name the offer _Home: Returning Users_.
1. Enter _Welcome back! Use promo code BACK30 during checkout to get a 10% discount._ as the HTML code.
1. Save the new offer.

    ![Create Home HTML Offer](assets/offer_home_returning_users.jpg)

### Create the San Diego Offer

When "DJ" is returned to the ThankYou activity, logic in the filterRecommendationBasedOnOffer() function will display a banner for "Rock Night with DJ SAM":

1. Name the offer _Promotion for San Diego_.
1. Enter _DJ_ as the HTML code.
1. Save the new offer.

![Create "San Diego" Offer](assets/offer_san_diego.jpg)

### Create Offer for Users going to Los Angeles

When "Universal" is returned to the ThankYou activity, logic in the filterRecommendationBasedOnOffer() function will display a banner for "Universal Studios" will display:

1. Name the offer _Promotion for Los Angeles_.
1. Enter _Universal_ as the HTML code.
1. Save the new offer.

![Create "Los Angeles" Offer](assets/offer_los_angeles.jpg)

## Conclusion

Now we have our Audiences and Offers. In the next lesson, we'll build activities that tie the locations, audiences, and offers together to create the personalized experiences!

**[NEXT : "Personalize Layouts" >](personalize-layouts.md)**
