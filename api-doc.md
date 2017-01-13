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
	"url": "http://www.sample.com/{route/to/canonical/product/page}",
  	"html": "<html>{raw html of the product page that is loaded}</html>",
  	"images": [
    	{
      		"id_tag": null,
      		"class_tag": null,
      		"xpath": "/html/body/div[1]/div[4]/div/div[2]/segment[1]/div[1]/div[1]/div[1]/div/div[1]/div/div/ul/li[1]/img",
      		"height": 54,
      		"width": 54,
      		"magnitude": 76.36753236814714,
      		"theta": 0.7853981633974483,
      		"img_url": "http://demandware.edgesuite.net/sits_pod20-adidas/dw/image/v2/aaqx_prd/on/demandware.static/-/Sites-adidas-products/en_US/dw16bf7c60/zoom/S97153_21_model.jpg?sw=60&sfrm=jpg",
      		"tag_idx": 1958,
      		"top": 137.0000061035156,
      		"state": 0
    	}
  	]
}
```



##### Sample Response

```http
HTTP/1.1 200 OK
Content-Type: application/json
Location: https://www.findmine.com/api/v1/items/{item_id:int}
```



##### JSON Body Parameters
- `url` - Url of the product page that contains the identifiable item.
- `html` - Raw and rendered version of the html code of the product page.
- `words` - TODO
- `images` - TODO
- `sport` - TODO
- `category` - TODO
- `title` - TODO
- `description` - TODO
- `price` - TODO
- `pid` - TODO
- `uni` - TODO
- `stock` - TODO
- `brand` - TODO
- `season` - TODO
- `details` - TODO



##### Return Codes

- **200** - Item was found on the system.

- **201** - Item was not found but was scraped and added to the system with the help of the provided JSON encoded body parameters.

- **400** - Something is wrong with the request. Either required headers or parameters are missing. Malformed Request.

- **403** - Credentials were not provided with the request and the user is unauthorized to perform the operation.

- **500** - Internal server error. Something went wrong and you should email support@findmine.com

  ​

## Generating Recommended Sets

```http
GET /api/v1/match/sets/{item_id:int}
```

blah blah blah some explanations

> notes to pay attention to.



##### Sample Request

```http
GET https://www.findmine.com/api/v1/match/sets/{item_id:int} HTTP/1.1
Referer: http://www.sample.com/{route/to/canonical/product/page}
Accept: */*, application/json
```



##### Sample Response

```http
HTTP/1.1 200 OK
Content-Type: application/json
Location: https://www.findmine.com/api/v1/items/{item_id:int}
```



##### Query Parameters

- `limit` - blah blah blah
- `fields` - blah blah blah
- `store_ids` - blah blah blah
- `published` - blah blah blah
- `branded` - blah blah blah
- `teamed` - blah blah blah
- `sported` - blah blah blah



##### Return Codes

- **200** - Item wa
- **201** - Item was n
- **400** - Something is w
- **403** - Credentials w
- **500** - Internal serv
