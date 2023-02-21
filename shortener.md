# Shortener

An [API Key](api-key.md) <mark style="color:red;">is</mark> required for this service. See [Shared Responses](shared-responses/) for common error responses.

{% swagger method="post" path="/create" baseUrl="https://yiff.rocks" summary="Shorten A URL" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="query" name="editable" type="Boolean" %}
If the shortened url should be editable (you will get a code to edit with)
{% endswagger-parameter %}

{% swagger-parameter in="body" name="code" type="String" %}
The code to use, random if not specified.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="credit" type="String" %}
The name to credit, 

`Unknown`

 if not specified.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="url" type="String" required="true" %}
The URL to shorten.
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="Already Exists" %}
```javascript
{
  "success": true,
  "data": {
    "code": "",
    "createdAt": "0000-00-00T00:00:00.000Z",
    "modifiedAt": "0000-00-00T00:00:00.000Z", // nullable
    "url": "",
    "pos": 0,
    "credit": "",
    "fullURL": "https://yiff.rocks/{code}",
    "managementCode": null
  }
}
```
{% endswagger-response %}

{% swagger-response status="201: Created" description="Success" %}
```javascript
{
  "success": true,
  "data": {
    "code": "",
    "createdAt": "0000-00-00T00:00:00.000Z",
    "modifiedAt": "0000-00-00T00:00:00.000Z", // nullable
    "url": "",
    "pos": 0,
    "credit": "",
    "fullURL": "https://yiff.rocks/{code}",
    "managementCode": "" // nullable, save if you plan on editing later
  }
}
```
{% endswagger-response %}

{% swagger-response status="409: Conflict" description="Code In Use" %}
```javascript
{
  "success": false,
  "error": "Code already in use.",
  "code": 1072
}
```
{% endswagger-response %}

{% swagger-response status="422: Unprocessable Entity" description="Code Too Long" %}
```javascript
// Max: 50
{
  "success": false,
  "error": "Provided code is too long.",
  "code": 1070
}
```
{% endswagger-response %}

{% swagger-response status="422: Unprocessable Entity" description="Invalid Code" %}
```javascript
// Allowed: a-z, A-Z, -, 0-9
{
  "success": false,
  "error": "Invalid characters in code.",
  "code": 1071
}
```
{% endswagger-response %}

{% swagger-response status="422: Unprocessable Entity" description="Invalid URL" %}
```javascript
// RegEx: /^(?:(?:(?:https?|ftp):)?\/\/)(?:\S+(?::\S*)?@)?(?:(?!(?:10|127)(?:\.\d{1,3}){3})(?!(?:169\.254|192\.168)(?:\.\d{1,3}){2})(?!172\.(?:1[6-9]|2\d|3[0-1])(?:\.\d{1,3}){2})(?:[1-9]\d?|1\d\d|2[01]\d|22[0-3])(?:\.(?:1?\d{1,2}|2[0-4]\d|25[0-5])){2}(?:\.(?:[1-9]\d?|1\d\d|2[0-4]\d|25[0-4]))|(?:(?:[a-z0-9\u00a1-\uffff][a-z0-9\u00a1-\uffff_-]{0,62})?[a-z0-9\u00a1-\uffff]\.)+(?:[a-z\u00a1-\uffff]{2,}\.?))(?::\d{2,5})?(?:[/?#]\S*)?$/i
{
  "success": false,
  "error": "Invalid url provided.",
  "code": 1073
}
```
{% endswagger-response %}

{% swagger-response status="422: Unprocessable Entity" description="Credit Too Long" %}
```javascript
// Max: 50
{
  "success": false,
  "error": "Provided credit is too long.",
  "code": 1074
}
```
{% endswagger-response %}
{% endswagger %}

{% swagger method="get" path="/:code" baseUrl="https://yiff.rocks" summary="Get A Short URL (Redirect)" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-response status="302: Found" description="Redirect" %}
```javascript
// Redirected to original url
```
{% endswagger-response %}

{% swagger-response status="404: Not Found" description="Not Found" %}
```javascript
Unknown short url code.
```
{% endswagger-response %}
{% endswagger %}

{% swagger method="get" path="/:code+" baseUrl="https://yiff.rocks" summary="Get A Short URL (Preview)" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-response status="200: OK" description="Success" %}
```javascript
// HTML Page
```
{% endswagger-response %}

{% swagger-response status="404: Not Found" description="Not Found" %}
```javascript
Unknown short url code.
```
{% endswagger-response %}
{% endswagger %}

{% swagger method="get" path="/:code.json" baseUrl="https://yiff.rocks" summary="Get A Short URL (JSON)" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-response status="200: OK" description="Success" %}
```javascript
{
  "success": true,
  "data": {
    "code": "",
    "createdAt": "0000-00-00T00:00:00.000Z",
    "modifiedAt": "0000-00-00T00:00:00.000Z", // nullable
    "url": "",
    "pos": 0,
    "credit": "",
    "fullURL": "https://yiff.rocks/{code}"
  }
}
```
{% endswagger-response %}

{% swagger-response status="404: Not Found" description="Not Found" %}
```javascript
{
  "success": false,
  "error": "A short url with that code was not found.",
  "code": 1075
}
```
{% endswagger-response %}
{% endswagger %}

{% swagger method="delete" path="/:code" baseUrl="https://yiff.rocks" summary="Delete A Short URL" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="body" name="managementCode" type="String" required="true" %}
The management code you received when creating the shorturl.
{% endswagger-parameter %}

{% swagger-response status="204: No Content" description="Success" %}
```javascript
// No Content
```
{% endswagger-response %}

{% swagger-response status="401: Unauthorized" description="Management Code Required" %}
```javascript
{
  "success": false,
  "error": "You must provide an authorization code. These are created at the time the short url was created.",
  "code": 1076
}
```
{% endswagger-response %}

{% swagger-response status="401: Unauthorized" description="Management Code Mismatch" %}
```javascript
{
  "success": false,
  "error": "That management code does not match this short url.",
  "code": 1078
}
```
{% endswagger-response %}

{% swagger-response status="403: Forbidden" description="No Management Code" %}
```javascript
{
  "success": false",
  "error": "That short url does not have a management code, so it cannot be deleted.",
  "code": 1077
}
```
{% endswagger-response %}

{% swagger-response status="404: Not Found" description="Not Found" %}
```javascript
{
  "success": false,
  "error": "A short url with that code was not found.",
  "code": 1075
}
```
{% endswagger-response %}
{% endswagger %}

{% swagger method="patch" path="/:code" baseUrl="https://yiff.rocks" summary="Modify A Short URL" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="body" name="managementCode" type="String" required="true" %}
The management code you received when creating the shorturl.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="credit" type="String" %}
The new credit name for the url.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="url" type="String" %}
The new url for the shorturl.
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="Success" %}
```javascript
{
  "success": true,
  "data": {
    "code": "",
    "createdAt": "0000-00-00T00:00:00.000Z",
    "modifiedAt": "0000-00-00T00:00:00.000Z", // nullable
    "url": "",
    "pos": 0,
    "credit": "",
    "fullURL": "https://yiff.rocks/{code}"
  }
}
```
{% endswagger-response %}

{% swagger-response status="400: Bad Request" description="No Changes Detected" %}
```javascript
{
  "success": false,
  "error": "No changes were detected.",
  "code": 1080
}
```
{% endswagger-response %}

{% swagger-response status="401: Unauthorized" description="Management Code Required" %}
```javascript
{
  "success": false,
  "error": "You must provide an authorization code. These are created at the time the short url was created.",
  "code": 1076
}
```
{% endswagger-response %}

{% swagger-response status="401: Unauthorized" description="Management Code Mismatch" %}
```javascript
{
  "success": false,
  "error": "That management code does not match this short url.",
  "code": 1078
}
```
{% endswagger-response %}

{% swagger-response status="403: Forbidden" description="No Management Code" %}
```javascript
{
  "success": false",
  "error": "That short url does not have a management code, so it cannot be modified.",
  "code": 1077
}
```
{% endswagger-response %}

{% swagger-response status="404: Not Found" description="Not Found" %}
```javascript
{
  "success": false,
  "error": "A short url with that code was not found.",
  "code": 1075
}
```
{% endswagger-response %}

{% swagger-response status="409: Conflict" description="URL In Use" %}
```javascript
{
  "success": false,
  "error": "The provided url is already in use.",
  "code": 1079
}
```
{% endswagger-response %}

{% swagger-response status="422: Unprocessable Entity" description="Invalid URL" %}
```javascript
// RegEx: /^(?:(?:(?:https?|ftp):)?\/\/)(?:\S+(?::\S*)?@)?(?:(?!(?:10|127)(?:\.\d{1,3}){3})(?!(?:169\.254|192\.168)(?:\.\d{1,3}){2})(?!172\.(?:1[6-9]|2\d|3[0-1])(?:\.\d{1,3}){2})(?:[1-9]\d?|1\d\d|2[01]\d|22[0-3])(?:\.(?:1?\d{1,2}|2[0-4]\d|25[0-5])){2}(?:\.(?:[1-9]\d?|1\d\d|2[0-4]\d|25[0-4]))|(?:(?:[a-z0-9\u00a1-\uffff][a-z0-9\u00a1-\uffff_-]{0,62})?[a-z0-9\u00a1-\uffff]\.)+(?:[a-z\u00a1-\uffff]{2,}\.?))(?::\d{2,5})?(?:[/?#]\S*)?$/i
{
  "success": false,
  "error": "Invalid url provided.",
  "code": 1073
}
```
{% endswagger-response %}

{% swagger-response status="422: Unprocessable Entity" description="Credit Too Long" %}
```javascript
// Max: 50
{
  "success": false,
  "error": "Provided credit is too long.",
  "code": 1074
}
```
{% endswagger-response %}
{% endswagger %}

