# Javascript Module On-boarding Process

In this document are described the steps one should follow in order to complete the on-boarding process with the FINDMINE Inc. technology. These bullet point steps explain the overall technical steps needed in order to fully integrate the FINDMINE Inc. technology using the currently developed javascript module. The specific technical information pertaining to the javascript code itself, and the information of how to integrate it, can be found at [Javascript Module Integration Guide](https://github.com/findmine/docs/blob/master/javascript-module-integration-guide.md) and of course for any technical assistance please feel free to contact us at [support@findmine.com](mailto://support@findmine.com)

### 1. Product Feed via SFTP or API integration
In order for the FINDMINE Inc. system to operate with one's technology the system first and foremost must have access to the current/latest product feed information. This information can be provided though a number of channels however currently we support out of the box two methods. The first one is via an sftp server which FINDMINE Inc. hosts at `sftp.findmine.com` and, the second, is provided, if exists, through a client's product catalog API. Any on-boarding process begins by establishing a channel by which the FINDMINE Inc. system could continuously receive a product feed information on a frequent basis. This is to ensure that ingest product information always stays up to date. Before any initial submission of a product feed to the sftp, the FINDMINE Inc. team must create an sftp user account. In order to achieve this, please communicate with your person of contact or touch base at [support@findmine.com](mailto://support@findmine.com). Once all the legal details are resolved, the FINDMINE Inc. team will create a user account in a jiffy.
> More frequent the access to the product feed provides better product data synchronization. The FINDMINE Inc. team can accommodate custom product feed integrations if needed.

### 2. Integrate the Javascript Module
Please find your way to the technical explanation at [Javascript Module Integration Guide](https://github.com/findmine/docs/blob/master/javascript-module-integration-guide.md) explaining exactly how to integrate the FINDMINE Inc. javascript module onto your site. The javascript module is responsible for two primary functionalities related to the presentation of the FINDMINE Inc. recommendations. The javascript module allows one to communicate with the FINDMINE Inc. API without really deep diving into the API implementation. This allows customers looking to integrate our technology onto their webpage oriented service (product page, checkout page, etc.) Therefore, the primary functioning of the module is to perform data communication with the FINDMINE Inc. servers. The second functionality that the module provides, allows one to render the results of the recommendation onto the webpage. This means, that when the javascript module successfully communicated with the FINDMINE Inc. servers and obtaining a recommendation, and is now ready to render the recommendation onto the screen, the javascript module will automatically generate required html in the specified location on the page. The details of this can be found inside of the Integration Guide mentioned above.

### 3.  Custom Look and Feel
When using the javascript module, unless provided an alternative, the default FINDMINE Inc. styling will be applied onto the rendered recommendation. We understand that most clients would like to match the aesthetics of the rendered recommendation to match their own website. In order to do so, please feel free to apply custom css styling in a separate file and communicate this file to the FINDMINE Inc. development team. We will upload this file onto our Content Delivery Network ("CDN") and make sure to serve these files specifically for your domain together with the javascript module. In order to develop a custom styling, one must first ensure that the javascipt module is integrated on a development environment and some dummy recommendations are served. To do that, please communicate to the FINDMINE Inc. team your development information such as the development domain name, the dummy products used for testing the integration, and any additional information that will allow the FINDMINE Inc. team to ensure recommendations are served on your development environment. Once done, your developers will be able to see live dummy recommendations within your store's development environment and the styling could be directly developed and applied using tools such as Chrome DevTools, FireBug, etc. When the file is prepared make sure to send it to FINDMINE Inc. to [support@findmine.com](mailto://support@findmine.com).

## Done!
At this point all your technical work is done. Make sure to follow up with your person of contact in order to ensure that your merchandising training is scheduled and that FINDMINE Inc. team has received any outfit styling guides such as look-books or runway photo shoots.