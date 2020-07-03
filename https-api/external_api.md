# Devices

## Devices

Get datastream value \(via HTTP GET\):

* `/external/api/get?token={token}&pin={pin}`
* `/external/api/get?token={token}&dataStreamId={id}`

Update datastream value \(via HTTP GET\):

* `/external/api/update?token={token}&pin={pin}&value={value}`
* `/external/api/update?token={token}&dataStreamId={id}&value={value}`
* `/external/api/update/property?token={token}&pin={pin}&{property}={value}`

## Log event

* `/external/api/logEvent?token={token}&code={event_name}`
* `/external/api/logEvent?token={token}&code={event_name}&description={event_desciption}`





{% api-method method="get" host="/external/api/" path="update?token={token}&pin={pin}&value={value}" %}
{% api-method-summary %}
Update Datastream value
{% endapi-method-summary %}

{% api-method-description %}

{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="" type="string" required=false %}

{% endapi-method-parameter %}
{% endapi-method-path-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```

```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="get" host="/external/api/" path="get?token={token}&pin={pin}" %}
{% api-method-summary %}
Get Virtual Pin value
{% endapi-method-summary %}

{% api-method-description %}

{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="token" type="string" required=false %}

{% endapi-method-parameter %}

{% api-method-parameter name="pin" type="string" required=false %}

{% endapi-method-parameter %}
{% endapi-method-path-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```

```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="get" host="/external/api/" path="update?token={token}&pin={pin}&value={value}" %}
{% api-method-summary %}
Update Virtual Pin value
{% endapi-method-summary %}

{% api-method-description %}

{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="token" type="string" required=true %}
AuthToken of device
{% endapi-method-parameter %}

{% api-method-parameter name="pin" type="string" required=true %}
Virtual Pin number. e.g. V1
{% endapi-method-parameter %}

{% api-method-parameter name="value" type="string" required=true %}
value to update
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```

```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="get" host="/external/api/" path="get?token={token}&pin={pin}" %}
{% api-method-summary %}

{% endapi-method-summary %}

{% api-method-description %}

{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="" type="string" required=false %}

{% endapi-method-parameter %}
{% endapi-method-path-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```

```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

