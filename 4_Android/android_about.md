#ARToolKit for Android
ARToolKit is a computer vision library that provides the tracking functionality required to build augmented reality applications. It has been ported to various hardware and software platforms, with recent focus specifically on the mobile domain.

This section of the ARToolKit support library describes the port of ARToolKit to the [Android][android] mobile platform. Android is an open-source software stack for mobile devices that provides the operating system, as well as middleware, key applications and APIs. In addition to the appeal of the open environment, Android has also seen an increasing consumer market share, making it an attractive platform for commercial apps and advertising.

For application development, Android offers a rich [SDK][sdk] and development tools, based around the Java programming language. While Java is sufficient for the majority of applications, the JNI framework (Java Native Interface) can be used to implement parts of a Java application in C/C++. The [NDK][ndk] (Native Development Kit) provides the necessary tools, headers and libraries to take advantage of JNI on Android. There are two major motivations for using native code: to potentially increase performance, and to reuse existing C/C++ libraries. In the case of porting ARToolKit to Android, both of these motivations come into play.

The first section, *ARToolKit's SDK Structure* link below, covers the structure of ARToolKit and how to use it to develop your own augmented reality applications on Android. The SDK offers several different development paths, depending on the developer’s preference for Java or native coding. A certain amount of prior knowledge of Android development is essential, and assumed.

##Index

- [ARToolKit's SDK Structure][android_sdk]
- [Example Applications][android_examples]
- [Developing with ARToolKitWrapper and ARBaseLib][android_developing]
- [Native Development Information][android_native]
- [Camera Preferences][android_preferences_activity]
- [Using Automatic Online Camera Calibration Retrieval][android_camera_calibration_service]
- [ARToolKit Camera Calibration for Android][android_camera_calibration] - [View in Google Play Store][camera_calibration]
- [Codex Interactivus for Android][example_codex_interactivus] - [View in Google Play Store][codex_interactivus]
- [Advanced Device-Specific Setup - Epson Moverio BT-200][android_bt]

[android_sdk]: 4_Android:android_sdk
[android_examples]: 4_Android:android_examples
[android_developing]: 4_Android:android_developing
[android_native]: 4_Android:android_native
[android_preferences_activity]: 4_Android:android_preferences_activity
[android_camera_calibration_service]: 4_Android:android_camera_calibration_service
[android_bt]: 4_Android:android_bt-200
[android_camera_calibration]: 4_Android:android_camera_calibration
[example_codex_interactivus]: 7_Examples:example_codex_interactivus

[camera_calibration]: https://play.google.com/apps/testing/com.artoolworks.ar.utils.calib_camera
[codex_interactivus]: https://play.google.com/store/apps/details?id=com.artoolworks.CodexInteractivus
[android]: http://developer.android.com/index.html
[sdk]: http://developer.android.com/sdk/index.html
[ndk]: http://developer.android.com/sdk/ndk/overview.html
