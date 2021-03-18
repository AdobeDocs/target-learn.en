---
title: Personalize Layouts
description: In this final lesson, we build two personalization activities in Target for our Audiences. Learn how to load and display the activities in the app and validate that content is displaying at the right time in the right locations.  
role: Developer
level: Intermediate
topic: Mobile, Personalization
feature: Implement Mobile
doc-type: tutorial
kt: 3040
thumbnail:
author: Daniel Wright
---

# Personalize Layouts

Now it's time to bring everything together and create the personalized experiences. An _Activity_ is the [!DNL Target] mechanism that links the locations, audiences, and offers together, so that when the request is made from the app, [!DNL Target] responds with the personalized content. We'll build two personalization activities in [!DNL Target] and validate that personalized content is displays to the right user at the right time and in the right location.

## Learning Objectives

At the end of this lesson, you will be able to:

* Build Activities in Adobe Target
* Validate the Activities in the sample App

## Create Activities in Adobe Target

Learn how to create Engage Users and Contextual Offers activities.

### First Activity - "Engage Users"

Here is a summary of the activity we'll build:

| Audience | Locations | Offers |
|---|---|---|
| New Mobile App Users | wetravel_engage_home, wetravel_engage_search | Home: Engage New Users, Search: Engage New Users |
| Returning Mobile App Users | wetravel_engage_home, wetravel_engage_search | Home: Returning Users, default_content |

In the [!DNL Target] interface do the following:

1. Select **[!UICONTROL Activities]** > **[!UICONTROL Create Activity]** > **[!UICONTROL Experience Targeting]**.

    ![Create Activity](assets/activity_create_1.jpg)

1. Click **[!UICONTROL Mobile App]**.
1. Select the **[!UICONTROL Form composer]**.
1. Select your workspace (the same workspace you used in previous lessons).
1. Select your Property  (the same property you used in previous lessons).
1. Click **[!UICONTROL Next]**.

    ![Create Activity](assets/activity_create_2.jpg)

1. Change the activity title to **[!UICONTROL Engage Users]**.
1. Select the **[!UICONTROL ellipsis]** > **[!UICONTROL Change Audience]**.
    ![New Mobile App Users Change Audience](assets/activity_create_3.jpg)
1. Set the audience to **[!UICONTROL New Mobile App Users]**.
1. Click **[!UICONTROL Done]**.
    ![New Mobile App Users Audience](assets/activity_create_4.jpg)

1. Change the location to _wetravel_engage_home_.
1. Select the dropdown arrow next to Default Content and select **[!UICONTROL Change HTML Offer]**.

    ![New Mobile App Users Audience](assets/activity_create_5.jpg)

1. Select the **[!UICONTROL Home: Engage New Users]** offer.
1. Select **[!UICONTROL Done]**.

    ![New Mobile App Users Audience](assets/activity_create_6.jpg)

1. Select **[!UICONTROL Add Location]**.
    ![New Mobile App Users Audience](assets/activity_create_7.jpg)

1. Select the _wetravel_engage_search_ location.
1. Change the HTML offer.

    ![New Mobile App Users Audience](assets/activity_create_8.jpg)

1. Select the **[!UICONTROL Search: Engage New Users]** offer.
1. Click **[!UICONTROL Done]**.

    ![New Mobile App Users Audience](assets/activity_create_9.jpg)

You've just connected an audience to locations and offers, creating the personalized experience for the New Mobile App Users! The experience  should now look like this:

![Experience A Final](assets/activity_engage_users_a_final.jpg)

Now create an experience for Returning Mobile App Users:

1. Select **[!UICONTROL Add Experience Targeting]** on the left.
1. Select the Audience **[!UICONTROL Returning Mobile App Users]**.
1. Select **[!UICONTROL Done]**.
   ![Returning Mobile App Users Audience](assets/activity_create_11.jpg)

Now use the same process we used earlier to configure the new experience. The configuration for the Returning Mobile App Users experience  should look like this:

![Returning Mobile App Users Final](assets/activity_engage_users_b_final.jpg)

Let's continue to the next screen in the setup:

1. Click **[!UICONTROL Next]** to advance to the **[!UICONTROL Targeting]** screen.
1. Use the default settings for Targeting. If you had experiences for audiences that overlapped (e.g. _New York Users_ and _First Time Users_) you could arrange the priority order on this screen.
1. Click **[!UICONTROL Next]** to advance to **[!UICONTROL Goals & Settings]**.

    ![Engage Users Activity - Targeting Default](assets/activity_engage_users_targeting.jpg)

Now let's complete the activity setup:

1. Set the **[!UICONTROL Primary Goal]** to **[!UICONTROL Conversion]**.
1. Set the action to **[!UICONTROL Viewed an mbox]** > _wetravel_context_dest_ (Since this location is on the confirmation screen, we can use it to measure conversions).

    ![Engage Users Activity - Goals](assets/activity_create_12.jpg)

1. Keep all other settings on the screen to the defaults.
1. Click **[!UICONTROL Save & Close]** to save the Activity.
1. Activate the **[!UICONTROL Activity]** on the next screen.

![Experience B Audience](assets/activity_create_13.jpg)

Our first activity is now live and ready to test!

### Second Activity - "Contextual Offers"

Here is a summary of the second activity we'll build:

| Audience | Location | Offers |
| --- | --- | --- |
| Destination: San Diego | wetravel_context_dest | Promotion for San Diego |
| Destination: Los Angeles | wetravel_context_dest | Promotion for Los Angeles |

Repeat the same process as above for the next Activity - "Contextual Offers". The Final configuration for both experiences are shown below:

#### San Diego

![Contextual Offers - Experience A](assets/activity_contextual_a_final.jpg)

#### Los Angeles

![Contextual Offers - Experience B](assets/activity_contextual_b_final.jpg)

On the Goals & Settings step, we'll change the Primary Goal to the location on booking confirmation screen:

1. Under the **[!UICONTROL Reporting Settings]**, set the **[!UICONTROL Primary Goal]** to **[!UICONTROL Conversion]**.
1. Set the action to **[!UICONTROL Viewed an mbox]** > _wetravel_context_dest_ (in this activity, this metric is basically meaningless since this is also the same location which delivers the experience).
1. Click **[!UICONTROL Save & Close]**.

![Contextual Offers - Experience](assets/activity_create_14.jpg)

Activate the Activity on the next screen.

Now our second activity is live and ready to test!

## Validate the Home Offer

Run the Emulator and watch for the first offer to display at the bottom of the home screen. If you're a returning user with 5 or more app launches, you would see the _welcome back_ offer displayed. If you're a new user (less than 5 app launches), you should see the _new user_ message:

![Validate Home Offer](assets/layout_home_validate.jpg)

If the new user offer doesn't display, try wiping the data for your emulator. That will reset the app launches to 1 the next time you launch. This is done under **[!UICONTROL Tools]** > **[!UICONTROL AVD Manager]**. You might need to restart Android Studio, too, if Logcat does not work properly:

![Wipe Emulator](assets/layout_home_validate_avd_wipe.jpg)

You can also validate the response in Logcat by filtering for _wetravel_engage_home_:

![Validate Home Offer - Logcat](assets/layout_home_validate_logcat.jpg)

## Validate the Search Offer

Select **[!UICONTROL San Jose]** as your **[!UICONTROL Departure]** and **[!UICONTROL San Diego]** as your **[!UICONTROL Destination]** and click **[!UICONTROL Find Bus]** to search for available buses. 

On the results screen, you should see the _use filters_ message. If you're a returning user with 5 or more app launches, no message will appear here since default content is set for this location (which is blank):

![Validate Search Offer](assets/layout_search_validate.jpg)

## Validate the Contextual Offers on the Thank You Screen

Now continue through the booking process:

* Select a bus on the results screen.
* Select a seat on the checkout screen.
* Select **[!UICONTROL Credit Card]** on the payment screen (leave the payment info blank - no actual booking will take place).

Since San Diego was selected as the destination, you should see the _DJ SAM_ offer banner on the confirmation screen:

![Validate Context Offer - San Diego](assets/layout_context_san_diego.jpg)

Now select **[!UICONTROL Done]** and try another booking with Los Angeles as the destination. The confirmation screen should display the _Universal Studios_ banner:

![Validate Context Offer - Los Angeles](assets/layout_context_los_angeles.jpg)

## Conclusion

Congratulations! This concludes the main portion of the Adobe Target SDK 4.x for Android Tutorial. You now have the skills to implement personalization in Android apps! You can refer to this documentation and demo app as a reference for your future projects.

Next: Feature Flagging is another feature that can be implemented with Adobe Target in Android. To learn about feature flagging, check out the next lesson.

**[NEXT : Feature Flagging >](feature-flagging.md)**
