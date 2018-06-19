# Distributed and Remote Notifications

[![travis-badge][]][travis] [![release-badge][]][cargo] [![docs-badge][]][docs] [![license-badge][]][license]

Synchronize and deliver notifications across all of your computers and mobile
devices.


## Current Status

Nothing working at all yet, don't bother trying anything.


## Infrastructure

A typical deployment consists of a personal AWS SQS queue used to distribute
notifications to the various listening devices. Notifications can be privately
encrypted using a symmetric shared key stored only on your devices. AWS SNS can
also be used for more complicated fan-out setups or delivery via SMS, email, etc.

### Hosted Service

A future goal is to host a service (or integrate with an existing one) to
eliminate the need to set up your own infrastructure. A simple server to run as
an alternative to using AWS would also be great.


## Components

### Notification Sender

A [`notify-send`](http://manpages.ubuntu.com/manpages/xenial/man1/notify-send.1.html)
style application that creates notifications to be delivered to any subscribed
devices. This can be easily integrated into scripts and other applications in
order to generate remote notifications.

### Notification Monitor

On graphical systems that already run a traditional notification daemon, this
monitor will snoop for shown notifications and send them out to be mirrored on
your other devices.

Currently this only supports systems using libnotify - macOS can probably be
done using private APIs or some other hooks, and Windows can use the [notification listener](https://docs.microsoft.com/en-us/windows/uwp/design/shell/tiles-and-notifications/notification-listener).
An iOS tweak or Android support would be a great way to send SMS or iMessage
notifications on a PC.

### libnotify Daemon

On headless systems that generate notifications, this daemon will listen for
libnotify notifications and send them out to be delivered to other devices. You
might run this on a server hosting weechat as an example.

### Notification Client

Running on any devices you own, the client subscribes to notifications and sends
them off to your local notification server to display remote notifications
locally. Alternatively, notifications can be sent to external push notification
services to be displayed on a mobile device.


[travis-badge]: https://img.shields.io/travis/arcnmx/notificate/master.svg?style=flat-square
[travis]: https://travis-ci.org/arcnmx/notificate
[release-badge]: https://img.shields.io/crates/v/notificate-core.svg?style=flat-square
[cargo]: https://crates.io/crates/notificate-core
[docs-badge]: https://img.shields.io/badge/API-docs-blue.svg?style=flat-square
[docs]: http://arcnmx.github.io/notificate/notificate_core/
[license-badge]: https://img.shields.io/badge/license-MIT-ff69b4.svg?style=flat-square
[license]: https://github.com/arcnmx/notificate/blob/master/COPYING
