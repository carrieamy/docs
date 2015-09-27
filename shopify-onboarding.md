 ### 1. Click Install
To begin on-boarding of our service on your e-commerce site locate our findmine app on shopify's app-store and hit the get button found on the app's page. Then when the new page pops hit the install FINDMINE button and move on the the next instruction. Alternatively you have received a link from us instructing you to follow that link. By hitting the link you will be redirected to the same page where you can find the install FINDMINE button. Hit it and move on the following instruction. 

### 2. Findmine Got Your Permission
If you paid close attention to the installation button, by installing the findmine app through the shopify's app-store you have given our system permission to begin building sets for your products and our representatives as well as a professional develop will get in touch with you very soon to talk about the look for your customized plugin. To ensure our recommendations fit your brand's style and feel we want to not only build sets that represent that look but also work with you on designing the look for our embedded system.

### 3. Request the Module
To begin integration with our system you must ensure that our module is downloaded when your customers visit your product pages. To do so please include this snippet of code in your product html file's head tag. By doing so, each time one of your customer's visits your site our module we be invoked on your site and a global findmine object will be created through which the entire functionality is exposed at the developer's level. If you are not a developer, don't be afraid because one of our representative's must have already realized this and assigned a personal developer to your account who is currently getting in touch with you. Alternatively if you are a developer and you can see the illustration of the created global object below. For exact documentation feel free to refer to our documentation page: [API Documentations](https://github.com/Mishki/docs)
```
<script src="http://www.findmine.us/findmine-latest.js"></script>
```


### 4.
Curabitur accumsan enim at mi viverra vulputate. Sed scelerisque tempus nisl, in molestie eros accumsan eu. Nulla suscipit mollis risus sit amet pretium. Sed feugiat viverra elementum. Sed vitae nisl id est iaculis congue quis eget massa. Vivamus nec nisi tempor, varius metus nec, tincidunt tortor. Curabitur malesuada lectus eget quam scelerisque, vel auctor nunc egestas. Pellentesque dapibus pellentesque dui, sit amet lobortis ipsum molestie posuere. Suspendisse sagittis est sit amet elit facilisis lacinia. Duis a sollicitudin sapien.
```
$(window).load(function() {
    if (typeof findmine !== "undefined") {
        findmine.match(null, true).done(function() {
            // Generate information to the screen
        });
    }
});
```

### 5. 
Curabitur accumsan enim at mi viverra vulputate. Sed scelerisque tempus nisl, in molestie eros accumsan eu. Nulla suscipit mollis risus sit amet pretium. Sed feugiat viverra elementum. Sed vitae nisl id est iaculis congue quis eget massa. Vivamus nec nisi tempor, varius metus nec, tincidunt tortor. Curabitur malesuada lectus eget quam scelerisque, vel auctor nunc egestas. Pellentesque dapibus pellentesque dui, sit amet lobortis ipsum molestie posuere. Suspendisse sagittis est sit amet elit facilisis lacinia. Duis a sollicitudin sapien.
```
{
    uni: "{{ product.id }}",
    url: "{{ shop.url }}{{ product.url }}",
    price: {{ product.selected_or_first_available_variant.price | money_without_currency }},
    title: '{{ product.title }}',
    stock: {{ product.available }},
    images: [
        "{{ product.featured_image | img_url: 'grande' }}",
        "{{ product.featured_image | img_url: '1024x1024' }}",
        "{{ product.featured_image | img_url: '2048x2048' }}"
    ]
}
```

### 6. 
Curabitur accumsan enim at mi viverra vulputate. Sed scelerisque tempus nisl, in molestie eros accumsan eu. Nulla suscipit mollis risus sit amet pretium. Sed feugiat viverra elementum. Sed vitae nisl id est iaculis congue quis eget massa. Vivamus nec nisi tempor, varius metus nec, tincidunt tortor. Curabitur malesuada lectus eget quam scelerisque, vel auctor nunc egestas. Pellentesque dapibus pellentesque dui, sit amet lobortis ipsum molestie posuere. Suspendisse sagittis est sit amet elit facilisis lacinia. Duis a sollicitudin sapien.

### 7. 
Curabitur accumsan enim at mi viverra vulputate. Sed scelerisque tempus nisl, in molestie eros accumsan eu. Nulla suscipit mollis risus sit amet pretium. Sed feugiat viverra elementum. Sed vitae nisl id est iaculis congue quis eget massa. Vivamus nec nisi tempor, varius metus nec, tincidunt tortor. Curabitur malesuada lectus eget quam scelerisque, vel auctor nunc egestas. Pellentesque dapibus pellentesque dui, sit amet lobortis ipsum molestie posuere. Suspendisse sagittis est sit amet elit facilisis lacinia. Duis a sollicitudin sapien.
