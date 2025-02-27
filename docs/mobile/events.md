<!--- Hugo front matter used to generate the website version of this page:
linkTitle: Events
--->

# Semantic conventions for mobile events

**Status**: [Development][DocumentStatus]

This document defines semantic conventions for instrumentations that emit
events on mobile platforms. All mobile events MUST use a namespace of
`device` in the EventName LogRecord property.

<!-- toc -->

- [Lifecycle instrumentation](#lifecycle-instrumentation)
  - [Device app lifecycle event](#device-app-lifecycle-event)

<!-- tocstop -->

## Lifecycle instrumentation

This section defines how to apply semantic conventions when instrumenting
application lifecycle.

### Device app lifecycle event

<!-- semconv event.device.app.lifecycle -->
<!-- NOTE: THIS TEXT IS AUTOGENERATED. DO NOT EDIT BY HAND. -->
<!-- see templates/registry/markdown/snippet.md.j2 -->
<!-- prettier-ignore-start -->
<!-- markdownlint-capture -->
<!-- markdownlint-disable -->

**Status:** ![Development](https://img.shields.io/badge/-development-blue)

The event name MUST be `device.app.lifecycle`.

This event represents an occurrence of a lifecycle transition on Android or iOS platform.

The event body fields MUST be used to describe the state of the application at the time of the event.
This event is meant to be used in conjunction with `os.name` [resource semantic convention](/docs/resource/os.md) to identify the mobile operating system (e.g. Android, iOS).
The `android.state` and `ios.state` fields are mutually exclusive and MUST NOT be used together, each field MUST be used with its corresponding `os.name` value.

**Body fields:**

| Body Field  | Type | Description  | Examples  | [Requirement Level](https://opentelemetry.io/docs/specs/semconv/general/attribute-requirement-level/) | Stability |
|---|---|---|---|---|---|
| `android.state` | enum | This attribute represents the state the application has transitioned into at the occurrence of the event. [1] | `created` | `Conditionally Required` if and only if `os.name` is `android` | ![Development](https://img.shields.io/badge/-development-blue) |
| `ios.state` | enum | This attribute represents the state the application has transitioned into at the occurrence of the event. [2] | `active` | `Conditionally Required` if and only if `os.name` is `ios` | ![Development](https://img.shields.io/badge/-development-blue) |

**[1]:** The Android lifecycle states are defined in [Activity lifecycle callbacks](https://developer.android.com/guide/components/activities/activity-lifecycle#lc), and from which the `OS identifiers` are derived.

**[2]:** The iOS lifecycle states are defined in the [UIApplicationDelegate documentation](https://developer.apple.com/documentation/uikit/uiapplicationdelegate), and from which the `OS terminology` column values are derived.

`android.state` has the following list of well-known values. If one of them applies, then the respective value MUST be used; otherwise, a custom value MAY be used.

| Value  | Description | Stability |
|---|---|---|
| `background` | Any time after Activity.onPause() or, if the app has no Activity, Context.stopService() has been called when the app was in the foreground state. | ![Development](https://img.shields.io/badge/-development-blue) |
| `created` | Any time before Activity.onResume() or, if the app has no Activity, Context.startService() has been called in the app for the first time. | ![Development](https://img.shields.io/badge/-development-blue) |
| `foreground` | Any time after Activity.onResume() or, if the app has no Activity, Context.startService() has been called when the app was in either the created or background states. | ![Development](https://img.shields.io/badge/-development-blue) |

`ios.state` has the following list of well-known values. If one of them applies, then the respective value MUST be used; otherwise, a custom value MAY be used.

| Value  | Description | Stability |
|---|---|---|
| `active` | The app has become `active`. Associated with UIKit notification `applicationDidBecomeActive`. | ![Development](https://img.shields.io/badge/-development-blue) |
| `background` | The app is now in the background. This value is associated with UIKit notification `applicationDidEnterBackground`. | ![Development](https://img.shields.io/badge/-development-blue) |
| `foreground` | The app is now in the foreground. This value is associated with UIKit notification `applicationWillEnterForeground`. | ![Development](https://img.shields.io/badge/-development-blue) |
| `inactive` | The app is now `inactive`. Associated with UIKit notification `applicationWillResignActive`. | ![Development](https://img.shields.io/badge/-development-blue) |
| `terminate` | The app is about to terminate. Associated with UIKit notification `applicationWillTerminate`. | ![Development](https://img.shields.io/badge/-development-blue) |

<!-- markdownlint-restore -->
<!-- prettier-ignore-end -->
<!-- END AUTOGENERATED TEXT -->
<!-- endsemconv -->

[DocumentStatus]: https://opentelemetry.io/docs/specs/otel/document-status
