---
keywords: faq;frequently asked questions;analytics for target;a4T;lift;ad hoc;report builder;confidence
description: Find answers to questions about lift and confidence when using Analytics for [!DNL Target] (A4T). A4T lets you use Analytics reporting for [!DNL Target] activities.
title: Where Can I Find Information about Lift And Confidence with A4T?
feature: Analytics for Target (A4T)
exl-id: 42fd179b-944a-4a0a-b299-85ea4a7ea244
---
# Lift and confidence - A4T FAQ

This topic contains answers to questions that are frequently asked about lift and confidence when using [!DNL Adobe Analytics] as the reporting source for [!DNL Adobe Target] (A4T).

## Can I perform offline calculations for A4T? {#section_55B5B750E17D414CAECBEECE27B15D81}

You can perform offline calculations for A4T, but it requires a step with data exports in [!DNL Analytics]. For more information, see "Performing Offline Calculations for Analytics for Target (A4T)" in [Confidence Level and Confidence Interval](/help/c-reports/conversion-rate.md#concept_0D0002A1EBDF420E9C50E2A46F36629B).

## How is lift calculated? {#section_8CAE788EED5646C4B1D64A0D22070734}

Lift is the percent difference between your control page results and a successful test variant.

## How is confidence calculated? {#section_97DB24D833E742988318CA65DA65DAD9}

The confidence level is the probability that the measured conversion rate differs from the champion page conversion rate for reasons other than chance alone.

## Why can't I see lift and confidence on calculated metrics? {#lift-confidence}

Calculated metrics are not currently supported in lift and confidence functions. Analytics calculates metrics at an aggregate-level, rather than at a visitor-level. Confidence, in particular, is a visitor-level calculation. 

Non-calculated (standard) events are supported in lift and confidence. They become the numerator in the lift function; the numerator cannot be a calculation itself. The denominator is the normalizing metrics (impressions, visits, or visitors). Some examples of standard events include orders, revenue, activity conversions, custom events 1-1000, and so on. Common optimization metrics, such as conversation rate (Orders/Visitor) and RPV (Revenue/Visitor) are supported in lift and confidence.

Examples of unsupported metrics or use cases include:

* Average Order Value (Revenue/Order, per Visitor). AOV is not supported because the numerator is a calculated metric. Instead, the recommendation is to consider the two influencing metrics of AOV - Revenue Per Visitors and Conversion Rate.
* Calculated metrics that are the sum of standard events. For example, you can track ten different lead forms into ten separate events, and then add them together to get total lead submissions. A recommended method to track these events is to implement a single lead submission event in Analytics and then use an eVar to collect the type of lead form. Using this method requires fewer variables and ensures that you can use the single lead submission metric in lift and confidence functions.

## How does A4T handle confidence calculations? {#section_66115EAF1BA34F7A8FCED7B08DA4F99C}

A4T uses non-binary metric calculations with the sum of square data. The variance is calculated using the sum of squares data. Extreme orders are not considered. Also, the confidence calculation does not apply a Bonferroni correction for multiple offers.

## Do lift and confidence work in Ad Hoc and Report Builder? If it's not native, can I do it in there myself? {#section_D8BB69AE700B4C5CB5FD28DB51F9A4E9}

Lift and confidence do not work in Ad Hoc or Report Builder, and cannot be calculated yourself for continuous variables. It is possible to calculate it manually for binary metrics.
