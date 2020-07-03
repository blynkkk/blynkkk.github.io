# Events API

To trigger [Events](../product/events/) creation from hardware \(or other sources\) and render them on Timeline in Device profile pages on the web and in the mobile apps, use this API call:

```text
/external/api/logEvent?token={token}&code={event_name}
```

`event_name` should be taken from [Product Template Settings](../product/product-template-settings.md) &gt; [Events](../product/events/)

\*\*\*\*

**Options:** 

To render custom description of the event on the Timeline, use `event_description` parameter

`/external/api/logEvent?token={token}&code={event_name}&description={event_desciption}`



&gt;&gt;IMAGE OF TIMELINE WITH EVENT DESCRIPTION \(MOBILE AND WEB\)

