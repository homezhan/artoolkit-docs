#Android Examples
ARToolKit includes a number of fully-working examples on Android that demonstrate basic and advanced techniques. You can copy and build on the examples to create your own application. Each app is built against a selected API level of the Android SDK Platform and does not have dependencies on Google APIs. The ARToolKit SDK example apps are in the process of being upgraded to be built over the latest and greatest Android SDK Platform API level. However, the example apps will likely lag behind as newer Android SDK Platforms are released. Coming soon - the example apps projects are being migrated to the Android Studio integrated development environment (IDE) from the Eclipse projects.

The examples are divided into 3 sets.

1.  All Java-based: examples where all user-developed code is in Java, and is based on the provided ARBaseLib classes.
2.  Mixed Java and native C/C++ using Android NDK: examples where user-developed code is split between the Java environment and native C/C++ environment. Code can use the provided ARBaseLib java classes while also addressing ARToolKit in C/C++ via the libARWrapper C/C++ API.
3.  AR and rendering code in native C/C++ using Android NDK: examples where most of the user-developed code is native C/C++. These examples offer the greatest power to the AR developer and direct access to the full native ARToolKit API.

The examples are as follows:

##All Java-based

-   **ARSimple**: An example that extends the ARActivity class in ARBaseLib to create a simple augmented reality application.
-   **ARSimpleInteraction**: An example that adds simple interaction to ARSimple.
-   **ARMulti**: An example that shows how to configure and usenmulti marker tracking.
-   **ARDistanceOpenGLES20**: An example on how to measure the distance and draw a line between two markers. The line is drawn using OpenGL ES 2.0 library features.
-   **ARMarkerDistance**: An example on how to measure the distance and draw a line between two markers. The lin is drawn using OpenGL ES 1.0 library features.
-   **ARSimpleOpenGLES20**: Pretty much the same as ARSimple with the extension of using OpenGL ES 2.0 features for drawing and coloring the cube.

##Mixed Java and Native C/C++ Using Android NDK

-   **ARSimpleNative**: An example that uses an additional native library to perform rendering in C rather than Java.
-   **ARSimpleNativeCars**: An example that uses a native OBJ model loader.

##AR and Rendering Code in Native C/C++ Using Android NDK

-   **ARNative**: An example that uses the ARToolKit libraries directly and renders with OpenGL ES 2.0.
-   **ARNativeES1**: An example that uses the ARToolKit libraries directly and renders with OpenGL ES 1.0.
-   **ARNativeOSG**: An example that uses the ARToolKit libraries directly and loads and renders 3D model content using the advanced OpenSceneGraph framework.
-   **nftSimple**: An example that performs NFT (texture tracking) and renders with OpenGL.
-   **nftBook**: An example that performs NFT (texture tracking) and loads and renders 3D model content using the advanced OpenSceneGraph framework.
-   **ARMovie**: An example that performs NFT (texture tracking) and loads and renders 2D video content on devices running Android 4.0.3 and later.

####ARNative
Loads marker names from a configuration file. (Square markers only.) The tracking will automatically be set to match the types of square markers (template (pictorial) vs. matrix (barcode)) used in the configuration file. It is not recommended that template and matrix markers are mixed in the same application, as this lowers the tracking reliability of both types.

####ARNativeOSG
Loads marker names from a configuration file. (Square markers only.) The tracking will automatically be set to match the types of square markers (template (pictorial) vs. matrix (barcode)) used in the configuration file. It is not recommended that template and matrix markers are mixed in the same application, as this lowers the tracking reliability of both types.

Management of OSG objects is encapsulated in a C-pseudoclass named VirtualEnvironment, which in turn acts through the API offered by the ARosg library. ARosg contains a reasonable amount of functionality for manipulating the scene graph. See the [API documentation for libARosg][1].

####nftSimple
Loads NFT dataset names from a configuration file.

The example uses the "Pinball.jpg" image supplied in the "Misc/patterns" folder. ARToolKit NFT requires a fast device, preferably dual-core for good operation, e.g. Samsung Galaxy SII or similar. Build/deployment for Android API 9 (Android OS v2.3) or later is recommended.

####nftBook
Loads NFT dataset names from a configuration file.

The example uses the "Pinball.jpg" image supplied in the "Misc/patterns" folder. ARToolKit NFT requires a fast device, preferably dual-core for good operation, e.g. Samsung Galaxy SII or similar. Build/deployment for Android API 9 (Android OS v2.3) or later is recommended.

Management of OSG objects is encapsulated in a C-pseudoclass named VirtualEnvironment, which in turn acts through the API offered by the ARosg library. ARosg contains a reasonable amount of functionality for manipulating the scene graph. See the [API documentation for libARosg][1].

####ARMovie
Shows an example of playback of a video file on a marker surface. The example is NDK (native)-based. Movie playback is only supported by Android OS v4.0 ("Ice Cream Sandwich") and later (Android API level 14), and support varies in quality and reliability from device to device. It is highly recommended that you provide alternate playback mechanisms for devices where playback in the AR environment cannot proceed, e.g. full screen playback.

[1]: http://www.artoolworks.com/support/doc/artoolkit5/apiref/arosg_h/index.html