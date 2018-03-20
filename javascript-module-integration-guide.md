# Integration Guide

#### Requirements
This document presumes that the reader is familiar with html, javascript, and jQuery.

#### Terminology
- **FINDMINE**: the FINDMINE server and API platform, which is responsible for processing and generating the recommendation data as well as identifying your products.
- **findmine.js**: a javascript file that contains the client-side code for automating the submission of requests to the server side as well as rendering the recommendations.
- **findmine**: a javascript global object, created upon the execution of findmine.js, which provides front-end functionality for accessing data returned from FINDMINE. 
- **item**: a unit representing a single identified product page. The product upon which the recommendation is being generated may be referred to as **sample item**, in contrast to the items which comprise a recommended set.
- **set**: a collection of items that complement the currently displayed sample item. Each set may or may not contain the sample item amongst the items associated to the set.

### 1. Embed findmine.js Module into your Website
**findmine.js** creates a global javascript object called **findmine**, which you can use to request recommendations. In order to embed the findmine.js module, simply include the following lines in the header section of the html code pertaining to the product detail pages.
```html
<script src="http://www.findmine.com/findmine-latest.js"> </script>
```

Once the module is loaded, the **findmine** object will be created globally and may be interacted with via the console.
![Findmine Global](https://github.com/Mishki/docs/blob/master/assets/findmine-global.gif)

### 2. The findmine Object Description
The findmine object exposes two important methods:

```javascript
findmine.match(identity)
```
The match method takes information about a product and returns matching product sets (outfits).

`identity` is a dictionary that must include: 
 - The uniquely identifying id as specified in your feed file. Generally a product-color specific sku. 
   - `unique_id` (str)
 - Other infrmation used to update Findmine in realtime, by default:
   - `price` (float)
   - `stock` (str, either `"in stock"` or `"out of stock"`)
   
(for more details see example below)
   
If desired or requried by your business rules `identity` may also contain other information used to inform the matching algorithm, or to realtime update information.

```javascript
findmine.render(selector)
```
The render function renders the necessary html to the specified tag by the **selector** parameter. This is simply a css selector string pointing to the empty div object where this html should be generated.

### 3. Example match() and render() call:
The following code calls match() and attaches the .then() handler to the Deferred object. Note that the handlers are chained in jQuery fashion. Please see jQuery’s Deferred documentation for more details.

```javascript
$(window).load(function() {
    var identity = {
        "product_color_id": "P123-C123",
        "price": 29.99,
        "stock": "in stock"
    }
    findmine.match(identity).then(function() {
        findmine.render('#findmine-container');
    });
});
```

Please ensure that there is a provided html container for the module to be rendered to. This container is referenced using the css selection inside of the render() function above.

```html
<div id="findmine-container"></div>
```

### 4. Styling the module

For styling and html integration you will work with our representatives and use our team to build out a CSS stylesheet and HTML tailored to your page. We will give you a custom css file to link in your header.

Alternatively, the match() method stores our recommendations within the findmine object, in findmine.matched. Therefore, you can access this data and update your page however you’d like. The render() method will produce a bare-bones html elements containing the recommendations data from the match() results. You may style this element as you see fit. If you chose to use our default styling make sure to include the approapriate link tag in the header section of your product html code.
```html
<link rel="stylesheet" type="text/css" href="https://www.findmine.com/static/css/findmine.css">
```

### 5. The End

That's it. Nothing else is left to do and now it is time to sit back and enjoy automatically generated complimentary product sets on your site. Keep in mind that the recommendations may not appear right away and will only start working officially once our technical team processes your activation the system and once sets are approved by your merchandising team (if desired).

**NOTE**

If for some reason something is not working or these instructions are not sufficient to get the module running on your website, absolutely feel free to email us at support@findmine.com so we can help.
