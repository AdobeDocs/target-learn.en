---
title: How to Set Up A4T Reports in [!DNL Analysis Workspace] for [!UICONTROL Auto-Allocate] Activities
description: How do I configure A4T reports in [!DNL Analysis Workspace] to get the expected results when running [!UICONTROL Auto-Allocate] activities.
role: User
badgeBeta: label="Beta" type="Informative" url="https://experienceleague.adobe.com/docs/target/using/introduction/intro.html?lang=en#beta newtab=true" tooltip="What are Target Beta release features?"
level: Intermediate
topic: Personalization, Integrations
feature: Analytics for Target (A4T), Auto-Target, Integrations
doc-type: tutorial
kt: null
exl-id: 7d53adce-cc05-4754-9369-9cc1763a9450
---
# Setting up A4T reports in [!DNL Analysis Workspace] for [!DNL Auto-Allocate] activities

An [!DNL Auto-Allocate] activity identifies a winner among two or more experiences and automatically reallocates more traffic to the winner while the test continues to run and learn. The [!UICONTROL Analytics for Target] (A4T) integration for [!UICONTROL Auto-Allocate] allows you to see your reporting data in [!DNL Adobe Analytics], and you can even optimize for custom events or metrics defined in [!DNL Analytics]. 

Although rich analysis capabilities are available in [!DNL Adobe Analytics] [!DNL Analysis Workspace], a few modifications to the default **[!UICONTROL Analytics for Target]** panel are required to correctly interpret [!DNL Auto-Allocate] activities, due to the nuances in [optimization criteria](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t-at-aa.html?lang=en#supported). 

This tutorial walks through the recommended modifications for analyzing [!DNL Auto-Allocate] activities in [!DNL Analysis Workspace]. The key concepts are: 

* [!UICONTROL Visitors] should always be used as the normalizing metric in [!DNL Auto-Allocate] activities.
* When the metric is an [!DNL Adobe Analytics] metric, the appropriate numerator for the conversion rate depends on the type of optimization criteria chosen during activity setup.
  * The "maximize unique visitor conversion rate" optimization criterion has a conversion rate whose numerator is a count of the unique visitors with a positive value of the metric. 
  * The "maximize metric value per visitor* has a conversion rate whose numerator is the regular metric value in [!DNL Adobe Analytics]. This is provided by default in the **[!UICONTROL Analytics for Target]** panel in [!DNL Analysis Workspace].
* When your optimization metric is a [!DNL Target] defined conversion metric, the default **[!UICONTROL Analytics for Target]** panel in [!DNL Analysis Workspace] handles configuring your panel. 
* The [!UICONTROL Confidence] numbers seen in [!DNL Analysis Workspace] do not reflect the [more conservative statistics used by [!UICONTROL Auto-Allocate]](https://experienceleague.adobe.com/docs/target/using/activities/auto-allocate/automated-traffic-allocation.html?lang=en#section_98388996F0584E15BF3A99C57EEB7629), and so should be disregarded. Instead, please reference these values in [!DNL Target] reporting. 

## Create the A4T for [!DNL Auto-Allocate] panel in [!DNL Analysis Workspace]

To create an A4T for [!DNL Auto-Allocate] report start with the **[!UICONTROL Analytics for Target]** panel in [!DNL Analysis Workspace], as shown below. Then make the following selections:

1. **[!UICONTROL Control Experience]**: You can choose any experience.
2. **[!UICONTROL Normalizing Metric]**: Select Visitors. [!DNL Auto-Allocate] always normalizes conversion rates by unique visitors.
3. **[!UICONTROL Success Metrics]**: Select the same metric that you used during activity creation. If this was a [!DNL Target] defined conversion metric, select **Activity Conversion**. Otherwise, select the [!DNL Adobe Analytics] metric that you used.

![[!UICONTROL Analytics for Target] panel setup for [!DNL Auto-Allocate] activities.](assets/AAFigure1.png)

*Figure 1: [!UICONTROL Analytics for Target] panel setup for [!DNL Auto-Allocate] activities.*

>[!NOTE]
>
> You can also arrive at a pre-built **[!UICONTROL Analytics for Target]** panel if you click the link from the report screen in [!DNL Adobe Target].

## [!DNL Target] [!UICONTROL Conversion] metrics or [!DNL Analytics] metrics with "Maximize Metric Value Per Visitor" optimization criteria

The default A4T panel handles [!DNL Auto-Allocate] activities in which the goal metric is either a [!DNL Target] conversion or an [!DNL Analytics] metric with optimization criterion "Maximize Metric Value Per Visitor." 

One example of this panel is shown for the [!UICONTROL Revenue] metric, where "Maximize Metric Value Per Visitor" was selected as the optimization criteria at activity creation time. As previously mentioned, [!DNL Auto-Allocate] uses more conservative confidence calculations compared to the ones used in the **[!UICONTROL Analytics for Target]** panel. Adobe recommends that you remove the confidence metric, as well as the related lower and upper lift metrics.  

![[!UICONTROL Analytics for Target - AutoAllocate Report] panel](assets/AAFigure2.png)

*Figure 2: The recommended report for [!DNL Auto-Allocate] activities with an [!DNL Analytics] metric "Maximize Metric Value Per Visitor optimization" criteria. For these types of metrics, as well as [!DNL Target] defined conversion metrics, the default  **[!UICONTROL Analytics for Target]** panel in [!DNL Analysis Workspace] can be used.* 

## [!DNL Analytics] metrics with "Maximize Unique Visitor Conversion Rate" optimization criteria

When an [!DNL Adobe Analytics] metric is used with an optimization criterion of *Maximize Unique Visitor Conversion Rate*, the default **[!UICONTROL Analytics for Target]** panel in [!DNL Analysis Workspace] must be modified. 

The success metric is now a count of unique visitors for whom the conversion metric was positive. This can be achieved by creating a segment that filters to hits with a positive value of the metric. Create this segment as follows:

1. Select the **[!UICONTROL Components]** > **[!UICONTROL Create Segment]** option in the [!DNL Analysis Workspace] toolbar.
1. Drag the metric used at activity creation time from the left-hand panel to the **[!UICONTROL Definition]** box of the segment.
1. Select values of the metric that are **greater than** a numeric value of 0. 
1. From the **[!UICONTROL Include]** drop-down, select **[!UICONTROL Visitors]**.
1. Give your segment an appropriate name.

An example of the segment creation is shown in the figure below, where you select [!UICONTROL Visitors With Positive Revenue]. 

![[!UICONTROL Visitors with Positive Revenue] segment in [!DNL Analysis Workspace]](assets/AAFigure3.png)

*Figure 3: Segment creation for [!DNL Adobe Analytics] metrics with optimization criteria equal to "[!UICONTROL Maximize Unique Visitor Conversion Rate]." In this example, the metric is [!UICONTROL Revenue], and the optimization goal is to maximize the number of visitors with positive revenue.*

After the appropriate segment has been created, the default  **[!UICONTROL Analytics for Target]** panel in [!DNL Analysis Workspace] can be modified. 

1. Add a second **Unique Visitors** metric alongside the existing [!UICONTROL Visitors] metric column.
2. Drag the newly-created segment under the first column to produce a panel that resembles Figure 4. Notice the difference: the number of unique visitors with positive revenue is a fraction of the total number of unique visitors assigned to each experience.

   ![Figure4.png](assets/AAFigure4.png)

   *Figure 4: Filtering [!UICONTROL Unique Visitors] by the newly created segment*

3. A conversion rate can be [quickly calculated](https://experienceleague.adobe.com/docs/analytics-learn/tutorials/components/calculated-metrics/quick-calculated-metrics-in-analysis-workspace.html?lang=en) by highlighting both the first and second columns, right-clicking, selecting **[!UICONTROL Create Metric from selection]** > **[!UICONTROL Divide]**. 

   The default conversion rate should be removed and replaced with this new calculated metric, as shown in the image below. You might need to edit the newly created calculated metric to display as a **[!UICONTROL Format]** > **[!UICONTROL Percent]** up to two decimal places as shown.

   ![Figure5.png](assets/AAFigure5.png)

   *Figure 5: The final [!UICONTROL Auto-Allocate] panel showing the conversion rates for a binarized revenue conversion metric*

## Summary

The steps in this tutorial demonstrated how to correctly configure [!DNL Analysis Workspace] to display [!UICONTROL Auto-Allocate] reporting data. 

To summarize:

* When the metric is a [!DNL Target] defined conversion metric or an [!DNL Adobe Analytics] metric with optimization criterion "Maximize Metric Value Per Visitor," the default workspace panel configured with visitors as a normalizing metric should be used.
* When the metric is an [!DNL Adobe Analytics] metric with optimization criterion "Maximize Unique Visitor Conversion Rate," you must use a conversion rate that is defined as the fraction of visitors for whom the metric is positive. This is done by creating a corresponding segment that filters the [!UICONTROL Unique Visitor] metric.
