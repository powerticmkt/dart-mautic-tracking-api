# mautic_tracking_api

 App [User Monitoring and Tracking](https://www.mautic.org/docs/en/contacts/contact_monitoring.html) easily for Dart and Flutter using [Mautic: Open Source Marketing Automation Software](https://github.com/mautic/mautic).

The essence of monitoring what happens in an App is similar to monitoring what happens on a website.

In short, this package use **Named Screen Path** (e.g. `main_screen`) in your App as your `page_url` field in the tracker, **Named Screen Title** (e.g. `Home Screen`) as your `page_title` field and the **Contact E-mail** as unique identifier. See [Mautic Contact Monitoring](#mautic-contact-monitoring) section for detailed instructions.

This package also use native **Mautic Tracking Cookies** `mtc_id`, `mtc_sid` and `mautic_device_id` to make Tracking more effective.

Made with :heart: by **Mautic Specialists** at [Powertic](https://powertic.com).

## Install

Add this package to your package's ```pubspec.yaml``` file:

```yaml
dependencies:
  mautic_tracking_api:
```

Run `flutter pub get` on terminal to download and install packages and import on your `main.dart`:

```dart
import 'package:mautic_tracking_api/mautic_tracking_api.dart';
```

## Usage

Create a global instance of `MauticTracking` and import this global instance on all your files.

```dart
var MauticTracking mautic;
```

On your `main.dart` you can [setting up](#setting-up) the `MauticTracking` object:

```dart
// Setting Up
void main() async {

  // Start Tracking
  mautic = MauticTracking(
    "https://mkt.mymautic.com",
    appName: "MyApp",
    email: "contact@email.com",
    appVersion: '1.0.0',
    appBundleName: 'com.mydomain.myapp',
  );

  // Track App Start
  await mautic.trackAppStart();

}
```

When the App is Started, this event will be fired:

![Started App](https://github.com/powerticmkt/dart-mautic-tracking-api/raw/master/docs/started_app.png)

If the contact doesn't exists on Mautic, the contact will be identified by `app_started`.

![Contact Identified](https://github.com/powerticmkt/dart-mautic-tracking-api/raw/master/docs/contact_identified.png)

See a complete Flutter example at [example/example_app/lib/main.dart](https://github.com/powerticmkt/dart-mautic-tracking-api/blob/master/example/example_app/lib/main.dart)

## Setting Up

There are some options to instantiate `MauticTracking`:

```dart
MauticTracking(
    this._base_url, {
    this.email,
    this.appName,
    this.appVersion,
    this.appBundleName,
    this.closeConnectionAfterRequest = true,
    this.userAgent =
        'Mozilla/5.0 (compatible; MSIE 9.0; Windows NT 6.0; Trident/5.0)',
  });
```

These are the constructor options:

| Property                      | Type     | Required | Description                    |
| ----------------------------- | -------- | -------- | ------------------------------ |
| `_base_url`                   | `String` | Yes      | Mautic Base URL                |
| `email`                       | `String` | No       | Mautic Contact Email           |
| `appName`                     | `String` | No       | App Name                       |
| `appVersion`                  | `String` | No       | App Version                    |
| `appBundleName`               | `String` | No       | App Bundle Name                |
| `closeConnectionAfterRequest` | `bool`   | No       | Close Connection after Request |
| `userAgent`                   | `String` | No       | Request User Agent             |

## Mautic Contact Monitoring

The act of monitoring the traffic and activity of contacts can sometimes be somewhat technical and frustrating to understand. Mautic Tracking API makes this monitoring simple and easy to configure.

![Contact Timeline](https://github.com/powerticmkt/dart-mautic-tracking-api/raw/master/docs/contact_timeline.png)

## Tracking Screens

Send App Screen info to Mautic.

![Screen Track](https://github.com/powerticmkt/dart-mautic-tracking-api/raw/master/docs/screen_track.png)

**Method Definition:**

```dart
Future<void> trackScreen(String screenPath, [String screenName]) async;
```

| Property     | Type     | Required | Description               |
| ------------ | -------- | -------- | ------------------------- |
| `screenPath` | `String` | Yes      | Unique Screen Route Path  |
| `screenName` | `String` | No       | Unique Screen Route Label |

**Usage:**

You can send screen tracking info only with `screenPath`.

Create your screen paths using **_** to separate words and always use **small caps**.

```dart
mautic.trackScreen("main");
```

You can also send screen tracking info using `screenPath` and `screenName`. Fell free to use space and capitalized words for Screen Name.

```dart
mautic.trackScreen("main", "Main Page");
```

## Tracking Events

Send App Event info to Mautic.

![Event Track](https://github.com/powerticmkt/dart-mautic-tracking-api/raw/master/docs/event_track.png)

**Method Definition:**

```dart
Future<void> trackEvent(String eventKey, String eventName, String screenPath, [String screenName]) async;
```

| Property     | Type     | Required | Description               |
| ------------ | -------- | -------- | ------------------------- |
| `eventKey`   | `String` | Yes      | Unique Event Key          |
| `eventName`  | `String` | Yes      | Unique Event Name         |
| `screenPath` | `String` | Yes      | Unique Screen Route Path  |
| `screenName` | `String` | No       | Unique Screen Route Label |

**Usage:**

You can send screen tracking info only with `screenPath`.

Create your screen paths using **_** to separate words and always use **small caps**.

```dart
mautic.trackEvent('click_getting_start', 'Click Get Start Button', 'home');
```

You can also send screen tracking info using `screenPath` and `screenName`. Fell free to use space and capitalized words for Scren Name and Event Name.

```dart
mautic.trackEvent('click_getting_start', 'Click Get Start Button', 'home', 'Home Page');
```

### Adding Contact Tags

Add tag to contact.

![Contact Timeline](https://github.com/powerticmkt/dart-mautic-tracking-api/raw/master/docs/added_tag.png)

```dart
mautic.addTag({'a', 'b'});
```

| Property | Type  | Required | Description        |
| -------- | ----- | -------- | ------------------ |
| `params` | `Set` | Yes      | `Set` of tag names |

### Removing Contact Tags

Remove tag to contact.

![Contact Timeline](https://github.com/powerticmkt/dart-mautic-tracking-api/raw/master/docs/removed_tag.png)

```dart
mautic.removeTag({'a', 'b'});
```

| Property | Type  | Required | Description        |
| -------- | ----- | -------- | ------------------ |
| `params` | `Set` | Yes      | `Set` of tag names |

## Contribute

Please file feature requests and bugs at the [issue tracker](https://github.com/powerticmkt/dart-mautic-tracking-api/issues).
