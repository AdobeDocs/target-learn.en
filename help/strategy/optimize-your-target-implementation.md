---
title: Optimize your Adobe Target implementation
description: Get an overview of Adobe Target implementation and structure. Learn how to understand and audit your organization's set up. Learn the common troubleshooting techniques and tips on creating a knowledge repository for your team.
solution: Target
exl-id: 49b69f41-0993-437c-bb69-84392be427df
---
# Optimize your Adobe Target implementation

If you are new to your organization and want to become familiar with what is in place from a testing and optimization practice, this article helps you get started. We'll begin with an overview of Adobe Target implementation and structure. You'll learn how to understand and audit your organization's set up. Finally, we'll discuss common troubleshooting techniques and tips on creating a knowledge repository for your team.

Adobe Target is a tool that allows testing and targeting of unique content to different visitors. For an overview of the features available, [visit this guide](https://experienceleague.adobe.com/docs/target/using/introduction/intro.html?lang=en).

## Target implementation and structure

Before we dive into the implementation process for Adobe Target or how it is structured, it's helpful to first understand some fundamentals about the software.

Adobe Target is a tool that allows testing and targeting of unique content to different visitors without changing the native website code. Target temporarily changes the end user experience, as well as tracks the behavior of users after seeing the change. Target also offers the ability to alter the experience for end users based on profile information or previous actions.

There are three Target fundamental activity types:

1. A/B test
2. Multivariate testing (MVT)
3. Experience testing

**The A/B test** compares two or more experiences to see which best improves conversions throughout a pre-specified test period. The A/B test is a highly controlled experiment with traffic measurements, split by percentages rather than by a rule, allowing you:

* to analyze the test data.
* to glean insights about your audience.
* to determine which experience performs the best.

**Multivariate testing** (MVT) compares combinations of offers among elements on a page to see which combination performs the best for a specific audience. This test also identifies which element of the page best improves conversions throughout a pre-specified test period. MVT provides:

* A way to display multiple offers in multiple elements.
* A method to test the resulting unique experience against a specific goal.
* Insight as to which elements have the greatest negative or positive impact on visitor interactions.

**Experience testing** (Experienced Targeting) delivers content to a specific audience based on a set of marketer-defined rules and criteria. This method provides a way to target specific content to a specific audience based on a set of defined allocation rules.

How does Target work?

Here is a high-level example of how Target works:

1. A visitor requests a page from your server, and it displays in the browser.
1. A first party cookie is set in the visitor's browser to store behavior.
1. The page then calls Adobe Target.
1. The content displays based on the rules of the user's activity.
1. Adobe Target captures specific metrics as defined in the activity configuration to gauge the impact of the test experiences.

Target is built on an &quot;global Mbox&quot; that provides the ability to impact anything on the page. This feature deploys on page load either as a hardcoded link to the at.js file or it is delivered using a Tag Manager like Adobe Launch.

## Understand your current implementation

To understand your current Implementation, Adobe recommends that you review your Target User Interface implementation along with your Tag Manager and Page Load implementation.

**To review your [!DNL Target] user interface:**

1. Begin your review on the [!DNL Target] UI:

   * Review the [!DNL Target] technology stack
   * Confirm the available features
   * Identify where the deployment is live

1. Review activities for best practices:

   * Review historical campaigns for program maturity

1. Deactivate old activities:
  
   * Archive and clean up [!DNL Target] asset that no longer have current or future use

1. Review audiences.

1. Review environment definitions and associated domains.

1. Review profile scripts for applicability

   * All profile scripts run on every target call
   * Maintain call efficiency by removing non applicable scripts

To review the tag manager and page load:

1. Confirm the following in tag manager:
  
   * The deployment of the expected [!DNL Target] JavaScript code
   * The appropriate content hiding solution
   * Set Necessary rules to populate the [!DNL Target] calls with the expected parameters

1. Confirm the following during page load:
  
   * Matching version numbers for the request URL and [!DNL Target] Request URL
   * Populated Experienced Cloud ID value (Cloud Body)
   * Present expected integration values (Cloud Body)
   * Populated [!DNL Target] parameters on the appropriate pages

## [!DNL Target] audit activities

To avoid manually going through each page to audit [!DNL Target] activities, use the Adobe Auditor to help with understanding the current technical state of your implementation. Adobe Auditor is powered by ObservePoint and can be set up to run at a manual level, to identify high level implementation issues on your site.

The Adobe Auditor provides:

* A high site health
* Quick call outs for implementation issues

Adobe recommends performing monthly manual audits to:

* Identify untagged pages
* Identify inconsistent versions
* Find out-of-date versions
* Provide detailed information that can be exported

## Common troubleshooting

>[!NOTE]
>
>Adobe recommends installing the Adobe Experience Platform Debugger.

The following are general troubleshooting tips when entering the Experience:

### Cache and cookies**

* Clearing cache and cookies
* Be careful using private mode (for example: private mode in Firefox can block [!DNL Target])

### Are you qualified for the activity?

* Check that you have performed the same steps that the audience used in the activity
* Use `mboxTrace` or response tokens to check profile and segment values

### General troubleshooting tips when validating visual/ functional

If are in the [!DNL Target] experience and you do not see the expected visual experience:

Check the [!DNL Target] response:

* If the code is not executed:

1. Check conflicting activities
1. Contact Client Care

* If the code is executed:

1. Re-work the code in that scenario

## Maintaining a knowledge repository

A knowledge repository is an online platform used for documenting and sharing information. The knowledge repository contains information specific to your implementation and can contain team specific information.

Ideally, the repository should allow editing and auto saving within the platform. Once it is initially configured, it is easy to maintain and keep up to date. Content within the Knowledge Repository is curated based on user roles.

Typical documents in a Knowledge Repository include:

* **Overview document** - a document used to clearly explain program goals, objectives, processes and structure
* **Ideation repository** - a document used to manage and prioritize potential ideas that are not ready for the testing process
* **Program roadmap** - a document used to manage all aspects of testing activities once ideas are ready to start the testing process
* **Activity plan document** - a document used to outline information needed to build and launch activities
* **Activity plan document** - a document used to communicate results and recommended next steps to stakeholders
* **Program dashboard** - a document used to track program performance, cadence, and revenue benefits over time.

For more information, review our [webinar](https://adobecustomersuccess.adobeconnect.com/p4p7xlp7dh42mp4/) with Senior Consultant, Wilder Freed.

Learn more about strategy and thought leadership at the [Customer Success](https://experienceleague.corp.adobe.com/docs/customer-success/customer-success/overview.html) hub.
