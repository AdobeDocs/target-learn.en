---
title: How to Use Response Tokens and at.js Custom Events
description: Learn how to use Response Tokens and at.js Custom Events to share profile information from Target to third-party systems.
role: Developer
level: Experienced
topic: Personalization, Architecture, Development
feature: Implementation
doc-type: technical video
kt:
author: Daniel Wright
exl-id: d6ce5367-a453-4e6c-8545-9fa676977f04
---
# Use Response Tokens and at.js Custom Events with Adobe Target

Response Tokens and `at.js` Custom Events allow you to share profile information from [!DNL Target] to third-party systems. Any object in the [!DNL Target] visitor profile, including custom profile attributes, geographic information, activity details, and built-in profiles can be added to the [!DNL Target] response where you can use custom JavaScript to integrate with a third-party.

>[!VIDEO](https://video.tv.adobe.com/v/23253/?quality=12)

## How to use Response Tokens and at.js Custom Events

1. Determine which data you need from [!DNL Target]
1. Turn on the Response Tokens for the data that you need by flipping the toggle on the Setup-&gt;Response Tokens screen
1. Determine which event listener you need to use
1. Write the JavaScript necessary to listen for the Adobe Target event, read the response tokens, and do what you need for your integration
1. Deploy your event listener JavaScript using a custom code action in Launch after the "Load Target" action or add it to the Library Footer section of at.js on the Setup-&gt;Implementation screen and save a new at.js file
1. QA and publish your integration

## Additional resources

* [Use the Experience Cloud Debugger with Adobe Target](../troubleshooting/troubleshoot-with-the-experience-cloud-debugger.md)
* [Response Token Documentation](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html?lang=en)
* [Using Data Providers in Adobe Target](use-data-providers-to-integrate-third-party-data.md)
