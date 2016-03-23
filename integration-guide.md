#Integration Guide

####Requirements
This document presumes that the reader is familiar with html, javascript, and jQuery.

####Terminology
- **FINDMINE**: the Findmine server and API platform, which is responsible for processing and generating the recommendation data as well as identifying your products.
- **findmine.js**: a javascript file that contains the client-side code for automating the submission of requests to the server side as well as rendering the returning recommendations.
- **findmine**: a javascript global object, created upon the execution of findmine.js, which provides front-end functionality for accessing data returned from FINDMINE. 
- **item**: a unit representing a single identified product page. The product based on which the recommendation is being generated may be referred to as **sample item**, in contrast to the items which comprise a single recommended set.
- **set**: a collection of items that complement the currently displayed sample item. Each set may or may not contain the sample item amongst the items associated to the set.

###1. Embed findmine.js Module into your Website
**findmine.js** creates a global javascript object called **findmine**, which you can use to request recommendations. In order to embed the findmine.js module simply include the following lines in the header section of the html code pertaining to the product pages.
```html
<script src="http://www.findmine.us/findmine-latest.js?shop={{shop.key}}"> </script>
```
In place of **{{shop.key}}** you must provide the key identity for your store. This key may be obtained from our representatives. This key allows our system to generate a unique findmine.js file for your store in case we were tasked with the responsibility of designing your store's styling and look. If you provide a key that our system does not recognizes or omit the key entirely (as shown below) then our system will return a default version of the findmine.js module.
```html
<script src="http://www.findmine.us/findmine-latest.js"> </script>
```

Once the module is loaded **findmine** object will be created globally and may be interacted with via the console.
![Findmine Global](https://github.com/Mishki/docs/blob/master/assets/findmine-global.gif)

###2. The findmine Object Description
The findmine object exposes three important methods:

```javascript
findmine.identify(identity)
```
This method connects to FINDMINE in order to identify the item on the page. The function returns returns a jQuery Deferred object containing the data returned from the server upon success or the error status codes upon failure. This function accepts an object as it's parameter for the purpose of overriding some of the data that FINDMINE would otherwise attempt to determine on its own using machine learning mechanisms. This method may be ignored, unless used for testing or development purposes.

```javascript
findmine.match(identity, inquiry)
```
The match method communicates with FINDMINE to find recommendation for the sample item and stores the resulting recommendations in the **matched** section of the findmine object. Match internally invokes the identify function described above and therefore can be used exclusively without invoking identify before hand. This module returns a jQuery Deferred object containing the recommended sets data upon success or the error status codes upon failure. This function accepts two objects as it's arguments. The idenitity is passed internatlly to the identity function. Just as described above, the purpose of this parameter is for overriding some of the data that FINDMINE otherwise has to determine using machine learning. This allows for better accuracy and maintenance. The inquiry object may contain to keys internally. These are **union** and **mixed**. These keys are very specific to the recommendations your store would have and therefore should be consulted before providing. Alternatively inquiry can just be undefined or null.

```javascript
findmine.render(selector, config)
```
The render function renders the necessary html to the specified tag by the **selector** parameter. This is simply a css selector string pointing to the empty div object where this html should be generated. This function is optional and may be avoided alltogether in case you decide to implement your own front end. Alternatively this function may be used in conjunstion with your own styling file for a customized styling. The config parameter helps fill in some customization information when the html is being generated. Below is an example of the information you may be able to switch. 
```javascript
{
    header: "Complete the Look",
    next: "Next Outfit",
    previous: "Previous Outfit"
}
```

###3. Call match(), and Configure the Callback Methods
When match() completes it returns a Deferred object, and you really would be able to attach asyn-chronous handlers to be called upon its completion. This section also applies to identify(). For example, the following code calls match() and attaches the .done() and .fail() handlers to the Deferred object. Note that the handlers are chained in jQuery fashion. Please see jQuery’s documentation for more details.

```javascript
$(window).load(function() {
    if (typeof findmine !== "undefined") {
        findmine.match(null, true).done(function() {
            // Place your custom code here.
            // The results data is in findmine.matched

            // Or use the helper function.
            findmine.render('#findmine-container');
        }).fail(function() {
            // Handle exceptions here
            alert("The system is down.")
        });
    }
});
```

###3. Create your Own html or Style with Ours
The match() method stores our recommendations within the findmine object, in findmine.matched. Therefore, you can access this data and update your page however you’d like. The render() method will produce a bare-bones html elements containing the recommendations data from the match() results. Therefore, you can style this element as you see fit. If you chose to use our default styling make sure to include the approapriate link tag in the header section of your product html code.
```html
<link rel="stylesheet" type="text/css" href="https://www.findmine.us/static/css/findmine.css">
```
Alternatively you may either implement your own styling or work with our representatives to obtain the appropriate url for the stylesheet file FINDMINE have built for your store.

###4. Work with us to improve the data Findmine identifies from your items
Findmine identifies and recommends items based on several pieces of data that we gather from your website. This data includes:
- title
- descriptions
- images
- price

We use a machine learning model by default to find these pieces of data in your page. But you can make item recognition even more accurate by tagging this data in your page in a CSS-identifiable way. We will then work with you to develop a protocol for retrieving your tagged data.

### 5. The End
This is it. Nothing else is left to do and now it is time to sit back and enjoy automatically generated product recommendations on your site. Keep in mind that the recommendations may not appear right away and will only start working officially once our technical team process your activates the system.

**NOTE**

If for some reason something is not working or these instructions are not sufficient to get the module running on your website absolutely feel free to email us at support@findmine.us and we will make sure to resolve any problem you have with setting our system.
