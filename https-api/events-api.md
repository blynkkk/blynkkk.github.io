# Events

**Create Event**

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

Result: 

&gt;&gt;IMAGE OF TIMELINE WITH EVENT DESCRIPTION \(MOBILE AND WEB\)

