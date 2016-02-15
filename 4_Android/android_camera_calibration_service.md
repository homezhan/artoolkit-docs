#Camera Calibration Service
Every device uses a different camera, and each of these cameras have variables which affect the ability of ARToolKit (and all computer vision) to work properly. The camera calibration service is a cloud-and-crowd-based solution to generating and retrieving these camera-specific variables.

##What Information is Collected?
This service does not store or transmit any personally identifying information.

If a network connection is available, the following information may be transmitted to an ARToolworks server for the purpose of retrieving camera calibration information for your specific Android device:

-   The make and model of device (e.g. Samsung Galaxy S).
-   Which camera on the device is being used.

No personally identifying data is transmitted or stored during any part of the process. Additionally, the data is transferred via a secure HTTPS connection.

##Requirements
The camera calibration service has a few requirements to use. Namely, internet.

###Library Linkage
#### ARToolKit for Android v5.3.1 and later.
All apps running the camera calibration service depend on native library libcurl. As of ARToolKit v5.3.1, libcurl and its dependencies libssl and libcrypto are supplied as a statically linked library. Applications that link to ARBaseLib or libARWrapper will automatically load these dependencies.

#### ARToolKit for Android v4.x - v5.3
All apps running the camera calibration service depend on native library libcurl. In ARToolKit v4.x - v5.3.0, libcurl and its dependencies libcrypto and libssl are supplied as dynamic libraries. Applications that link to ARBaseLib will automatically load these dependencies, but other examples not based on ARBaseLib must add these loadLibrary calls, ideally in a subclass of Android.Application or Android.Activity:
<pre>
    System.loadLibrary("crypto");
    System.loadLibrary("ssl");
    System.loadLibrary("curl");
</pre>

###Manifest
<pre>
    <uses-permission android:name="android.permission.CAMERA" />
    <uses-permission android:name="android.permission.INTERNET" />
    <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
    <uses-feature android:name="android.hardware.camera.any" />
    <uses-feature android:name="android.hardware.camera" android:required="false" />
    <uses-feature android:name="android.hardware.camera.autofocus" android:required="false" />
    <uses-feature android:glEsVersion="0x00010100" />
</pre>

##How do I Contribute to the Service?
Currently, the service is used exclusively on the Android platform through the [Camera Calibration App for Android][calib_app].

[calib_app]: 4_Android:android_camera_calibration
