---
keywords: a/b;a/a;aa;
description: Learn what an A/A test is, why you might want to perform an A/A test, how long you should run the test, and how to interpret the results.
title: What is A/A Testing?
feature: A/B Tests
exl-id: 7489f4f5-3655-45f9-a743-651ba1c23c53
---
# A/A testing

Before performing an A/A test on your site using [!DNL Adobe Target], it is important to understand what an A/A test is, why you might want to perform an A/A test, how long you should run the test, and how to interpret the results.

## What is A/A testing?

Before explaining A/A testing, it is good to review A/B testing so we can then discuss the differences.

In a standard A/B test, traffic is allocated to two or more different experiences. One experience is typically the “control” and variations of the experience are tested against the control to see which experience creates the most lift in a given metric.

A/A testing, however, involves allocating traffic to two identical experiences, normally with a 50/50 traffic allocation split. With a standard A/B test, you typically want to discover a lift in conversion. This differs from an A/A test in which your goal is usually to determine that there is *no* difference in lift between the identical experiences.

## Why would you want to test two identical experiences and what does this accomplish?

Some organizations perform A/A testing when implementing a new testing tool, such as [!DNL Target], to determine whether:

* The activity was set up correctly
* The code was implemented correctly
* The reporting is accurate

Although few organizations run A/A tests, it is actually good practice to run them as “sanity” experiments to build trust after implementing the tool or before performing A/B tests that could impact conversion and revenue.

## Why might you see lift for one experience when the experiences are identical?

There are numerous reasons why you might see lift in one experience over the another (identical) experience:

### The A/A test was not allowed to run long enough

A common problem in running any kind of test, including an A/A test, is to prematurely stop a test and declare a winning experience. Analysts often do what is called “data peeking.” Data peeking involves looking at the test data early and frequently while trying to determine which experience is performing better. The risk is to stop the test prematurely, which could invalidate the results.

In an A/A test, data peeking can often cause analysts to see lift in one experience, when they assume that there should be no difference, because the two experiences are identical. Given time and sufficient visits the difference in lift should shrink.

As with a regular A/B test, you should therefore decide ahead of time what sample size to use, based on the minimum effect size, power, and significance levels you find acceptable. In an A/A test, the goal would then be to *not* see a statistically significant result after your test has reached the desired sample size.

The [!UICONTROL Adobe Target Sample Size Calculator] is an important tool to help you determine what sample size you should aim for and how long you should run the test.

* [Adobe Target Size Calculator](/help/c-activities/t-test-ab/sample-size-determination.md#section_6B8725BD704C4AFE939EF2A6B6E834E6)

In addition, see the following articles for information about how long you should run an activity, as well as other helpful tips and tricks:

* [How long should you run an A/B test?](/help/c-activities/t-test-ab/sample-size-determination.md)
* [Ten common A/B pitfalls and how to avoid them](/help/c-activities/t-test-ab/common-ab-testing-pitfalls.md)

### Statistical significance impacts your test results

The significance level of a test determines how likely it is that the test reports a significant difference in conversion rates between two different offers when, in fact, there is no real difference. This is known as a false positive, or a Type I error. The significance level is a threshold specified by the user and there is a trade-off between the tolerance for false positives and the number of visitors that must be included in the test in choosing the proper significance level.

A commonly used significance level in A/A and A/B testing is 5%, which corresponds to a confidence level of 95% (confidence level = 100% - significance level). A confidence level of 95% means that every time you perform a test, there is a 5% chance of detecting a statistically significant lift even if there is no difference between the experiences.
 
Suppose you want to achieve a 95% confidence level with your A/A test. With a 95% confidence level, 1 in 20 A/A tests could show statistically significant lift in conversions. With a 90% confidence level, 1 in 10 tests could show lift in conversions when testing identical experiences.

## Best Practice

If you decide that an A/A test is necessary in your organization, be aware that the identical experiences might temporarily show a difference from the control. This can be normal, depending on the time the test is allowed to run. The difference should shrink given more time and visitors.

Best practice is to use regular A/B testing methodology: decide the sample size ahead of time based on a minimum effect size, desired power and significance by using the [Adobe Target Size Calculator](/help/c-activities/t-test-ab/sample-size-determination.md#section_6B8725BD704C4AFE939EF2A6B6E834E6).

Then, allow adequate time and visitors before you reach any conclusions, and remember that depending on the significance level of your test, there is a chance that one experience will show a difference in lift, and even be declared the winner.
