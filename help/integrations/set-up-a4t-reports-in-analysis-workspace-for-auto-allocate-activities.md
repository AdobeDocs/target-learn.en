---
title: How to Set Up A4T Reports in [!DNL Analysis Workspace] for [!UICONTROL Auto-Allocate] Activities
description: How do I configure A4T reports in [!DNL Analysis Workspace] to get the expected results when running [!UICONTROL Auto-Allocate] activities.
role: User
level: Intermediate
topic: Personalization, Integrations
feature: Analytics for Target (A4T), Auto-Target, Integrations
doc-type: tutorial
kt: null
exl-id: 7d53adce-cc05-4754-9369-9cc1763a9450
---
# Setting up A4T reports in [!DNL Analysis Workspace] for [!DNL Auto-Allocate] activities

An [!DNL Auto-Allocate] activity identifies a winner among two or more experiences and automatically reallocates your traffic to the winner while the test continues to run and learn. The [!UICONTROL Analytics for Target] (A4T) integration for [!UICONTROL Auto-Allocate] allows you to see your reporting data in [!DNL Adobe Analytics], and you can even optimize for custom events or metrics defined in [!DNL Analytics]. 

Although rich analysis capabilities are available in [!DNL Adobe Analytics] [!DNL Analysis Workspace], a few modifications to the default **[!UICONTROL Analytics for Target]** panel might be required to correctly interpret [!DNL Auto-Allocate] activities, due to the nuances in [optimization metric criteria](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t-at-aa.html#supported){target=_blank}. 

This tutorial walks through the recommended modifications for analyzing [!DNL Auto-Allocate] activities in [!DNL Analysis Workspace]. The key concepts are: 

* [!UICONTROL Visitors] should always be used as the normalizing metric in [!DNL Auto-Allocate] activities.
* When the metric is an [!DNL Adobe Analytics] metric, calculation of conversion rate varies, depending on the type of optimization criteria defined during activity setup.
  * The "maximize unique visitor conversion rate" conversion rate numerator is a count of unique visitors *with a positive value of the metric*. 
  * This method does not require an additional segment in order to match the conversion rate displayed in the [!DNL Target] UI.
* The "maximize metric value per visitor" conversion rate numerator is the regular metric value in [!DNL Adobe Analytics]. This metric is provided by default in the [!DNL Analytics for Target] panel in [!DNL Analysis Workspace].
  * What this means: maximizes the number of visitors who convert ("count once per visitor").
  * This method requires creation of an additional segment in reporting to match the conversion rate displayed in the [!DNL Target] UI.
* When your optimization metric is a [!DNL Target] defined conversion metric, the default **[!UICONTROL Analytics for Target]** panel in [!DNL Analysis Workspace] handles configuring your panel.
* For all [!UICONTROL Auto-Allocate] activities created before the [!DNL Target Standard/Premium] 23.3.1 release (March 30, 2023) [!DNL Analytics Workspace] and [!DNL Target] display the same value for [!UICONTROL Confidence]. 

  For all [!UICONTROL Auto-Allocate] activities created after March 30, 2023, the confidence interval values seen in [!DNL Analysis Workspace] do not reflect the [more conservative statistics used by [!UICONTROL Auto-Allocate]](https://experienceleague.adobe.com/docs/target/using/activities/auto-allocate/automated-traffic-allocation.html#section_98388996F0584E15BF3A99C57EEB7629){target=_blank} in   if these activities have *both* of the following conditions:
  
  * [!DNL Analytics] as the reporting source (A4T)
  * [!DNL Analytics] optimization metrics

  The confidence metrics should be removed from the A4T panel. Instead, reference these values in [!DNL Target] reporting. 

## Create the A4T for [!DNL Auto-Allocate] panel in [!DNL Analysis Workspace]

To create an A4T panel for an [!DNL Auto-Allocate] report start with the **[!UICONTROL Analytics for Target]** panel in [!DNL Analysis Workspace], as shown below. Then make the following selections:

1. **[!UICONTROL Control Experience]**: You can choose any experience.
1. **[!UICONTROL Normalizing Metric]**: Select Visitors (Visitors is included in the A4T panel by default). [!DNL Auto-Allocate] always normalizes conversion rates by unique visitors.
1. **[!UICONTROL Success Metrics]**: Select the same metric that you used during activity creation. If this was a [!DNL Target] defined conversion metric, select **Activity Conversion**. Otherwise, select the [!DNL Adobe Analytics] metric that you used.

![[!UICONTROL Analytics for Target] panel setup for [!DNL Auto-Allocate] activities.](assets/AAFigure1.png)

*Figure 1: [!UICONTROL Analytics for Target] panel setup for [!DNL Auto-Allocate] activities.*

 You can also arrive at a pre-built **[!UICONTROL Analytics for Target]** panel if you click the link from the report screen in [!DNL Adobe Target].

## [!DNL Target] [!UICONTROL Conversion] metrics or [!DNL Analytics] metrics with "Maximize Metric Value Per Visitor" optimization criteria

When the goal metric is either:

* A Target conversion metric
* Analytics metric with the optimization criterion "Maximize Metric Value per Visitor"

The default A4T panel automatically configures the report.

One example of this panel is shown for the [!UICONTROL Revenue] metric, where "Maximize Metric Value Per Visitor" was selected as the optimization criteria at activity creation time. As previously mentioned, [!DNL Auto-Allocate] uses more conservative confidence calculations compared to the ones used in the **[!UICONTROL Analytics for Target]** panel. Adobe recommends that you remove the confidence metric from the A4T panel, as well as the related lower and upper lift metrics. Instead, reference the confidence values in [!DNL Target] reporting.

>[!NOTE]
>
>Confidence values in A4T reporting are less conservative than [!DNL Target] reporting and might prematurely indicate a winner for an [!UICONTROL Auto-Allocate] activity.


![[!UICONTROL Analytics for Target - AutoAllocate Report] panel](assets/AAFigure2.png)

*Figure 2: The recommended report for [!DNL Auto-Allocate] activities with an [!DNL Analytics] metric "Maximize Metric Value Per Visitor optimization" criteria. For these types of metrics, as well as [!DNL Target] defined conversion metrics, the default  **[!UICONTROL Analytics for Target]** panel in [!DNL Analysis Workspace] can be used.* 

## [!DNL Analytics] metrics with "Maximize Unique Visitor" optimization criteria

The optimization criterion "Maximize Unique Visitor with Conversion Rate" refers to the count of visitors for whom the metric value is positive. For example, if the conversion rate is defined as revenue, then the "Maximize Unique Visitor with Conversion Rate" criterion would be optimizing on the count of unique visitors for whom revenue was greater than 0. In other words, this criterion would maximize the count of visitors that generate revenue, rather than the value of revenue itself.

>[!NOTE]
>
>Conversion rate as referenced here can refer to actions outside of orders, such as clicks, impressions, and so forth. In these cases, the criterion would still be maximizing the count of visitors that click, or view the page, respectively.

The [!DNL Analytics for Target] panel in [!DNL Analysis Workspace] must be modified if this optimization criterion is used with an [!DNL Adobe Analytics] metric.

When this optimization criterion is used, the success metric is a count of unique visitors for whom the conversion metric was positive. Therefore, to view this value, a new segment must be created that filters to hits with a positive value for the metric. 

Create this segment as follows:

1. Select the **[!UICONTROL Components]** > **[!UICONTROL Create Segment]** option in the [!DNL Analysis Workspace] toolbar.
1. Drag the metric used at activity creation time from the left-hand panel to the **[!UICONTROL Definition]** box of the segment.
1. Select values of the metric that are **greater than** a numeric value of 0. 
1. From the **[!UICONTROL Include]** drop-down, select **[!UICONTROL Visitors]**.
1. Give your segment an appropriate name.

An example of the segment creation is shown in the figure below, where the success metric is [!UICONTROL Visitors With Positive Revenue]. 

![[!UICONTROL Visitors with Positive Revenue] segment in [!DNL Analysis Workspace]](assets/AAFigure3.png)

*Figure 3: Segment creation for [!DNL Adobe Analytics] metrics with optimization criteria equal to "[!UICONTROL Maximize Unique Visitor Conversion Rate]." In this example, the metric is [!UICONTROL Revenue], and the optimization goal is to maximize the number of visitors with positive revenue.*

After the appropriate segment has been created, you can modify the default  **[!UICONTROL Analytics for Target]** panel in [!DNL Analysis Workspace] to view the optimization criterion values. This is achieved by doing the following: 

1. Add a second **Unique Visitors** metric alongside the existing [!UICONTROL Visitors] metric column.
2. Drag the newly-created segment under the first column to produce a panel that resembles Figure 4. Notice the difference in values of the columns: the number of unique visitors with positive revenue should be a fraction of the total number of unique visitors assigned to each experience (as shown below).

   ![Figure4.png](assets/AAFigure4.png)

   *Figure 4: Filtering [!UICONTROL Unique Visitors] by the newly created segment*

3. A conversion rate can be [quickly calculated](https://experienceleague.adobe.com/docs/analytics-learn/tutorials/components/calculated-metrics/quick-calculated-metrics-in-analysis-workspace.html) by highlighting both the first and second columns, right-clicking, selecting **[!UICONTROL Create Metric from selection]** > **[!UICONTROL Divide]**. 

   The default conversion rate should be removed and replaced with this new calculated metric, as shown in the image below. You might need to edit the newly created calculated metric to display as a **[!UICONTROL Format]** > **[!UICONTROL Percent]** up to two decimal places as shown.

   ![Figure5.png](assets/AAFigure5.png)

   *Figure 5: The final [!UICONTROL Auto-Allocate] panel showing the conversion rates for a binarized revenue conversion metric*

## Summary

The steps in this tutorial demonstrated how to correctly configure [!DNL Analysis Workspace] to display [!UICONTROL Auto-Allocate] reporting data. 

To summarize:

* When the metric is a [!DNL Target] defined conversion metric or an [!DNL Adobe Analytics] metric with optimization criterion "Maximize Metric Value Per Visitor," the default workspace panel configured with visitors as a normalizing metric should be used.
* When the metric is an [!DNL Adobe Analytics] metric with optimization criterion "Maximize Unique Visitor Conversion Rate," you must determine the fraction of visitors with positive metric value over total visitors. This is done by creating a corresponding segment that filters the [!UICONTROL Unique Visitor] on that metric.
