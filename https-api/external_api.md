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

Get device json \(via HTTP GET\):

* `/external/api/device?token={token}`

### Log event

* `/external/api/logEvent?token={token}&code={event_name}`
* `/external/api/logEvent?token={token}&code={event_name}&description={event_desciption}`

## Devices

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

#### Update Widget parameters

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

### Events

#### Create Event

Use HTTP **GET** method to create a new Event on Device Timeline

```text
/external/api/logEvent?token={token}&code={event_name}&description={event_desciption}
```

**Parameters:**

* `token`: AuthToken of the device
* `code`: code of the event. Can be found in Product Template - [Events](https://github.com/blynkkk/blynkkk.github.io/tree/ba877e83fafb998294c9504da8a7bba02318caf5/en/product-1/events/README.md)
* `description`: optionally you can add custom description to the event and it will be rendered on Device Timeline in mobile apps and on the web

Example:

```text
curl --get 'https://blynk.io/external/api/logEvent?token=123&code=critical_error&description="custom description"'
```

Create Event on Device Timeline

* `/external/api/logEvent?token={token}&code={event_name}`

\`\`

* `/external/api/logEvent?token={token}&code={event_name}&description={event_desciption}`

