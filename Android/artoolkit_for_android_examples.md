#ARToolkit for Android Examples

ARToolKit for Android includes a number of fully-working examples that demonstrate basic and advanced techniques. You can copy and build on the examples to create your own application.

The examples are divided into 3 sets.

1.  Java-based: examples where all user-developed code is in Java, and is based on the provided ARBaseLib classes.
2.  Mixed Java/C/C++: examples where user-developed code is split between the Java environment and native C/C++ (NDK) environment. Code can use the provided ARBaseLib java classes while also addressing ARToolKit in C/C++ via the libARWrapper C/C++ API.
3.  C/C++-based: examples where most of the user-developed code is native C/C++ (NDK). These examples offer the greatest power to the AR developer and direct access to the full native ARToolKit API.

The examples are as follows:

### Java-based

-   ARSimple: An example that extends the ARActivity class in ARBaseLib to create a simple augmented reality application.
-   ARSimpleInteraction: An example that adds simple interaction to ARSimple.

### Mixed Java/C/C++

-   ARSimpleNative: An example that uses an additional native library to perform rendering in C rather than Java.
-   ARSimpleNativeCars: An example that uses a native OBJ model loader.

### AR and rendering code in C/C++

-   ARNative: An example that uses the ARToolKit libraries directly and renders with OpenGL.
-   ARNativeOSG: An example that uses the ARToolKit libraries directly and loads and renders 3D model content using the advanced OpenSceneGraph framework.
-   nftSimple: An example that performs NFT (texture tracking) and renders with OpenGL.
-   nftBook: An example that performs NFT (texture tracking) and loads and renders 3D model content using the advanced OpenSceneGraph framework.
-   ARMovie: An example that performs NFT (texture tracking) and loads and renders 2D video content on devices running Android 4.0.3 and later.

### ARNative

Loads marker names from a configuration file. (Square markers only.) The tracking will automatically be set to match the types of square markers (template (pictorial) vs. matrix (barcode)) used in the configuration file. It is not recommended that template and matrix markers are mixed in the same application, as this lowers the tracking reliability of both types.

### ARNativeOSG

Loads marker names from a configuration file. (Square markers only.) The tracking will automatically be set to match the types of square markers (template (pictorial) vs. matrix (barcode)) used in the configuration file. It is not recommended that template and matrix markers are mixed in the same application, as this lowers the tracking reliability of both types.

Management of OSG objects is encapsulated in a C-pseudoclass named VirtualEnvironment, which in turn acts through the API offered by the ARosg library. ARosg contains a reasonable amount of functionality for manipulating the scene graph. See the [API documentation for libARosg](http://www.artoolworks.com/support/doc/artoolkit4/apiref/arosg_h/index.html).

### nftSimple

Loads NFT dataset names from a configuration file.

The example uses the "Pinball.jpg" image supplied in the "Misc/patterns" folder. ARToolKit NFT requires a fast device, preferably dual-core for good operation, e.g. Samsung Galaxy SII or similar. Build/deployment for Android API 9 (Android OS v2.3) or later is recommended. 

### nftBook

Loads NFT dataset names from a configuration file.

The example uses the "Pinball.jpg" image supplied in the "Misc/patterns" folder. ARToolKit NFT requires a fast device, preferably dual-core for good operation, e.g. Samsung Galaxy SII or similar. Build/deployment for Android API 9 (Android OS v2.3) or later is recommended.

Management of OSG objects is encapsulated in a C-pseudoclass named VirtualEnvironment, which in turn acts through the API offered by the ARosg library. ARosg contains a reasonable amount of functionality for manipulating the scene graph. See the [API documentation for libARosg](http://www.artoolworks.com/support/doc/artoolkit4/apiref/arosg_h/index.html).

### ARMovie

Shows an example of playback of a video file on a marker surface. The example is NDK (native)-based. Movie playback is only supported by Android OS v4.0 ("Ice Cream Sandwich") and later (Android API level 14), and support varies in quality and reliability from device to device. It is highly recommended that you provide alternate playback mechanisms for devices where playback in the AR environment cannot proceed, e.g. full screen playback.
