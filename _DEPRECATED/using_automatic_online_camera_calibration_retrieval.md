
###Library Linkage
All examples depend on native library libcurl, and its dependencies libcrypto and libssl. Applications which link to ARBaseLib will automatically load these dependencies, but other examples not based on ARBaseLib must now add these loadLibrary calls, ideally in a subclass of Android.Application or Android.Activity:
<pre>
    System.loadLibrary("crypto");
    System.loadLibrary("ssl");
    System.loadLibrary("curl");
</pre>

###Java API
The interface for `com.artoolworks.ar.base.camera.CameraEventListener.cameraPreviewStarted()` and `com.artoolworks.ar.base.ARToolKit.initialiseAR()` have changed. Two new parameters have been added.

-   <pre>cameraIndex</pre> Zero-based index of the camera in use. If only one camera is present, will be 0.
-   <pre>cameraIsFrontFacing</pre> false if camera is rear-facing (the default) or true if camera is facing toward the user.

Users who have implemented CameraEventListener in their own classes are advised to take a look at `org.artoolkit.ar.base.ARActivity`'s implementation for usage.

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