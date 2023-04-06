# Images

An [API Key](api-key.md) is <mark style="color:red;">not</mark> required for MOST endpoints of this service. See [Shared Responses](shared-responses/) for common error responses.

{% swagger method="get" path="/online" baseUrl="https://v2.yiff.rest" summary="Online Check" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-response status="200: OK" description="Success" %}
```javascript
{
  "success": true,
  "uptime": 0
}
```
{% endswagger-response %}
{% endswagger %}

{% swagger method="get" path="/categories" baseUrl="https://v2.yiff.rest" summary="List Categories" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-response status="200: OK" description="Success" %}
```javascript
{
  "success": true,
  "data": {
    "enabled": [
      {
        "name": "Animals > Birb",
        "db": "animals.birb"
      }
      // (...)
    ],
    "disabled": [
      {
        "name": "Animals > Fox",
        "db": "animals.fox",
        "_comment": "Category has never had any content."
      }
      // (...)
    ]
  }
}
```
{% endswagger-response %}
{% endswagger %}

{% swagger method="get" path="/categories/:db" baseUrl="https://v2.yiff.rest" summary="Get Information About A Category" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="path" name="db" type="String" required="true" %}
The "db" representation of the category (see  

[GET /categories](./#list-categories)

)
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="Success" %}
```javascript
{
  "success": true,
  "data": {
    "name": "Animals > Birb",
    "db": "animals.birb",
    "dir": "/app/public/V2/animals/birb",
    // _comment can also be present
    "disabled": false,
    "files": {
      "exists": true,
      "list": {
        "total": 65,
        "size": {
          "total": 107429688,
          "totalM": 102.453, // Mebibytes
          "average": 1652764.431,
          "averageM": 1.576 // Mebibytes
        },
        "types": {
        // mime types - none guaranteed
          "image/jpeg": 22,
          "image/gif": 6,
          "image/png": 37
        }
      }
    }
  }
}
```
{% endswagger-response %}

{% swagger-response status="404: Not Found" description="Not Found" %}
```javascript
{
  "success": false,
  "error": {
    "message": "Category not found in list."
  },
  "code": 1030
}
```
{% endswagger-response %}
{% endswagger %}

{% swagger method="get" path="/images/:id.json" baseUrl="https://v2.yiff.rest" summary="Get Image" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="path" name="id" type="String" required="true" %}
The ID of the image.
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="Success" %}
```javascript
{
  "success": true,
  "data": {
    "artists": [].
    "sources": [],
    "width": 0,
    "height": 0,
    "url": "https://v2.yiff.media/{id}.{ext}",
    "yiffMediaURL": "https://v2.yiff.media/{id}.{ext}",
    "type": "{mime}",
    "name": "{name}.{ext}",
    "id": "{id}",
    "ext": "{ext}",
    "size": 0,
    "reportURL": null,
    "shortURL": "https://yiff.rocks/{id}",
    "category": "" // db format
  }
}
```
{% endswagger-response %}

{% swagger-response status="404: Not Found" description="Not Found" %}
```javascript
{
  "success": false,
  "error": "No image was found with that id.",
  "code": 1040
}
```
{% endswagger-response %}
{% endswagger %}

{% swagger method="get" path="/:category" baseUrl="https://v2.yiff.rest" summary="Get Random Image" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="path" name="category" type="String" required="true" %}
The category, see 

[GET /categories](./#list-categories)

 (

`db`

, replace periods with forward slashes)
{% endswagger-parameter %}

{% swagger-parameter in="query" name="amount" type="Number" required="false" %}
The amount of images to request, between 1-5.
{% endswagger-parameter %}

{% swagger-parameter in="query" name="notes" type="String" required="false" %}
If notes should be hidden. Use the literal string "disabled".
{% endswagger-parameter %}

{% swagger-parameter in="query" name="sizeLimit" type="Number" %}
The maximum size of image to get, in powers of 2.  Prefixes such as KB/MB can be used.
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="Success" %}
```javascript
// Notes:
// 0: null
// 1: This api host (api.furry.bot) is being removed on June 9th, 2021. Please migrate to https://yiff.rest.
// 2: We're moving to using subdomains for api versioning! e.g. https://v2.yiff.rest. They have the same functionality, just without the version in the path. The /V2 route will not be removed, but v3 and forward will only use the subdomain.
// 3: Hey, we see you aren't using an api key. They're free! To get one, join our support server (https://yiff.rest/support), and run the command "/apikey", you'll see how to use it there.
// 4: WARNING! This list is STATIC, it can be inaccurate! We recommended parsing the dot notation in https://v2.yiff.rest/categories instead of this!
// 5: Since images are getting bigger, we're adding a size limit parameter. Add ?sizeLimit=<size> to limit the size of images we provide you. We process sizes in powers of 2, not 10.
// 6: You can now hide these notes by setting the notes parameter to disabled. (ex: ?notes=disabled)
{
  "success": true",
  "$schema": "https://schema.yiff.rest/V2.json",
  "notes": [
    {
      "id": 0,
      "content": ""
    }
  ],
  "images": [
    {
      "artists": [].
      "sources": [],
      "width": 0,
      "height": 0,
      "url": "https://v2.yiff.media/{id}.{ext}",
      "type": "{mime}",
      "name": "{name}.{ext}",
      "id": "{id}",
      "ext": "{ext}",
      "size": 0,
      "reportURL": null,
      "shortURL": "https://yiff.rocks/{id}"
    }
  ]
}
```
{% endswagger-response %}

{% swagger-response status="400: Bad Request" description="Limit <1" %}
```javascript
{
  "success": false,
  "error": "Amount must be 1 or more.",
  "code": 1051
}
```
{% endswagger-response %}

{% swagger-response status="400: Bad Request" description="Limit >5" %}
```javascript
{
  "success": false,
  "error": "Amount must be 5 or less.",
  "code": 1052
}
```
{% endswagger-response %}

{% swagger-response status="400: Bad Request" description="Invalid Response Type" %}
```javascript
{
  "success": false,
  "error": {
    "message": "invalid response type",
    "type": "client".
    "code": 1023
  }
}
```
{% endswagger-response %}

{% swagger-response status="400: Bad Request" description="No Results Found" %}
```javascript
{
  "success": false,
  "error": "No results were found. Try changing your search parameters.",
  "code": 1041
}
```
{% endswagger-response %}

{% swagger-response status="404: Not Found" description="Category Not Found" %}
```javascript
{
  "success": false,
  "error": "Category not found.",
  "code": 1030
}
```
{% endswagger-response %}

{% swagger-response status="500: Internal Server Error" description="Internal Server Error" %}
```javascript
{
  "success": false,
  "error": "There was an internal error while attempting to perform that action.",
  "code": 0
}
```
{% endswagger-response %}
{% endswagger %}

{% swagger method="post" path="/bulk" baseUrl="https://v2.yiff.rest" summary="Get Images Bulk" %}
{% swagger-description %}
Get an arbitrary amount of images across many categories. This endpoint requires an api key, and is restricted to developer approval.

By default, a maximum of 100 images total can be fetched in one request. You can request your limit to be raised by contacting a developer.
{% endswagger-description %}

{% swagger-parameter in="path" name="sizeLimit" %}
The maximum size of image to get, in powers of 2.  Prefixes such as KB/MB can be used.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="some.category" type="Number" required="true" %}
A map of category (in db format) to the amount of images. See 

[List Categories](./#list-categories)

 for the list of categories.
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="Success" %}
```javascript
// a map of category (in db format) to the requested imagess
{
  "some.category": [
    {
      "artists": [].
      "sources": [],
      "width": 0,
      "height": 0,
      "url": "https://v2.yiff.media/{id}.{ext}",
      "type": "{mime}",
      "name": "{name}.{ext}",
      "id": "{id}",
      "ext": "{ext}",
      "size": 0,
      "reportURL": null,
      "shortURL": "https://yiff.rocks/{id}"
    }
  ]
}
```
{% endswagger-response %}

{% swagger-response status="400: Bad Request" description="Invalid Body" %}
```javascript
{
  "success": false,
  "error": "Invalid body, or no categories specified.",
  "code": 1054
}
```
{% endswagger-response %}

{% swagger-response status="400: Bad Request" description="Invalid Category" %}
```javascript
{
  "success": false,
  "error": "Invalid category specified: invalid.category",
  "code": 1055
}
```
{% endswagger-response %}

{% swagger-response status="400: Bad Request" description=">Max Images Requested" %}
```javascript
{
  "success": false,
  "error": "Total amount of images requested is greater than {limit} ({total})",
  "code": 1056
}
```
{% endswagger-response %}
{% endswagger %}
