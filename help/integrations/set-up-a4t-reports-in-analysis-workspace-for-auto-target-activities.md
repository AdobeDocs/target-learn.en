---
title: How to Set Up A4T Reports in Analysis Workspace for Auto-Target Activities
description: How to configure A4T reports in Analysis Workspace to get expected results when running Auto-Target activities
kt:
audience: business user
doc-type: tutorial
activity: use, setup
feature: Analytics for Target (A4T), Auto-Target
topic: Analytics for Target (A4T), Auto-Target
solution: Target
author: Judy Kim
---

# How to set up A4T reports in Analysis Workspace for [!DNL Auto-Target] activities

The Analytics for Target (A4T) integration for [!DNL Auto-Target] activities uses Adobe Target’s ensemble machine learning (ML) algorithms to choose the best experience for each visitor based on their profile, behavior, and context, all while using an Adobe Analytics goal metric.

While rich analysis capabilities are available in Adobe Analytics Analysis Workspace, a few modifications to the default **[!UICONTROL Analytics for Target]** panel are required to correctly interpret [!DNL Auto-Target] activities, due to differences between experimentation activities (manual A/B and Auto-Allocate) and personalization activities ([!DNL Auto-Target]).

This article walks through the recommended modifications for analyzing [!DNL Auto-Target] activities in Workspace, which are based on the following key concepts:

* The **[!UICONTROL Control vs Targeted]** dimension can be used to distinguish between Control experiences versus those served by the [!DNL Auto-Target] ensemble ML algorithm.
* Visits should be used as the normalizing metric when viewing Experience-level breakdowns of performance. In addition, [Adobe Analytics’ default counting methodology may include visits where the user does not actually see activity content](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t-faq/a4t-faq-viewing-reports.html?lang=en#metrics), but this default behavior can be modified by using an appropriately scoped segment (details below).
* Visit-lookback scoped attribution—also known as the "visit lookback window" on the prescribed attribution model—is used by Adobe Target’s ML models during their training phases, and the same (non-default) attribution model should ideally be used when breaking down the goal metric.  

## Create the A4T for [!DNL Auto-Target] panel in Workspace

To create an A4T for [!DNL Auto-Target] report, either start with the typical Analytics for Target panel in Workspace, as shown below, or begin with a freeform table. Then make the following selections:

1. **[!UICONTROL Control Experience]**: You may choose any experience; however, we will override this choice later. Note that for [!DNL Auto-Target] activities, the control experience is really a control strategy, which is either to a) Randomly serve among all experiences, or b) Serve a single experience (this choice is made at activity creation time in Adobe Target). Even if you opted for choice (b)—your [!DNL Auto-Target] activity designated a specific experience as the Control—you should still follow the approach outlined in this article for analyzing A4T for [!DNL Auto-Target] activities.
1. **[!UICONTROL Normalizing Metric]**: Select Visits.
1. **[!UICONTROL Success Metrics]**: Although you may select any metric(s) on which to report, you should generally view reports on the same metric that was chosen for optimization during activity creation in Adobe Target.

![Figure1.png](assets/figure1.png)
*Figure 1: Analytics for Target  panel setup for [!DNL Auto-Target] activities.*

>[!NOTE]
>
>To set up your Analytics for Target panel for Auto-Target activities, choose any control experience, choose Visits as the normalizing metric, and choose the same goal metric that was chosen for optimization during Target activity creation.

## Use the Control vs. Targeted dimension for comparing Adobe Target’s ensemble ML model to your control

The default A4T panel is designed for classic (manual) A/B tests or Auto-Allocate activities where the goal is to compare the performance of individual experiences against the Control experience. In [!DNL Auto-Target] activities, however, the first order comparison should be between the Control *strategy* and the Targeted *strategy* (in other words, determining the lift of the overall performance of the [!DNL Auto-Target] ensemble ML model over the Control strategy). 

To perform this comparison, use the **[!UICONTROL Control vs Targeted (Analytics for Target)]** dimension. Drag and drop to replace the **[!UICONTROL Target Experiences]** dimension in the default A4T report.

Note that this replacement invalidates the default Lift and Confidence calculations on the A4T panel. To avoid confusion, you can remove these metrics from the default panel, leaving the following report:

![Figure2.png](assets/figure2.png)
*Figure 2: The recommended baseline report for [!DNL Auto-Target] activities. This report has been configured to compare Targeted traffic (served by the ensemble ML model) against your Control traffic*

>[!NOTE]
>
>Currently, Lift and Confidence numbers are not available for Control vs. Targeted dimensions for A4T reports for Auto-Target. Until support is added, Lift and Confidence can be computed manually by downloading the [confidence calculator](https://experienceleague.adobe.com/docs/target/assets/complete_confidence_calculator.xlsx?lang=en).

## Understanding Experience-level breakdowns of metrics

To gain further insight into how the ensemble ML model is performing, you may examine Experience-level breakdowns of the **[!UICONTROL Control vs Targeted]** dimension. In Workspace, drag the **[!UICONTROL Target Experiences]** dimension onto your report, then break down each of the Control and Targeted dimensions separately. 

![Figure3.png](assets/figure3.png)
*Figure 3: Breaking down the Targeted dimension by Target Experiences*

An example of the resulting report is shown here.

![Figure4.png](assets/figure4.png)
*Figure 4: A standard [!DNL Auto-Target] report with Experience-level breakdowns. Note your goal metric may be different, and your Control strategy may have a single experience.*

>[!TIP]
>
>In Workspace, click the gear icon to hide the Percentages in the Conversion Rate column, to help keep the focus on the experience conversion rates. Note the conversion rates will then be formatted as decimals, but interpret them as percentages accordingly.

## Why “Visits” is the correct normalizing metric for [!DNL Auto-Target] activities

When analyzing an [!DNL Auto-Target] activity, always choose Visits as the default normalizing metric. [!DNL Auto-Target] personalization selects an experience for a visitor once per visit (formally, once per Adobe Target session), which means the Experience shown to a user can change on every single visit. Thus, if we used unique visitors as the normalizing metric, a single user may end up seeing multiple experiences (across different visits), which would lead to confusing conversion rates. 

A simple example demonstrates this point: consider a scenario in which two visitors enter a campaign which has only two experiences. The first visitor visits twice. They are assigned to Experience A on the first visit, but Experience B on the second visit (due to their profile state changing on that second visit). After the second visit, the visitor converts by placing an order. The conversion is attributed to the most recently shown experience (Experience B). The second visitor also visits twice, and is shown Experience B both times, but never converts. 

Let us compare visitor-level and visit-level reports:

|Experience|Unique Visitors|Visits|Conversions|Visitor norm. Conv. Rate|Visit norm. Conv. Rate|
| --- | --- | --- | --- | --- | --- |
|A|1|1|-|0%|0%|
|B|2|3|1|50%|33.3%|
|Totals|2|4|1|50%|25%|
*Table 1: Example comparing visitor-normalized and visit-normalized reports for a scenario in which decisions are sticky to a visit (and not visitor, as with regular A/B testing). Visitor-normalized metrics are confusing in this scenario.*

As shown in the table, there is a clear incongruence of visitor-level numbers. Despite the fact there are two total unique visitors, this is not a sum of individual unique visitors to each experience. While the visitor-level conversion rate is not necessarily wrong, when one compares individual experiences, visit-level conversion rates arguably make much more sense. Formally, the unit of analysis (“visits”) is the same as the unit of decision stickiness, which means that sums and comparisons of experience-level breakdowns of metrics make sense. 

## Advanced: Non-default visit counting methodology

Adobe Analytics’ default counting methodology for visits to a Target activity may include visits where the user did not interact with the Target activity. This is due to the way Target activity assignments are persisted in the Analytics visitor context. As a result, the number of visits to the Target activity can sometimes be inflated, resulting in a depression of conversion rates. 

If you would prefer to report on visits where the user actually interacted with the Auto-Target activity (either through entry to the activity, a display/visit event, or a conversion), you can:

1. Create a specific segment that includes hits from the Target activity in question, and then
1. Filter the Visits metric using this segment. 

### To create the right segment:

1. Select the **[!UICONTROL Components > Create Segment]** option in the Workspace toolbar.
1. Enter a **[!UICONTROL Title]** for your segment. In the example shown below, the segment is named [!DNL "Hit with specific Auto-Target activity"].
1. Drag the **[!UICONTROL Target Activities]** dimension to the segment **[!UICONTROL Definition]** section.
1. Use the **[!UICONTROL equals]** operator.
1. Search for your specific Target activity.
1. Select the gear icon, and select **[!UICONTROL Attribution model > Instance]** as shown in the figure below.
1. Click **[!UICONTROL Save]**.

![Figure5.png](assets/figure5.png)
*Figure 5: Use a segment such as the one shown here to filter the Visits metric in your A4T for [!DNL Auto-Target] report*

Once the segment has been created, we can use it to filter the Visits metric, so that it only includes visits where the user interacted with the Target activity.  

### To filter Visits using this segment:

1. Drag the newly created segment from the components toolbar, and hover over the base of the **[!UICONTROL Visits]** metric label until a blue **[!UICONTROL Filter by]** prompt appears.
1. Release the segment. The filter will be applied to that metric.

The final panel will appear as follows.

![Figure6.png](assets/figure6.png)
*Figure 6: Reporting panel with the "Hit with specific Auto-Target Activity" segment applied to the [!UICONTROL Visits] metric. This ensures only visits where a user actually interacted with the Target activity in question are included in the report.*

## Advanced: Visit-scope attribution for goal metrics

The A4T integration allows [!DNL Auto-Target]’s ML model to be *trained* using the same conversion event data that is used to *generate performance reports* in Adobe Analytics. However, there are certain assumptions which must be employed in interpreting this data when training the ML models, which differ from the default assumptions made during the reporting phase in Adobe Analytics.

Specifically, Adobe Target’s ML models use a visit-scoped attribution model. That is, they assume a conversion must happen in the same visit as a display of content for the activity, in order for the conversion to be “attributed” to the decision made by the ML model. This is required for Target to guarantee timely training of its models; Target cannot wait for up to 30 days for a conversion (the default attribution window for reports in Adobe Analytics), before including it in the training data for its models. 

Thus, the difference between the attribution used by Target’s models (during training) versus the default attribution used in querying data (during report generation) may lead to discrepancies. It may even appear that the ML models are performing poorly, when in fact the issue lies with attribution.

>[!TIP]
>
>If the ML models are optimizing for a metric that is attributed differently from that of the metrics you are viewing in a report, the models may not perform as expected! To avoid this, ensure the goal metrics on your report use the same attribution used by Target's ML models.

To view goal metrics that have the same attribution methodology used by Adobe Target's ML models, follow these steps:

  1. Hover over the goal metric’s gear icon:
  ![gearicon.png](assets/gearicon.png)
  1. From the resulting menu, scroll to **[!UICONTROL Data settings]**.
  1. Select **[!UICONTROL Use non-default  attribution model]** (if not already selected):
  ![non-defaultattributionmodel.png](assets/non-defaultattributionmodel.png)
  1. Click **[!UICONTROL Edit]**.
  1. Select **[!UICONTROL Model]**: **[!UICONTROL Participation]**, and **[!UICONTROL Lookback window]**: **[!UICONTROL Visit]**.
  ![ParticipationbyVisit.png](assets/ParticipationbyVisit.png)
  1. Click **[!UICONTROL Apply]**.
 
These steps ensure your report will attribute the goal metric to the display of the experience, if the goal metric event happened *any time* (“participation”) in the same visit that an experience was shown. 

## Final Step: Conversion rates with visit-scoped attribution and filtered visit normalization

With the modifications to the Visit and goal metrics in preceding sections, the final modification you should make to your default A4T for [!DNL Auto-Target] reporting panel is to create conversion rates that are the correct ratio—that of a goal metric with the right attribution, to an appropriately filtered “Visits” metric. 

Do this by creating a Calculated Metric using the following steps:

1. Select the **[!UICONTROL Components > Create Metric]** option in the Workspace toolbar. 
1. Enter a **[!UICONTROL Title]** for your metric. For example, "Visit-corrected Conversion Rate for Activity XXX."
1. Select **[!UICONTROL Format]** = Percent and **[!UICONTROL Decimal Places]** = 2.
1. Drag the relevant goal metric for your activity (for example, Activity Conversions) into the definition, and use the gear icon on this goal metric to adjust the attribution model to (Participation|Visit), as described earlier.
1. Select **[!UICONTROL Add > Container]** from the upper right of the **[!UICONTROL Definition]** section.
1. Select the division (&#247;) operator between the two containers.
1. Drag your previously created segment—named "Hit with specific [!DNL Auto-Target] activity" in this article—for this specific [!DNL Auto-Target] activity.
1. Drag the **[!UICONTROL Visits]** metric into the segment container.
1. Click **[!UICONTROL Save]**.

The complete calculated metric definition is shown here.

![Figure7.png](assets/figure7.png)
*Figure 7: The visit- and attribution-corrected model conversion rate metric definition. (Note this metric is dependent on your goal metric and activity. In other words, this metric definition is not re-usable across activities.)*

>[!IMPORTANT]
>
>The Conversion rate metric from the A4T panel is not linked to the conversion event or the normalizing metric in the table. When you make the modifications suggested in this article, the Conversion rate does not adapt to the changes. Therefore, if you make the modification to one (or both) the conversion event attribution and the normalizing metric, then you must remember as a final step to also modify the Conversion rate, as shown above.

## Summary: Final sample Workspace panel for [!DNL Auto-Target] reports

Combining all of the above steps into a single panel, the figure below shows a complete view of the recommended report for [!DNL Auto-Target] A4T activities. This report is the same as that used by Target's machine learning models to optimize your goal metric, and it incorporates all the nuances and recommendations discussed in this article. This report is also closest to the counting methodologies used in traditional Target-reporting driven [!DNL Auto-Target] activities. 

![Figure8.png](assets/figure8.png)
*Figure 8: The final A4T [!DNL Auto-Target] report in Adobe Analytics Workspace, which combines all the adjustments to metric definitions described in the previous sections of this document.*
