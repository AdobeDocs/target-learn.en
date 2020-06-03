---
title: Use Recommendations APIs
keywords: recommendations;adobe recommendations;premium;api;apis
description: Adobe Target Recommendations includes a dedicated set of APIs that allow you to manage your catalog of recommendable products and/or content; manage your recommendations algorithms and campaigns; and deliver recommendations in JSON, HTML, or XML objects to be displayed in web, mobile, email, IOT, and other channels.
kt: KT-3815
audience: developer
doc-type: tutorial
activity: use
feature: recommendations;adobe recommendations;premium;api;apis
topics: recommendations;adobe recommendations;premium;api;apis
solution: Adobe Target
author: Judy Kim
---

# Configure Adobe I/O Authentication

The Adobe Target Admin APIs, including [!DNL Recommendations] Admin APIs, are secured by authentication to ensure only authorized users use them to access Adobe Target. Use the [Adobe I/O console](https://console.adobe.io/) to manage this authentication for all Adobe Experience Cloud solutions, including [!DNL Target].

This lesson walks through the preliminary steps required to generate authentication tokens that will be needed to successfully interact with Adobe Target APIs. In the sections that follow, you will:

1. Create an Adobe I/O integration.
2. Export Integration Details and Generate a Bearer Access Token.
3. Test the bearer access token.

## Create an Adobe I/O Target integration

In this section, you will access the Adobe I/O Console and create an integration for [!DNL Adobe Target]. For more information on integrations, reference the [documentation](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/integrations.md).

1. Generate your private key and public certificate, per [the documentation](https://www.adobe.io/authentication/auth-methods.html#!AdobeDocs/adobeio-auth/master/JWT/JWTCertificate.md). <!--as described in **Step 1** of [How to set up Adobe IO: Authentication - Step by Step](https://helpx.adobe.com/marketing-cloud-core/kb/adobe-io-authentication-step-by-step.html). After completing Step 1, return to this tutorial and resume with Step 2, below.--> The outcome of this step should be the creation of a `private.key` file and a `certificate_pub.crt` file. Return to this tutorial once you have generated these two files.

2. In the [Adobe Admin Console](https://adminconsole.adobe.com/), ensure your Adobe user account has been granted both [Product Admin](https://helpx.adobe.com/enterprise/using/admin-roles.html) and [Developer](https://helpx.adobe.com/enterprise/using/manage-developers.html) level access to [!DNL Target].

3. In the [Adobe I/O console](https://console.adobe.io/), click [!UICONTROL Create Integration].

   ![Admin Console Welcome screen](assets/configure-io-target-create-1-welcome.png)

4. Select **[!UICONTROL Access an API]**, then click **[!UICONTROL Continue]**.

5. Select the Experience Cloud Organization for which you want to create this integration. (Note it is likely you may only have access to a single Experience Cloud Organization.) 

   ![configure-io-target-create-1a-org.png](assets/configure-io-target-create-1a-org.png)

6. Select **[!DNL Adobe Target]**.

   ![configure-io-target-create-2-target](assets/configure-io-target-create-2-target.png)

7. Click **[!UICONTROL Continue]**.

8. Type a **name** and **description** for your integration, add your **public key**, and select the [product profile(s)](https://helpx.adobe.com/enterprise/using/manage-products-and-profiles.html) corresponding to the properties in which you are using [!DNL Recommendations]. (If you are not using properties, select the Default Workspace option.)

   ![configure-io-target-create-2a-target](assets/configure-io-target-create-2a-target.png)

   >[!NOTE]
   > 
   >In this tutorial, we name our integration "Target Integration." If you anticipate using your integration for more than just Adobe Target, you may want to name it accordingly. For example, you might choose to name it "Adobe APIs" or "Experience Cloud APIs," since it may be used with other solutions in the Adobe Experience Cloud.

9.  Click **[!UICONTROL Create Integration]**. You should receive the following message.
    ![configure-io-target-create-3-target](assets/configure-io-target-create-3-target.png)

## Export Integration Details and Generate the Bearer Access Token

Now that you have an Adobe I/O integration you can use for [!DNL Target], you will need to make sure to send details of that integration along with your Adobe API requests. These details are required in order to interact with several Adobe APIs, including several [!DNL Target] APIs. For example, the integration details include authorization and authentication information required by the [!DNL Target] Admin APIs. Therefore, to use the APIs with Postman, you will need to get the details of your Adobe I/O integration into Postman.

There are many ways to specify the details of your integration in Postman, but in this section, we take advantage of some pre-built features and collections. First, you will export the details of your integration into a Postman environment. Next, you will generate a bearer access token to grant you access to the necessary Adobe resources.

>[!NOTE]
>
>For video instructions applicable for any Experience Cloud solution, including [!DNL Target], see [Use Postman with Experience Platform APIs](https://docs.adobe.com/content/help/en/platform-learn/tutorials/apis/postman.html). The following sections of [Use Postman with Experience Platform APIs](https://docs.adobe.com/content/help/en/platform-learn/tutorials/apis/postman.html) are relevant to the [!DNL Target] APIs:
>
> 1. Export Adobe I/O Integration Details to Postman
> 2. Generate an Access Token with Postman
>
> A summary of these steps is shown below.

1. Still in the [Adobe I/O console](https://console.adobe.io/), navigate to your new integration's **[!UICONTROL Overview]** page. Note you may view your **Public key(s)**, **API Key (Client ID)**, and other information here.

   ![JWT1](assets/configure-io-target-jwt1.png)

2. In the **[!UICONTROL Overview]** tab, click **[!UICONTROL Export Details to Postman]**.
   ![JWT3a](assets/configure-io-target-jwt3a.png)
   This creates a JSON file of the environment.
3. In Postman, import the JSON file (environment).
   ![JWT3b](assets/configure-io-target-jwt3b.png)
4. In the Postman **Manage Environments** modal, click the name of the newly imported environment to inspect it. (Your environment name may be different from the one shown here.)
   ![JWT3c](assets/configure-io-target-jwt3c.png)
5. Note `CLIENT_SECRET` and `API_KEY` (along with other variables) have their values pre-populated, taken from your integration as defined in Adobe I/O. By contrast, note `PRIVATE_KEY`, `JWT_TOKEN`, and `ACCESS_TOKEN` are blank.
   ![JWT3d](assets/configure-io-target-jwt3d.png)
6. Copy and paste your private key, created earlier in the tutorial, into the **INITIAL VALUE** and **CURRENT VALUE** fields.
   ![JWT3e](assets/configure-io-target-jwt3e.png)
7. Generate your access token using the **[!UICONTROL IMS: JWT Generate + Auth via User Token]** request in the [Adobe I/O Access Token Generation Postman collection](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/ims).
   ![JWT3ff](assets/configure-io-target-jwt3ff.png)

   >[!NOTE]
   >
   >This bearer access token will be valid for 24 hours. Send the request again whenever you need to generate a new token.
8. Open the Manage Environments modal again, and select your environment.
   ![JWT3g](assets/configure-io-target-jwt3g.png)
9. Note the `ACCESS_TOKEN` value is now populated.
   ![JWT3h](assets/configure-io-target-jwt3h.png)

>[!NOTE]
>
>Q: We used to have to generate a JSON Web Token (JWT), which we would then exchange for the bearer access token. Is the JWT no longer required?
>
>A: The JWT is still required, but in the steps above, it is handled through the IMS request. One less step!

## Test the bearer access token

In this exercise, you will use your new bearer access token by sending an API request that retrieves a list of activities from your [!DNL Target] account. A successful response indicates your Adobe I/O integration and authentication are operating as expected in order to use the API.

1. Import the [Adobe Target Admin APIs Postman Collection](https://developers.adobetarget.com/api/#admin-postman-collection). Note the **[!UICONTROL List activities]** request.
   ![testtoken1](assets/configure-io-target-testtoken1.png)
2. Note that variables such as `{{access_token}}` are initially unresolved. You could resolve this in several different ways—for example, you could define a new collection variable called `{{access_token}}`—but in this tutorial, you will instead change the API request to leverage the Postman environment you were previously using. This will enable the environment to continue to serve as a single, consistent consolidation of all variables common across Adobe APIs.
   ![testtoken2](assets/configure-io-target-testtoken2.png)
3. Type to replace `{{access_token}}` with `{{ACCESS_TOKEN}}`.
   ![testtoken3](assets/configure-io-target-testtoken3.png)
4. Type to replace `{{api_key}}` with `{{API_KEY}}`.
   ![testtoken4](assets/configure-io-target-testtoken4.png)
5. Type to replace `{{tenant}}` with `{{TENANT_ID}}`. Note `{{TENANT_ID}}` is not yet recognized.
   ![testtoken4](assets/configure-io-target-testtoken4a.png)
6. Open the Manage Environments modal, and select your environment.
   ![JWT3g](assets/configure-io-target-jwt3g.png)
7. Type to add a new `{{TENANT_ID}}` environment variable. Copy and paste your Tenant ID value into the **INITIAL VALUE** and **CURRENT VALUE** fields for your new `TENANT_ID` environment variable.
   ![testtoken5](assets/configure-io-target-testtoken5.png)
      >[!NOTE]
   >
   >The Tenant ID is different from your [!DNL Target] `clientcode`. The Tenant ID exists in the URL when you are logged in to [!DNL Target]. To obtain your Tenant ID, log in to the [!DNL Adobe Experience Cloud], open [!DNL Target], and click the [!DNL Target] card. Use the Tenant ID value as noted in the URL subdomain.
   >
   >For example, if your URL when logged in to Adobe Target is
   >https://mycompany.experiencecloud.adobe.com/...
   >then your Tenant ID is "mycompany."

8. Send your request, after ensuring you have selected the correct environment. You should receive a response containing your list of activities.
   ![testtoken6](assets/configure-io-target-testtoken6.png)

Congratulations! Now that you have verified your Adobe I/O authentication, let's continue to use it, this time with the [!DNL Recommendations] API.

[Next "Managing Your Catalog with APIs" >](3manage-catalog.md)
