# Using Automative Online Camera Calibration Retrieval

ARToolKit 5.1 introduces a significant new feature on Android, fetching of camera calibration data from an ARToolworks-provided server. On request, ARToolworks provides developers access to an on-device verson of calib_camera which submits calibration data to ARToolworks' server, making it available to all users of that device.

The underlying changes to support this include a native version of libARvideo for Android which provides the functions to fetch camera calibration data (note that libARvideo on Android does not handle frame retrieval from the camera; that still happens on the Java side).

## Changes required in current ARToolKit for Android apps

Existing native apps which wish to use the functionality should follow the example usage from the ARNative example, and also link against libarvideo, and its additional dependencies libcurl, libssl and libcrypto.

### Change in library linkage

All examples now depend on native library libcurl, and its dependencies libcrypto and libssl. Applications which link to ARBaseLib will automatically load these dependencies, but other examples not based on ARBaseLib must now add these loadLibrary calls, ideally in a subclass of Android.Application or Android.Activity:

<pre>
System.loadLibrary("crypto");
System.loadLibrary("ssl");
System.loadLibrary("curl");
</pre>

### Changes to Java API

As part of these changes, the interface for <pre>com.artoolworks.ar.base.camera.CameraEventListener.cameraPreviewStarted()</pre> and <pre>com.artoolworks.ar.base.ARToolKit.initialiseAR()</pre> have changed. Two new parameters have been added.

-   <pre>cameraIndex</pre> Zero-based index of the camera in use. If only one camera is present, will be 0.
-   <pre>cameraIsFrontFacing</pre> false if camera is rear-facing (the default) or true if camera is facing toward the user.

Users who have implemented CameraEventListener in their own classes are advised to take a look at <pre>com.artoolworks.ar.base.ARActivity</pre>'s implementation for usage.

### Changes to manifest

All examples now require permission to access the Internet and to check network state. A typical permissions block in an ARToolKit-based application looks like:
<pre>
<uses-permission android:name="android.permission.CAMERA" />
<uses-permission android:name="android.permission.INTERNET" />
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
<uses-feature android:name="android.hardware.camera.any" />
<uses-feature android:name="android.hardware.camera" android:required="false" />
<uses-feature android:name="android.hardware.camera.autofocus" android:required="false" />
<uses-feature android:glEsVersion="0x00010100" />
</pre>