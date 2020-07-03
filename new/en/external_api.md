#### Hardware

Get Virtual datastream value:
- HTTP GET ```/external/api/get?token={token}&pin={pin}```
- HTTP GET ```/external/api/get?token={token}&dataStreamId={id}```

Update Virtual datastream value:
- HTTP GET ```/external/api/update?token={token}&pin={pin}&value={value}```
- HTTP GET ```/external/api/update?token={token}&dataStreamId={id}&value={value}```
- HTTP GET ```/external/api/update/property?token={token}&pin={pin}&{property}={value}```

#### Log event

- ```/external/api/logEvent?token={token}&code={event_name}```
- ```/external/api/logEvent?token={token}&code={event_name}&description={event_desciption}```