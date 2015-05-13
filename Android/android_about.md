#ARToolKit for Android
ARToolKit is a computer vision library that provides the tracking functionality required to build augmented reality applications. It has been ported to various hardware and software platforms, with recent focus specifically on the mobile domain.

This section of the ARToolKit support library describes the port of ARToolKit to the [Android][android] mobile platform. Android is an open-source software stack for mobile devices that provides the operating system, as well as middleware, key applications and APIs. In addition to the appeal of the open environment, Android has also seen an increasing consumer market share, making it an attractive platform for commercial apps and advertising.

For application development, Android offers a rich [SDK][sdk] and development tools, based around the Java programming language. While Java is sufficient for the majority of applications, the JNI framework (Java Native Interface) can be used to implement parts of a Java application in C/C++. The [NDK][ndk] (Native Development Kit) provides the necessary tools, headers and libraries to take advantage of JNI on Android. There are two major motivations for using native code: to potentially increase performance, and to reuse existing C/C++ libraries. In the case of porting ARToolKit to Android, both of these motivations come into play.

This guide covers the [structure][2] of ARToolKit and how to use it to develop your own augmented reality applications on Android. The SDK offers several different development paths, depending on the developer’s preference for Java or native coding. A certain amount of prior knowledge of Android development is essential, and assumed.


##Index

- [ARToolKit's SDK Structure][android_sdk]
- [Example Applications][android_examples]
- [Developing with ARToolKitWrapper and ARBaseLib][android_developing]
- [Native Development Information][android_native]
- [Camera Preferences][android_preferences_activity]
- [Using automatic online camera calibration retrieval][android_camera_calibration_service]
- [ARToolKit Camera Calibration for Android][android_camera_calibration] - [View in Google Play Store][camera_calibration]
- [Codex Interactivus for Android][example_codex_interactivus] - [View in Google Play Store][codex_interactivus]
- [Advanced Device-Specific Setup - Epson Moverio BT-200][android_bt]

[android_sdk]: Android:android_sdk
[android_examples]: Android:android_examples
[android_developing]: Android:android_developing
[android_native]: Android:android_native
[android_preferences_activity]: Android:android_preferences_activity
[android_camera_calibration_service]: Android:android_camera_calibration_service
[android_bt]: Android:android_bt-200
[android_camera_calibration]: Android:android_camera_calibration
[example_codex_interactivus]: Examples:example_codex_interactivus

[camera_calibration]: https://play.google.com/apps/testing/com.artoolworks.ar.utils.calib_camera
[codex_interactivus]: https://play.google.com/store/apps/details?id=com.artoolworks.CodexInteractivus
[android]: http://developer.android.com/index.html
[sdk]: http://developer.android.com/sdk/index.html
[ndk]: http://developer.android.com/sdk/ndk/overview.html
