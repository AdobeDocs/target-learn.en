---
title: Recommend Products on a Product Page
description: Learn how to recommend products on a Product Page
seo-description:
seo-title: Recommend Products on a Product Page with Adobe Target
solution: Adobe Target
---

# Recommend products on a Product Page

## Exercise 2.3 – Tagging Your Site

### Strategy: Tagging Your Site

One common Recommendations implementation option uses both feeds and page parameters.

This method is often preferred by retailers, who tend to have relatively consistent product catalogs, but with frequent changes to a few product attributes (such as price and inventory) due to sales, seasonal promotions, or seasonal inventory changes.

Whether using a CSV file or Google product file, use a feed to provide all product attributes that stay fairly consistent over time.

Required:

* Item ID or SKU (entity.id)

Other static parameters:

* Category (entity.category)
* Brand (entity.brand)
* Description (entity.message)
* Other custom attributes

Attributes that are not consistent may be provided via feed, but often should also be provided on a more frequent basis via page parameters or API:

* Inventory level (entity.inventory)
* Price (entity.value)

Priority is given to whichever set of data is received most recently. If you pass the feed first and then update the page parameters, changes that are made in the page parameters will be shown, replacing item information passed in the feed.

#### Implementation According to Page Type

Page type will influence your Recommendations implementation. For example, the kinds of recommendations you want to present will differ between a product page, a category page, or your home page. For each page type, you should be sure to pass the appropriate key values for the right kind of recommendations.

The targetPageParams functions shown below is especially helpful if you are using a tag management solution to implement your pages. Adobe Launch or Adobe Dynamic Tag Manager (DTM) places the at.js/mbox.js reference and the targetPageParams function on your page and allows you to configure the values. You should either place that function before your at.js/mbox.js call, or put it in the Extra JavaScript section of your at.js/mbox.js.

#### Product Page

On a product page, you will want to recommend items that are related to the current item and/or the current item’s category. You also want to send any frequently changing attributes (such as value and inventory), in addition to the identifying key for the item.

![22](../images/image22.png)

#### Category Page

On a category page, you probably want to restrict your recommendations to products or content within that category. To achieve this, be sure to pass the category ID of the page:

![23](../images/image23.png)

#### Cart Page

On a cart page, you likely want to exclude some items from your recommendations, such as the items that are already in the cart.

![24](../images/image24.png)

#### Order Confirmation Page

On an order confirmation page, you might want to show the order total, and the order ID, and show the products that were purchased, without recommending additional items. You can implement a second mbox to capture the order information.

![25](../images/image25.png)

### Examine Adobe Target Call Using Developer Tools

Once your pages are properly tagged, you should review the Target server call to confirm if your implementation is working properly. By using native browser developer tools, we can inspect and evaluate components of the Target server request.

1. Navigate to a product detail page (e.g. <http://localhost:4503/content/we-retail/us/en/products/men/coats/el-gordo-down-jacket.html#meskwielt>)

2. In your Chrome browser window, open Developer Tools.

    ![26](../images/image26.png)

3. Select the Network tab and refresh the current page.

4. Type “mbox” in the search filter and select the request that appears.

5. After selecting the query at left, the **Headers** tab shows the information sent to Target, allowing you to confirm that the call is working as expected. Confirm that the **entity.id** and **entity.categoryId** are being sent to Target.

    ![27](../images/image27.png)

6. The **Preview** tab shows the actions returned from Target.

    ![28](../images/image28.png)

We’ll cover more advanced troubleshooting methods later which allow you to perform a deeper inspection of the Target Recommendations configuration.

## Add Entity Parameters for Recommendations (Target Premium)

Entity parameters are used in [Recommendations implementations](https://marketing.adobe.com/resources/help/en_US/target/recs/c_plan_implement.html) for three main reasons:

1. As a key to trigger product recommendations. For example, when using a recommendations algorithm like "People who viewed Product X, also viewed Y," "X" is the "key" of the recommendation. It is usually the product sku (`entity.id`) or category (`entity.categoryId`) that you are currently viewing.
1. To collect visitor behavior to power recommendations algorithms, such as "Recently Viewed Products" or "Most Viewed Products"
1. To populate the Recommendations catalog. Recommendations contains a database of all of the products or articles on your website, so they can be served in the recommendation offer. For example, when recommending products, you typically want to display attributes like the product name (`entity.name`) and image (`entity.thumbnailUrl`). Some customers populate their catalog using backend feeds, but they can also be populated using entity parameters in mbox calls.

Just give the parameter a name prefixed with "entity." and map it to the relevant data element. Note that some common entities have reserved names that must be used (e.g. entity.id for the product sku).

![Adding Entity Parameters](../images/target-entityParameters.png)

Below is an optional exercise for Target Premium customers to add the `entity.id` and `entity.categoryId` parameters to relevant pages in the global mbox request. In order to deliver recommendations without flicker, it is critical to pass the `entity.id` and `entity.categoryId` parameters at the top of the page, in the global mbox. If your data layer id defined before the Launch embed codes, you can pass the other catalog entities here, too. Since you have already created multiple data elements in this tutorial, screenshots are not included for every step.

>[!WARNING] If you have already implemented Recommendations in your Target account, completing the steps in this exercise add invalid products to your catalog. Create a new Host Group in Target and associate the `enablementadobe.com` domain with this new Group before proceeding. Alternatively, you can read through the instructions to understand the implementation

### Create Data Element for Product Id

You will use this to set the reserved `entity.id` parameter to key recommendations algorithms, collect visitor behavior, and populate the catalog

1. Click **[!UICONTROL Data Elements]** in the top navigation
1. Click **[!UICONTROL Add Data Element]**
1. Name the data element `Product ID`
1. Select **[!UICONTROL Data Element Type > JavaScript Variable]**
1. Use `digitalData.product.0.productInfo.sku` as the `Path to Variable`
1. Check the `Force lowercase value` option
1. Check the `Clean text` option
1. Click **[!UICONTROL Save to Library and Build]**

### Create Data Element for Product Category

You will use this to set the reserved `entity.categoryId` parameter to key recommendations algorithms, collect visitor behavior, and populate the catalog. It is possible to collect multiple category ids in a comma-separated list.

1. Click **[!UICONTROL Add Data Element]**
1. Name the data element `Product Category`
1. Select **[!UICONTROL Data Element Type > JavaScript Variable]**
1. Use `digitalData.product.0.productInfo.description` as the `Path to Variable`
1. Check the `Clean text` option
1. Click **[!UICONTROL Save to Library and Build]**

### Create Data Element for Product Name

You will use this to set the reserved `entity.name` parameter to populate the catalog with the product name

1. Click **[!UICONTROL Add Data Element]**
1. Name the data element `Product Name`
1. Select **[!UICONTROL Data Element Type > JavaScript Variable]**
1. Use `digitalData.product.0.productInfo.title` as the `Path to Variable`
1. Check the `Clean text` option
1. Click **[!UICONTROL Save to Library and Build]**

### Create Data Element for Product Path

You will use this to set the reserved `entity.pageUrl` parameter to populate the catalog with the URL path of the product detail page so you can create links in Recommendations offers

1. Click **[!UICONTROL Add Data Element]**
1. Name the data element `Product Path`
1. Select **[!UICONTROL Data Element Type > Page Info]**
1. Select  **[!UICONTROL Attribute > Pathname]**
1. Click **[!UICONTROL Save to Library and Build]**

### Create Data Element for Product Thumbnail Path

You will use this to set the reserved `entity.thumbnailUrl` parameter with the URL of a thumbnail image so you present visual product Recommendations

1. Click **[!UICONTROL Add Data Element]**
1. Name the data element `Product Thumbnail Path`
1. Select **[!UICONTROL Data Element Type > Custom Code]**
1. Use the following custom code:

   ```javascript
   var myStr = digitalData.page.pageInfo.pageName;
   var newStr = myStr.replace(/:/g, '/');
   return '/' + newStr + '/jcr:content/root/product/image.thumbnail.160.png';
   ```

1. Click **[!UICONTROL Save to Library and Build]**

## Add Entity Parameters to the Target request

### Add a Rule to Pass the Entity Parameters to the Global Mbox

Now that you have created all of the data elements you need to add them to the global mbox call. Most of these data elements only exist on the product detail pages, so you will need a new rule that will only fire on the product details page.

1. Go to the **[!UICONTROL Rules]** in the top navigation and then click **[!UICONTROL Add Rule]**

    ![Add a new rule](../images/target-recs-addRuleProdDetails.png)

1. Name the rule `Product Details - Library Loaded - 40`

1. Click **[!UICONTROL Events > Add]** to open the `Event Configuration` screen

    ![Name the rule and add the event](../images/target-recs-prodDetail-nameAddEvent.png)

   1. Select **[!UICONTROL Event Type > Library Loaded]**

   1. Change the `Order` to `40`

   1. Click **[!UICONTROL Keep Changes]**
  
    ![Configure the event](../images/target-recs-prodDetail-event.png)

1. Click **[!UICONTROL Conditions > Add]** to open the `Condition Configuration` screen

    ![Configure the event](../images/target-recs-prodDetail-addCondition.png)

   1. Select **[!UICONTROL Condition Type > Value Comparison]**
   1. Use the data element picker, choose `Product ID`
   1. Select  **[!UICONTROL Is Truthy]** from the comparison operator dropdown
   1. Click **[!UICONTROL Keep Changes]**

   ![Define the condition](../images/target-recs-prodDetail-condition.png)

1. Click **[!UICONTROL Actions > Add]** to open the `Action Configuration` screen

   ![Add a new action](../images/target-recs-prodDetail-addAction.png)

   1. Select **[!UICONTROL Extension > Adobe Target]**

   1. Select **[!UICONTROL Action Type > Add Params to Global Mbox]**

   1. Add the parameters for `entity.id`, `entity.name`, `entity.pageUrl`, `entity.categoryId`, `entity.thumbnailUrl`, assigning their values to the data elements created earlier

   1. Click  **[!UICONTROL Keep Changes]**

   ![Add a new action](../images/target-recs-prodDetail-action.png)

1. Click **[!UICONTROL Save to Library and Build]**

   ![Click Save to Library and Build](../images/target-recs-prodDetail-save.png)

Typically, you would set up a similar rule on the product category pages that would that would pass the `entity.categoryId` to Target on the category pages. You could then deliver category-based recommendations to these pages.

### Validate the Entity Parameters

1. Open the We.Retail site to a [product details page](https://aem.enablementadobe.com/content/we-retail/us/en/products/men/coats/portland-hooded-jacket.html#meotwipot-S)
1. Make sure the Debugger is mapping the Launch property to *your* Development environment, as described in the earlier lesson

   ![Your Launch development environment shown in Debugger](../images/switchEnvironments-debuggerOnWeRetail.png)
1. Open the Debugger
1. Go to the Target tab
1. Open your client code
1. You should see the entity parameters in every global mbox request on a product detail page:

   ![The Entity Parameters should be visible in the global mbox request on product detail pages](../images/target-debugger-recs.png)

1. Also, if you turn on console logging for Launch on the `Tools` tab

   ![The Entity Parameters should be visible in the global mbox request on product detail pages](../images/target-debugger-consoleLogging.png)

1. You should see that the rule fires

   ![The Entity Parameters should be visible in the global mbox request on product detail pages](../images/target-recs-consoleLogMet.png)

1. Now go to some pages that are not Product Detail pages. Do the Debugger logs show that the rule fires? Are the entity parameters added to the global mbox request?

## Optional: Add Custom Mboxes for Profile or Entity Values

Sometimes important data you would like to use for personalization is not defined on the page before the Launch embed codes. For example, it might be hardcoded on the bottom of the page or get returned from an asynchronous API request.

This data can still be sent to Target using an additional request. Although it will not be optimal to use this request for content delivery since the page will already visible, it can still be used to enrich the visitor profile for later use or to populate the Recommendations catalog.

Below is an optional exercise for Target Premium customers to add the `entity.value` and `entity.message` parameters to Product Detail pages to enrich the Recommendations catalog. The same technique can be used by Target Standard customers to pass profile parameters to enrich the visitor profile.

>[!WARNING] As mentioned in the earlier section `Add Entity Pararameters for Recommendations (Target Premium)`, if you have already implemented Recommendations in your Target account, completing the steps in this exercise add invalid products to your catalog. Create a new Host Group in Target and associate the `enablementadobe.com` domain with this new Group before proceeding. Alternatively, you can read through the instructions to understand the implementation

On the We.Retail site, for example, there are several attributes that would be useful to have in our Recommendations catalog for the `entity.value` and `entity.description` entities. However, the values are available in DOM elements below the Launch embed codes. Let's start by defining the data elements.

### Create Data Element for Product Price

You will use this to set the reserved `entity.value` parameter to populate the catalog with the price of the product

1. Click **[!UICONTROL Add Data Element]**
1. Name the data element `Product Price`
1. Select **[!UICONTROL Data Element Type > Custom Code]**
1. Use the following custom code:

    ```javascript
    return document.querySelectorAll(".we-Product-price")[0].textContent.slice(1);
    ```

1. Click **[!UICONTROL Save to Library and Build]**

### Create Data Element for Product Description

You will use this to set the reserved `entity.message` parameter to populate the catalog with a short description of the product

1. Click **[!UICONTROL Add Data Element]**
1. Name the data element `Product Description`
1. Select **[!UICONTROL Data Element Type > DOM Attribute]**
1. Use `.we-Product-description` as the **[!UICONTROL From the DOM element matching the CSS Selector]**
1. Select **[!UICONTROL Use the value of > text]**
1. Check the `Clean text` option
1. Click **[!UICONTROL Save to Library and Build]**

### Add a Rule to Pass the Entity Parameters in a Custom

1. Go to the **[!UICONTROL Rules]** in the top navigation and then click **[!UICONTROL Add Rule]**

    ![Add a new rule](../images/target-recs-addRuleProdDetails-windowLoaded.png)

1. Name the rule `Product Details - Window Loaded`

1. Click **[!UICONTROL Events > Add]** to open the `Event Configuration` screen

   ![Name the rule and add the event](../images/target-recs-prodDetail-nameAddEvent-windowLoaded.png)

   1. Select **[!UICONTROL Event Type > Window Loaded]**

   1. Click **[!UICONTROL Keep Changes]**
  
       ![Configure the event](../images/target-recs-prodDetail-event-windowLoaded.png)

1. Click **[!UICONTROL Conditions > Add]** to open the `Condition Configuration` screen

    ![Configure the event](../images/target-recs-prodDetail-addCondition-windowLoaded.png)

   1. Select **[!UICONTROL Condition Type > Value Comparison]**
   1. Use the data element picker, choose `Product ID`
   1. Select  **[!UICONTROL Is Truthy]** from the comparison operator dropdown
   1. Click **[!UICONTROL Keep Changes]**

      ![Define the condition](../images/target-recs-prodDetail-condition-windowLoaded.png)

1. Click **[!UICONTROL Actions > Add]** to open the `Action Configuration` screen

   ![Add a new action](../images/target-recs-prodDetail-addAction-windowLoaded.png)

   1. Select **[!UICONTROL Action Type > Custom Code]**

   1. Click the **[!UICONTROL </> Open Editor]** button to open the `Code Editor`

      ![Use a Custom Code action](../images/target-recs-prodDetail-actionCustom-windowLoaded.png)

   1. Paste the following code into the `Code Editor`. Note that we are are going to add one more parameter `entity.event.detailsOnly:true` to indicate that this request is simply for the collection of catalog data and should not increment a view for the product in the Recommendations algorithms.

      ```javascript
      adobe.target.getOffer({
        "mbox": "recs-entities",
        "params": {
          "entity.id": _satellite.getVar('Product ID'),
          "entity.value": _satellite.getVar('Product Price'),
          "entity.message": _satellite.getVar('Product Description'),
          "entity.event.detailsOnly":"true"
        },
        "success": function(offer) {
      },
        "error": function(status, error) {
          console.log('Error', status, error);
        }
      });
      ```

   1. Click the **[!UICONTROL Save]** button

      ![Save the Custom](../images/target-recs-prodDetail-customCode-windowLoaded.png)

   1. Click  **[!UICONTROL Keep Changes]**

      ![Click Keep Changes](../images/target-recs-prodDetail-keepChanges-windowLoaded.png)

1. Click **[!UICONTROL Save to Library and Build]**

   ![Click Save to Library and Build](../images/target-recs-prodDetail-save.png)

A few things to note:

* In the request, you also passed the `entity.id`. Since the `entity.id` is the key, this is required to make sure the other entities are attached to the correct catalog item.
* In order to avoid complications with the A4T integration, the custom mbox name `recs-entities` was used.

* Because the `applyOffer()` function was not used, this mbox cannot be used to apply offers to the page
  
* If your use case is to pass profile parameters instead of entity parameters, you would just update the parameter names and data elements in the code above.

### Validate the Custom Mbox and Parameters

1. Open the We.Retail site to a [product details page](https://aem.enablementadobe.com/content/we-retail/us/en/products/men/coats/portland-hooded-jacket.html#meotwipot-S)
1. Make sure the Debugger is mapping the Launch property to *your* Development environment, as described in the earlier lesson

   ![Your Launch development environment shown in Debugger](../images/switchEnvironments-debuggerOnWeRetail.png)
1. Open the Debugger
1. Go to the Target tab
1. Open your client code
1. You should see the new `recs-entities` request with the `entity.id`, `entity.value`, and `entity.message` parameters fire on all product detail pages:

   ![The new mbox and its Entity Parameters should be visible on product detail pages](../images/target-debugger-recsEntities.png)

In this lesson, you will learn effective techniques to recommend products on a Product Page

## Learning Objectives

At the end of this lesson, you will be able to:

1. do this

## Prerequisites

You should have already completed the lessons in .

## First thing

## Exercise 4.2 – Use Criteria on a Product Detail Page

We now need to put this Criteria into action on your product detail page! In order to make the most of our limited time in this lab, we’ve pre-created an Activity for you which contains an identical criteria to the one you just created. Find the activity titled **Lab Solution - Lesson 4.2 PDP Recs** and open the Activity Overview.

Note the activity location includes any URL that matches the string `https://aem.enablementadobe.com/content/we-retail/us/en/products.html` which means the recommendations will be displayed on all Product Detail Pages:

![84](../images/image84.png)

Note that the Criteria is selected and has results ready:

![85](../images/image85.png)

Use the **Download data** option and note that different recommendations have been produced per product SKU:

![86](../images/image86.png)

Once the activity has been activated, you will see recommendations that differ on each product detail page:

![87](../images/image87.png)

Note the following:

1. Recommended items differ by product viewed.
2. The recommended items are in the same category as the viewed item.
3. Not all slots in the design template are filled with recommended items.
4. Not all items have recommended items.

Items 3 & 4 are true because we did not enable backup recommendations and because we used a restrictive filtering rule (category equals current item’s category) to narrow down the recommended items. In the next exercise, we will see how we can use multiple sets of recommendations to fill in the rest of the slots.

### Creating a Sequence

We will create a sequence for our product detail page that displays in order of descending preference:

- People Who Viewed This, Viewed That (in the same category)
- People Who Viewed This, Viewed That (no category restriction)
- Backup items from Most Viewed across the site

1. Return to the **Recommendations > Criteria** library screen.

2. Click **Create Criteria** and select **Create Criteria Sequence**.

    ![88](../images/image88.png)

3. The first several steps are identical to those we did in Lesson 4.1 to create a Criteria.

    1. **Criteria Name:** This identifies the criteria in the Adobe Target application. Enter **YOURNUMBER – PDP Criteria Sequence**.

    2. **Display Title:** This public-facing display text can be returned in the recommendations template on pages using this criteria and can be used in troubleshooting. For this lab, enter the same title as above (**YOURNUMBER – PDP Criteria Sequence**).

    3. **Description:** An optional description detailing the purpose and/or selected settings of the algorithm.

    4. **Industry Vertical:** Our site is a web retailer, so leave the default option of **Retail / Ecommerce** selected.

    5. **Page Type:** We are creating recommendations for a **Product Page** so clear the **Home Page** selection, search for, and select **Product Page**.

        ![89](../images/image89.png)

4. Adjust the **Content** settings. When you create a criteria sequence, backup recommendation and partial design rendering settings are ignored for the individual criteria the make up the sequence. To use backup recommendations and partial design rendering you must enable them for the sequence. If you choose to allow backup recommendations, you can also choose whether to apply inclusion rules to the backups. Select the appropriate toggles to ensure we have a full tray of recommendations for every product in our catalog.

    ![90](../images/image90.png)

5. Add the criteria to the sequence under **Sequence Order:**

    1. Start by adding the **YOURNUMBER – Products from Same Category** criteria.

        ![91](../images/image91.png)

    1. Then add the **Solution - Products from Other Categories** criteria.

        ![92](../images/image92.png)

6. **Save and Close** the Criteria Sequence.

### Using the Sequence on the Product Detail Page

We now need to put this Criteria Sequence into action on your product detail page. In order to make the most of our limited time in this lab, we’ve pre-created an Activity for you which contains an identical criteria sequence to the one you just created. Find the activity titled **Lab Solution - Lesson 4.3 PDP Criteria Sequence** and open the Activity Overview.

As you did in Lesson 4.2, explore the configuration of this activity and examine the data download. Once the activity has been activated, you will see recommendations that differ on each product detail page. Note these similarities and differences from Lesson 4.2:

1. Recommended items still differ by product viewed.
2. The recommended items are no longer all in the same category as the viewed item.
3. Now, all slots in the design template are filled with recommended items.
4. Now, all items have recommended items.

## Exercise 4.4 - Troubleshooting with mboxTrace

mboxTrace enables you to receive trace information attached to mbox replies. Trace information reflects the outcome of an mbox call (for example, a conversion or an impression) and any additional data that may help in determining why this particular outcome happened, such as a set of available branches among which the selection was made in a campaign. Use this information to debug content delivery.

Because mboxTrace can expose campaign data and profile data to external parties, an authorization token is required. The authorization token can be retrieved in the Target UI. The token is valid for six hours.

To use the authorization token:

1. Click Setup > Implementation.
2. Click Generate Authentication Token.
3. Add the generated token as a parameter to your URL to enable one of the advanced debugging tools.

![93](../images/image93.png)

The following parameters are available:

![94](../images/image94.png)

### mboxTrace with the Experience Cloud Debugger

- Ensure you are still logged into Experience Cloud
- Navigate to the Target server call, then select “Target Trace”
- Toggle the switch for “Enable Target Traces”

![95](../images/image95.png)

![96](../images/image96.png)

When applying mboxTrace, the Recommendations area will contain “embedded” code that can be extracted to a text editor for further evaluation:

![97](../images/image97.png)

In the browser console, you can access mboxTrace by searching for “mbox” in the network call and finding “trace” in the preview of the global mbox request:

![98](../images/image98.png)
