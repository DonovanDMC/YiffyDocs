# Thumbnails

An [API Key](api-key.md) <mark style="color:red;">is</mark> required for this service. See [Shared Responses](shared-responses/) for common error responses.

{% swagger method="get" path="/:id" baseUrl="https://thumbs.yiff.rest" summary="Get Thumbnail Information" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="path" name="id" type="String" required="true" %}
The MD5 or ID of an e621 post.
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="Success" %}
```javascript
{
  "success": true,
  "gifURL": "https://thumbsyiff.media/{md5}.gif", // or null
  "pngURL": "https://thumbs.yiff.media/{md5}.png" // or null
}
```
{% endswagger-response %}

{% swagger-response status="404: Not Found" description="Invalid Post ID" %}
```javascript
{
  "success": false,
  "error": "Invalid Post ID",
  "code": 1062
}
```
{% endswagger-response %}

{% swagger-response status="404: Not Found" description="Invalid MD5" %}
```javascript
{
  "success": false,
  "error": "Invalid MD5",
  "code": 1063
}
```
{% endswagger-response %}
{% endswagger %}

{% swagger method="put" path="/:id/:type" baseUrl="https://thumbs.yifff.rest" summary="Create Thumbnail" %}
{% swagger-description %}
A 202 Accepted will be returned in most circumstances. This is a non committal answer. You must fetch `checkURL` at the specified `checkAt` time. (you will be given a new check time if it's still processing)

If generation has already been started by someone else, a 202 Accepted will still be returned.

If a thumbnail has already been created, a 200 OK will be returned
{% endswagger-description %}

{% swagger-parameter in="path" name="id" type="String" required="true" %}
The MD5 or ID of an e621 post.
{% endswagger-parameter %}

{% swagger-parameter in="path" name="type" type="String" required="true" %}
`gif`

 or 

`png`
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="Already Created" %}
```javascript
{
  "success": true,
  "status": "done",
  "url": "https://.yiff.media/{md5}.{type}"
}
```
{% endswagger-response %}

{% swagger-response status="202: Accepted" description="Success" %}
```javascript
{
  "success": true,
  "status": "processing",
  "checkURL": "https://thumbs.yiff.rest/check/{gif}/{type}",
  "checkAt": 0, // (unix millis) the time at which you should fetch the above url
  "time": 0, // the milliseconds after which you should check the above url (see checkAt)
  "startedAt": 0, // (unix millis) the time at which processing started
}
```
{% endswagger-response %}

{% swagger-response status="404: Not Found" description="Invalid Post ID" %}
```javascript
{
  "success": false,
  "error": "Invalid Post ID",
  "code": 1062
}
```
{% endswagger-response %}

{% swagger-response status="404: Not Found" description="Invalid MD5" %}
```javascript
{
  "success": false,
  "error": "Invalid MD5",
  "code": 1063
}
```
{% endswagger-response %}

{% swagger-response status="404: Not Found" description="Invalid Type" %}
```javascript
{
  "success": false,
  "error": "Invalid Type",
  "code": 1064
}
```
{% endswagger-response %}

{% swagger-response status="408: Request Timeout" description="Generation Timeout" %}
```javascript
// this will never be returned on initial generation, only
// if you make a request for one that has already started
{
  "success": false,
  "status": "timeout",
  "code": 1065
}
```
{% endswagger-response %}

{% swagger-response status="500: Internal Server Error" description="Generation Error" %}
```javascript
// this will never be returned on initial generation, only
// if you make a request for one that has already started
{
  "success": false,
  "status": "error",
  "code": 1060
}
```
{% endswagger-response %}
{% endswagger %}

{% swagger method="get" path="/check/:md5/:type" baseUrl="https://thumbs.yiff.rest" summary="Check Generation Progress" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="path" name="id" type="String" required="true" %}
The MD5 of an e621 post. This MUST be an md5, you will be given this if you did not have it.
{% endswagger-parameter %}

{% swagger-parameter in="path" name="type" type="String" required="true" %}
`gif`

 or 

`png`
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="Processing" %}
```javascript
{
  "success": true,
  "status": "processing",
  "checkURL": "https://thumbs.yiff.rest/check/{gif}/{type}",
  "checkAt": 0, // (unix millis) the time at which you should fetch the above url
  "time": 0, // the milliseconds after which you should check the above url (see checkAt)
  "startedAt": 0, // (unix millis) the time at which processing started
}
```
{% endswagger-response %}

{% swagger-response status="201: Created" description="Done" %}
```javascript
{
  "success": true,
  "status": "done",
  "url": "https://thumbs.yiff.media/{md5}.{type}"
}
```
{% endswagger-response %}

{% swagger-response status="404: Not Found" description="Invalid MD5" %}
```javascript
{
  "success": false,
  "error": "Invalid MD5",
  "code": 1061
}
```
{% endswagger-response %}

{% swagger-response status="404: Not Found" description="Invalid Type" %}
```javascript
{
  "success": false,
  "error": "Invalid Type",
  "code": 1064
}
```
{% endswagger-response %}

{% swagger-response status="404: Not Found" description="Not Found" %}
```javascript
{
  "success": false,
  "error": "Not Found",
  "code": 1066
}
```
{% endswagger-response %}

{% swagger-response status="408: Request Timeout" description="Generation Timeout" %}
```javascript
{
  "success": false,
  "status": "timeout",
  "code": 1065
}
```
{% endswagger-response %}

{% swagger-response status="500: Internal Server Error" description="Generation Error" %}
```javascript
{
  "success": false,
  "status": "error",
  "code": 1060
}
```
{% endswagger-response %}
{% endswagger %}

