---
keywords: known issues;resolved issues;release notes;bugs;issues;fixes
description: Find information about known issues in Adobe Target, including workaround information. When issues are resolved, they are moved to the Resolved section.
title: Where Can I Find Information About Known Issues and Resolved Issues?
feature: Release Notes
exl-id: 6eb854f7-ed46-4673-afeb-0b44970598cd
---
# Known issues and resolved issues

Information about known issues for [!DNL Adobe Target]. Also includes information about issues that have been resolved.

>[!NOTE]
>
>The issue numbers in parentheses are for internal Adobe use.

## Known Issues {#section_AEDC98B67CF24C9F8E0CF0D2EB9ACAEF}

The following sections list the known issues for [!DNL Target]:

### Traffic distribution of Auto-Allocate activities using A4T {#aa-a4t}

In some cases, the traffic distribution of [!UICONTROL Auto-Allocate] activities using [!UICONTROL Analytics for Target] (A4T) might vary from what should occur based on the reported conversion rate of each experience. This occurs more often for activities with a high proportion of return visitor traffic. Affected customers will be notified about affected activities. (TOP-131)

### Analytics for Adobe Target (A4T) metrics for Auto-Allocate and Auto-Target activities

The [!DNL Target] UI lets users select unsupported engagement and revenue metrics as the primary goal metric for optimization in [!UICONTROL Auto-Allocate] and [!UICONTROL Auto-Target] activities. Conversion metrics are supported; engagement and revenue metrics are *not* supported. If you select engagement or revenue goal metrics, an optimization model is not built.

For a list of supported and unsupported goal metrics, see [A4T support for Auto-Allocate and Auto-Target activities](/help/c-integrating-target-with-mac/a4t/a4t-at-aa.md). (TNT-38409)

### The Enhanced Experience Composer (EEC) does not support PUT requests.

An issue with the EEC currently prevents it from supporting PUT requests and results in a 504 timeout error. (TGT-41493)

### [!DNL Adobe Experience Platform] segment names do not display in the [!UICONTROL Important Attributes] report.

[!DNL Adobe Experience Platform] segment names do not display in the [!UICONTROL Important Attributes] report for [!UICONTROL Automated Personalization] (AP) and [!UICONTROL Auto-Target] (AT) activities. (TOP-3813)

### Archiving [!UICONTROL Auto Target] activities might cause sync issues

Attempting to archive inactive [!UICONTROL Auto-Target] activities might lead to synchronization issues. Until this issue is fixed, do not archive [!UICONTROL Auto-Target] activities. Leave them in the [!UICONTROL Inactive] state. (TGT-40885)

### Page delivery {#page-delivery}

If you add a template rule, such as URL contains (/checkout, /cart) in [page delivery](/help/c-activities/t-experience-target/t-xt-create/xt-activity-url.md), extra spaces are prefixed to your rules. These extra spaces are cosmetic and do not affect audience-definition creation and offer delivery. (TGT-35920)

### QA preview links

Activity QA preview links for saved activities might not load if there are too many saved activities in your account. Retry the preview links. Archive saved activities that are no longer actively used to prevent this issue from continuing to happen. (TNT-37294)

### QA mode for Recommendations activities

A known issue prevents preview if criteria used in the activity is item-based or category-based. (TNT-37455)

### Redirect offers {#redirect}

The following are known issues with redirect offers:

* A limited number of customers have reported higher degrees of variance in traffic distribution when using redirect offers in activities configured with Analytics for Target (A4T).
* Redirect activities in at.js implementations might cause the preview URL to enter into a loop (the offer is delivered repeatedly). You can use [QA Mode](/help/c-activities/c-activity-qa/activity-qa.md) instead to perform Preview and QA. This issue does not impact the actual delivery of the offer. (TGT-23019)

### Cancel loading of a page within the Visual Experience Composer (VEC) {#cancel}

* The following known issue currently exists when cancelling the loading of an [!UICONTROL A/B Test] or [!UICONTROL Experience Targeting] (XT) activity within the VEC that contains a redirect URL.

  In step one of the VEC guided workflow, when you cancel page loading, the [!UICONTROL Modifications] panel in the VEC displays and the redirect to URL template is applied on the experience (for example, "Experience B). When you progress to steps two or three and then come back to step one, the following situation occurs.

  On "Experience B," by default, the cancelled website loading template renders and the [!UICONTROL Modifications] panel is accessible, which should not be the case because this experience has a redirect to URL template applied. The redirect to URL template should display.

  To show the correct state of the experience in the VEC:

  If you switch to another experience, and then switch back to "Experience B," [!DNL Target] displays the redirect to URL template applied on this experience and the [!UICONTROL Modifications] panel is not accessible. (TGT-32138)

* For the Single Page Application (SPA) websites, cancelling loading does not allow you to edit actions under the [!UICONTROL Modifications] panel.

### Recommendations

The following are known issues with [!UICONTROL Recommendations] activities:

* When copying a [!UICONTROL Recommendation] activity with an active promotion, any change in the duplicate activity currently also affects the original activity, and conversely. (TGT-39155)

  As a temporary workaround:

  * Disable activity promotions
  * Duplicate the activity
  * Enable promotions again in each activity

* When [!DNL Target] returns a JSON offer with getOffer(), it returns with type of JSON. However, if you return a JSON Recommendations design it returns with a type of HTML.
* Entities are correctly expired after 60 days of receiving no updates via feed or API; however, the expired entities are not removed from the Catalog Search index after expiration. (IRI-857)
* The "Usage Info" overlays for Criteria and Designs do not reflect their usage in A/B and Experience Targeting activities (TGT-34331)
* Recommendations Offers in A/B and Experience Targeting activities do not show a visual preview of the Recommendations tray (TGT-33426)
* Collections, exclusions, criteria, and designs created via API are not visible in the Target user interface and can be edited only via API. Likewise, if you create any of these items in the Target UI and later edit them via API, those changes are not reflected in the Target UI. Items edited via API should continue to be edited via API to avoid loss of any modifications. (TGT-35777)
* Recommendations activities created via API can be viewed in the user interface, but can only be edited via API.
* The Custom Criteria feed status displayed in the Criteria list (card) view is refreshed every ten minutes and might be more than ten minutes out of date in rare circumstances. The status displayed in the Custom Criteria edit view is fetched in real time and is always up to date. (TGT-35896, TGT-36173)
* Criteria and design cards do not show the correct number of activities in which they are being used. If the criteria or design is used in an A/B activity, the card might incorrectly show that the design or criteria is not used, even when the design or criteria is used in the activity. (TGT-36621, TGT-37217)

### Multivariate Test (MVT) activities

In an MVT activity, the winner shown in the table and graph is not consistent when checking metrics. This situation occurs if a user switches from Summary to Graph View, then switches back to Summary View, changes a metric, and then switches to Graph View. When this issue occurs, the Summary View always shows the correct winner. If the user never switches Graph View between Summary views, the Graph View shows the correct winner.

### at.js {#atjs}

The following are known issues with at.js:

* Using at.js versions before 2.2.0, click tracking does not report conversions in Analytics for Target (A4T) if Adobe Analytics code is not present on page elements (such as buttons). A fix was introduced for this issue in at.js 2.2.0. [Please upgrade to the latest at.js version](/help/c-implementing-target/c-implementing-target-for-client-side-web/target-atjs-versions.md) if you experience this problem.
* If you create an experience with no modifications using at.js 2.1.1 or earlier (for example, a default experience), the experience might not be counted in reports, Analytics for Target (A4T), Adobe Analytics, or Google Analytics. In addition, the ttMeta plug-in might not work correctly.

  As a workaround, use a whitespace in the experience content. (TNT-33366)

  >[!NOTE]
  >
  >A fix for this issue was included in at.js 2.2.0. Upgrade to the [latest version or at.js](/help/c-implementing-target/c-implementing-target-for-client-side-web/target-atjs-versions.md) or use the workaround mentioned above only for at.js versions earlier than 2.2.0.

* When a page is loaded into the Visual Experience Composer (VEC), Target must determine if the global mbox setting is enabled or disabled and whether entityID or categoryID is present at the location where the user is trying to apply the recommendation in the VEC. Based on this information the criteria list is filtered. The default list has filtered algorithms, but the [Compatible checkbox](/help/c-recommendations/t-create-recs-activity/algo-select-recs.md) lets you view the complete algorithms list.

  When using at.js, the Compatibility checkbox is hidden, so you cannot see incompatible algorithms.

  This issue applies only to Recommendations activities that use the VEC.

  **Workaround**: Disable the [!UICONTROL Filter Incompatible Criteria] option in [!UICONTROL Recommendations > Settings]. After disabling this setting, all criteria (compatible and incompatible) will be shown in the criteria picker. (TGT-25949)

* Mboxes not firing on Microsoft Explorer 11 browsers after upgrading to at.js version 1.0 due to the interaction between at.js and Visitor API 2.2.0. This issue affects at.js version 0.9.6 and later. (TNT-27600)
* at.js might not work with Cordova/Hybrid apps because first-party cookies are not currently supported in them. (TNT-26166)

  **Workaround**: Configure at.js with the "x-only" option enabled and pass `mboxThirdPartyId` in calls to manage users.

### Success metrics

Success metrics with the advanced option "How will the count be incremented" set to "every impression" or "every impression (excluding refreshes)" cannot be used as a success metric that another metric depends on.

When a success metric is set to increment on every impression, Target counts the visitor again every time the visitor visits this success metric. Target then resets the success metric "membership" to 0 so it can count again on the next impression. Thus, if another metric requires this metric to have been seen first, Target never recognizes that the user has seen the first metric.

### Analytics for [!DNL Target] (A4T)

When using Target activity impressions and conversions in Analysis Workspace, apply the "Same Touch" Attribution IQ model to the metrics to ensure accurate counting. To apply a [non-default attribution model](https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/build-workspace-project/column-row-settings/column-settings.html), right-click on the metric to **modify Column Settings > enable Use non-default attribution model > select Same Touch model**. Without this model applied, the metrics are overstated. 

All current Analytics packages can add this model with Attribution IQ. If you do not have access to Attribution IQ, please rely on A4T data in Reports & Analytics.

### Target APIs

Customers cannot perform CRUD operations on Auto-Allocate activities through the v3 version of the A/B Activities API on Adobe I/O.

### GEO targeting

On May 10, 2020 Adobe updated the GEO provider files, which introduced some inconsistencies. For example, some values containing commas were added; although, values in existing audiences had no comma. Not all of Adobe delivery servers were affected by this change. As a result, audiences using such values might not have qualified all the correct visitors between May 10 and July 22 2020.

### Reporting - Inconsistent data in the downloadable .csv report versus the displayed report in the [!DNL Target] UI. {#csv}

Reports generated for download as .csv files are inconsistent if the activity uses more than one metric. The downloadable report is generated based on the report settings only and considers the same value for any other metrics used.

The source of truth is always the displayed report in the [!DNL Target] UI.

## Resolved Issues {#section_FD2FC86E7C734D60B1EDC9DEF60E1014}

As known issues above are resolved, they are moved to the following sections.Additional notes, if necessary, are added.

### Image offers showing “Processing” label

Image offers on the Offers page sometimes retain the “processing” label for several hours after the images were uploaded. In most cases this is an issue with the label only: the image offers can still be used in activities and be delivered. (MCUI-10264, TGT-37458)

This issue was fixed in the Target Standard/Premium 20.10.1 release.

### Analytics for Adobe Target (A4T) reporting

The following issues related to A4T have been resolved:

* An issue that impacted A4T activities using an [!DNL Analytics] goal metric that caused A4T reports to show an unexpected traffic split or artificially inflated conversions.

  This issue impacted A4T reporting under the following conditions:

  * The activity was created or saved between September 15 and November 5, 2020 (4 a.m. PST), and
  * The activity had an [!DNL Analytics] metric selected as the goal metric.

  [!DNL Target] correctly split traffic during this time. However, a 50/50 split in the activity setup could appear, for example, as a 90/10 split in A4T reports.

  For impacted activities, the correct traffic split is visible for first-time visitors to the activity after November 5 (4 a.m. PST). New activities created or saved after this time will report the traffic split correctly.

* An issue that impacted A4T activities using a [!DNL Target] goal metric that caused A4T reports to report low or no conversions.

  >[!NOTE]
  >
  >This issue affected A4T reporting only. It did not affect activity delivery.

  This issue impacted A4T reporting under the following conditions:

  * The A4T activity was live between September 22 and November 11, 2020 (2:30 p.m. PST), and
  * The activity had a [!DNL Target] metric selected as the goal metric, and
  * When a visitor hit the goal event for the activity (e.g. [!UICONTROL Clicked an Element]), there was also a lower priority non-A4T activity that matched the conversion event. This could happen if the non-A4T activity was either configured with the same metric as the A4T activity or if it was configured with the "any mbox" metric.

  This issue impacted reporting for A4T activities that were live between September 22 and November 11, 2020 (2:30 p.m. PST). Reporting for impacted A4T activities will show conversions correctly outside this date range. Reporting for non-A4T activities was not impacted.
  
If you have further questions, reach out to your Customer Success Manager (CSM) or [Adobe Customer Care](/help/cmp-resources-and-contact-information.md#reference_ACA3391A00EF467B87930A450050077C). (CSO 20201110016)

### Auto-Target reporting {#at-metrics}

An issue has been resolved that impacted [!DNL Adobe Target Premium] users’ [!UICONTROL Auto-Target] reporting from September 15, 2:30 p.m. (PDT) to October 6, 9:25 a.m. (PDT). When viewing reports for the impacted conversion metrics (configured using either the "[!UICONTROL Viewed a page]” or “[!UICONTROL Clicked on mbox]” option), the conversions rates are incorrectly reported. There is no known delivery issue at this time.

To resynchronize and correct your reporting:

1. Copy and save the impacted [!UICONTROL Auto-Target] activities.
1. Activate the newly saved activities (if impacted activities were live).
1. Delete the original (impacted) activities.

(TGT-38522, CSO 20201006007)

### Reporting {#conversions-audiences}

Conversions currently increment differently based on which audience is used.

For example, for the same visitor, if the conversion count is set to increment "Once per Entrant:"

* Audience: "All Qualified Visitors" for visit-level conversions increment one time only. This is the expected behavior.
* Audience: "New Visitors" for visit-level conversions incorrectly increment every time, instead of incrementing one time only. This is not the expected behavior.

If the conversion count is set to increment "On every impression:"

* Audience: "All Qualified Visitors" for visitor-level conversions incorrectly increment one time only, instead of incrementing every time. This is not the expected behavior.
* Audience: "New Visitors" for visitor-level conversions increment every time. This is the expected behavior.

Note that this problem is related to [!DNL Target] reporting only. This is not an issue when using [!UICONTROL Analytics for Target] (A4T) reporting.

This issue was resolved.

### Pages not loading in the Visual Experience Composer (VEC) or Enhanced Experience Composer (EEC) when using Google Chrome version 80+

This known issue is regarding Google's decision in changing the default behavior of cookies without the SameSite Attribute starting with Chrome version 80. Before the change Chrome defaulted all cookies without the SameSite attribute to “SameSite=None” and now it defaults to “SameSite=Lax” and this changes the way cookies are sent on GET and POST requests. See [SameSite Updates](https://www.chromium.org/updates/same-site).

For more information and a fix, see "How do the recently announced Google Chrome SameSite cookie enforcement policies impact the VEC and EEC?" in [Troubleshooting Issues Related to the Visual Experience Composer and Enhanced Experience Composer](/help/c-experiences/c-visual-experience-composer/r-troubleshoot-composer/issues-related-to-the-visual-experience-composer-vec-and-enhanced-experience-composer-eec.md#samesite).

### Graph report for an Auto-Target activity fails to render when using a custom experience as control

The graph report for an Auto-Target activity fails to render for "differential" modes (Average Lift and Daily Lift) if there is no data (0 visits) in any experience. This situation might occur during the early stage of an activity if the control experience is set to custom. For the other modes (Running Average Control and Targeted, Daily Control and Targeted, and Visits) it works fine. As soon as there is some data (non-zero visits), the report renders as expected.

This issue was fixed in the Target 19.7.1 release.

### Implementation: Global Mbox Auto Create

On the Implementation tab ([!UICONTROL Administration > Implementation]) the [!UICONTROL Global Mbox Auto Create] field will be "false" by default for a newly provisioned tenant.

When mbox.js is downloaded for the first time after provisioning, the [!UICONTROL Global Mbox Auto Create] field is set to "true" in the downloaded mbox.js file and in the [!DNL Target] backend, but it will continue to display as "false" on the [!UICONTROL Implementation] page in the UI until the page is refreshed (after the page is refreshed, the status will be "true.")

at.js will be downloaded with `global_mbox_autocreate = false` for a newly provisioned tenant. If mbox.js is downloaded first, global\_mbox\_autocreate is set to "true" and at.js will also be downloaded with `global_mbox_autocreate = true`. (TGT-15929)

### Enterprise Permissions support in [!DNL Target] APIs {#api}

Code offers created from the Target UI in the Offers library might display in the default workspace if the list of offers is pulled using GET APIs. This issue will be fixed in first week of March 2019. After this fix is in place, code offers will display in the appropriate workspace when pulled from APIs. This issue does *not* affect offers created from APIs. For example, code offers created from APIs display in the workspace in which they were created, whether fetched using GET APIs or from within the Target UI.

### Reporting and extreme orders

From November 25, 2019 until April 26, 2020, one Target server experienced an issue that led extreme order values to be counted in revenue-based report metrics (AOV, RPV). From December 19, 2019 until April 23, 2020, another server experienced the same issue. This issue did not affect all Target servers or all Target customers.

You were *not* affected if:

* Your Target implementation uses different servers.
* Your reports did not exclude extreme orders.
* You used a conversion metric to measure your activities.
* Your Target activities use Analytics for Target (A4T).
* You are located the Asia-Pacific (APAC) region.

To determine if this issue impacted your Target reporting, reach out to [Client Care](/help/cmp-resources-and-contact-information.md#concept_34A1CA16F2244D42930BB77846A5ABBB).

### Recommendations

* Recommendations feed index can show "Waiting for index" if the items in the feed are the same as in the previous run. The product ingestion for delivery is not impacted. (RECS-6663)

  This issue was fixed in the Target 19.4.2 release.

* Recommendations feeds take longer to process than expected. (COR-2836)

  Fixed in the Target 16.10.1 release.

* The Recommendation Feeds UI does not show the correct status of indexing. The backend jobs are functioning correctly, but the UI is not able to fetch and display the current state.

  This was fixed in the 17.10.1 release.

### Redirect offers

A race condition on your page might cause page views on the original page and on the redirect page to be counted. Updates are planned to the at.js implementation to ensure that this race condition can be avoided.

This issue was fixed in at.js 1.6.3.

### Exclusion groups

* When auto-dedupe is applied after creating exclusion groups, the count on the activity diagram might be incorrect in the UI.
* When existing activity with Exclusion Group is edited, the manual inclusions might not be correctly reflected in the UI.

These issues were resolved.

### Target APIs

v1 version of the Offer APIs on Adobe I/O treats all offers created through Target to be in the default workspace. (TTTEAM-41957)

This issue was resolved.

### at.js {#at-js-2}

Mboxes not firing on Microsoft Explorer 11 browsers after upgrading to at.js version 1.0 due to the interaction between at.js and Visitor API 2.2.0. This issue affects at.js version 0.9.6 and later. (TNT-27600)

Fixed with the release of API 2.3.0 or later.

### Geo targeting

Searching for a string that contains special characters (such as a space or a comma) is currently not working when creating geo-targeting audiences. This issue surfaces, for example, when creating audiences based on cities, states, countries, etc. For example, when searching for "new york", the search does not return valid results.

Fixed in November, 2018.

### at.js {#at-js-3}

When using at.js version 1.6.0, Analytics for Target (A4T) redirects occur, but without activity qualification.

Fixed with the release of at.js 1.6.2.

### Activities, Workspaces, and Delete activity API

Activities in the default workspace deleted via API continue to display in the Target UI. As a workaround, delete all activities in the default workspace using the Target UI. (TGT-31315)

Fixed October 25, 2018

### Automated Personalization (AP) offer-level reporting

When you click the targeted experience in an Automated Personalization (AP) activity's report to view offer-level reporting, currently you see empty results, an error message, or a spinning icon. (TNT-30695)

Fixed September 27, 2018.

### Code Editor

If you reload the VEC on step 1 of the three-step guided workflow while working with the Code Editor in Firefox and Internet Explorer, the Modifications tab does not render properly; however, the VEC's functionality is not impacted. (TGT-28730)

This was fixed in the 18.9.1 release.

### Recommendations activity that uses an Attribute Promotion rule

When you edit or copy a Recommendations activity that uses an Attribute Promotion rule, the "Has missing field" error displays when clicking Save .

This was fixed in the 17.8.1 release.

### Backup Recommendations

Backup recommendations erroneously display "Enabled" on Recently Viewed Items cards in the Target UI. (TGT-29308)

This was fixed in the 18.4.1 release so that "Disabled" displays.

### Auto-Target activities and reporting audiences

When a reporting audience's name used in an Auto-Target activity is changed, further updates from Target for that activity might fail with an error message.

This issue was fixed with the Target 18.5.1 (May 22, 2018) release.

### at.js {#at-js-4}

The algorithm for extracting the top-level domain that should be used when saving cookies has changed in at.js version 0.9.6. Because of this change, cookies cannot be saved to addresses that use IP. Most of the time, IP addresses are used for testing purposes, but as workarounds you can use DNS entries, adjust the hosts file on a local box, or use the targetGlobalSettings() at.js function to insert a code snippet to support IP addresses.

This issue was remedied in at.js version 1.2.

### Enterprise User Permissions for [!DNL Target] Premium

As part of the Enterprise Permissions migration, all Target Premium user management was moved from the Adobe Target UI to Adobe Admin Console.

As a result of the migration, there are two potential issues you should be aware of:

* Non-admin users received an email indicating that they now have access to Adobe Target. This indicates that the migration was completed for your organization. The email itself can be disregarded.
* Following the migration, there have been some reports of previously disabled users reappearing in the Adobe Admin Console. This could be an issue for your organization if disabled users in the Adobe Admin Console were still appearing on your user list in Target prior to the migration. We recommend that administrators review the list of users in Admin Console to validate access.

This issue was fixed on August 30, 2017

### Activity Creation

An issue with the 17.6.2 release may have affected activities created and/or updated between June 22, 2017 and June 29, 2017. Activities with the following were affected:

* Any experiences that were rearranged in Experience Targeting (XT) would have reverted back to the original order
* Any segment rules local to the activity (not saved within an audience) would have been lost: combined audiences, location refinements, and any rules on success metrics.

No other activities were affected.

**Important**: This issue is not fixed automatically. You must re-save any activity that was affected to fix the issue.

This issue was fixed on June 29, 2017

### Form-Based Experience Composer

The following known issues have been reported when using the Form-Based Experience Composer:

* If you use the Form-Based Experience Composer with an mbox other than the auto-created global mbox ( target-global-mbox ), and then choose an engagement metric as a success metric, the metric increments only on pages that have the mbox used in the activity. As an example, if your mbox is homepage\_mbox , the Pages Per Visit metric is the number of hits to the homepage\_mbox during that visit. (TGT-22789)
* A JavaScript exception is thrown when you delete an experience in an Experience Targeting (XT) activity when using the Form-Based Experience Composer during step 1 of the process. (TGT-24366)

The first issue was fixed in the Target 17.3.1 release (March 2017).

The second issue was fixed in the Target 17.6.1 release (June 2017).

### at.js {#at-js-5}

Since the release of Target 17.4.1 (April 27, 2017), using the Insert Image action in the Visual Experience Composer (VEC) causes the offer content to not be delivered when using the at.js library.

A fix for this issue has been made to at.js version 0.9.7 released May 22, 2017.

### Reporting: A/B and Experience Targeting (XT) activities

Between April 27 at 9:00 p.m. PST and May 5 at 6:00 a.m. PST, A/B and XT activities created or edited with any metrics using the “Viewed a Page” conversion action (that were not based on other metrics), might have incorrectly recorded conversions. This issue is now resolved; however, reporting on the “Viewed a Page” conversion action for these activities during the impacted time period might not be accurate and, unfortunately, cannot be corrected. We recommend that for any decisions based on “Viewed a Page” conversion actions for these activities you rely only on data recorded before or after the impacted period.

Reporting data for other metrics can still be used because they were not impacted.

Fixed in the Target 17.4.3 hotfix.

### Offers: A/B and Experience Targeting (XT) activities

The delivery and preview was impacted for offers in A/B and XT activities having at least two experiences and that were either created or edited using the Form-Based Experience Composer between Friday April 28 (9 p.m. PT) and Monday May 1 (9:15 p.m. PT). Only offers with default content were displayed.

Fixed in the Target 17.4.3 hotfix.

### at.js {#at-js-6}

The following actions caused the offer to not be delivered when using the Visual Experience Composer (VEC) and at.js: Move and Rearrange.

A fix for this issue was made to at.js version 0.9.6.

### Reports

The ability to view multiple metrics in a report, included in the Target 17.3.1 release (March 30, 2017) has been removed due to unexpected behavior. This feature will be available again in an upcoming release.

The ability to view multiple metrics in a report was included in the Target 17.4.1 release (April 27, 2017).

### Offers

Images deleted from the Image Offers library ( Offers \> Image Offers ) remain visible in the UI. In an upcoming release, these deleted images will no longer display. In the meantime, deleted images display in the UI, but have a status of Deleted . (TGT-23793)

Fixed in the Target 17.4.1 release (April 27, 2017).

### Redirect offers

For Recently Viewed criteria, entity based dynamic rules will lead to no recommendation if the entity.id parameter is not passed in the mbox request. (RECS-6241)

This issue was fixed after the Recommendations release (March 22, 2018). After the Recommendations release, Target skips the entity-based dynamic rules if entity.id is not passed in the mbox request.

### at.js {#at-js-7}

When users attempt to download at.js from the Implementations details page after updating at.js settings, mbox.js is downloaded instead of at.js . (TGT-23069)

Fixed in the Target 17.3.1 release (March 30, 2017).

### Global exclusion rules

Global exclusion rules are taking 10-20 minutes to propagate to the edge for Premium Recommendations. (RECS-5270)

Fixed in the Recommendations 17.2.2.0 release (March 6, 2017).

### Analytics for Adobe Target (A4T) reporting

Reports are not updated when the reporting metric is switched. This issue affects the UI only. There is no impact on reporting data collection or delivery. (TGT-22970)

Fixed in the Target 17.2.2.0 release (February 24, 2017).

### CSV reports

Downloaded reports do not honor the Exclude Extreme Orders setting. (TGT-21871)

Fixed in the Target 17.2.1.0 release.

### Pages not loading in VEC or EEC when using Chrome version 80+

* This known issue is regarding Chrome’s decision in changing the default behaviour of cookies without the SameSite Attribute starting with Chrome version 80.
Before the change Chrome defaulted all cookies without the SameSite attribute to “SameSite=None” and now it defaults to “SameSite=Lax” and this changes the way cookies are sent on GET and POST requests.(for more information please see https://www.chromium.org/updates/same-site)

* A fix has been found and deployed through Target-VEC-Helper chrome extension v0.5.3 but you can also disable the "SameSite by default cookies" flag from chrome://flags.

