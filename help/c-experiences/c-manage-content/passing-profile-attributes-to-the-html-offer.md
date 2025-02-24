---
keywords: dynamic data;assets;data;offers;personalized offers;personal offers;token replace
description: Learn how to pass dynamic data into [!DNL Adobe Target] Offers.
title: How Do I Pass Dynamic Data into Offers?
feature: Experiences and Offers
exl-id: b8f9c6eb-1000-41a2-aa3f-bc42c1ef5669
---
# Pass dynamic data into offers

You can dynamically display visitor information that is stored in the [!DNL Adobe Target] profile. Similarly, activity information (such as the name of the activity or the name of the experience) can also be used to create a single offer that dynamically returns personalized content based on the visitor's interests, past behavior, and overall profile.

## Business cases

* Promote a discounted offer to "refill" or "replenish" the last product purchased. Instead of creating a separate offer for every item in your catalog, you can create an offer with dynamic text that reads the "last product purchased" from the profile and displays a link in the offer.
* A visitor arrives on your landing page with `keyword=world` `cup`. You display the term *World cup* in the offer.
* Personalize a recommendations label with info such as (1) the last item added to a visitor's cart (Nike Air Max 1000s), (2) the visitor's color preference (black) and (3) the visitor's favorite non-shoe category (hoodies). Example: "Accessorize your 'Nike Air Max 1000s' with these cool 'black' 'hoodies'!"

## Technical advantages

Because visitor-specific preferences, behaviors, status, can be stored in the visitor's profile, you can repeat this message on their next visits. Dynamic offers enable greater scale by allowing you to set up a single offer within an activity that displays personalized messages for all your visitors. As the visitor's intent changes, your website content automatically reflects those changes.

## Example

* `mboxCreate("landingpage"`, `"profile.keyword=World Cup");` 

* HTML Offer code: `Get your ${profile.keyword} information here!` 
* Visitor sees: Get your World Cup information here!

The following values can be "token replaced":

|Value|Examples|
|--- |--- |
|In-mbox profile parameters|`${profile.age}`|
|Script profile parameters|`${user.lifetimeSpend}`|
|Mbox parameters|`${mbox.favoriteColor}`|
|Campaign information|`${campaign.name}`, `${campaign.recipe.name}`, `${campaign.id}`, `${campaign.recipe.id}`, and `${campaign.recipe.trafficType}`|
|Unique visitor id|`${user.pcId}`|
|Unique session id|`${user.sessionId}`|
|Visitor's first session (true or false)|`${user.isFirstSession}`|
|Past behavior|`${user.endpoint.lastPurchasedEntity}`, `${user.endpoint.lastViewedEntity}`, `${user.endpoint.mostViewedEntity}`, `${user.endpoint.categoryAffinity}`| 

Log information in the console for debugging purposes, such as `${campaign.name}`, `${campaign.id}`, `${campaign.recipe.name}`, `${campaign.recipe.id}`, `${offer.name}`, `${offer.id}`, `${campaign.name}`

For [!DNL Recommendations] designs, see additional examples in [Design Overview](/help/c-recommendations/c-design-overview/design-overview.md).

## Implementation

For profile parameters passed into an mbox, use the syntax:

`${profile.parameter}` 

For profile parameters created in a profile script, use the syntax:

`${user.parameter}`

When using dynamic attributes in a [!DNL Recommendations] design, you must insert a backslash ( &#92; ) before the dollar sign ( $ ) for the dynamic value to render properly: 

`\${user.endpoint.lastViewedEntity}`

These variables are replaced with the value on the server side, so no quotes or other JavaScript is required for the proper display. 

Default values can also be specified for values you want to expose to offers. The syntax is like this:

`${user.testAttribute default="All Items!"}`

When `testAttribute` doesn’t exist or is blank, "All Items!" is written out. If an empty attribute value is valid, and you want to write it out instead of showing the default, you can use:

`${user.testAttribute default="All Items!" show_blank="true"}`

You can also escape and unescape values to be displayed. If your value has an apostrophe, for example, you can escape the value so it does not break the JavaScript on the page. (Offers are written in JavaScript, so a single apostrophe can be confused for a quote.) For example:

`${user.encodedValue encode="unescape"}`

`${user.unencodedValue encode="escape"}`

For offer parameters (offer.name, offer.id) used in an offer's content:

If that offer is one of several offers set on an experience, the value of the last added offer populates the parameter's value. Meaning, these parameters are evaluated on the experience level.