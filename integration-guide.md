#Integration Guide

####Requirements
This document presumes that the reader is familiar with html, javascript, and jQuery.

####Terminology
- Findmine: the Findmine server and API, which responds to you, the client
- findmine.js: a javascript file that contains the client-side code
- findmine: a javascript object, created upon the execution of findmine.js, which provides front-end functionality for accessing Findmine
- item: one of your products, represented as a single product page
- recommendations set: a collection of items that complement the currently displayed item

###1. Embed the findmine.js module into your website
findmine.js creates a global javascript object called findmine, which you can use to request recommendations.
You should embed findmine.js into each item’s product page.
To embed findmine.js, simply include the following lines in your html:
<script src="http://www.findmine.us/findmine-latest.js"> </script>

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

Because match() returns a Deferred object, you really should attach asyn-
chronous handlers to be called upon its completion.

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

The match() method stores our recommendations within the findmine object,

in findmine.matched. Therefore, you can access this data and update your

page however you’d like.

The render() method will produce a bare-bones html element containing the

recommendations data from the match() results. Therefore, you can style this

element as you see fit.

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



### 1. Click Install
To begin on-boarding of our service on your e-commerce site locate our findmine app on shopify's app-store and hit the get button found on the app's page. Then when the new page pops hit the install FINDMINE button and move on the the next instruction. Alternatively you have received a link from us instructing you to follow that link. By hitting the link you will be redirected to the same page where you can find the install FINDMINE button. Hit it and move on the following instruction. 

### 2. Findmine Got Your Permission
If you paid close attention to the installation button, by installing the findmine app through the shopify's app-store you have given our system permission to begin building sets for your products and our representatives as well as a professional develop will get in touch with you very soon to talk about the look for your customized plugin. To ensure our recommendations fit your brand's style and feel we want to not only build sets that represent that look but also work with you on designing the look for our embedded system.

### 3. Request the Module
To begin integration with our system you must ensure that our module is downloaded when your customers visit your product pages. To do so please include this snippet of code in your product html file's head tag. By doing so, each time one of your customer's visits your site our module we be invoked on your site and a global findmine object will be created through which the entire functionality is exposed at the developer's level. If you are not a developer don't be afraid because one of our representatives must have already realized this and assigned a personal developer to your account who is currently getting in touch with you or setting this up for you. If that is the case you can skip the rest of the instructiosn. Alternatively, if you are a developer or just technically savy, keep reading on and look at the illustration of the created global object below. For exact documentation feel free to refer to our documentation page: [API Documentations](https://github.com/Mishki/docs)
```
<script src="http://www.findmine.us/findmine-latest.js"></script>
```
![Findmine Global](https://github.com/Mishki/docs/blob/master/assets/findmine-global.gif)

### 4.
> In this particular example we assume that your site uses the jQuery library to perform first time auto operations during the window onload event.

At this point you are pretty much ready and all that is needed is to make a request from the product's page to our servers to match the currently viewed product to a particular group of product sets and load the results to the screen. To do so you must run the match() function which in turn will retern a jQuery Deferred object on which you may perform the .done() function or the .fail() function to attach asynchronious handlers. In the code snippet below we are attaching the .done() handler in which you must place the code for rendering the results to the screen. To help you with the rendering we have included the render() function however you should use that function only if you know what you are doing. Otherwise make sure to get in touch with us so we could guide you through the process step by step. Please make sure you read through the documentation for the match() and render() functions to ensure utmost reliability of performance on your website.
```
$(window).load(function() {
    if (typeof findmine !== "undefined") {
        findmine.match(null, true).done(function() {
            // Place your custom code here.
        
            // Or use the help function.
            // findmine.render();
        });
    }
});
```

### 5. The End
This is it. Nothing else is left to do and now it is time to sit back and enjoy automatically generated product recommendations on your site. Keep in mind that the recommendations may not appear right away and will only start working officially once our representatives process your company's paper work.

**NOTE**

If for some reason something is not working or these instructions are not sufficient to get the module running on your website absolutely feel free to email us at support@findmine.us and we will make sure to resolve any problem you have with setting our system. 
