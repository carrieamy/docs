# GENERATING RECOMMENDATIONS

Two FINDMINE API endpoints are needed in order to generate a recommendation for a particular item: the items POST and the match sets GET calls. The match sets API call is the endpoint that actually generates the recommendation for a particular item. However, one must provide a FINDMINE `item_id` of the item for which the recommendation will be generated. Since, in most cases, the request to the FINDMINE servers is generated from the client side and that FINDMINE `item_id` is unknown to the client, a second API call can be used to obtain the id in question. 

By invoking the items POST call, a client is telling FINDMINE to identify the item in question, by providing parameters describing the item. Items POST will then return the `item_id` of the product. 

The way items POST is designed is to always return an `item_id`. What that means in practice is that if items POST was not able to identify the product whose information was provided, items POST will then create a new record for a new item in the FINDMINE system and return a new `item_id` value in the form of a `Location` HTTP header.

## Item Identification
```http
POST /api/v1/items
```

This request identifies the item that the recommendation will be based upon. The request ensures that the item of the recommendation has been previously ingested into the FINDMINE system and has been processed. To do so, the endpoint will accept information about the item from the user, and process it so that it conforms to FINDMINE standards. Finally, the endpoint returns a `Location` header pointing to the API endpoint where this item can be examined and manipulated. This endpoint will always return a `Location` header with the `item_id` integer, assuming the request was successful.

> This call is a synchronous call and will block for a few seconds if the item cannot be identified quickly and requires the recording of a new item and machine learning for processing the provided parameters. In order to ensure that one's system does not block, use some version of a promise or future objects to attach a callback for when this call is completed.

##### Sample Request
```http
POST /api/v1/items HTTP/1.1
Content-Type: application/json

{
    "url": "http://www.sample.com/{route/to/product/page}",
    "html": "{HTML}",
    "images": [
        {
            "img_url": "http://www.sample.com/product-image1.jpg",
            "state": 1
        },
        {
            "img_url": "http://www.sample.com/product-image2.jpg",
            "state": 1
        }
    ]
}
```

##### Sample Response
```http
HTTP/1.1 200 OK
Content-Type: application/json
Location: https://www.findmine.com/api/v1/items/<item_id:int>
```

##### JSON Body Parameters
> All passed parameters will be processed by the FINDMINE system and those parameters that are not specified by explicit numerical representation will be ingested using machine learning and mapping technologies to transform them into explicit IDs

- `url` [ *str* ] **required** - url of the product page that contains the identifiable item.
- `html` [ *str* ] - raw and rendered version of the html code of the product page.
- `words` - 
- `images` [ *list[dict]* ] - list of objects containing image information of the sample product.
- `sport` [ *int* | *str* ] - either an exact number representing the sport_id on the FINDMINE system or a string definition of the particular sport of the product.
- `category` [ *int* | *str* ] - either an exact number representing the category_id of the product or a string definition of the category for the product. For the string definition, this may include bread crumbs, category name, etc.
- `title` [ *str* ] - the title of the sample product.
- `description` [ *str* ] - description of the product. This can be any combination of words. The more the better. Our system will process out information from this and will help recognize the item better overall.
- `price` [ *int* | *float* ] - a numerical representation of the price for the product.
- `pid` [ *str* ] - (Product ID "pid") can be any string that represents a tracking id of the item at question. The purpose of this is to help you track one's products using your own tracking enumeration. FINDMINE will provide a unique id for a processed id in the form of `item_id` besides this value.
- `brand` [ *int* | *str* ] - either a number representing the explicit `brand_id` as provided by the FINDMINE system or a string definition of the brand name.
- `season` [ *int* | *str* ] - either the explicit `season_id` as recorded by the FINDMINE system or a string definition of the season name.
- `details` [ *dict* ] - extra storage information for any additional parameters that do not have direct access via the strucutres described above.

> `pid` does not have to be unique, however, if it is not when searching for those PID's the search result will provide multiple results.

##### Return Codes
- **200** - Item was found on the system.
- **201** - Item was not found but was scraped and added to the system with the help of the provided JSON encoded body parameters.
- **400** - Malformed Request. Something is wrong with the request; either required headers or parameters are missing. 
- **403** - Credentials were not provided with the request and the user is unauthorized to perform the operation.
- **500** - Internal server error. Something went wrong and you should email support@findmine.com

## Generating Recommended Sets
```http
GET /api/v1/match/sets/<item_id:int>
```

This request returns sets that are a match for the item indicated in url. The match sets `GET` request is meant to be called after an items `POST` request. The endpoint needs no information other than the FINDMINE `item_id`, returned by items `POST`, the `Referer` url, and the `Accept` format specifications. Currently only the json return format is supported. Assuming that the request was successful and sets were matched for the item in question, the response will include one or more sets of items with information pertaining to the set, as well as information about the items within each set. The request can fail, returning a `404 Not Found` response if for some reason the system was unable to generate an appropriate match for the requested item.

##### Sample Request
```http
GET https://www.findmine.com/api/v1/match/sets/<item_id:int> HTTP/1.1
Referer: http://www.sample.com/{route/to/canonical/product/page}
Accept: */*; application/json
```

##### Sample Response
```http
HTTP/1.1 200 OK
Content-Type: application/json

[
    {
        "item_ids": "[92573,87822,99384,68261]",
        "occasion_name": "Default Occasion",
        "brand_ids": "[2]",
        "flagged": 0,
        "user_id": 4,
        "style_id": 1,
        "date_created": "2016-12-21 22:40:19",
        "set_id": 2142,
        "occasion_id": 1,
        "style_name": "Default Style",
        "set_items": [
            {
                "item_url": "https://www.johnvarvatos.com/product?utm_campaign=JV&color=414&utm_source=FINDMINE&pid=J244S4-BFID&utm_medium=PDP",
                "season_name": "R16",
                "pid": "J244S4-BFID",
                "flagged": 0,
                "user_id": 4,
                "title": "Woodward Jean in Cotton Stretch",
                "sport_name": "Default Sport",
                "team_name": "Default Team",
                "category_name": "Jeans",
                "images": [
                    {
                        "item_id": 99384,
                        "img_url": "https://i1.adis.ws/i/johnvarvatos/J244S4-BFID-414-A/Woodward-Jean-in-Cotton-Stretch.jpg?img404=product-image-not-found&$productdetailprimary$",
                        "href": "https://www.findmine.com/api/v1/images/1008138",
                        "image_id": 1008138,
                        "state": 2
                    }
                ],
                "href": "https://www.findmine.com/api/v1/items/99384",
                "category_id": 38,
                "brand_name": "Collection",
                "store_id": 10,
                "price": 672.83,
                "brand_id": 2,
                "date_updated": "2016-12-22 15:42:43",
                "team_id": 1,
                "date_created": "2016-12-19 19:50:36",
                "set_id": 2142,
                "colors": [
                    {
                        "color_id": 532242,
                        "image_id": 1008138,
                        "href": "https://www.findmine.com/api/v1/colors/532242"
                    },
                    {
                        "color_id": 532243,
                        "image_id": 1008138,
                        "href": "https://www.findmine.com/api/v1/colors/532243"
                    }
                ],
                "item_id": 99384,
                "stock": 1,
                "sport_id": 1,
                "store_name": "John Varvatos",
                "season_id": 12
            },
            {
                "item_url": "https://www.johnvarvatos.com/product?pid=K736S4-QL6&utm_campaign=JV&utm_medium=PDP&utm_source=FINDMINE&color=444",
                "season_name": "R16",
                "pid": "K736S4-QL6",
                "flagged": 0,
                "user_id": 185,
                "title": "Linen V-Neck",
                "sport_name": "Default Sport",
                "team_name": "Default Team",
                "category_name": "T-Shirt",
                "images": [
                    {
                        "item_id": 87822,
                        "img_url": "https://i1.adis.ws/i/johnvarvatos/K736S4-QL6-444-A/Linen-V-Neck.jpg?img404=product-image-not-found&$productdetailprimary$",
                        "href": "https://www.findmine.com/api/v1/images/897434",
                        "image_id": 897434,
                        "state": 2
                    }
                ],
                "href": "https://www.findmine.com/api/v1/items/87822",
                "category_id": 5,
                "brand_name": "Collection",
                "store_id": 10,
                "price": 178.0,
                "brand_id": 2,
                "date_updated": "2016-10-31 23:19:07",
                "team_id": 1,
                "date_created": "2016-10-31 20:16:52",
                "set_id": 2142,
                "colors": [
                    {
                        "color_id": 463873,
                        "image_id": 897434,
                        "href": "https://www.findmine.com/api/v1/colors/463873"
                    }
                ],
                "item_id": 87822,
                "stock": 1,
                "sport_id": 1,
                "store_name": "John Varvatos",
                "season_id": 12
            },
            {
                "item_url": "https://www.johnvarvatos.com/product?pid=887447239831&utm_medium=PDP&utm_source=FINDMINE&color=001&utm_campaign=JV",
                "season_name": "Default Season",
                "pid": "887447239831",
                "flagged": 0,
                "user_id": 4,
                "title": "Morrison Sharpei Boot",
                "sport_name": "Default Sport",
                "team_name": "Default Team",
                "category_name": "Boots",
                "images": [
                    {
                        "item_id": 68261,
                        "img_url": "http://i1.adis.ws/i/johnvarvatos/F1158Q2-Y783-001-A/Morrison-Sharpei-Boot.jpg?img404=product-image-not-found&$productdetailprimary$",
                        "href": "https://www.findmine.com/api/v1/images/752686",
                        "image_id": 752686,
                        "state": 2
                    }
                ],
                "href": "https://www.findmine.com/api/v1/items/68261",
                "category_id": 109,
                "brand_name": "Collection",
                "store_id": 10,
                "price": 798.0,
                "brand_id": 2,
                "date_updated": "2016-09-22 15:46:46",
                "team_id": 1,
                "date_created": "2016-09-21 15:02:54",
                "set_id": 2142,
                "colors": [
                    {
                        "color_id": 371288,
                        "image_id": 752686,
                        "href": "https://www.findmine.com/api/v1/colors/371288"
                    }
                ],
                "item_id": 68261,
                "stock": 1,
                "sport_id": 1,
                "store_name": "John Varvatos",
                "season_id": 1
            }
        ],
        "date_updated": "2016-12-22 04:32:05",
        "published": 1,
        "store_ids": "[10]",
        "href": "https://www.findmine.com/api/v1/sets/2142"
    }
]
```

##### Query Parameters
- `limit` [ *int* ] - the limit parameter is an integer value that can be used to limit the number of items returned. If limit is not specified, then the default value is 100.
- `fields` [ *str* ] - comma separated fields indicates which of the fields associated with an item or set of items you would like returned. If no fields specified, the following fields will be returned by default: `set_id`,`item_ids`,`store_ids`,`brand_ids`,`user_id`,`published`,`flagged`,`style_id`,`style_name`,`occasion_id`,`occasion_name`,`date_created`,`date_updated`,`set_items` 
- `branded` [ *int* ] - if the branded parameter is passed, then it means that only sets with items of the same brand as the item passed in the request are returned. 
- `teamed` [ *int* ] - if the teamed parameter is passed, then only sets with items of the same team as the item passed in the request are returned.
- `sported` [ *int* ] - if the sported parameter is passed, then only sets with items of the same sport as the item passed in the request are returned.

> For `branded`,`teamed`,`sported` parameters the defaults are set per client's specification. This means that if those parameters are not provided the defaults kick in based on predefined information. These are for the purpose of overriding.

##### Return Codes
- **200** - Recommendation was generated successfully.
- **404** - The system could not generate a recommendation for the sample item.
- **500** - Internal server error has happened. Almost exclusively this means that something with the sample item is wrong. There is nothing that can be done from the user side and support@findmine.com should be contacted.
- **503** - Not all of the functionalities of this endpoints are implemented. If you encounter this response just know you are messing around with something we thought of but didn't have time to implement. If you see this, give us a call, we are hiring.

