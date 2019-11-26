### Events: Notification

Every event can additionally trigger notifications.

You can:
- Send Emails
- Send Push Notification on a smartphone/tablet
- Send SMS (additional charges apply)

#### Recipients
You can assign different recipients to each event. 

For example, some notifications should be sent to the end-customers, 
while others should be sent to the technical support team (for internal review only).

You need to define the recipient of notifications in Product Metadata before they become available as a selection.

When you add any of the following Metadata fields, they will be available as a recipient in notifications:
- ```Device owner``` is available as a recipient by default (no need to add such field)
- Contact metadata
- Email metadata

Example:
You would like your technical support team to be notified every time the vibration sensor is over the defined threshold.

1. In Products -> Your Product -> Metadata: 
Create a new Metadata field of type `Email` or `Contact`. 
Name it "Technical Support" and specify a default value (for example `support@yourcompany.com`)
2. In Products -> Your Product -> Events:
Create a new Event and set a recipient of email notification as ```Technical Support```
