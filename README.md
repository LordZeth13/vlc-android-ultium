# VLC for GM Ultium Head Units

This is an uofficial port of [VLC Player](https://videolan.org/vlc/) for the GM Ultium 17.7" head unit. The user interface has been optimized for the head unit screen, improving the user experience. It also resolves some crashes specific to the head unit.

VLC on the head unit plays all the same files as the classical version of VLC, and features a media database
for Audio and Video files and stream.

## Installation Instructions

- Download the APK from the Release page and copy it to a USB drive
- Plug the USB drive into your vehicle and download AnExplorer from the head unit's Google Play store
- AnExplorer. A popup will appear prompting you to grant it permission. Give it the permissions it asks for.
- Your USB drive should be displayed in the AnExplorer page. Click on it. The application will prompt you for permission again.
- Navigate to the directory on your drive with the APK.
- Once you see your APK file, there should be an expand icon in the top right of the tile. Click on that.
- This should create a sequence of popups that prompt you to confirm installing the app.
- Once complete, VLC Player will be on your vehicle.

## Project Structure

Here are the current folders of vlc-android project:

- extension-api : Application extensions SDK (not released yet)
- application : Android application source code, organized by modules.
- buildsystem : Build scripts, CI and maven publication configuration
- libvlc : LibVLC gradle module, VLC source code will be cloned in `vlc/` at root level.
- medialibrary : Medialibrary gradle module

## LibVLC

LibVLC is the Android library embedding VLC engine, which provides a lot of multimedia features, like:

- Play every media file formats, every codec and every streaming protocols
- Hardware and efficient decoding on every platform, up to 8K
- Network browsing for distant filesystems (SMB, FTP, SFTP, NFS...) and servers (UPnP, DLNA)
- Playback of Audio CD, DVD and Bluray with menu navigation
- Support for HDR, including tonemapping for SDR streams
- Audio passthrough with SPDIF and HDMI, including for Audio HD codecs, like DD+, TrueHD or DTS-HD
- Support for video and audio filters
- Support for 360 video and 3D audio playback, including Ambisonics
- Ability to cast and stream to distant renderers, like Chromecast and UPnP renderers.

And more.

![LibVLC stack](https://images.videolan.org/images/libvlc_stack.png)

You can use our LibVLC module to power your own Android media player.
Download the `.aar` directly from [Maven](https://search.maven.org/artifact/org.videolan.android/libvlc-all) or build from source.

Have a look at our [sample codes](https://code.videolan.org/videolan/libvlc-android-samples).

## License

VLC for Android is licensed under [GPLv2 (or later)](COPYING). Android libraries make this, de facto, a GPLv3 application.

VLC engine *(LibVLC)* for Android is licensed under [LGPLv2](libvlc/COPYING.LIB).

## Build

Native libraries are published on bintray. So you can:

- Build the application and get libraries via gradle dependencies (JVM build only)
- Build the whole app (LibVLC + Medialibrary + Application)
- Build LibVLC only, and get an .aar package

### Build Application

To build the project, you will need:

- [OpenJDK 21](https://www.openlogic.com/openjdk-downloads)
- [Gradle 8.14.4](https://gradle.org/releases/)

VLC-Android build relies on gradle build modes :

- `Release` & `Debug` will get LibVLC and Medialibrary from Bintray, and build application source code only.
- `SignedRelease` also, but it will allow you to sign application apk with a local keystore.
- `Dev` will build build LibVLC, Medialibrary, and then build the application with these binaries. (via build scripts only)
