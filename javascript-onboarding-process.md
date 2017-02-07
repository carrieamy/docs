# Javascript Module On-boarding Process

This document describes the steps to complete the on-boarding process with FINDMINE platform for retailers using the javascript module. These bullet point steps explain the overall technical steps needed in order to fully integrate the FINDMINE Inc. technology, and specific technical information pertaining to the javascript code itself, step-by-step installation instructions to install the module into ecommerce sites or other HTML5-based pages can be found at [Javascript Module Integration Guide](https://github.com/findmine/docs/blob/master/javascript-module-integration-guide.md) For additional technical assistance please feel free to contact us at [support@findmine.com](mailto://support@findmine.com)

### 1. Transfer Product Feed via SFTP or API integration
FINDMINE first needs to access your product information. There are two methods by which we recommend you share your product information on an ongoing basis: 
* Drop feed files to FINDMINE's sftp server, your feed file can be anything that contains basic product information such as title, description, price, image URL, item URL, etc. FINDMINE's SFTP is sftp.findmine.com. Your account rep will provide you a unique username and password. Set up a recurring feed drop to the SFTP. Work with your account rep to determine the best frequency, but we typically recommend once per day.   
> More frequent access to the product feed provides better product data synchronization. The FINDMINE Inc. team can accommodate custom product feed integrations if needed.

- Use your product API. If you have a product catalog API, send integration details to your account rep. This method ensures that product information always stays up to date, and more complex/custom integrations are possible. 

### 2. Integrate the Javascript Module into your customer-facing pages
Please see complete, step-by-step technical documentation at [Javascript Module Integration Guide](https://github.com/findmine/docs/blob/master/javascript-module-integration-guide.md) This document explains exactly how to integrate the FINDMINE Inc. javascript module onto your site or web oriented pages (e.g., product detail page, checkout page, customer support tools, associate resources etc.) The primary function of the module is to communicate data with the FINDMINE  servers, and also is responsible for the visual rendering of the results of the outfit suggestions onto the webpage. This means that when the javascript module successfully communicated with the FINDMINE Inc. servers and obtains outfit recommendations, the javascript module will automatically generate required html in the specified location on the page. More details can be found in the javascript Integration Guide mentioned above.

### 3.  Custom Look and Feel
When using the javascript module, the default FINDMINE styling will be applied. We understand that most clients would like to match the aesthetics of their site, so feel free to apply custom css styling in a separate file. Then simply share this file to with your FINDMINE account rep. We will upload this file onto our Content Delivery Network and serve the file together with the javascript module. In order to develop custom styling:
- Install the javascipt module into your development environment
- Work with your FINDMINE account rep to ensure outfits are appearing. Please communicate to the rep:
 * Your development domain name
 * A sample product you'd like to match outfits to in order to test
 * And any additional information to ensure outfits are showing up 
* Then you should be able to see live outfit suggestions with dummy products in your store's development environment, and you can develop the styling directly using tools such as Chrome DevTools, FireBug, etc. 
* Once the CSS file is prepared, send to your FINDMINE account rep for hosting 

## Done!
At this point all your technical work is done. Make sure to follow up with your account rep in order to ensure that your merchandising team's training is scheduled and that FINDMINE team has received any outfit styling guides such as look-books or runway photo shoots that you may have.
