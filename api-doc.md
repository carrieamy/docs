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
Location: https://www.findmine.com/api/v1/items/<item_id:int>
```

##### JSON Body Parameters
> All passed parameters will be processed by the FINDMINE system and those parameters that are not specified by explicit numerical representation will be ingested using machine learning and mapping technologies to transform them into explicit IDs

- `url` [ *str* ] **required** - url of the product page that contains the identifiable item.
- `html` [ *str* ] - raw and rendered version of the html code of the product page.
- `words` - TODO
- `images` [ *list[dict]* ] - list of objects containing image information of the sample product.
- `sport` [ *int* | *str* ] - either an exact number representing the sport_id on the FINDMINE system or a string definition of the particular sport of the product.
- `category` [ *int* | *str* ] - either an exact number representing the category_id of the product or a string definition of the category for the product. For the string definition, this may include bread crumbs, category name, etc.
- `title` [*str*] - the title of the sample product.
- `description` [*str*] - description of the product. This can be any combination of words. The more the better. Our system will process out information from this and will help recognize the item better overall.
- `price` [*int* | *float*] - a numerical representation of the price for the product.
- `pid` [*str*] - (Product ID "pid") can be any string that represents a tracking id of the item at question. The purpose of this is to help you track one's products using your own tracking enumeration. FINDMINE will provide a unique id for a processed id in the form of `item_id` besides this value.
- `brand` [*int* | *str*] - either a number representing the explicit `brand_id` as provided by the FINDMINE system or a string definition of the brand name.
- `season` [*int* | *str*] - either the explicit `season_id` as recorded by the FINDMINE system or a string definition of the season name.
- `details` [*dict*] - extra storage information for any additional parameters that do not have direct access via the strucutres described above.

> `pid` does not have to be unique, however, if it is not when searching for those PID's the search result will provide multiple results.

##### Return Codes
- **200** - Item was found on the system.
- **201** - Item was not found but was scraped and added to the system with the help of the provided JSON encoded body parameters.
- **400** - Something is wrong with the request. Either required headers or parameters are missing. Malformed Request.
- **403** - Credentials were not provided with the request and the user is unauthorized to perform the operation.
- **500** - Internal server error. Something went wrong and you should email support@findmine.com

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

- `limit` - The limit parameter is an integer value that can be used to limit the number of items returned. If limit is not specified, then the default value is 100.

- `fields` - Fields indicates which of the fields associated with an item or set of items you would like returned.

  If you don't specify any fields, the following fields will be returned by default:

  > set_id, item_ids, store_ids, brand_ids, user_id, published, flagged, style_id, style_name, occasion_id, occasion_name, date_created, date_updated, set_items

- `store_ids` - a list of store id values that items in the set can belong to. This makes it possible to generate cross-store outfits. // Not live functionality. 

- `published` - the published parameter is an integer value that indicates whether the returned sets should be published sets, or live on the client site (1) or unpublished sets, prevented from appearing on the client site (0). If the published parameter is not specified, the default value is published (1).

- `branded` - if the branded parameter is passed, then it means that only sets with items of the same brand as the item passed in the request are returned. 

- `teamed` - if the teamed parameter is passed, then only sets with items of the same team as the item passed in the request are returned. (Default)

- `sported` - If the sported parameter is passed, then only sets with items of the same sport as the item passed in the request are returned. (Default)


** potentially we could have seasoned too.. its in the query, but not in match_sets.py

** and flagged?!

##### JSON Body Parameters

An array of JSON objects, each representing a set.

- `brand_ids` - The possible set of brand ids for the items in the returned set. If branded was passed as a parameter, then `brand_ids` will simply be the `brand_id` of the item. If branded was not specified, then the `brand_ids` will be all the brands associated with the store.
- `date_created` - The datetime that the set was created
- `date_updated` - The datetime that the set was last updated
- `flagged` - a `0` or `1` integer indicating whether the set was flagged for review. 
- `href` - blah blah blah
- `item_ids` - blah blah blah
- `occasion_id` - blah blah blah
- `occasion_name` - blah blah blah
- `published` - blah blah blah
- `set_id` - blah blah blah
- `set_items` - an array of JSON objects, each representing an item in the set
  - `brand_id` - blah blah blah
  - `brand_name` - blah 
  - `category_id`
  - `category_name`
  - `colors` - an array of JSON objects, each representing the colors in an item in the set
    - `color_id`
    - `href`
    - `image_id`
  - `date_created`
  - `date_updated`
  - `flagged`
  - `href`
  - `images` - an array of JSON objects, each representing the image of an item in the set
    - `href`
    - `image_id`
    - `img_url`
    - `item_id`
    - `state`
  - `item_id`
  - `item_url`
  - `pid`
  - `price`
  - `season_id`
  - `season_name`
  - `set_id`
  - `sport_id`
  - `sport_name`
  - `stock`
  - `store_id`
  - `store_name`
  - `team_id`
  - `team_name`
  - `title`
  - `user_id`

##### Return Codes

- **200** - Item 
