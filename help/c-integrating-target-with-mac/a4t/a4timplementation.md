---
keywords: A4T;Adobe Analytics;Analytics-based activity;Analytics report suite;report suite;Analytics Target integration;configure report suite;at.js;atjs;adobe experience platform web sdk;aep web sdk;platform web sdk
description: Follow the steps required to implement Analytics for [!DNL Target] (A4T) in your Adobe [!DNL Target] and Adobe Analytics solutions.
title: How do I Implement Analytics for [!DNL Target] (A4T)?
feature: Analytics for Target (A4T)
exl-id: b5269b9e-01ef-449a-bb03-3dcc2cd68af7
---
# Analytics for [!DNL Target] implementation

Several steps are required when implementing [!DNL Adobe Analytics] as the reporting source for [!DNL Adobe Target] (A4T). The process varies depending on whether you implement A4T with the [[!DNL Adobe Experience Platform Web SDK]](https://experienceleague.adobe.com/docs/experience-platform/edge/home.html) or with at.js.

## ![Adobe Experience Platform Web SDK badge](/help/assets/platform.png) Implementation steps for an Adobe Experience Platform Web SDK implementation {#platform}

The following sections describe the steps required to deploy this integration to your site if you are plan to use the Platform Web SDK:

### Step 1: Request provisioning for [!DNL Analytics] and [!DNL Target]

Before you implement A4T, you must be provisioned for [!DNL Analytics] and [!DNL Target]. [Use this form to request to be provisioned](https://adobe.allegiancetech.com/cgi-bin/qwebcorporate.dll?idx=X8SVES).

### Step 2: Set up user permissions

User account requirements must be met before you can create an activity based on [!DNL Analytics] in [!DNL Target]. See [User permission requirements](/help/c-integrating-target-with-mac/a4t/account-reqs.md).

### Step 3: Create an Edge configuration

Create an Edge configuration using [!DNL Adobe Experience Platform] using the edge configuration tool. Configure the [[!DNL Analytics] and [!DNL Target] edge configuration settings](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/datastreams.html). 

### Step 4: Install and configure the Platform Web SDK

To start delivering [!DNL Target] experiences and to apply [!DNL Analytics] for tracking and analysis purposes, [Install](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/installing-the-sdk.html) and [configure](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html) the Platform Web SDK on your site pages.

### Step 5: Enable the options for using A4T

In the [!DNL Target] UI, click **[!UICONTROL Administration]** > **[!UICONTROL Visual Experience Composer]**, then choose either **[!UICONTROL Select per activity]** or **[!UICONTROL Adobe Analytics]**.

* **[!UICONTROL Select per activity]** lets you choose between [!DNL Target] and [!DNL Analytics] when creating each activity.
* **[!UICONTROL Adobe Analytics]** sets [!DNL Analytics] as the reporting source for all activities that you create.

## ![at.js badge](/help/assets/atjs.png) Implementation steps for an at.js implementation{#section_73961BAD5BB4430A95E073DE5C026277}

The following sections describe the steps required to deploy this integration to your site if you are plan to use at.js: 

### Step 1: Request provisioning for Analytics and Target

After you implement [!DNL Analytics] as the reporting source for [!DNL Target], you must be provisioned for [!DNL Analytics] and [!DNL Target]. [Use this form to request to be provisioned](https://www.adobe.com/go/audiences).

### Step 2: Set up user permissions

User account requirements must be met before you can create an [!DNL Analytics]-based activity in [!DNL Target]. See [User permission requirements](/help/c-integrating-target-with-mac/a4t/account-reqs.md).

### Step 3: Implement the Experience Cloud Visitor ID service

The visitor ID service lets you identify users across [!DNL Adobe Experience Cloud] solutions. Implement or migrate to the required version of the Experience Cloud Visitor ID. For more information, see "Implementation Requirements" in [Before you implement](/help/c-integrating-target-with-mac/a4t/before-implement.md).

See [Implement the Experience Cloud ID Service for Target](https://experienceleague.adobe.com/docs/id-service/using/implementation/setup-target.html) in the *Experience Cloud Visitor ID Service* documentation.

### Step 4: Update AppMeasurement for JavaScript or s_code

Implement or migrate to the required version of appMeasurement.js. For more information, see "Implementation Requirements" in [Before you implement](/help/c-integrating-target-with-mac/a4t/before-implement.md).

For new implementations, see [JavaScript implementation overview](https://experienceleague.adobe.com/docs/analytics/implementation/js/overview.html) in the *Analytics Implementation Guide*.

For a migration, see [Migrating to AppMeasurement for JavaScript](https://experienceleague.adobe.com/docs/analytics/implementation/js/migrate-from-hcode.html) in the *Analytics Implementation Guide*.

### Step 5: Download and update at.js

Implement or migrate to the required version of at.js using your production account. No modifications are required on the code.

For more information, see "Implementation Requirements" in [Before you implement](/help/c-integrating-target-with-mac/a4t/before-implement.md).

### Step 6: Host at.js

If you previously deployed at.js, you can replace your existing file with the updated version. For more information, see "Implementation Requirements" in [Before you implement](/help/c-integrating-target-with-mac/a4t/before-implement.md).

Otherwise, this file can be hosted along with the Visitor ID service and AppMeasurement for JavaScript files. These files must be hosted on a web server that is accessible to all pages on your site. You need the path to these files in the next step.

### Step 7: Reference at.js on all site pages {#step7}

Include at.js below VisitorAPI.js by adding the following line of code in the tag on each page:

For at.js:

```javascript
<script language="JavaScript" type="text/javascript"
src="http://INSERT-DOMAIN-AND-PATH-TO-CODE-HERE/at.js"></script>
```

The VisitorAPI.js must be loaded before at.js. If you are updating an existing at.js file, make sure that you verify the load order.

The default setting for [!DNL Target] and [!DNL Analytics] integration, from an implementation perspective, is to use the SDID that is passed from the page to stitch the [!DNL Target] and [!DNL Analytics] request together on the backend automatically. 

You can control how and when to send analytics data related to [!DNL Target] to [!DNL Analytics] for reporting purposes. If you do not want to opt in to the default settings of having [!DNL Target] and [!DNL Analytics] automatically stitch the analytics data via the SDID, set **analyticsLogging = client_side** via **window.targetGlobalSettings**. Note: any versions below 2.1 do not support this approach.

For example:

```javascript
window.targetGlobalSettings = {
  analyticsLogging: "client_side"
};
```

This set up has a global effect, which means that every call made by at.js has **analyticsLogging: "client_side"** sent within the [!DNL Target] requests and an analytics payload is returned for every request. When this option is set up, the format of the payload that is returned looks like the following:

```javascript
"analyticsDetails": [{
   "payload": {
      "pe": "tnt",
      "tnta": "167169:0:0|0|100,167169:0:0|2|100,167169:0:0|1|100"
   }
}]
```

The value from the `payload.tnta` property can then be forwarded to Analytics via the [Data Insertion API](https://helpx.adobe.com/analytics/kb/data-insertion-api-post-method-adobe-analytics.html) via the parameter `<a4t>`. For Auto-Allocate and Auto-Target activities, you must also forward the sessionId. For more information, see [Analytics for Target (A4T) reporting](https://adobetarget-sdks.gitbook.io/docs/integration-with-experience-cloud/analytics-for-target-a4t-reporting) in the *Adobe Target SDKs* guide. 

If a global setting is not desired and a more on-demand approach is preferable, use the at.js function [getOffers()](/help/c-implementing-target/c-implementing-target-for-client-side-web/adobe-target-getoffers-atjs-2.md) by passing in **analyticsLogging: "client_side"**. The analytics payload is returned for this call only and the [!DNL Target] backend does not forward the payload to [!DNL Analytics]. By pursuing this approach, every at.js [!DNL Target] request returns the payload by default, but instead only when desired and specified. 

For example:

```javascript
adobe.target.getOffers({
      request: {
        experienceCloud: {
          analytics: {
            logging: "client_side"
          }
        },
        prefetch: {
          mboxes: [{
            index: 0,
            name: "a1-serverside-xt"
          }]
        }
      }
    })
    .then(console.log)
```

This call invokes a response from which you can extract the analytics payload. 

The response looks like the following:

```javascript
{
  "prefetch": {
    "mboxes": [{
      "index": 0,
      "name": "a1-serverside-xt",
      "options": [{
        "content": "<img src=\"http://s7d2.scene7.com/is/image/TargetAdobeTargetMobile/L4242-xt-usa?tm=1490025518668&fit=constrain&hei=491&wid=980&fmt=png-alpha\"/>",
        "type": "html",
        "eventToken": "n/K05qdH0MxsiyH4gX05/2qipfsIHvVzTQxHolz2IpSCnQ9Y9OaLL2gsdrWQTvE54PwSz67rmXWmSnkXpSSS2Q==",
        "responseTokens": {
          "profile.memberlevel": "0",
          "geo.city": "bucharest",
          "activity.id": "167169",
          "experience.name": "USA Experience",
          "geo.country": "romania"
        }
      }],
      "analytics": {
        "payload": {
          "pe": "tnt",
          "tnta": "167169:0:0|0|100,167169:0:0|2|100,167169:0:0|1|100"
        }
      }
    }]
  }
}
```

The payload can then be forwarded to [!DNL Analytics] via the [Data Insertion API](https://helpx.adobe.com/analytics/kb/data-insertion-api-post-method-adobe-analytics.html).

### Step 8: Validate the implementation {#step8}

Load your pages after you have updated the JavaScript libraries to confirm that the `mboxMCSDID` parameter values in [!DNL Target] calls match the `sdid` parameter value in the [!DNL Analytics] page-view call.

It is especially important to confirm that these values match in Single Page Applications (SPAs) where the order of calls is not always predictable.

>[!NOTE]
>
>The matching of these values is required for A4T to function correctly.

### Step 9: (Optional) Remove previous integration code

Adobe recommends that you remove the previous integration to simplify your implementation and eliminate the need to sort out discrepancies between the systems. You can remove any code you have deployed for a previous SC to T&T integration, including `mboxLoadSCPlugin`.

### Step 10: Enable the options for using Analytics as the reporting source for Target

In [!DNL Target], click **[!UICONTROL Administration > Visual Experience Composer]** and choose either **[!UICONTROL Select per activity]** or **[!UICONTROL Adobe Analytics]** to enable the options.

* **[!UICONTROL Select per activity]** lets you choose between [!DNL Target] and [!DNL Analytics] when creating each activity.
* **[!UICONTROL Adobe Analytics]** sets [!DNL Analytics] as the reporting source for all activities that you create.


