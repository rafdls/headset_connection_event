# Headset Connection Event Flutter Plugin

A Flutter plugin to get a headset event.

[![.github/workflows/flutter.yaml](https://github.com/themobilecoder/headset_connection_event/actions/workflows/flutter.yaml/badge.svg)](https://github.com/themobilecoder/headset_connection_event/actions/workflows/flutter.yaml)

_This is a clone of [headset_event](https://github.com/flutter-moum/flutter_headset_event), but with fix on swift errors and bluetooth connection events for Android and iOS_

Migrated to AndroidX

## Current Status

| Platform | Physical Headset | Bluetooth |
| -------- | ---------------- | --------- |
| iOS      | ✅               | ✅        |
| Android  | ✅               | ✅        |

## Usage

To use this plugin, add `headset_connection_event` as a [dependency in your pubspec.yaml file](https://flutter.io/platform-plugins/).

### Example

```dart
    // Import package
    import 'package:headset_connection_event/headset_event.dart';

    // Instantiate it
    HeadsetEvent headsetPlugin = new HeadsetEvent();
    HeadsetState headsetEvent;

    /// if headset is plugged
    headsetPlugin.getCurrentState.then((_val){
      setState(() {
        headsetEvent = _val;
      });
    });

    /// Detect the moment headset is plugged or unplugged
    headsetPlugin.setListener((_val) {
      setState(() {
        headsetEvent = _val;
      });
    });
```

### Android setup

Update `compileSdkVersion` to **33** in your `build.properties` under `app` directory

Make the following changes to your project's main `AndroidManifest.xml` file:

```xml
<activity...
 <!-- ADD THIS BELOW "ACTIVITY" -->
 android:exported="true"





    <!-- ADD THIS "RECEIVER" Element Before </application> -->
  <receiver android:name="flutter.moum.headset_event.HeadsetBroadcastReceiver"
        android:exported="true">
           <intent-filter>
               <action android:name="android.intent.action.HEADSET_PLUG" />
               <action android:name="android.intent.action.MEDIA_BUTTON" />
           </intent-filter>
       </receiver>


  </application>
</manifest>
```

Please see example project AndroidManifest.xml for more information.

Android 12 requires bluetoothConnect permission. You may request it using the following:

```dart
HeadsetPlugin.requestPermission();
```
