---
description: These may show up on any given route in any service.
---

# Shared Responses

<mark style="color:red;">The content of</mark> <mark style="color:red;"></mark><mark style="color:red;">`error`</mark> <mark style="color:red;"></mark><mark style="color:red;">is unreliable, use</mark> <mark style="color:red;"></mark><mark style="color:red;">`code`</mark> <mark style="color:red;"></mark><mark style="color:red;">instead. See</mark> <mark style="color:blue;"></mark> [<mark style="color:blue;">Error Codes</mark>](error-codes.md) <mark style="color:red;">for a full list.</mark>



<details>

<summary>Invalid API Key</summary>

{% code title="401 Unauthorized" %}
```javascript
{
  "success": false,
  "error": "Invalid api key.",
  "code": 1010
}
```
{% endcode %}

</details>

<details>

<summary>API Key Is Inactive</summary>

{% code title="401 Unauthorized" %}
```javascript
{
  "success": false,
  "error": "Api key is inactive.",
  "code": 1011
}
```
{% endcode %}

</details>

<details>

<summary>API Key Disabled</summary>

{% code title="403 Forbidden" %}
```javascript
{
  "success": "false",
  "error": "Your api key has been disabled by an administrator. See \"extra.reason\" for the reasoning.",
  "extra": {
    "reason": "",
    "support": "https://yiff.rest/support"
  },
  "code": 1012
}
```
{% endcode %}

</details>

<details>

<summary>Bad User Agent</summary>



{% code title="403 Forbidden" %}
```javascript
// Reasons:
// Bots are not allowed to crawl our api.
// This is a default library user agent, and does not give us any information about the client making the request. Please set an informative user agent.
// The user agent you supplied is non-informative, it's likely just one word or something meaningless. Please provide actual client info in your user agent.
// You did not supply a user agent. You need to supply one with valid client information.
// This user agent has been blocked for spamming our api. Don't do that.
{
  "success": false,
  "error": "Your user agent has been blocked. See \"extra\" for the reasoning.",
  "extra": {
    "reason": "(see top)",
    "help": "https://yiff.rest/support"
  },
  "code": 1021
}
```
{% endcode %}

</details>

<details>

<summary>No Access To Service</summary>

{% code title="403 Forbidden" %}
```javascript
{
  "success": false,
  "error": "You do not have access to this service.",
  "code": 1022
}
```
{% endcode %}

</details>

<details>

<summary>Unknown API Route</summary>

{% code title="404 Not Found" %}
```javascript
{
  "success": false,
  "error": "Unknown api route.",
  "code": 1024
}
```
{% endcode %}

</details>

<details>

<summary>Rate Limited</summary>

{% code title="429 Too Many Requests" %}
```javascript
// global headers will also be present
{
  "success": false,
  "error": "Request Limit Exceeded",
  "code": 1000,
  "info": {
    "limit": 0, // X-RateLimit-Limit
    "remaining": 0, // X-RateLimit-Remaining
    "reset": 0, // X-RateLimit-Reset
    "resetAfter": 0, // X-RateLimit-Reset-After
    "retryAfter": 0, // Retry-After
    "bucket": "", // X-RateLimit-Bucket
    "precision": "millisecond", // X-RateLimit-Precision
    "global": false
  }
}
```
{% endcode %}

</details>

<details>

<summary>Globally Rate Limited</summary>

{% code title="429 Too Many Requests" %}
```javascript
// route specific headers will also be present
{
  "success": false,
  "error": "Request Limit Exceeded",
  "code": 1001,
  "info": {
    "limit": 0, // X-RateLimit-Global-Limit
    "remaining": 0, // X-RateLimit-Global-Remaining
    "reset": 0, // X-RateLimit-Global-Reset
    "resetAfter": 0, // X-RateLimit-Global-Reset-After
    "retryAfter": 0, // Retry-After
    "bucket": null,
    "precision": "millisecond", // X-RateLimit-Global-Precision
    "global": true
  }
}
```
{% endcode %}

</details>

<details>

<summary>Server Disk Full</summary>

{% code title="507 Insufficient Storage" %}
```javascript
// because serving images gets wonky when the server's disk is full
{
  "success": false,
  "error":   "Internal disk is full, try again later.",
  "code": 1020
}
```
{% endcode %}

</details>
