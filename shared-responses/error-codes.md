# Error Codes

{% hint style="info" %}
The codes below can be returned by any route.

The following codes are reserved for general use: 0, 1, 1000-1022, 1024-1029
{% endhint %}

| Code |           Description           |
| :--: | :-----------------------------: |
|   0  |          Internal Error         |
|   1  |          Access Denied          |
| 1000 |       Ratelimited (Route)       |
| 1001 |       Ratelimited (Global)      |
| 1002 | Suspected Browser Impersonation |
| 1003 |       Down For Maintenance      |
| 1010 |         Invalid API Key         |
| 1011 |         Inactive API Key        |
| 1012 |         Disabled API Key        |
| 1013 |         API Key Required        |
| 1014 |       Anonymous Restricted      |
| 1020 |         Server Disk Full        |
| 1021 |        Blocked User-Agent       |
| 1022 |       No Access To Service      |
| 1024 |          Unknown Route          |
| 1025 |        Method Not Allowed       |



{% hint style="info" %}
The codes below can only be returned in the [Images](../) service.

The following codes are reserved for this service: 1023, 1030-1059
{% endhint %}

|   Code   |        Description       |
| :------: | :----------------------: |
|   1023   |   Invalid Response Type  |
|   1030   |    Category Not Found    |
| ~~1031~~ |    ~~Empty Category~~    |
|   1040   |         Not Found        |
|   1041   |        No Results        |
|   1051   |         Amount <1        |
|   1052   |         Amount >5        |
|   1053   | Images Response Disabled |
|   1054   |   \[Bulk] Invalid Body   |
|   1055   | \[Bulk] Invalid Category |
|   1056   |    \[Bulk] Number >Max   |

{% hint style="info" %}
The codes below can only be returned in the [Thumbnails](../thumbnails.md) service.

The following codes are reserved for this service: 1060-1069
{% endhint %}

|   Code   |      Description     |
| :------: | :------------------: |
|   1060   |     Generic Error    |
| ~~1061~~ | ~~API Key Required~~ |
|   1062   |    Invalid Post ID   |
|   1063   |      Invalid MD5     |
|   1064   |     Invalid Type     |
|   1065   |        Timeout       |
|   1066   |    Check Not Found   |

{% hint style="info" %}
The codes below can only be returned in the [Shortener](../shortener.md) service.

The following codes are reserved for this service: 1070-1090
{% endhint %}

| Code |        Description       |
| :--: | :----------------------: |
| 1070 |       Code Too Long      |
| 1071 |       Invalid Code       |
| 1072 |        Code In Use       |
| 1073 |        Invalid URL       |
| 1074 |      Credit Too Long     |
| 1075 |         Not Found        |
| 1076 | Management Code Required |
| 1077 |    No Management Code    |
| 1078 | Management Code Mismatch |
| 1079 |        URL In Use        |
| 1080 |        No Changes        |

t
