# NearDropPlusPlus
**NearDropPlusPlus** is a partial implementation of [Google's Nearby Share](https://blog.google/products/android/nearby-share/)/Quick Share for macOS.

The app lives in your menu bar and saves files to your downloads folder. It's that simple, really.

It is based on [NearDrop](https://github.com/grishka/NearDrop) by [grishka](https://github.com/grishka).

[Protocol documentation](/PROTOCOL.md) is available separately.

## Why "PlusPlus" ?
It contains many enhancements built by other community members that are not accepted by the original creator.

Grishka, the original creator of this project, made a distinction between *open-source* and *community-driven*, as in, the community around an open-source project does not necessarily get to decide how it develops and what features it has (https://github.com/grishka/NearDrop/pull/127#issuecomment-2029534303). Based on this, grishka has rejected many contributions that added more features to the project.

This is an important distinction, and I totally agree with grishka. I also fully respect the decision of limiting what PRs get to be accepted. On the other hand, it's unfortunate to see community member's effort of improving the project not being accepted and scattered across multiple repos/PRs. Hence, I created this fork to combine some of the enhancements built by other community members into one.

### List of Enhancements

#### Text, phone number and URL sharing

Author: [@d4rk-lucif3r](https://github.com/d4rk-lucif3r)
Source: [Repository](https://github.com/d4rk-lucif3r/NearDrop)

#### Version info menu item

Author: [@Jaehwa-Noh](https://github.com/Jaehwa-Noh)
Source: [Repository](https://github.com/Jaehwa-Noh/NearDrop)

#### Preference options 

Author: [@krispykalsi](https://github.com/krispykalsi)
Source: [Repository](https://github.com/krispykalsi/NearDrop/tree/text-and-links)

#### Remember devices

Author: [@neorth](https://github.com/neorth)
Source: [Repository](https://github.com/neorth/NearDrop/tree/remember-devices)

## Limitations

* **Wi-Fi LAN only**. Your Android device and your Mac need to be on the same network for this app to work. Google's implementation supports multiple mediums, including Wi-Fi Direct, Wi-Fi hotspot, Bluetooth, some kind of 5G peer-to-peer connection, and even a WebRTC-based protocol that goes over the internet through Google servers. Wi-Fi direct isn't supported on macOS (Apple has their own, incompatible, AWDL thing, used in AirDrop). Bluetooth needs further reverse engineering.
* **Visible to everyone on your network at all times** while the app is running. Limited visibility (contacts etc) requires talking to Google servers, and becoming temporarily visible requires listening for whatever triggers the "device nearby is sharing" notification.

## Installation

Download the latest build from the releases section, unzip, move to your applications folder. When running for the first time, right-click the app and select "Open", then confirm running an app from unidentified developer.

If you want the app to start on boot, [follow these steps to add NearDrop as a login item.](https://support.apple.com/guide/mac-help/open-items-automatically-when-you-log-in-mh15189/mac)

#### Installation with Homebrew

This is for original NearDrop only.

```
brew install --no-quarantine grishka/grishka/neardrop
```

## Contributing

You are welcome to submit your own pull reqests or suggest any forks/PRs.

But, please note:

* Try to follow common patterns.
* Always document your PR.
* PR that only make minor changes to readme will not be accepted.

Also, by contributing to this project, you agree the following statement:
> I dedicate any and all copyright interest in this software to the public domain. I make this dedication for the benefit of the public at large and to the detriment of my heirs and successors. I intend this dedication to be an overt act of relinquishment in perpetuity of all present and future rights to this software under copyright law.


## FAQ

#### The app would not open because "Apple cannot check it for malicious software", you gotta fix your shit

Right-click the app in Finder and select "Open". Or, open System Settings -> Privacy and security, scroll down and allow the app to run.

#### My Android device doesn't see my Mac

Make sure both devices are on the same Wi-Fi network. Local network communication may not work on some public networks — for example, in coffee shops or hotels. If you're on your own network, check your router settings to make sure it's not blocking local devices from talking to each other.

#### How do I send files?

Right-click a file in Finder, select Share, then select NearDrop.

#### How do I send links?

From the menu bar: File -> Share -> NearDrop. Safari also has a share button on the toolbar.

#### My Mac doesn't see my Android device

Unfortunately, Android listens for specific BLE (Bluetooth Low Energy) broadcasts to automatically become visible, and macOS doesn't allow apps to send them.

##### Samsung devices

After the Quick Share update, [there's currently no known workaround for this problem](https://github.com/grishka/NearDrop/issues/152). Subscribe to that issue to get notified if/when one becomes available.

##### Non-Samsung devices

As a workaround, you have to open the "Google Files" and tap "Receive" on the "Nearby Share" tab.

To make it more easily accessible and/or if you don't want to install Google Files, you can use an app like [one of these](https://forum.xda-developers.com/t/how-to-manually-create-a-homescreen-shortcut-to-a-known-unique-android-activity.4336833/) to create a shortcut to launch one of these activity intents:

- Option 1:
  - Action: `com.google.android.gms.RECEIVE_NEARBY`
  - Mime type: `*/*`
- Option 2:
  - Component name: `com.google.android.gms/.nearby.sharing.ReceiveSurfaceActivity`

#### Can the menu bar icon be removed?

Yes. Drag the icon off the menu bar while holding cmd. To bring it back, launch the app a second time, while it's already running.

#### I'm sending something to my Mac, the Android device displays a PIN code, but nothing happens on the Mac

Make sure you have "do not disturb" off. The notification may also sometimes (rarely) end up in the notification center without being shown as a popup first — I'm not sure why this happens.

#### Why not the other way around, i.e. AirDrop on Android?

While I am an Android developer, and I have looked into this, this is nigh-impossible. AirDrop uses [AWDL](https://stackoverflow.com/questions/19587701/what-is-awdl-apple-wireless-direct-link-and-how-does-it-work), Apple's own proprietary take on peer-to-peer Wi-Fi. This works on top of 802.11 itself, the low-level Wi-Fi protocol, and thus can not be implemented without messing around with the Wi-Fi adapter drivers and raw packets and all that. It might be possible on Android, but it would at the very least require root and possibly a custom kernel. There is [an open-source implementation of AWDL and AirDrop for Linux](https://owlink.org/code/).

#### Similar Projects
[rquickshare](https://github.com/Martichou/rquickshare)
