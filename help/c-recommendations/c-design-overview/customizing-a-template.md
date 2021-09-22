---
keywords: custom design;velocity;decimal;comma;customize design
description: Learn how to use the open-source Velocity design language to customize recommendation designs in Adobe [!DNL Target] Recommendations.
title: How Do I Customize a Design Using Velocity?
feature: Recommendations
exl-id: 035d7988-80d8-4080-bb0d-1d0e9f8856d1
---
# ![PREMIUM](/help/assets/premium.png) Customize a design using Velocity

Use the open-source Velocity design language to customize recommendation designs in [!DNL Adobe Target Recommendations].

## Velocity overview {#section_C431ACA940BC4210954C7AEFF6D03EA5}

Information about Velocity can be found at [https://velocity.apache.org](https://velocity.apache.org).

All Velocity logic, syntax, and so on can be used for a recommendation design. This means that you can create *for* loops, *if* statements, and other code using Velocity rather than JavaScript.

Any variable sent to [!DNL Recommendations] in the `productPage` mbox or the CSV upload can be displayed in a design. These values are referenced with the following syntax:

```
$entityN.variable
```

Variable names must follow Velocity shorthand notation, which consists of a leading *$* character, followed by a Velocity Template Language (VTL) Identifier. The VTL Identifier must start with an alphabetic character (a-z or A-Z).

Velocity variable names are restricted to the following types of characters:

* Alphabetic (a-z, A-Z) 
* Numeric (0-9) 
* Hyphen ( - ) 
* Underscore ( _ )

The following variables are available as Velocity arrays. As such, they can be iterated over or referenced via index.

* `entities` 
* `entityN.categoriesList`

For example:

```
#foreach ($category in $entity1.categoriesList) 
<br/>$category 
#end
```

Or

```
#if ($entities[0].categoriesList.size() >= 3 ) 
$entities[0].categoriesList[2] 
#end
```

For more information about Velocity variables, see [https://velocity.apache.org/engine/releases/velocity-1.7/user-guide.html#variables](https://velocity.apache.org/engine/releases/velocity-1.7/user-guide.html#variables).

If you use a profile script in your design, the $ preceding the script name must be escaped with a \. For example, `\${user.script_name}`.

>[!NOTE]
>
>The maximum number of entities that can be referenced in a design, either hard-coded or via loops, is 99. The template script length can contain up to 65,000 characters.

For example, if you want a design that displays something similar to this:

![](assets/velocity_example.png)

you can use the following code:

```
<table style="border:1px solid #CCCCCC;"> 
<tr> 
<td colspan="3" style="font-size: 130%; border-bottom:1px solid  
#CCCCCC;"> You May Also Like... </td> 
</tr> 
<tr> 
<td style="border-right:1px solid #CCCCCC;"> 
<div class="search_content_inner" style="border-bottom:0px;"> 
<div class="search_title"><a href="$entity1.pageUrl"  
style="color: rgb(112, 161, 0); font-weight: bold;"> 
$entity1.id</a></div> 
By $entity1.message <a href="?x14=brand;q14=$entity1.message"> 
(More)</a><br/> 
sku: $entity1.prodId<br/> Price: $$entity1.value 
<br/><br/> 
</div> 
</td> 
<td style="border-right:1px solid #CCCCCC; padding-left:10px;"> 
<div class="search_content_inner" style="border-bottom:0px;">  
<div class="search_title"><a href="$entity2.pageUrl"  
style="color: rgb(112, 161, 0); font-weight: bold;"> 
$entity2.id</a></div> 
By $entity2.message <a href="?x14=brand;q14=$entity2.message"> 
(More)</a><br/> 
sku: $entity2.prodId<br/> 
Price: $$entity2.value 
<br/><br/> 
</div> 
</td> 
<td style="padding-left:10px;"> 
<div class="search_content_inner" style="border-bottom:0px;"> 
<div class="search_title"><a href="$entity3.pageUrl"  
style="color: rgb(112, 161, 0); font-weight: bold;"> 
$entity3.id</a></div> 
By $entity3.message <a href="?x14=brand;q14=$entity3.message"> 
(More)</a><br/> 
sku: $entity3.prodId<br/> Price: $$entity3.value 
<br/><br/> 
</div> 
</td> 
</tr>  
</table>
```

>[!NOTE]
>
>If you want to add text after the value of a variable before a tag that indicates the variable name has finished, you can do so using formal notation to enclose the name of the variable. For example: `${entity1.thumbnailUrl}.gif`.

You can also use `algorithm.name` and `algorithm.dayCount` as variables in designs, so one design can be used to test multiple criteria, and the criteria name can be dynamically displayed in the design. This shows the visitor that he or she is looking at "top sellers" or "people who viewed this bought that." You can even use these variables to display the `dayCount` (number of days of data used in the criteria, like "top sellers over the last 2 days," etc.

## Working with numbers in Velocity templates

By default, Velocity templates treat all entity attributes as string values. You might want to treat an entity attribute as a numeric value in order to perform a math operation or compare it to another numerical value. To treat an entity attribute as a numeric value, follow these steps:

1. Declare a dummy variable and initialize it to an arbitrary integer or double value.
1. Ensure that the entity attribute you want to use is not blank (required for Target Recommendations' template parser to validate and save the template).
1. Pass the entity attribute into the `parseInt` or `parseDouble` method on the dummy variable you created in step 1 to turn the string into an integer or double value.
1. Perform the math operation or comparison on the new numeric value.

### Example: Calculating a discount price

Suppose you want to reduce the displayed price of an item by $0.99 to apply a discount. You could use the following approach to achieve this result:

```
#set( $double = 0.1 )

#if( $entity1.get('priceBeforeDiscount') != '' )
    #set( $discountedPrice = $double.parseDouble($entity1.get('priceBeforeDiscount')) - 0.99 )
    Item price: $$discountedPrice
#else
    Item price unavailable
#end
```

### Example: Choosing the number of stars to display based on an item's rating

Suppose you want to display an appropriate number of stars based on an item's numerical average customer rating. You could use the following approach to achieve this result:

```
#set( $double = 0.1 )

#if( $entity1.get('rating') != '' )
    #set( $rating = $double.parseDouble($entity1.get('rating')) )
    #if( $rating >= 4.5 )
        <img src="5_stars.jpg">
    #elseif( $rating >= 3.5 )
        <img src="4_stars.jpg">
    #elseif( $rating >= 2.5 )
        <img src="3_stars.jpg">
    #elseif( $rating >= 1.5 )
        <img src="2_stars.jpg">
    #else
        <img src="1_star.jpg">
    #end
#else
    <img src="no_rating_default.jpg">
#end
```

### Example: Calculating the time in hours and minutes based on an item's length in minutes

Suppose you store the length of a movie in minutes, but want to display the length in hours and minutes. You could use the following approach to achieve this result:

```
#if( $entity1.get('length_minutes') )
#set( $Integer = 1 )
#set( $nbr = $Integer.parseInt($entity1.get('length_minutes')) )
#set( $hrs = $nbr / 60)
#set( $mins = $nbr % 60)
#end
```

## Displaying a key item with recommended products {#section_7F8D8C0CCCB0403FB9904B32D9E5EDDE}

You can modify your design to show your key item alongside other recommended products. For example, you might want to show the current item for reference next to the recommendations.

To do this, create a column in your design that uses the `$key` attribute you are basing your recommendation on rather than the `$entity` attribute. For example, the code for your key column might look like this:

```
<div class="at-table-column"> 
   <a href="$key.pageURL"> 
      <img src=$key.thumbnailUrl" class="at-thumbnail"/> 
      <br/><h3>$key.name</h3> 
      <br/><p class="at-light">$key.message</p> 
      <br/><p class="at-light">$key.value</p> 
   </a> 
</div>
```

The result is a design like the following, where one column shows the key item.

![](assets/rec_key.png)

When you are creating your [!DNL Recommendations] activity, if the key item is taken from the visitor's profile, such as "last purchased item," [!DNL Target] displays a random product in the [!UICONTROL Visual Experience Composer] (VEC). This is because a profile is not available while you design the activity. When visitors view the page, they will see the expected key item.

## Performing replacements in a string value {#section_01F8C993C79F42978ED00E39956FA8CA}

You can modify your design to replace values within a string. For example, replacing the decimal point delimiter used in the United States with the comma delimiter used in Europe and other countries.

The following code shows a single line in a conditional sale pricing example:

```
<span class="price">$entity1.value.replace(".", ",") €</span><br>
```

The following code is a complete conditional example of a sale price:

```
<div class="price"> 
    #if($entity1.hasSalesprice==true) 
    <span class="old">Statt <s>$entity1.salesprice.replace(".", ",") €</s></span><br> 
    <span style="font-size: 10px; float: left;">jetzt nur</span> $entity1.value.replace(".", ",") €<br> #else 
    <span class="price">$entity1.value.replace(".", ",") €</span><br> #end 
    <span style="font-weight:normal; font-size:10px;"> 
                                        $entity1.vatclassDisplay 
                                        <br/> 
                                        $entity1.delivery 
                                        <br> 
                                    </span>
```

## Customizing the template size and checking for blank values {#default}

Using a Velocity script to control for dynamic sizing of the entity display, the following template accommodates a 1-to-many result to avoid creating empty HTML elements when there aren't enough matching entities returned from [!DNL Recommendations]. This script is best for scenarios when back-up recommendations wouldn't make sense and [!UICONTROL Partial Template Rendering] is enabled.

The following HTML snippet replaces the existing HTML portion in the 4x2 default design (the CSS is not included here, for the sake of brevity):

* If a fifth entity exists, the script inserts a closing div and opens a new row with `<div class="at-table-row">`.
* With 4x2, the maximum results shown will be eight, but this could be customized for smaller or larger lists by modifying `$count <=8`.
* Be aware that the logic won't balance the entities on multiple rows. For example, if there are five or six entities to display, it won't dynamically become three on top and two on the bottom (or three on top and three on the bottom). The top row will display four items before starting a second row.

```
<div class="at-table">
  <div class="at-table-row">
    #set($count=1) 
    #foreach($e in $entities)  
        #if($e.id != "" && $count < $entities.size() && $count <=8) 
            #if($count==5) 
                </div>
                <div class="at-table-row">
            #end
            <div class="at-table-column">
                <a href="$e.pageUrl"><img src="$e.thumbnailUrl" class="at-thumbnail" />
                    <br/>
                    <h3>$e.name</h3>
                    <br/>
                    <p class="at-light">$e.message</p>
                    <br/>
                    <p class="at-light">$$e.value</p>
                </a>
            </div>
            #set($count = $count + 1) 
        #end 
    #end
  </div>
</div>
```
