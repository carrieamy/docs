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

###2. The findmine Object Description
The findmine object exposes three important methods:

```javascript
findmine.identify(identity)
```
This method connects to FINDMINE in order to identify the item on the page. The function returns returns a jQuery Deferred object containing the data returned from the server upon success or the error status codes upon failure. This function accepts an object as it's parameter for the purpose of overriding some of the data that FINDMINE would otherwise attempt to determine on its own using machine learning mechanisms.

This method may be ignored, unless used for testing or development purposes.

```javascript
findmine.match(identity, inquiry)
```


```javascript
findmine.render(selector, config)
```

balhd
– selector: the CSS selector for the html element to be rendered into,

defaulting to "#findmine-container"

– config: a javascript object for configuring render’s output, defaulting

to:

{

header: "Complete the Look",

next: "Next Outfit",

previous: "Previous Outfit"

}

Helper function that renders the results of match() into an html element.

###3. Call match(), and configure the callback methods
This section also applies to identify()
Because match() returns a Deferred object, you really should attach asyn-chronous handlers to be called upon its completion.
For example, the following code calls match() and attaches the .done() and
.fail() handlers to the Deferred object.
Note that the handlers are chained in jQuery fashion. Please see jQuery’s doc-
umentation for more details.

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

###3. Create your own html or style ours
The match() method stores our recommendations within the findmine object, in findmine.matched. Therefore, you can access this data and update your page however you’d like.
The render() method will produce a bare-bones html element containing the recommendations data from the match() results. Therefore, you can style this element as you see fit.

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
