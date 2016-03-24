### 1. Click Install
To begin on-boarding of our service on your e-commerce site locate our Shopify app at https://apps.shopify.com/findmine and hit the get button found on the app's page. Then, hit the install FINDMINE button and move on the the next instruction. Alternatively you have received a link from us instructing you to follow that link. By hitting the link you will be redirected to the same page where you can find the install FINDMINE button. Hit it and move on the following instruction. 

### 2. FINDMINE Will Reach Out to You
By installing the FINDMINE app, you have alerted our team to begin building sets for your products and a representatives will  get in touch with you (if they haven't already) to sign our licensing agreement and to talk about the look for your customized plugin. To ensure our curated product sets fit your brand's style and feel we want to not only build sets that represent that look but also help you in designing the look and feel for where the sets will appear on your page.

### 3. Request the Module
To begin integration with our system you must ensure that our module is downloaded when your customers visit your product pages. To do so please include this snippet of code in your product html file's head tag. By doing so, each time one of your customer's visits your site our module we be invoked on your site and a global findmine object will be created through which the entire functionality is exposed at the developer's level. If you are not a developer don't be afraid because one of our representatives must have already realized this and assigned a personal developer to your account who is currently getting in touch with you or setting this up for you. If that is the case you can skip the rest of these instructions. 

Alternatively, if you are a developer, keep reading and look at the illustration of the created global object below. For exact documentation feel free to refer to our documentation page: [API Documentations](https://github.com/Mishki/docs)
```
<script src="http://www.findmine.us/findmine-latest.js"></script>
```
![Findmine Global](https://github.com/Mishki/docs/blob/master/assets/findmine-global.gif)

### 4.
> In this particular example we assume that your site uses the jQuery library to perform first time auto operations during the window onload event.

Finally, all that remains is to make a request from the product's page to our servers to match the currently viewed product to a particular group of product sets and load the results to the screen. To do so you must run the match() function which in turn will retern a jQuery Deferred object on which you may perform the .done() function or the .fail() function to attach asynchronious handlers. In the code snippet below we are attaching the .done() handler in which you must place the code for rendering the results to the screen. To help you with the rendering we have included the render() function. Please make sure you read through the documentation for the match() and render() functions to ensure utmost reliability on your website.
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
