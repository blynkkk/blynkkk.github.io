# Datastreams API

## Hardware

Get datastream value \(via HTTP GET\):

* `/external/api/get?token={token}&pin={pin}`
* `/external/api/get?token={token}&dataStreamId={id}`

Update datastream value \(via HTTP GET\):

* `/external/api/update?token={token}&pin={pin}&value={value}`
* `/external/api/update?token={token}&dataStreamId={id}&value={value}`
* `/external/api/update/property?token={token}&pin={pin}&{property}={value}`

Get device json \(via HTTP GET\):

* `/external/api/device?token={token}`

## Log event

* `/external/api/logEvent?token={token}&code={event_name}`
* `/external/api/logEvent?token={token}&code={event_name}&description={event_desciption}`

