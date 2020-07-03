# email

## Email

Email widget allows you to send email from your hardware to any address.

Example code:

```cpp
Blynk.email("my_email@example.com", "Subject", "Your message goes here");
```

It also contains `to` field. With this field you may define receiver of email in the app. You may skip `to` field when you want to send email to your Blynk app login email:

```cpp
 Blynk.email("Subject", "Your message goes here");
```

You can send either `text/html` or `text/plain` \(some clients don't support `text/html`\) email. You can change this content type of email in the Mail widget settings.

Additionally you may use `{DEVICE_NAME}`, `{DEVICE_OWNER_EMAIL}` and `{VENDOR_EMAIL}` \(for the local server\) placeholders in the mail for the `to`, `subject` and `body` fields:

```cpp
Blynk.email("{DEVICE_OWNER_EMAIL}", "{DEVICE_NAME} : Alarm", "Your {DEVICE_NAME} has critical error!");
```

Limitations :

* Maximum allowed email + subject + message length is 120 symbols. However you can increase this limit if necessary 

  by adding `#define BLYNK_MAX_SENDBYTES XXX` to you sketch. Where `XXX` is desired max length of your email. 

  For example for ESP you can set this to 1200 max length `#define BLYNK_MAX_SENDBYTES 1200`. The 

  `#define BLYNK_MAX_SENDBYTES 1200` must be included before any of the Blynk includes.

* Only 1 email per 5 seconds is allowed;
* In case you are using gmail you are limited with 500 mails per day \(by google\). Other providers may have similar

  limitations, so please be careful;

* User is limited with 100 messages per day;

## Unicode in email

The library handles all strings as UTF8 Unicode. If you're facing problems, try to print your message to the Serial and see if it works \(the terminal should be set to UTF-8 encoding\). If it doesn't work, probably you should read about unicode support of your compiler. If it works, but your message is truncated - you need to increase message length limit \(all Unicode symbols consume at least twice the size of Latin symbols\).

## Increasing message length limit

You can increase maximum message length by putting on the top of your sketch \(before Blynk includes\):

```cpp
#define BLYNK_MAX_SENDBYTES 256 // Default is 128
```

**Sketch:** [Email](https://github.com/blynkkk/blynk-library/blob/master/examples/Widgets/Email/Email.ino)

