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
Referer: http://www.sample.com/{route/to/canonical/product/page}
Origin: http://www.sample.com


{
    "url": "http://www.sample.com/{route/to/product/page}"
}
```
 > Note that Referer and Origin are required headers

##### Sample Response
```http
HTTP/1.1 200 OK
Content-Type: application/json
Location: https://www.findmine.com/api/v1/items/<item_id:int>
```

##### JSON Body Parameters
> All passed parameters will be processed by the FINDMINE system and those parameters that are not specified by explicit numerical representation will be ingested using machine learning and mapping technologies to transform them into explicit IDs

- `url` [ *str* ] **required** - url of the product page that contains the identifiable item.

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
Origin: http://www.sample.com
Accept: */*; application/json
```

##### Sample Response
```http
HTTP/1.1 200 OK
Content-Type: application/json

[
  {
    "published": 1,
    "occasion_id": 1,
    "store_ids": "[10]",
    "flagged": 0,
    "user_id": 195,
    "style_id": 1,
    "set_id": 2710,
    "href": "https://www.findmine.com/api/v1/sets/2710",
    "style_name": "Default Style",
    "occasion_name": "Default Occasion",
    "set_items": [
      {
        "category_name": "Boots",
        "price": 498.0,
        "flagged": 0,
        "team_id": 1,
        "store_id": 10,
        "size_id": 1,
        "images": [
          {
            "img_url": "https://i1.adis.ws/i/johnvarvatos/F3456T2-Y541-218-A/Sullivan-Boot.jpg?img404=product-image-not-found&$productdetailprimary$",
            "item_id": 279250,
            "image_id": 3970213,
            "href": "https://www.findmine.com/api/v1/images/3970213",
            "state": 2
          }
        ],
        "sale_id": 1,
        "season_name": "F17",
        "item_url": "https://www.johnvarvatos.com/product?utm_campaign=JV&utm_source=FINDMINE&pid=F3456T2-Y541&color=218&utm_medium=PDP",
        "sale_name": "Full Price",
        "category_id": 109,
        "brand_name": "Collection",
        "pid": "F3456T2-Y541",
        "date_created": "2017-07-14 16:11:32",
        "size_name": "Default Size",
        "item_id": 279250,
        "sport_name": "Default Sport",
        "user_id": 204,
        "set_id": 2710,
        "href": "https://www.findmine.com/api/v1/items/279250",
        "store_name": "John Varvatos",
        "title": "Sullivan Boot",
        "sport_id": 1,
        "stock": 1,
        "season_id": 16,
        "brand_id": 2,
        "priority": 0,
        "team_name": "Default Team",
        "colors": [
          {
            "color_id": 1754671,
            "image_id": 3970213,
            "href": "https://www.findmine.com/api/v1/colors/1754671"
          },
          {
            "color_id": 1754673,
            "image_id": 3970213,
            "href": "https://www.findmine.com/api/v1/colors/1754673"
          },
          {
            "color_id": 1754676,
            "image_id": 3970213,
            "href": "https://www.findmine.com/api/v1/colors/1754676"
          },
          {
            "color_id": 1754677,
            "image_id": 3970213,
            "href": "https://www.findmine.com/api/v1/colors/1754677"
          }
        ],
        "date_updated": "2017-07-14 22:06:59"
      },
      {
        "category_name": "Jeans",
        "price": 298.0,
        "flagged": 0,
        "team_id": 1,
        "store_id": 10,
        "size_id": 1,
        "images": [
          {
            "img_url": "https://i1.adis.ws/i/johnvarvatos/J244T2-AZHA-412-A/Woodward-Cotton-Stretch-Jean.jpg?img404=product-image-not-found&$productdetailprimary$",
            "item_id": 161050,
            "image_id": 1828794,
            "href": "https://www.findmine.com/api/v1/images/1828794",
            "state": 2
          }
        ],
        "sale_id": 1,
        "season_name": "F17",
        "item_url": "https://www.johnvarvatos.com/product?pid=J244T2-AZHA&utm_medium=PDP&utm_campaign=JV&color=412&utm_source=FINDMINE",
        "sale_name": "Full Price",
        "category_id": 38,
        "brand_name": "Collection",
        "pid": "J244T2-AZHA",
        "date_created": "2017-06-18 01:24:42",
        "size_name": "Default Size",
        "item_id": 161050,
        "sport_name": "Default Sport",
        "user_id": 204,
        "set_id": 2710,
        "href": "https://www.findmine.com/api/v1/items/161050",
        "store_name": "John Varvatos",
        "title": "Woodward Cotton Stretch Jean",
        "sport_id": 1,
        "stock": 1,
        "season_id": 16,
        "brand_id": 2,
        "priority": 0,
        "team_name": "Default Team",
        "colors": [
          {
            "color_id": 928040,
            "image_id": 1828794,
            "href": "https://www.findmine.com/api/v1/colors/928040"
          }
        ],
        "date_updated": "2017-06-19 18:21:16"
      },
      {
        "category_name": "Pullover",
        "price": 428.0,
        "flagged": 0,
        "team_id": 1,
        "store_id": 10,
        "size_id": 1,
        "images": [
          {
            "img_url": "https://i1.adis.ws/i/johnvarvatos/Y2246T2-ATL8-368-A/Broken-Fair-Isle-Sweater.jpg?img404=product-image-not-found&$productdetailprimary$",
            "item_id": 155130,
            "image_id": 1742589,
            "href": "https://www.findmine.com/api/v1/images/1742589",
            "state": 2
          }
        ],
        "sale_id": 1,
        "season_name": "F17",
        "item_url": "https://www.johnvarvatos.com/product?color=368&utm_source=FINDMINE&pid=Y2246T2-ATL8&utm_campaign=JV&utm_medium=PDP",
        "sale_name": "Full Price",
        "category_id": 41,
        "brand_name": "Collection",
        "pid": "Y2246T2-ATL8",
        "date_created": "2017-05-19 15:14:46",
        "size_name": "Default Size",
        "item_id": 155130,
        "sport_name": "Default Sport",
        "user_id": 195,
        "set_id": 2710,
        "href": "https://www.findmine.com/api/v1/items/155130",
        "store_name": "John Varvatos",
        "title": "Broken Fair Isle Sweater",
        "sport_id": 1,
        "stock": 1,
        "season_id": 16,
        "brand_id": 2,
        "priority": 0,
        "team_name": "Default Team",
        "colors": [
          {
            "color_id": 886917,
            "image_id": 1742589,
            "href": "https://www.findmine.com/api/v1/colors/886917"
          },
          {
            "color_id": 886918,
            "image_id": 1742589,
            "href": "https://www.findmine.com/api/v1/colors/886918"
          }
        ],
        "date_updated": "2017-05-24 18:57:35"
      }
    ],
    "brand_ids": "[2]",
    "item_ids": "[155130,155753,161050,279250]",
    "date_updated": "2017-07-24 18:46:23",
    "date_created": "2017-05-24 18:49:56"
  },
  {
    "published": 1,
    "occasion_id": 1,
    "store_ids": "[10]",
    "flagged": 0,
    "user_id": 195,
    "style_id": 1,
    "set_id": 2313,
    "href": "https://www.findmine.com/api/v1/sets/2313",
    "style_name": "Default Style",
    "occasion_name": "Default Occasion",
    "set_items": [
      {
        "category_name": "Bag",
        "price": 298.0,
        "flagged": 0,
        "team_id": 1,
        "store_id": 10,
        "size_id": 1,
        "images": [
          {
            "img_url": "https://i1.adis.ws/i/johnvarvatos/G031T1B-Y978-412-A/Croc-Inspired-Backpack.jpg?img404=product-image-not-found&$productdetailprimary$",
            "item_id": 155139,
            "image_id": 1742708,
            "href": "https://www.findmine.com/api/v1/images/1742708",
            "state": 2
          }
        ],
        "sale_id": 1,
        "season_name": "S17",
        "item_url": "https://www.johnvarvatos.com/product?pid=G031T1B-Y978&utm_campaign=JV&utm_source=FINDMINE&color=412&utm_medium=PDP",
        "sale_name": "Full Price",
        "category_id": 120,
        "brand_name": "U.S.A",
        "pid": "G031T1B-Y978",
        "date_created": "2017-05-19 16:02:50",
        "size_name": "Default Size",
        "item_id": 155139,
        "sport_name": "Default Sport",
        "user_id": 204,
        "set_id": 2313,
        "href": "https://www.findmine.com/api/v1/items/155139",
        "store_name": "John Varvatos",
        "title": "Croc-Inspired Backpack",
        "sport_id": 1,
        "stock": 1,
        "season_id": 14,
        "brand_id": 3,
        "priority": 0,
        "team_name": "Default Team",
        "colors": [
          {
            "color_id": 886980,
            "image_id": 1742708,
            "href": "https://www.findmine.com/api/v1/colors/886980"
          }
        ],
        "date_updated": "2017-05-21 22:30:18"
      },
      {
        "category_name": "Polo Shirt",
        "price": 98.0,
        "flagged": 0,
        "team_id": 1,
        "store_id": 10,
        "size_id": 1,
        "images": [
          {
            "img_url": "http://i1.adis.ws/i/johnvarvatos/K1381T1B-BHZ4B-001-A/Mercerized-Peace-Polo.jpg?img404=product-image-not-found&$productdetailprimary$",
            "item_id": 146105,
            "image_id": 1608995,
            "href": "https://www.findmine.com/api/v1/images/1608995",
            "state": 2
          }
        ],
        "sale_id": 1,
        "season_name": "S17",
        "item_url": "https://www.johnvarvatos.com/product?utm_campaign=JV&utm_source=FINDMINE&pid=K1381T1B-BHZ4B&utm_medium=PDP&color=001",
        "sale_name": "Full Price",
        "category_id": 7,
        "brand_name": "U.S.A",
        "pid": "K1381T1B-BHZ4B",
        "date_created": "2017-04-20 20:31:27",
        "size_name": "Default Size",
        "item_id": 146105,
        "sport_name": "Default Sport",
        "user_id": 190,
        "set_id": 2313,
        "href": "https://www.findmine.com/api/v1/items/146105",
        "store_name": "John Varvatos",
        "title": "Mercerized Peace Polo",
        "sport_id": 1,
        "stock": 1,
        "season_id": 14,
        "brand_id": 3,
        "priority": 0,
        "team_name": "Default Team",
        "colors": [
          {
            "color_id": 824268,
            "image_id": 1608995,
            "href": "https://www.findmine.com/api/v1/colors/824268"
          }
        ],
        "date_updated": "2017-04-28 17:10:30"
      },
      {
        "category_name": "Jeans",
        "price": 198.0,
        "flagged": 0,
        "team_id": 1,
        "store_id": 10,
        "size_id": 1,
        "images": [
          {
            "img_url": "https://i1.adis.ws/i/johnvarvatos/J306T1B-ARCO-100-A/Bowery-Cotton-Stretch-Jean.jpg?img404=product-image-not-found&$productdetailprimary$",
            "item_id": 108437,
            "image_id": 1066504,
            "href": "https://www.findmine.com/api/v1/images/1066504",
            "state": 2
          }
        ],
        "sale_id": 1,
        "season_name": "S17",
        "item_url": "https://www.johnvarvatos.com/product?utm_medium=PDP&pid=J306T1B-ARCO&utm_source=FINDMINE&color=100&utm_campaign=JV",
        "sale_name": "Full Price",
        "category_id": 38,
        "brand_name": "U.S.A",
        "pid": "J306T1B-ARCO",
        "date_created": "2017-01-27 00:48:24",
        "size_name": "Default Size",
        "item_id": 108437,
        "sport_name": "Default Sport",
        "user_id": 4,
        "set_id": 2313,
        "href": "https://www.findmine.com/api/v1/items/108437",
        "store_name": "John Varvatos",
        "title": "Bowery Cotton Stretch Jean",
        "sport_id": 1,
        "stock": 1,
        "season_id": 14,
        "brand_id": 3,
        "priority": 0,
        "team_name": "Default Team",
        "colors": [
          {
            "color_id": 567786,
            "image_id": 1066504,
            "href": "https://www.findmine.com/api/v1/colors/567786"
          }
        ],
        "date_updated": "2017-03-09 18:53:32"
      }
    ],
    "brand_ids": "[3]",
    "item_ids": "[108437,146105,149731,155139]",
    "date_updated": "2017-06-28 18:44:02",
    "date_created": "2017-03-03 23:54:09"
  },
  {
    "published": 1,
    "occasion_id": 1,
    "store_ids": "[10]",
    "flagged": 0,
    "user_id": 195,
    "style_id": 1,
    "set_id": 2804,
    "href": "https://www.findmine.com/api/v1/sets/2804",
    "style_name": "Default Style",
    "occasion_name": "Default Occasion",
    "set_items": [
      {
        "category_name": "Bag",
        "price": 298.0,
        "flagged": 0,
        "team_id": 1,
        "store_id": 10,
        "size_id": 1,
        "images": [
          {
            "img_url": "https://i1.adis.ws/i/johnvarvatos/G031T1B-Y978-412-A/Croc-Inspired-Backpack.jpg?img404=product-image-not-found&$productdetailprimary$",
            "item_id": 155139,
            "image_id": 1742708,
            "href": "https://www.findmine.com/api/v1/images/1742708",
            "state": 2
          }
        ],
        "sale_id": 1,
        "season_name": "S17",
        "item_url": "https://www.johnvarvatos.com/product?pid=G031T1B-Y978&utm_campaign=JV&utm_source=FINDMINE&color=412&utm_medium=PDP",
        "sale_name": "Full Price",
        "category_id": 120,
        "brand_name": "U.S.A",
        "pid": "G031T1B-Y978",
        "date_created": "2017-05-19 16:02:50",
        "size_name": "Default Size",
        "item_id": 155139,
        "sport_name": "Default Sport",
        "user_id": 204,
        "set_id": 2804,
        "href": "https://www.findmine.com/api/v1/items/155139",
        "store_name": "John Varvatos",
        "title": "Croc-Inspired Backpack",
        "sport_id": 1,
        "stock": 1,
        "season_id": 14,
        "brand_id": 3,
        "priority": 0,
        "team_name": "Default Team",
        "colors": [
          {
            "color_id": 886980,
            "image_id": 1742708,
            "href": "https://www.findmine.com/api/v1/colors/886980"
          }
        ],
        "date_updated": "2017-05-21 22:30:18"
      },
      {
        "category_name": "Shorts",
        "price": 98.0,
        "flagged": 0,
        "team_id": 1,
        "store_id": 10,
        "size_id": 1,
        "images": [
          {
            "img_url": "http://i1.adis.ws/i/johnvarvatos/S155T1B-AIFB-001-A/Linen-Flat-Front-Shorts.jpg?img404=product-image-not-found&$productdetailprimary$",
            "item_id": 120741,
            "image_id": 1234893,
            "href": "https://www.findmine.com/api/v1/images/1234893",
            "state": 2
          }
        ],
        "sale_id": 1,
        "season_name": "S17",
        "item_url": "https://www.johnvarvatos.com/product?utm_campaign=JV&color=001&pid=S155T1B-AIFB&utm_medium=PDP&utm_source=FINDMINE",
        "sale_name": "Full Price",
        "category_id": 12,
        "brand_name": "U.S.A",
        "pid": "S155T1B-AIFB",
        "date_created": "2017-03-29 00:29:24",
        "size_name": "Default Size",
        "item_id": 120741,
        "sport_name": "Default Sport",
        "user_id": 185,
        "set_id": 2804,
        "href": "https://www.findmine.com/api/v1/items/120741",
        "store_name": "John Varvatos",
        "title": "Linen Flat Front Shorts",
        "sport_id": 1,
        "stock": 1,
        "season_id": 14,
        "brand_id": 3,
        "priority": 0,
        "team_name": "Default Team",
        "colors": [
          {
            "color_id": 647064,
            "image_id": 1234893,
            "href": "https://www.findmine.com/api/v1/colors/647064"
          }
        ],
        "date_updated": "2017-05-05 09:08:14"
      },
      {
        "category_name": "Sneakers",
        "price": 130.0,
        "flagged": 0,
        "team_id": 1,
        "store_id": 10,
        "size_id": 1,
        "images": [
          {
            "img_url": "https://i1.adis.ws/i/johnvarvatos/151285-C-020-A/Chuck-Taylor-Blanket-Stitch.jpg?img404=product-image-not-found&$productdetailprimary$",
            "item_id": 37899,
            "image_id": 590699,
            "href": "https://www.findmine.com/api/v1/images/590699",
            "state": 2
          }
        ],
        "sale_id": 1,
        "season_name": "S17",
        "item_url": "https://www.johnvarvatos.com/product?pid=151285-C&color=020&utm_source=FINDMINE&utm_medium=PDP&utm_campaign=JV",
        "sale_name": "Full Price",
        "category_id": 25,
        "brand_name": "U.S.A",
        "pid": "151285-C",
        "date_created": "2016-05-03 22:37:23",
        "size_name": "Default Size",
        "item_id": 37899,
        "sport_name": "Default Sport",
        "user_id": 4,
        "set_id": 2804,
        "href": "https://www.findmine.com/api/v1/items/37899",
        "store_name": "John Varvatos",
        "title": "Chuck Taylor Blanket Stitch",
        "sport_id": 1,
        "stock": 1,
        "season_id": 14,
        "brand_id": 3,
        "priority": 0,
        "team_name": "Default Team",
        "colors": [
          {
            "color_id": 265182,
            "image_id": 590699,
            "href": "https://www.findmine.com/api/v1/colors/265182"
          },
          {
            "color_id": 265183,
            "image_id": 590699,
            "href": "https://www.findmine.com/api/v1/colors/265183"
          },
          {
            "color_id": 265184,
            "image_id": 590699,
            "href": "https://www.findmine.com/api/v1/colors/265184"
          },
          {
            "color_id": 265185,
            "image_id": 590699,
            "href": "https://www.findmine.com/api/v1/colors/265185"
          },
          {
            "color_id": 265187,
            "image_id": 590699,
            "href": "https://www.findmine.com/api/v1/colors/265187"
          },
          {
            "color_id": 265188,
            "image_id": 590699,
            "href": "https://www.findmine.com/api/v1/colors/265188"
          }
        ],
        "date_updated": "2017-03-30 15:58:03"
      },
      {
        "category_name": "T-Shirt",
        "price": 88.0,
        "flagged": 0,
        "team_id": 1,
        "store_id": 10,
        "size_id": 1,
        "images": [
          {
            "img_url": "https://i1.adis.ws/i/johnvarvatos/K1213R2B-KW3B1-103-A/Cotton-Eyelet-Crew.jpg?img404=product-image-not-found&$productdetailprimary$",
            "item_id": 36933,
            "image_id": 581657,
            "href": "https://www.findmine.com/api/v1/images/581657",
            "state": 2
          }
        ],
        "sale_id": 1,
        "season_name": "S17",
        "item_url": "https://www.johnvarvatos.com/product?pid=K1213R2B-KW3B1&color=103&utm_source=FINDMINE&utm_medium=PDP&utm_campaign=JV",
        "sale_name": "Full Price",
        "category_id": 5,
        "brand_name": "U.S.A",
        "pid": "K1213R2B-KW3B1",
        "date_created": "2016-03-03 02:19:39",
        "size_name": "Default Size",
        "item_id": 36933,
        "sport_name": "Default Sport",
        "user_id": 189,
        "set_id": 2804,
        "href": "https://www.findmine.com/api/v1/items/36933",
        "store_name": "John Varvatos",
        "title": "Cotton Eyelet Crew",
        "sport_id": 1,
        "stock": 1,
        "season_id": 14,
        "brand_id": 3,
        "priority": 0,
        "team_name": "Default Team",
        "colors": [
          {
            "color_id": 258428,
            "image_id": 581657,
            "href": "https://www.findmine.com/api/v1/colors/258428"
          },
          {
            "color_id": 258432,
            "image_id": 581657,
            "href": "https://www.findmine.com/api/v1/colors/258432"
          }
        ],
        "date_updated": "2017-03-03 22:43:07"
      }
    ],
    "brand_ids": "[3]",
    "item_ids": "[120741,36933,37899,149731,155139]",
    "date_updated": "2017-06-28 18:43:23",
    "date_created": "2017-06-16 17:13:27"
  }
]
```

##### Query Parameters
- `limit` [ *int* ] - the limit parameter is an integer value that can be used to limit the number of sets returned. If limit is not specified, then the default value is 3.
- `fields` [ *str* ] - comma separated fields indicates which of the fields associated with an item or set of items you would like returned. If no fields specified, the following fields will be returned by default: `href`,`set_id`,`item_ids`,`store_ids`,`brand_ids`,`user_id`,`published`,`flagged`,`style_id`,`style_name`,`occasion_id`,`occasion_name`,`date_created`,`date_updated`,`set_items`
- `branded` [ *int* ] - if the branded parameter is passed as 1, then it means that only sets with items of the same brand as the item passed in the request are returned.
- `teamed` [ *int* ] - if the teamed parameter is passed as 1, then only sets with items of the same team (or default team) as the item passed in the request are returned.
- `sported` [ *int* ] - if the sported parameter is passed as 1, then only sets with items of the same sport (or default sport) as the item passed in the request are returned.
- `sized` [ *int* ] - if the sized parameter is passed as 1, then only sets with items of the same size as the item passed in the request are returned.
- `saled` [ *int* ] - if the saled parameter is passed as 1, then only sets with items of the same sale as the item passed in the request are returned. If the saled parameter is passed as 2, then on sale items will not appear in sets that are returned

> For `branded`, `teamed`, `sported`, `sized`, and `saled` parameters the defaults are set per client's specification. This means that if those parameters are not provided the defaults kick in based on predefined information. These are for the purpose of overriding.

##### Return Codes
- **200** - Recommendation was generated successfully.
- **404** - The system could not generate a recommendation for the sample item.
- **500** - Internal server error has happened. Almost exclusively this means that something with the sample item is wrong. There is nothing that can be done from the user side and support@findmine.com should be contacted.
- **503** - Not all of the functionalities of this endpoints are implemented. If you encounter this response just know you are messing around with something we thought of but didn't have time to implement. If you see this, give us a call, we are hiring.

