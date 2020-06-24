---
title: Use Response Tokens and at.js Custom Events with Adobe Target
seo-title: Use Response Tokens and at.js Custom Events with Adobe Target
description: Response Tokens and at.js Custom Events allow you to share profile information from Target to third-party systems. Any object in the Target visitor profile, including custom profile attributes, geographic information, activity details, and built-in profiles can be added to the Target response where you can use custom JavaScript to integrate with a third-party.
audience: developer
difficulty: 5
author: Daniel Wright
doc-type: implement
activity-type: technical-video
---

# Use Response Tokens and at.js Custom Events with Adobe Target

Response Tokens and `at.js` Custom Events allow you to share profile information from [!DNL Target] to third-party systems. Any object in the [!DNL Target] visitor profile, including custom profile attributes, geographic information, activity details, and built-in profiles can be added to the [!DNL Target] response where you can use custom JavaScript to integrate with a third-party.

>[!VIDEO](https://video.tv.adobe.com/v/23253/?quality=12)

## How to use Response Tokens and at.js Custom Events

1. Determine which data you need from [!DNL Target]
1. Turn on the Response Tokens for the data that you need by flipping the toggle on the Setup-&gt;Response Tokens screen
1. Determine which event listener you need to use
1. Write the JavaScript necessary to listen for the Adobe Target event, read the response tokens, and do what you need for your integration
1. Deploy your event listener JavaScript using a custom code action in Launch after the “Load Target” action or add it to the Library Footer section of at.js on the Setup-&gt;Implementation screen and save a new at.js file
1. QA and publish your integration

## Additional Resources

* [Use the Experience Cloud Debugger with Adobe Target](../troubleshooting/troubleshoot-with-the-experience-cloud-debugger.md)
* [Response Token Documentation](https://docs.adobe.com/help/en/target/using/administer/response-tokens.html)
* [At.js Custom Event Documentation](https://docs.adobe.com/content/help/en/target/using/implement-target/client-side/functions-overview/atjs-custom-events.html)
* [Using Data Providers in Adobe Target](use-data-providers-to-integrate-third-party-data.md)