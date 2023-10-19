---
title: How to Set Up A4T Reports in [!DNL Analysis Workspace] for [!UICONTROL Auto-Allocate] Activities
description: How do I configure [!UICONTROL Analytics for Target] (A4T) reports in [!DNL Adobe] [!DNL Analysis Workspace] when running [!UICONTROL Auto-Allocate] activities.
role: User
level: Intermediate
topic: Personalization, Integrations
feature: Analytics for Target (A4T), Auto-Target, Integrations
doc-type: tutorial
kt: null
exl-id: 7d53adce-cc05-4754-9369-9cc1763a9450
---
# Setting up A4T reports in [!DNL Analysis Workspace] for [!DNL Auto-Allocate] activities 

An [!UICONTROL Auto-Allocate] activity in [!DNL Adobe Target] identifies a winner among two or more experiences and automatically reallocates visitor traffic to the winner while the test continues to run and learn. The [!UICONTROL Analytics for Target] (A4T) integration for [!UICONTROL Auto-Allocate] lets you view reporting data in [!DNL Adobe Analytics], and you can optimize for custom events or metrics defined in [!DNL Analytics].

Although rich analysis capabilities are available in [!DNL Adobe Analytics] [!DNL Analysis Workspace], a few modifications to the default [!UICONTROL Analytics for Target] panel might be required to correctly interpret [!UICONTROL Auto-Allocate] activities. These modifications are needed due to the nuances in [optimization metric criteria](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t-at-aa.html#supported){target=_blank}.

Each type of optimization metric requires a different report configuration in A4T, as follows:

* Using an [!DNL Analytics] metric 

  * [!UICONTROL Maximize metric value per visitor]
  * [!UICONTROL Maximize unique visitor conversion rate] 

* Using a [!DNL Target]-defined conversion metric

This tutorial covers overall A4T guidance, and criteria-specific report configuration steps.

## Analytics metrics with "[!UICONTROL Maximize Metric Value Per Visitor]" optimization criteria

**Definition**: (Overall Metric Value) / (# of Visitors)

To configure the report, make the following changes in the A4T report:

|Changes required|[!DNL Target]-triggered report|A4T Panel report|
| --- | --- | --- |
|Maximize metric value for an [!DNL Analytics] metric|<ul><li>[!UICONTROL Confidence] metrics should be removed.</li><li>[!UICONTROL Lift (Low)] and [!UICONTROL Lift (High)] should be removed.</li><li>Uncheck the percentage presentation from the [!UICONTROL Conversion Rate] column to avoid confusion. See [Overall Guidance](#guidance) below.</li><li>Conversion rate metric should be renamed to "Metric / Visitor."</li></ul>|<ul><li>[!UICONTROL Confidence] metrics should be removed.</li><li>[!UICONTROL Lift (Low)] and [!UICONTROL Lift (High)] should be removed.</li><li>Uncheck the percentage presentation from the [!UICONTROL Conversion Rate] column to avoid confusion. See [Overall Guidance](#guidance) below.</li><li>Conversion rate metric should be renamed to "Metric / Visitor."</li><li>Ensure that the date and time ranges align with the values you see in the [!DNL Target] report. See [Overall Guidance](#guidance) below.</li></ul>|

![Maximize metric value for revenue](/help/integrations/assets/maximize-metric-value-revenue.png)

## [!DNL Analytics] metrics with "[!UICONTROL Unique Visitor Conversion Rate]" optimization criteria

**Definition**: (# of Unique Visitors with a positive value of the metric) / (Total # of Unique Visitors)

Example: Suppose that your optimization metric is [!UICONTROL Revenue]. There are five unique visitors in the activity, and three of those unique visitors make a purchase. In this example, this value = (3 visitors for whom [!UICONTROL Revenue] is positive) / (5 total unique visitors) = 0.6 = 60%.

>[!NOTE]
>
>Conversion rate as referenced here can refer to actions outside of orders, such as clicks, impressions, and so forth. In these cases, the criterion would still be maximizing the count of visitors that click, or view the page, respectively.

To configure the report, make the following changes in the A4T report:

|Changes required|Target-triggered report|A4T Panel report|
| --- | --- | --- |
|Maximize conversions for an [!DNL Analytics] metric|<ul><li>[!UICONTROL Confidence] metrics should be removed.</li><li>All [!UICONTROL Lift] metrics should be removed.</li><li>Uncheck the percentage presentation from the [!UICONTROL Conversion Rate] column to avoid confusion. See [Overall Guidance](#guidance) below.</li></ul>|<ul><li>[!UICONTROL Confidence] metrics should be removed.</li><li>All [!UICONTROL Lift] metrics should be removed.</li><li>Create a segment to filter visitors with a positive metric value who viewed the activity analyzed. See [Create a segment](#segment) below.</li><li>Replace the auto-populated [!UICONTROL Conversion Rate] metric so that is the division between [!UICONTROL Unique visitors] with a positive metric value and unique visitors. See [Update the Conversion Rate metric](#update-conversion-metric) below.</li><li>Uncheck the percentage presentation from the [!UICONTROL Conversion Rate] column to avoid confusion. See [Overall Guidance](#guidance) below.</li><li>Ensure that the date and time ranges align with the values you see in the [!DNL Target] report. See [Overall Guidance](#guidance) below.</li></ul>|

### Default A4T Panel report - additional guidance

The following sections contain more information about additional guidance as you set up your default A4T panel report.

#### Create a segment {#segment}

1. Click the **"+" sign** next to **[!UICONTROL Segments]** in the left rail.

   ![Plus sign next to segments in the left rail.](/help/integrations/assets/plus-sign.png)

1. Title the segment "Visitors with Positive Metric Value."
1. Under **[!UICONTROL Definition]**, next to **[!UICONTROL Include]**, select **[!UICONTROL Visitor]**.
1. Under **[!UICONTROL Definition]**, select the optimization metric in your activity.

   In this example, assume [!UICONTROL Revenue] as the optimization metric.
   
1. Select the "[!UICONTROL is greater than]" operator, then specify "0".

   These settings filter for all visitors with a positive metric value.
   
1. Click **[!UICONTROL Save]**.

   ![Positive metric value](/help/integrations/assets/positive-metric-value.png)

1. Add the newly created segment named "Visitors with positive metric value" to the A4T panel.
1. Drag and drop the [!UICONTROL Unique Visitors] metric in the same column as the "Visitors with Positive Metric Value". 

   This configuration creates a segment of all unique visitors for whom the metric value is positive. In this example, all unique visitors whose revenue was greater than zero.

#### Update the [!UICONTROL Conversion Rate] metric {#update-conversion-metric}

1. If you have not already done so, remove the existing [!UICONTROL Conversion Rate] column from the panel, as explained below.
1. Add a metric by clicking the "+" sign next to the **[!UICONTROL Metrics]** section in the left rail.
1. Name the metric "Conversion Rate" and define it as "([!UICONTROL Unique Visitors] with positive metric value)" divided by "Unique Visitors," as shown below. 

   Add the newly created segment (steps defined below) of "Visitors with positive metric value," the division operator, the "Unique Visitors" metric in the numerator, and "Unique Visitors" as the denominator.

   ![Conversion rate in A4T panel.](/help/integrations/assets/conversion-rate.png)

1. Click **[!UICONTROL Save]**.

1. Drag and drop in your newly created "Conversion Rate" metric into your existing panel. 
1. Click the gear icon, then deselect the **[!UICONTROL Percent]** checkbox, because this value can lead to confusion.

   The correct configuration of the report should yield a result that resembles the following illustration:

   ![Unique visit conversion rate in A4T panel report](/help/integrations/assets/a4t-aa-maximize-metric-value-revenue.png)

## [!DNL Target]-defined conversion rate

To configure the report, make the following changes in the A4T report:

|Changes required|Target-triggered report|A4T Panel report|
| --- | --- | --- |
|[!DNL Analytics] reporting with [!DNL Target] conversion metric|<ul><li>[!UICONTROL Confidence] metrics should be removed.</li><li>[!UICONTROL Lift (Low)] and [!UICONTROL Lift (High)] should be removed.</li><li>Uncheck the percentage presentation from the [!UICONTROL Conversion Rate] column to avoid confusion. See [Overall Guidance](#guidance) below.</li></ul>|<ul><li>[!UICONTROL Confidence] metrics should be removed.</li><li>[!UICONTROL Lift (Low)] and [!UICONTROL Lift (High)] should be removed.</li><li>Uncheck the percentage presentation from the [!UICONTROL Conversion Rate] column to avoid confusion. See [Overall Guidance](#guidance) below.</li><li>Ensure that the date and time ranges align with the values you see in the [!DNL Target] report. See [Overall Guidance](#guidance) below.</li></ul>|

The correct configuration of the report should yield a result that resembles the following illustration: 
   
![Activity conversions](/help/integrations/assets/optimized-table.png)

## Overall guidance for [!UICONTROL Analytics for Target] (A4T) {#guidance}

You can navigate to a pre-built [!UICONTROL Analytics for Target] panel by clicking the link from the report screen in [!UICONTROL Adobe Target] (this is referred to later in this guide as the "[!DNL Target]-triggered report"). Alternatively, you can build the A4T panel in [!DNL Analytics] (details later in this section). 

The following sections specify which configurations are required, depending on which of these methods you choose. However, the following steps serve as overall guidance:

* The confidence metrics should be removed from the A4T panel regardless of the panel creation method (both are detailed below). Instead, reference these values in [!DNL Target] reporting. Additionally, activity winners can be identified in [!DNL Target] reporting. Details on activity winner identification can be found in the [Identify the Activity Winner](#winner) section below.
>
>* To avoid confusion, uncheck the "[!UICONTROL Percent]" presentation of the [!UICONTROL Conversion Rate] metric. See [Hide the percentage from the [!UICONTROL Conversion Rate] column](#hide-percentage) below. 
>
>* If you are building an A4T panel, ensure that the date and time ranges match that of your [!DNL Target] report. See [Align the date and time in the A4T panel](#aligning-date-and-time) below.

### Hide the percentage from the [!UICONTROL Conversion Rate] column {#hide-percentage}

1. Click the **gear** icon next to the title of the [!UICONTROL Conversion Rate] column.

   ![Gear icon in the Conversion Rate column](/help/integrations/assets/coversion-rate-gear-icon.png)

   The [!UICONTROL Column] settings dialog box displays:

   ![Column settings dialog box](/help/integrations/assets/column-settings-dialog-box.png){width="200"}

1. Deselect the **[!UICONTROL Percent]** checkbox.

   Your A4T panel now does not include percentages as the Conversion Rate and matches [!DNL Target], as shown below:

   ![Conversion Rate column showing no percentages](/help/integrations/assets/no-percentages.png)

### Align the date and time in the A4T panel {#aligning-date-and-time}

1. below each panel, check the date range that the panel references to ensure that the date range matches that of the [!DNL Target] report. 

   ![Date range in A4T panel](/help/integrations/assets/date-range.png)

1. In [!DNL Analytics], set the time range to 12:00am – 11:59pm.

### Identify the activity winner {#winner}

[!DNL Auto-Allocate] activity winners are selected when there is a winning conversion rate with confidence values greater than or equal to 95%. These values should be referenced in the [!DNL Target] reports, as confidence calculations reflect the more conservative methods [!DNL Target] recommends for [!UICONTROL Auto-Allocate] activities. See [Statistical guarantees of Auto-Allocate](https://experienceleague.adobe.com/docs/target/using/activities/auto-allocate/determine-winner.html#section_7AF3B93E90BA4B80BC9FC4783B6A389C){target=_blank} in the *[!UICONTROL Adobe Target Business Practitioner Guide]*.

>[!NOTE]
>
>The "No Winner Yet" and "Winner" badges are not available in the A4T panel in [!DNL Analysis Workspace]. Also, the winner "star" badge displayed in [!DNL Target] reports for [!UICONTROL Auto-Allocate] activities should be ignored. See [Auto-Allocate](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t-at-aa.html?lang=en#aa){target=_blank} in *A4T support for Auto-Allocate and Auto-Target activities* in the *[!UICONTROL Adobe Target Business Practitioner Guide]*.

### Create the A4T for [!UICONTROL Auto-Allocate] panel in [!DNL Analysis Workspace]

1. To create an A4T panel for an [!UICONTROL Auto-Allocate] activity report, start with the [!UICONTROL Analytics for Target] panel in [!DNL Analysis Workspace], as shown below.

   ![Analytics for Target - Auto-Allocate report](/help/integrations/assets/a4t-auto-allocate-report.png)

1. Make the following selections:

   * **[!UICONTROL Control Experience]**: Choose any experience.
   * **[!UICONTROL Normalizing Metric]**: Select **[!UICONTROL Visitors]** (included in the A4T panel by default). [!UICONTROL Auto-Allocate] always normalizes conversion rates by unique visitors.
   * **Success Metrics**: Select the same (optimization) metric that you used during activity creation. If this was a [!DNL Target]-defined conversion metric, select **[!UICONTROL Activity Conversion]**. Otherwise, select the [!DNL Adobe Analytics] metric that you used.



   





