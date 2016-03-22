#Integration Guide

####Requirements
This document presumes that the reader is familiar with html, javascript, and jQuery.

####Terminology
- **FINDMINE**: the Findmine server and API platform, which is responsible for processing and generating the recommendation data as well as identifying your products.
- **findmine.js**: a javascript file that contains the client-side code for automating the submission of requests to the server side as well as rendering the returning recommendations.
- **findmine**: a javascript global object, created upon the execution of findmine.js, which provides front-end functionality for accessing data returned from FINDMINE. 
- **item**: a unit representing a single identified product page. The product based on which the recommendation is being generated may be referred to as **sample item**, in contrast to the items which comprise a single recommended set.
- **set**: a collection of items that complement the currently displayed sample item. Each set may or may not contain the sample item amongst the items associated to the set.

###1. Embed the findmine.js module into your website
**findmine.js** creates a global javascript object called **findmine**, which you can use to request recommendations. In order to embed the findmine.js module simply include the following lines in the header section of the html code pertaining to the product pages.
```html
<script src="http://www.findmine.us/findmine-latest.js?shop={{shop.id}}"> </script>
```
In place of the **{{shop.id}}** you must provide the id number for your store.  


###2. Get acquainted with the findmine object
The findmine object exposes three important methods:

• identify(params)

– params: a javascript object to override some of the data that Find-
mine would otherwise attempt to determine on its own (see API

Documentation for details)

Asks Findmine for its representation of the item on the page.

Receives the item’s data, then stores it in the findmine.identity vari-
able.

Returns a jQuery Deferred object.

This method can be ignored, unless you would like to use it for test-
ing/development purposes.

• match(params, branded)

– params: same as in identify()

– branded: a boolean value (see API Documentation for details)

Asks Findmine for recommendation sets!

Receives a list of recommendation sets, then stores it in the

findmine.matched variable.

Returns a jQuery Deferred object.

• render(selector, config)

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
