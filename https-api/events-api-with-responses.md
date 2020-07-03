# Events API \(with responses\)

{% api-method method="post" host="/external/api/" path="logEvent?token={token}&code={event\_name}&description={event\_desciption}" %}
{% api-method-summary %}
Create Event
{% endapi-method-summary %}

{% api-method-description %}
This endpoint will create new Event on Timeline in Device profile pages on the web and in the mobile apps
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="token" type="string" required=true %}
AuthToken of the device
{% endapi-method-parameter %}

{% api-method-parameter name="code" type="string" required=true %}
event\_code from Product Template
{% endapi-method-parameter %}

{% api-method-parameter name="description" type="string" required=false %}
custom Event description
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```
no response
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=302 %}
{% api-method-response-example-description %}
event code is missing. Check Product Template to see if you are using correct 
{% endapi-method-response-example-description %}

```
{"error":{"message":"Event code is not provided."}}
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=500 %}
{% api-method-response-example-description %}
Invalid token
{% endapi-method-response-example-description %}

```
{"error":{"message":"Invalid token."}}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}



