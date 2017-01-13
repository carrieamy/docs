# FINDMINE API

A reference guide to the FINDMINE API

## Item Identification
```http
POST /api/v1/items
```

This request identifies the product that the recommendation will be based upon. The request ensure that the "sample" product of the recommendation has been previously ingested into the FINDMINE system and has been processed. To do so, the endpoint will accept information about the product from the user, process it to conform the provided information to the FINDMINE standards, and finally return a `Localtion` header pointing to the api endpoint where this item can be examined and manipulated. This endpoint will always return a `Location` header with the `item_id` integer, assuming the request was successful.

> notes to pay attention to.

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
  },
  {
    "item_ids": "[42005,42237,42476,42562]",
    "occasion_name": "Default Occasion",
    "brand_ids": "[3,2]",
    "flagged": 0,
    "user_id": 185,
    "style_id": 1,
    "date_created": "2016-12-16 15:19:19",
    "set_id": 2065,
    "occasion_id": 1,
    "style_name": "Default Style",
    "set_items": [
      {
        "item_url": "https://www.johnvarvatos.com/product?utm_medium=PDP&pid=J315S3B-AOIE&utm_source=FINDMINE&color=207&utm_campaign=JV",
        "season_name": "F16",
        "pid": "J315S3B-AOIE",
        "flagged": 0,
        "user_id": 185,
        "title": "Coated Wight Jean",
        "sport_name": "Default Sport",
        "team_name": "Default Team",
        "category_name": "Jeans",
        "images": [
          {
            "item_id": 42476,
            "img_url": "https://i1.adis.ws/i/johnvarvatos/J315S3B-AOIE-207-A/Coated-Wight-Jean.jpg?img404=product-image-not-found&$productdetailprimary$",
            "href": "https://www.findmine.com/api/v1/images/637684",
            "image_id": 637684,
            "state": 2
          }
        ],
        "href": "https://www.findmine.com/api/v1/items/42476",
        "category_id": 38,
        "brand_name": "Collection",
        "store_id": 10,
        "price": 228.0,
        "brand_id": 2,
        "date_updated": "2016-12-13 23:01:34",
        "team_id": 1,
        "date_created": "2016-08-09 17:18:37",
        "set_id": 2065,
        "colors": [
          {
            "color_id": 297176,
            "image_id": 637684,
            "href": "https://www.findmine.com/api/v1/colors/297176"
          },
          {
            "color_id": 297178,
            "image_id": 637684,
            "href": "https://www.findmine.com/api/v1/colors/297178"
          }
        ],
        "item_id": 42476,
        "stock": 1,
        "sport_id": 1,
        "store_name": "John Varvatos",
        "season_id": 4
      },
      {
        "item_url": "https://www.johnvarvatos.com/product?color=014&pid=K2915S3B-BFV2B&utm_campaign=JV&utm_source=FINDMINE&utm_medium=PDP",
        "season_name": "F16",
        "pid": "K2915S3B-BFV2B",
        "flagged": 0,
        "user_id": 4,
        "title": "RHCP Tiger Graphic Tee",
        "sport_name": "Default Sport",
        "team_name": "Default Team",
        "category_name": "T-Shirt",
        "images": [
          {
            "item_id": 42237,
            "img_url": "https://i1.adis.ws/i/johnvarvatos/K2915S3B-BFV2B-014-A/RHCP-Tiger-Graphic-Tee.jpg?img404=product-image-not-found&$productdetailprimary$",
            "href": "https://www.findmine.com/api/v1/images/637084",
            "image_id": 637084,
            "state": 2
          }
        ],
        "href": "https://www.findmine.com/api/v1/items/42237",
        "category_id": 5,
        "brand_name": "Collection",
        "store_id": 10,
        "price": 78.0,
        "brand_id": 2,
        "date_updated": "2016-08-18 03:40:25",
        "team_id": 1,
        "date_created": "2016-08-09 15:58:46",
        "set_id": 2065,
        "colors": [
          {
            "color_id": 295500,
            "image_id": 637084,
            "href": "https://www.findmine.com/api/v1/colors/295500"
          },
          {
            "color_id": 295501,
            "image_id": 637084,
            "href": "https://www.findmine.com/api/v1/colors/295501"
          },
          {
            "color_id": 295503,
            "image_id": 637084,
            "href": "https://www.findmine.com/api/v1/colors/295503"
          },
          {
            "color_id": 295505,
            "image_id": 637084,
            "href": "https://www.findmine.com/api/v1/colors/295505"
          }
        ],
        "item_id": 42237,
        "stock": 1,
        "sport_id": 1,
        "store_name": "John Varvatos",
        "season_id": 4
      },
      {
        "item_url": "https://www.johnvarvatos.com/product?utm_campaign=JV&pid=F3315S3B-A12B&utm_medium=PDP&color=001&utm_source=FINDMINE",
        "season_name": "F16",
        "pid": "F3315S3B-A12B",
        "flagged": 0,
        "user_id": 4,
        "title": "Barrett Creeper Mid Top Zip Sneaker",
        "sport_name": "Default Sport",
        "team_name": "Default Team",
        "category_name": "Sneakers",
        "images": [
          {
            "item_id": 42562,
            "img_url": "https://i1.adis.ws/i/johnvarvatos/F3315S3B-A12B-001-A/Barrett-Creeper-Mid-Top-Zip-Sneaker.jpg?img404=product-image-not-found&$productdetailprimary$",
            "href": "https://www.findmine.com/api/v1/images/637877",
            "image_id": 637877,
            "state": 2
          }
        ],
        "href": "https://www.findmine.com/api/v1/items/42562",
        "category_id": 25,
        "brand_name": "U.S.A",
        "store_id": 10,
        "price": 278.0,
        "brand_id": 3,
        "date_updated": "2016-08-17 19:22:26",
        "team_id": 1,
        "date_created": "2016-08-09 17:47:02",
        "set_id": 2065,
        "colors": [
          {
            "color_id": 297774,
            "image_id": 637877,
            "href": "https://www.findmine.com/api/v1/colors/297774"
          },
          {
            "color_id": 297778,
            "image_id": 637877,
            "href": "https://www.findmine.com/api/v1/colors/297778"
          },
          {
            "color_id": 297779,
            "image_id": 637877,
            "href": "https://www.findmine.com/api/v1/colors/297779"
          },
          {
            "color_id": 297780,
            "image_id": 637877,
            "href": "https://www.findmine.com/api/v1/colors/297780"
          }
        ],
        "item_id": 42562,
        "stock": 1,
        "sport_id": 1,
        "store_name": "John Varvatos",
        "season_id": 4
      }
    ],
    "date_updated": "2016-12-16 15:19:19",
    "published": 1,
    "store_ids": "[10]",
    "href": "https://www.findmine.com/api/v1/sets/2065"
  },
  {
    "item_ids": "[67855,67639,42144,61079,67784]",
    "occasion_name": "Default Occasion",
    "brand_ids": "[2]",
    "flagged": 0,
    "user_id": 4,
    "style_id": 1,
    "date_created": "2016-09-20 20:11:07",
    "set_id": 1515,
    "occasion_id": 1,
    "style_name": "Default Style",
    "set_items": [
      {
        "item_url": "https://www.johnvarvatos.com/product?color=609&utm_source=FINDMINE&utm_campaign=JV&pid=Y2088S3-BEF6&utm_medium=PDP",
        "season_name": "F16",
        "pid": "Y2088S3-BEF6",
        "flagged": 0,
        "user_id": 4,
        "title": "Linen Wool Crewneck Sweater",
        "sport_name": "Default Sport",
        "team_name": "Default Team",
        "category_name": "Pullover",
        "images": [
          {
            "item_id": 67784,
            "img_url": "https://i1.adis.ws/i/johnvarvatos/Y2088S3-BEF6-609-A/Linen-Wool-Crewneck-Sweater.jpg?img404=product-image-not-found&$productdetailprimary$",
            "href": "https://www.findmine.com/api/v1/images/748517",
            "image_id": 748517,
            "state": 2
          }
        ],
        "href": "https://www.findmine.com/api/v1/items/67784",
        "category_id": 41,
        "brand_name": "Collection",
        "store_id": 10,
        "price": 298.0,
        "brand_id": 2,
        "date_updated": "2016-09-20 21:02:40",
        "team_id": 1,
        "date_created": "2016-09-20 10:35:27",
        "set_id": 1515,
        "colors": [
          {
            "color_id": 367967,
            "image_id": 748517,
            "href": "https://www.findmine.com/api/v1/colors/367967"
          }
        ],
        "item_id": 67784,
        "stock": 1,
        "sport_id": 1,
        "store_name": "John Varvatos",
        "season_id": 4
      },
      {
        "item_url": "https://www.johnvarvatos.com/product?utm_medium=PDP&color=001&utm_source=FINDMINE&utm_campaign=JV&pid=B055S3B-Y985",
        "season_name": "W16",
        "pid": "B055S3B-Y985",
        "flagged": 0,
        "user_id": 4,
        "title": "Leather Nail Head Belt",
        "sport_name": "Default Sport",
        "team_name": "Default Team",
        "category_name": "Belt",
        "images": [
          {
            "item_id": 67639,
            "img_url": "https://i1.adis.ws/i/johnvarvatos/B055S3B-Y985-001-A/Leather-Nail-Head-Belt.jpg?img404=product-image-not-found&$productdetailprimary$",
            "href": "https://www.findmine.com/api/v1/images/746969",
            "image_id": 746969,
            "state": 2
          }
        ],
        "href": "https://www.findmine.com/api/v1/items/67639",
        "category_id": 17,
        "brand_name": "Collection",
        "store_id": 10,
        "price": 138.0,
        "brand_id": 2,
        "date_updated": "2016-09-20 20:10:01",
        "team_id": 1,
        "date_created": "2016-09-20 01:49:50",
        "set_id": 1515,
        "colors": [
          {
            "color_id": 366947,
            "image_id": 746969,
            "href": "https://www.findmine.com/api/v1/colors/366947"
          },
          {
            "color_id": 366948,
            "image_id": 746969,
            "href": "https://www.findmine.com/api/v1/colors/366948"
          },
          {
            "color_id": 366949,
            "image_id": 746969,
            "href": "https://www.findmine.com/api/v1/colors/366949"
          },
          {
            "color_id": 366951,
            "image_id": 746969,
            "href": "https://www.findmine.com/api/v1/colors/366951"
          }
        ],
        "item_id": 67639,
        "stock": 1,
        "sport_id": 1,
        "store_name": "John Varvatos",
        "season_id": 2
      },
      {
        "item_url": "https://www.johnvarvatos.com/product?pid=JVD835-BEBH&utm_medium=PDP&color=602&utm_source=FINDMINE&utm_campaign=JV",
        "season_name": "W16",
        "pid": "JVD835-BEBH",
        "flagged": 0,
        "user_id": 4,
        "title": "Austin Stripe Dress Pant",
        "sport_name": "Default Sport",
        "team_name": "Default Team",
        "category_name": "Slacks",
        "images": [
          {
            "item_id": 67855,
            "img_url": "https://i1.adis.ws/i/johnvarvatos/JVD835-BEBH-602-A/Austin-Stripe-Dress-Pant.jpg?img404=product-image-not-found&$productdetailprimary$",
            "href": "https://www.findmine.com/api/v1/images/749186",
            "image_id": 749186,
            "state": 2
          }
        ],
        "href": "https://www.findmine.com/api/v1/items/67855",
        "category_id": 40,
        "brand_name": "Collection",
        "store_id": 10,
        "price": 345.0,
        "brand_id": 2,
        "date_updated": "2016-09-20 20:09:10",
        "team_id": 1,
        "date_created": "2016-09-20 13:36:33",
        "set_id": 1515,
        "colors": [
          {
            "color_id": 368458,
            "image_id": 749186,
            "href": "https://www.findmine.com/api/v1/colors/368458"
          },
          {
            "color_id": 368461,
            "image_id": 749186,
            "href": "https://www.findmine.com/api/v1/colors/368461"
          },
          {
            "color_id": 368462,
            "image_id": 749186,
            "href": "https://www.findmine.com/api/v1/colors/368462"
          }
        ],
        "item_id": 67855,
        "stock": 1,
        "sport_id": 1,
        "store_name": "John Varvatos",
        "season_id": 2
      },
      {
        "item_url": "https://www.johnvarvatos.com/product?utm_campaign=JV&pid=F2468S3-Y1084&utm_medium=PDP&color=001&utm_source=FINDMINE",
        "season_name": "F16",
        "pid": "F2468S3-Y1084",
        "flagged": 0,
        "user_id": 4,
        "title": "Cooper Waterproof Moto Boot",
        "sport_name": "Default Sport",
        "team_name": "Default Team",
        "category_name": "Boots",
        "images": [
          {
            "item_id": 42144,
            "img_url": "https://i1.adis.ws/i/johnvarvatos/F2468S3-Y1084-001-A/Cooper-Waterproof-Moto-Boot.jpg?img404=product-image-not-found&$productdetailprimary$",
            "href": "https://www.findmine.com/api/v1/images/636858",
            "image_id": 636858,
            "state": 2
          }
        ],
        "href": "https://www.findmine.com/api/v1/items/42144",
        "category_id": 109,
        "brand_name": "Collection",
        "store_id": 10,
        "price": 798.0,
        "brand_id": 2,
        "date_updated": "2016-08-18 03:52:33",
        "team_id": 1,
        "date_created": "2016-08-09 15:25:42",
        "set_id": 1515,
        "colors": [
          {
            "color_id": 294848,
            "image_id": 636858,
            "href": "https://www.findmine.com/api/v1/colors/294848"
          },
          {
            "color_id": 294850,
            "image_id": 636858,
            "href": "https://www.findmine.com/api/v1/colors/294850"
          },
          {
            "color_id": 294852,
            "image_id": 636858,
            "href": "https://www.findmine.com/api/v1/colors/294852"
          }
        ],
        "item_id": 42144,
        "stock": 1,
        "sport_id": 1,
        "store_name": "John Varvatos",
        "season_id": 4
      }
    ],
    "date_updated": "2016-10-12 16:41:58",
    "published": 1,
    "store_ids": "[10]",
    "href": "https://www.findmine.com/api/v1/sets/1515"
  }
]
```

##### JSON Body Parameters
> All passed parameters will be processed by the FINDMINE system and those parameters that are not specified by explicit numerical representation will be ingested using machine learning and mapping technologies to transform them into explicit IDs

- `url` [ *str* ] **required** - url of the product page that contains the identifiable item.
- `html` [ *str* ] - raw and rendered version of the html code of the product page.
- `words` - TODO
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
- **200** - item was found on the system.
- **201** - item was not found but was scraped and added to the system with the help of the provided JSON encoded body parameters.
- **400** - something is wrong with the request. Either required headers or parameters are missing. Malformed Request.
- **403** - credentials were not provided with the request and the user is unauthorized to perform the operation.
- **500** - internal server error. Something went wrong and you should email support@findmine.com

## Generating Recommended Sets
```http
GET /api/v1/match/sets/<item_id:int>
```

blah blah blah some explanations

> notes to pay attention to.

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
Location: https://www.findmine.com/api/v1/items/<item_id:int>
```

##### Query Parameters
- `limit` [ *int* ] - the limit parameter is an integer value that can be used to limit the number of items returned. If limit is not specified, then the default value is 100.
- `fields` [ *str* ] - comma separated fields indicates which of the fields associated with an item or set of items you would like returned. If no fields specified, the following fields will be returned by default: `set_id`,`item_ids`,`store_ids`,`brand_ids`,`user_id`,`published`,`flagged`,`style_id`,`style_name`,`occasion_id`,`occasion_name`,`date_created`,`date_updated`,`set_items` 
- `branded` [ *int* ] - if the branded parameter is passed, then it means that only sets with items of the same brand as the item passed in the request are returned. 
- `teamed` [ *int* ] - if the teamed parameter is passed, then only sets with items of the same team as the item passed in the request are returned.
- `sported` [ *int* ] - if the sported parameter is passed, then only sets with items of the same sport as the item passed in the request are returned.

> For `branded`,`teamed`,`sported` parameters the defaults are set per client's specification. This means that if those parameters are not provided the defaults kick in based on predefined information. These are for the purpose of overriding.

##### Return Codes
- **200** - recommendation was generated successfully.
- **404** - the system could not generate a recommendation for the sample item.
- **500** - internal server error has happened. Almost exclusively this means that something with the sample item is wrong. There is nothing that can be done from the user side and support@findmine.com should be contacted.
- **503** - not all of the functionalities of this endpoints are implemented. If you encounter this response just know you are messing around with something we thought of but didn't have time to implement. If you see this, give us a call, we are hiring.
