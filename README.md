# SecCamAndroidTV

An Android TV application for viewing compatible NVR cameras over a local network. It supports up to 16 channels in the interface, side-by-side, stacked and grid layouts, fullscreen viewing and automatic reconnection. Actual capacity depends on the NVR, network and TV.

The connection uses the RTSP substream format of Xiongmai/XMeye NVRs; other protocols and devices require testing. Configure the IP address, port, username and password in the app. The password is encrypted using Android Keystore. Credentials are used in the RTSP connection, so use a trusted network.

The application ID is retained to allow updates to previous installations when signed with the same key. Available NVR sessions are shared with other devices.

This project's code uses the [MIT License](LICENSE). Review [THIRD_PARTY.md](THIRD_PARTY.md) for the licenses of bundled components before distributing an APK.

## Build

Open this directory in Android Studio with JDK 17 and Android SDK 36, or run:

```sh
./gradlew :app:assembleDebug
```

The debug APK is generated under `app/build/outputs/apk/debug/`, unless `CAMTV_BUILD_DIR` is set. An unsigned release can be generated with `./gradlew :app:assembleRelease`. To update an existing installation, sign it with the same key used for the previous installation; do not share the key.

`org.videolan.android:libvlc-all:3.7.7` is downloaded from the repositories configured in Gradle. The app supports ARMv7 and ARM64 on Android 8.0 or newer. Video decoding capacity varies by TV.

## Local tests

```sh
mkdir -p /tmp/camtv-tests
javac -encoding UTF-8 -d /tmp/camtv-tests app/src/main/java/br/com/camxp/tv/Model.java tests/ModelTest.java
java -cp /tmp/camtv-tests br.com.camxp.tv.ModelTest
```

Model tests do not replace testing playback, layouts, recovery and remote navigation on a real device.
