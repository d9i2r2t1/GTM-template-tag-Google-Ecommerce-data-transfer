# Custom Template for Google Tag Manager: Google Enhanced Ecommerce data transfer to remarketing pixels

This tag gets data from [Google Enhanced Ecommerce configured via dataLayer](https://developers.google.com/tag-manager/enhanced-ecommerce) and sends it to dynamic remarketing pixels:

* [VK](https://vk.com)
* [Facebook](https://facebook.com)
* [myTarget](https://target.my.com)

This tag uses Google Enhanced Ecommerce **configured via dataLayer** to get event and product data, so you need it to be on your site, otherwise this tag will not work.

This tag intercepts dataLayer.push, so it should be fired only via **All Pages** or **DOM Ready** triggers.

You can run several copies of the tag on the page, for example, one for VK, the second for Facebook, etc.

The tag injects [this script](https://github.com/oleg-dirtrider/oleg-dirtrider.github.io/blob/master/ga_enhanced_ecom_data_transfer_to_remarketing_pixels.js) to the site for its work.

If your security policy does not allow loading third-party scripts, you can install this data transfer script as a [GTM Custom HTML tag](https://github.com/oleg-dirtrider/gtm_tag-google_ecommerce_data_transfer/blob/master/gtm_tag-google_ecommerce_data_transfer.js). In this case, no third-party scripts will be loaded to your site. To do this, fill the settings object in the code with your data and set All Pages trigger for this GTM Custom HTML tag.


## Events and event data structure

Pixels events and data structure of each event are compiled in accordance with the official documentation of each pixel.

The tag doesn't add anything from itself to the event or product data, it takes only what is in Google Enhanced Ecommerce.
If Google Enhanced Ecommerce is missing something, it will be absent in dynamic remarketing pixels as well.

Description of events and data structures:

* [VK events](#vk_pixel)
* [Facebook events](#fb_pixel)
* [myTarget events](#mt_pixel)

### <a name="vk_pixel">Available events for VK pixel</a>

* [view_home](#view_home)
* [view_category](#view_category)
* [view_search](#view_search)
* [view_other](#view_other)
* [view_product](#view_product)
* [add_to_cart](#add_to_cart)
* [remove_from_cart](#remove_from_cart)
* [init_checkout](#init_checkout)
* [purchase](#purchase)

#### <a name="view_home">view_home</a>

Website homepage view.

Event data structure:

```js
{
    priсeListID, // Price list ID
    name, // Event name
    {
        [
            {
                id, // Product ID
                group_id, // Product brandname
                price // Product price
            },
            …
        ],
        category_ids // Product categories, for example: 'phones,tablets,headphones'
    }
}
```

#### <a name="view_category">view_category</a>

Website catalog page view.

Event data structure:

```js
{
    priсeListID, // Price list ID
    name, // Event name
    {
        [
            {
                id, // Product ID
                group_id, // Product brandname
                price // Product price
            },
            …
        ],
        category_ids // Product categories, for example: 'phones,tablets,headphones'
    }
}
```

#### <a name="view_search">view_search</a>

Page with site search results view. 

Event data structure:

```js
{
    priсeListID, // Price list ID
    name, // Event name
    {
        [
            {
                id, // Product ID
                group_id, // Product brandname
                price // Product price
            },
            …
        ],
        category_ids, // Product categories, for example: 'phones,tablets,headphones'
        search_string // Search query
    }
}
```

#### <a name="view_other">view_other</a>

Other page view.

Event data structure:

```js
{
    priсeListID, // Price list ID
    name, // Event name
    {
        [
            {
                id, // Product ID
                group_id, // Product brandname
                price // Product price
            },
            …
        ],
        category_ids // Product categories, for example: 'phones,tablets,headphones'
    }
}
```

#### <a name="view_product">view_product</a>

Product detail view.

Event data structure:

```js
{
    priсeListID, // Price list ID
    name, // Event name
    {
        [
            {
                id, // Product ID
                group_id, // Product brandname
                price // Product price
            },
            …
        ],
        category_ids, // Product categories, for example: 'phones,tablets,headphones'
        currency_code, // Currency code
        total_price // Total price
    }
}
```

#### <a name="add_to_cart">add_to_cart</a>

Add product to cart.

Event data structure:

```js
{
    priсeListID, // Price list ID
    name, // Event name
    {
        [
            {
                id, // Product ID
                group_id, // Product brandname
                price // Product price
            },
            …
        ],
        category_ids, // Product categories, for example: 'phones,tablets,headphones'
        currency_code, // Currency code
        total_price // Total price
    }
}
```

#### <a name="remove_from_cart">remove_from_cart</a>

Remove product from cart.

Event data structure:

```js
{
    priсeListID, // Price list ID
    name, // Event name
    {
        [
            {
                id, // Product ID
                group_id, // Product brandname
                price // Product price
            },
            …
        ],
        category_ids, // Product categories, for example: 'phones,tablets,headphones'
        currency_code, // Currency code
        total_price // Total price
    }
}
```

#### <a name="init_checkout">init_checkout</a>

Checkout process start.

Event data structure:

```js
{
    priсeListID, // Price list ID
    name, // Event name
    {
        [
            {
                id, // Product ID
                group_id, // Product brandname
                price // Product price
            },
            …
        ],
        category_ids, // Product categories, for example: 'phones,tablets,headphones'
        currency_code, // Currency code
        total_price // Total price
    }
}
```

#### <a name="purchase">purchase</a>

Product purchase.

Event data structure:

```js
{
    priсeListID, // Price list ID
    name, // Event name
    {
        [
            {
                id, // Product ID
                group_id, // Product brandname
                price // Product price
            },
            …
        ],
        category_ids, // Product categories, for example: 'phones,tablets,headphones'
        currency_code, // Currency code
        total_price // Total price
    }
}
```

### <a name="fb_pixel">Available events for Facebook pixel</a>

* [ViewHome](#ViewHome)
* [ViewCategory](#ViewCategory)
* [Search](#Search)
* [ViewOther](#ViewOther)
* [ViewContent](#ViewContent)
* [AddToCart](#AddToCart)
* [RemoveFromCart](#RemoveFromCart)
* [InitiateCheckout](#InitiateCheckout)
* [Purchase](#Purchase_fb)

#### <a name="ViewHome">ViewHome</a>

Website homepage view.

Event data structure:

```js
{
    'trackCustom', // Method of data send
    name, // Event name
    {
        [
            {
                id, // Product ID
                quantity, // Product quantity
                item_price // Product price
            },
            …
        ],
        content_name, // Product names, for example: 'Apple iPhone X Black,Samsung Galaxy A80 128Gb'
        content_type // Product type
    }
}
```

#### <a name="ViewCategory">ViewCategory</a>

Website catalog page view.

Event data structure:

```js
{
    'trackCustom', // Method of data send
    name, // Event name
    {
        [
            {
                id, // Product ID
                quantity, // Product quantity
                item_price // Product price
            },
            …
        ],
        content_name, // Product names, for example: 'Apple iPhone X Black,Samsung Galaxy A80 128Gb'
        content_type // Product type
    }
}
```

#### <a name="Search">Search</a>

Page with site search results view. 

Event data structure:

```js
{
    'track', // Method of data send
    name, // Event name
    {
        [
            {
                id, // Product ID
                quantity, // Product quantity
                item_price // Product price
            },
            …
        ],
        content_category, // Product categories, for example: 'phones,tablets,headphones'
        search_string // Search query
    }
}
```

#### <a name="ViewOther">ViewOther</a>

Other page view.

Event data structure:

```js
{
    'trackCustom', // Method of data send
    name, // Event name
    {
        [
            {
                id, // Product ID
                quantity, // Product quantity
                item_price // Product price
            },
            …
        ],
        content_name, // Product names, for example: 'Apple iPhone X Black,Samsung Galaxy A80 128Gb'
        content_type // Product type
    }
}
```

#### <a name="ViewContent">ViewContent</a>

Product detail view.

Event data structure:

```js
{
    'track', // Method of data send
    name, // Event name
    {
        [
            {
                id, // Product ID
                quantity, // Product quantity
                item_price // Product price
            },
            …
        ],
        content_name, // Product names, for example: 'Apple iPhone X Black,Samsung Galaxy A80 128Gb'
        content_type, // Product type
        currency, // Currency code
        value // Total price 
    }
}
```

#### <a name="AddToCart">AddToCart</a>

Add product to cart.

Event data structure:

```js
{
    'track', // Method of data send
    name, // Event name
    {
        [
            {
                id, // Product ID
                quantity, // Product quantity
                item_price // Product price
            },
            …
        ],
        content_name, // Product names, for example: 'Apple iPhone X Black,Samsung Galaxy A80 128Gb'
        content_type, // Product type
        currency, // Currency code
        value // Total price 
    }
}
```

#### <a name="RemoveFromCart">RemoveFromCart</a>

Remove product from cart.

Event data structure:

```js
{
    'trackCustom', // Method of data send
    name, // Event name
    {
        [
            {
                id, // Product ID
                quantity, // Product quantity
                item_price // Product price
            },
            …
        ],
        content_name, // Product names, for example: 'Apple iPhone X Black,Samsung Galaxy A80 128Gb'
        content_type, // Product type
        currency, // Currency code
        value // Total price 
    }
}
```

#### <a name="InitiateCheckout">InitiateCheckout</a>

Checkout process start.

Event data structure:

```js
{
    'track', // Method of data send
    name, // Event name
    {
        [
            {
                id, // Product ID
                quantity, // Product quantity
                item_price // Product price
            },
            …
        ],
        content_category, // Product categories, for example: 'phones,tablets,headphones'
        num_items, // Number of product items
        currency, // Currency code
        value // Total price 
    }
}
```

#### <a name="Purchase_fb">Purchase</a>

Product purchase.

Event data structure:

```js
{
    'track', // Method of data send
    name, // Event name
    {
        [
            {
                id, // Product ID
                quantity, // Product quantity
                item_price // Product price
            },
            …
        ],
        content_name, // Product names, for example: 'Apple iPhone X Black,Samsung Galaxy A80 128Gb'
        content_type, // Product type
        currency, // Currency code
        value, // Total price 
        num_items // Number of product items
    }
}
```

### <a name="mt_pixel">Available events for myTarget counter</a>

* [home](#home)
* [category](#category)
* [searchresults](#searchresults)
* [other](#other)
* [product](#product)
* [cart](#cart)
* [purchase](#purchase_mt)

#### <a name="home">home</a>

Website homepage view.

Event data structure:

```js
{
    id, // Counter ID
    type, // Event type
    [productid, …], // Product ID(s)
    pagetype, // Event name
    list // Feed ID
}
```

#### <a name="category">category</a>

Website catalog page view.

Event data structure:

```js
{
    id, // Counter ID
    type, // Event type
    [productid, …], // Product ID(s)
    pagetype, // Event name
    list // Feed ID
}
```

#### <a name="searchresults">searchresults</a>

Page with site search results view. 

Event data structure:

```js
{
    id, // Counter ID
    type, // Event type
    [productid, …], // Product ID(s)
    pagetype, // Event name
    list // Feed ID
}
```

#### <a name="other">other</a>

Other page view.

Event data structure:

```js
{
    id, // Counter ID
    type, // Event type
    [productid, …], // Product ID(s)
    pagetype, // Event name
    list // Feed ID
}
```

#### <a name="product">product</a>

Product detail view.

Event data structure:

```js
{
    id, // Counter ID
    type, // Event type
    [productid, …], // Product ID(s)
    pagetype, // Event name
    list, // Feed ID
    totalvalue // Total price
}
```

#### <a name="cart">cart</a>

Add product to cart.

Event data structure:

```js
{
    id, // Counter ID
    type, // Event type
    [productid, …], // Product ID(s)
    pagetype, // Event name
    list, // Feed ID
    totalvalue // Total price
}
```

#### <a name="purchase_mt">purchase</a>

Product purchase.

Event data structure:

```js
{
    id, // Counter ID
    type, // Event type
    [productid, …], // Product ID(s)
    pagetype, // Event name
    list, // Feed ID
    totalvalue // Total price
}
```
