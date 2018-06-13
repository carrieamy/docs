# FINDMINE Feed Documentation

To optimize FINDMINE performance, we would like to receive in-stock product information down to sku at the color level.

These data points do not need to be in separate field FINDMINE will just need a way to grab this data.

### Data points we will need per product

#### Required data:

##### Product Id down to color 
We do not want each size of an item in the feed, this ID will be the unique identifier in our system that will be used to call the FM API or FM JS module

##### Title
Product title

##### Price
Product price

##### Availability
In Stock or Out of Stock

##### Image
Product image url

##### URL
URL for the product detail page

##### Category Id - 
Should map to site categories (breadcrumbs) as opposed to generic categories like Google Categories

##### Note: 
The fields in your feed do not need to be named exactly as indicated. We can map your values to ours. For example, your feed may include Image URL instead of Image, etc.

#### Additional data based on your business rules:

Additional data we can glean from the feed. This data does not explicitly need to be separate fields, we just need some way to  these heuristics. We’ve included examples of how some of our other clients have provided these data points.

##### Sale price or discount 
ex: could be indicated by price ending in .99, marked as a separate field or discount field

##### Size type 
Big & tall, petite, plus - ex: can be pulled from product title, or URL

##### Team 
ex: can be pulled from product title

##### Sport 
ex: can be pulled from product title

##### Gender 
ex: can be pulled from product title

##### Brand 
ex: can be pulled from product title

#### Description

#### Sizes 
ex: s,m,l - 0,2,4,6

#### Color Name 
ex: teal, green camo

#### Materials 
ex: silk, linen

#### Pattern 
ex: floral, animal, gingham, etc.

#### Style 
ex: edgy, formal, casual, athletic

#### Occasion
ex: prom, night out, weekend, festival

#### Example feed contents (example in XML but format is not required):

```
<product id="66926">
	<colors>
		<color>P66926_C106</color>
		<color>P66926_C7313</color>
	</colors>
            <title> Cami With Criss Cross Neckline </title>
<image>https://www.yourbrand.com/is/image/ProdATG/66926_C106</image>                <producturl>http://link.mercent.com/redirect.ashx?mr:merchantID=merchant1&amp;mr:trackingCode=5A02183A-550C-E811-80F7-0050569428E8&amp;mr:targetUrl=https://www.yourbrand.com/product/cami-with-criss-cross-neckline-/66926</producturl>
            <description>imported 97% cotton 3% spandex machine wash Fabric and care: imported 97% cotton 3% spandex machine wash</description>
            <price>18.00</price>
            <sale_price>10.00</sale_price>
            <discount>0.00</discount>
            <instock>TRUE</instock>
            <categoryid>Knit Basics</categoryid>
            <gender>Womens</gender>
            <size_type>Plus</size_type>
            <team>Houston Rockets</team>
            <sport>Basketball</sport>
            <brand>Your Brand</brand>
</product>
```

