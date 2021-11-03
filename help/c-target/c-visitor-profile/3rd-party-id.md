---
keywords: mbox;mbox3rdPartyId;profile syncing;profile synch;PCID
description: Learn how to use the mbox3rdPartyId, which is your organization's visitor ID, such as membership ID or your organization's loyalty program.
title: How Do I Use Real-Time Profile Syncing for mbox3rdPartyId?
feature: Audiences
exl-id: ed409225-fa35-49da-87d1-1770221f2ae0
---
# Real-time profile syncing for mbox3rdPartyId

The `mbox3rdPartyId` in [!DNL Adobe Target] is your company's visitor ID, such as the membership ID for your company's loyalty program.

When a visitor logs in to a company's site, the company typically creates an ID that is tied to the visitor's account, loyalty card, membership number, or other applicable identifiers for that company.

When a visitor accesses a page on which [!DNL Target] is enabled, that visitor is assigned a [!DNL Target] PCID. If the visitor then logs in, and the implementation passes the `mbox3rdPartyId` to [!DNL Target], [!DNL Target] connects that visitor's `mbox3rdPartyId` with the [!DNL Target] PCID.

Every three to five minutes, updates are synced with the database. When the visitor logs out, the merged data replaces the previous data associated with the `mbox3rdPartyId`, creating a complete record of that visitor's actions. If the same attribute exists in both IDs--for example, the PCID has category=hats and the `mbox3rdPartyId` has category=skis, or if the visitor saw experience A before logging in, but experience B is stored in the `mbox3rdPartyId`--the attribute stored in the `mbox3rdPartyId` overwrites the attribute from the PCID. If the visitor was in one activity or experience before logging in, but a different activity and experience are stored in the `mbox3rdPartyId`, after logging in, that visitor is placed into the `mbox3rdPartyId` activity and experience.

|  PCID (Not Logged In)  | mbox3rdPartyId (Logged In)  | Merged and Saved to mbox3rdPartyId  |
|---|---|---|
|  category=hats  | category=skis  | category=skis  |
|   | store=94103  | store=94103  |
|  Activity 1, Experience A  | Activity 1, Experience B  | Activity 1, Experience B  |
|  Activity 1  |  | Activity 1  |

When the visitor logs out, the merged profile is maintained.

>[!NOTE]
>
>If you want to distinguish between authenticated (logged-in) users versus non-authenticated users, use the [!DNL Adobe Experience Cloud Identity Service] (ECID) instead of mbox3rdPartyID. After a user is associated with mbox3rdPartyID, it remains associated with the user even after signing out.

>[!NOTE]
>
>[!DNL Adobe Analytics] goals are not tracked in cases where the [!DNL Adobe Experience Cloud] ID (ECID) changes (for example, the visitor changes devices), even though the [!DNL Target] profile might be merged based on the mbox3rdPartyId and still has activity information. For visitors identified with the same ECID (those who access the page with the same device), [!DNL Analytics for Target] (A4T) should work as expected.

## Considerations {#considerations}

* If your page contains several mboxes and only some use `3rdPartyID`, [!DNL Target] does not have a separate visitor profile/context for each visitor request. The `3rdPartyID` context takes priority over the PCID context. It’s enough for one mbox to pass `3rdPartyId` for its context to take priority over PCID.

  For example, suppose that a visitor accesses a page before logging in and sees an experience. The global mbox does not use `3rdPartyID`. After logging in, the visitor sees one of three experiences with child mboxes, some of which use `3rdPartyID`. The visitor visits various pages on the site and then uses the Back button to return to the main page accessed before logging in and sees a different experience. In this scenario, the global mbox did not pass `3rdPartyID`, but one or more of the child mboxes did. `3rdPartyID` took priority over PCID.

* You can send visitors' customer IDs to [!DNL Target] using two approaches:

  1. Use `mbox3rdPartyId`/`thirdPartyId`.
    
     * `mbox3rdPartyId` is the parameter name when you use `targetPageParams` or `targetPageParamsAll`
     * `thirdPartyId` is the parameter name you set in the Delivery API payload directly.
     * You can send only one value in this parameter.

  1. Use the `setCustomerId`/`customerIds` function of ECID Service.

     * `setCustomerId` is a function you can use on client-side (browser) implementations when VisitorAPI.js is available on the page.
     * `customerIds` is the parameter name used when you set it in the Delivery API payload directly and is usually done on server-side or IOT (Internet of Things) implementations.
     * Unlike `mbox3rdPartyId`/`thirdPartyId`, you can send multiple IDs as a list in this approach, but because [!DNL Target] supports only a single customer ID per TnT Id, it uses the first ID in the list with a known alias (alias configured in the Customer Attributes UI).

  >[!IMPORTANT]
  >
  > Using both approaches mentioned above interchangeably for a single visitor can result in incorrect profile merges of the unauthenticated and authenticated [!DNL Target] profiles. 
  >
  >Adobe does not recommend that you use both `mbox3rdPartyId`/`thirdPartyId` and `setCustomerID`/`customerIds` together.
  >
  >If you must use both approaches interchangeably, ensure that the first ID in the list used by `setCustomerID`/`customerIds` is what is used by `thirdPartyId`/`mbox3rdPartyId` and vice-versa. 

