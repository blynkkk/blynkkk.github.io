# Devices

## Datastreams API

### Hardware

Get datastream value \(via HTTP GET\):

* `/external/api/get?token={token}&pin={pin}`
* `/external/api/get?token={token}&dataStreamId={id}`

Update datastream value \(via HTTP GET\):

* `/external/api/update?token={token}&pin={pin}&value={value}`
* `/external/api/update?token={token}&dataStreamId={id}&value={value}`
* `/external/api/update/property?token={token}&pin={pin}&{property}={value}`

### Log event

* `/external/api/logEvent?token={token}&code={event_name}`
* `/external/api/logEvent?token={token}&code={event_name}&description={event_desciption}`

### Devices

#### Get datastream value

Use HTTP **GET** method to get value of a Datastream or Virtual Pin

Using Datastream ID:

```text
/external/api/get?token={token}&dataStreamId={id}
```

Using Virtual Pin:

```text
/external/api/get?token={token}&pin={pin}
```

**Parameters:**

* `token`: AuthToken of the device
* `pin`: Virtual Pin number. e.g. V0
* `dataStreamId`: can be found in Product Settings &gt; Datastreams

Example:

```text
curl --get 'https://blynk.io/external/api/get?token=123&pin=V0'
```

#### Update Datastream value \(using GET\):

You can use HTTP **GET** method to update value of a Datastream or Virtual Pin

Using Datastream ID:

```text
/external/api/update?token={token}&dataStreamId={id}&value={value}
```

Using Virtual Pin number:

```text
/external/api/update?token={token}&pin={pin}&value={value}
```

**Path parameters:**

* `token`: AuthToken of the device
* `dataStreamId`: can be found in Product Settings &gt; Datastreams
* `pin`: Virtual Pin number. e.g. V0

Example:

```text
curl --get 'https://blynk.io/external/api/update?token=123&dataStreamId=1&value=100'
```

#### Update Widget parameters from device

You can update variuous properties of a widget \(in the mobile app\) which is using a specified Virtual Pin. Full list of properties here\(LINK\)

```text
/external/api/update/property?token={token}&pin={pin}&{property}={value}
```

**Path parameters:**

* `token`: AuthToken of the device
* `property`: property name. Full list of properties is here \(LINK\)
* `pin`: Virtual Pin number. e.g. V0

Example:

```text
curl --get 'https://blynk.io/external/api/update/property?token=123&pin=V0&isDisabled=true'
```

### 

{% api-method method="get" host="/external/api/" path="device?token={token}" %}
{% api-method-summary %}
Device Info and Metadata
{% endapi-method-summary %}

{% api-method-description %}
Get device information including metadata
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="token" type="string" required=true %}
AuthToken of device
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
Returns device object in JSON format including device info and metadata values
{% endapi-method-response-example-description %}

```
{
  "id" : 605,
  "productId" : 5,
  "orgId" : 1,
  "name" : "Device Name",
  "boardType" : "Generic Board",
  "token" : "TWDpVlZVCET0iNP8WZL-Sj_oMHSH5FAD",
  "updatedAt" : 1594058851813,
  "status" : "ONLINE",
  "activatedAt" : 1578483203021,
  "activatedBy" : "email@email.com",
  "disconnectTime" : 1593842713088,
  "ipInfo" : {
    "ip" : "91.235.102.114",
    "country" : "Ukraine",
    "lat" : 50.4333,
    "lon" : 30.5167,
    "tz" : "Europe/Kiev"
  },
  "lastReportedAt" : 1594058851812,
  "metadataUpdatedAt" : 1594058829632,
  "metadataUpdatedBy" : "email@email.com",
  "metaFields" : [ {
    "id" : 1,
    "name" : "Device Name",
    "isDefault" : true,
    "value" : "Device Name",
    "type" : "DeviceName"
  }, {
    "id" : 2,
    "name" : "Device Owner",
    "isDefault" : true,
    "value" : "email@email.com",
    "userId" : 10,
    "userOrgId" : 10,
  }, {
    "id" : 3,
    "name" : "Job Site",
    "lat" : 7.1645,
    "lon" : 125.572972,
    "type" : "Location"
  }, {
    "id" : 8,
    "name" : "Serial Number",
    "type" : "Text"
  } ],
  "productName" : "Product Name",
  "orgName" : "Acme Inc",
  "owner" : "email@email.com",
  "ownerId" : 10,
  "manufacturer" : "Acme Inc",
  "hardwareInfo" : {
    "version" : "0.666",
    "blynkVersion" : "0.2.1",
    "templateId" : "TMPL000XX",
    "heartbeatInterval" : 10,
    "buffIn" : 1024
  }
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}



