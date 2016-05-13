#ARToolKit's SDK Structure on Android
Most applications on Android are developed in Java, and Android provides a rich framework of classes to support this. It is, however, also possible to develop parts of an application in native C/C++ code using the Android NDK. This is intended for accessing existing C/C++ codebases or potentially optimizing performance critical functions.
 
The general approach is to build a native C/C++ shared library containing functions that are exposed using the JNI naming scheme. A Java application can then load the library and map the native functions to Java methods, which can then be called like any other method in Java.
 
Using this approach it is now possible to create ARToolKit applications on Android. Certain parts of these applications, must be implemented in Java, other parts can be written in C/C++. Therefore, applications will typically be a combination of C/C++, Java, and the “glue” in between.

This SDK includes components in both C/C++ and Java to permit the development of ARToolKit applications on Android. These components include:

-   ARToolKit core modules. These are native static libraries which can be used to build a shared library.
-   ARToolKitWrapper: a C++ wrapper around ARToolKit, providing high level access to ARToolKit functions and marker management, with C and JNI interfaces. This is a native shared library that can be included in an Android application.
-   ARBaseLib: a Java Android library that communicates with ARToolKitWrapper. By using the classes provided ARBaseLib, an Android application gains easy access to the native functionality of ARToolKit.

With these components, several development strategies are possible, ranging in complexity:

-   Native development by creating a new shared library that links to the ARToolKit static libraries.
-   Native development by creating a new shared library that utilizes ARToolKitWrapper.
-   Java development using the provided ARBaseLib (Java) and ARToolKitWrapper (native) libraries.

Note: Regardless of the approach, all applications require some Java components in order to operate as an Android application. For example, the main Activity class, and video capture classes, must be implemented in Java.

Examples that demonstrate basic operation of the SDK, and the various development approaches available, are included. See [ARToolKit for Android examples][1].

##Video Capture on Android
The ARToolKit port includes almost all of the core modules; the notable exception being the video capture module, which in other ARToolKit versions provides a standard interface for accessing video capture on different platforms and hardware.

Android does not currently permit camera access from native code. Instead, only Java code can open the camera and capture frames. Additionally, a live camera preview must be included in the current Activity’s view for frames to be captured. This means that ARToolKit itself cannot initiate video capture, but must instead wait on the Java application to pass video information and frames using JNI.

Therefore, video capture requires coordination between corresponding libraries on either side of JNI. While this forces a slightly fragmented approach, ARToolKitWrapper and ARBaseLib libraries are provided to handle the issue. Alternatively, the ARNative example included in the SDK demonstrates how to pass video independently of these libraries.

##SDK Requirements
This SDK targets devices running Android 2.1 (Eclair) or later.

A working Android development environment with AndroidStudio is required. For native development, the Android NDK is also needed. For more details about native development see [here][android_native]

The SDK is currently tested predominantly on the Mac OSX platform, however we also support development with Windows. Not actively supported but also working is the development with ARToolKit and AndroidStudio on Linux.

A printer will be required to print out markers.

[1]: 4_Android:android_examples
[android_native]: 4_Android:android_native
