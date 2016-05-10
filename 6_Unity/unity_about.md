#ARToolKit for Unity
ARToolKit for Unity is a plugin for the [Unity][unity] game engine that integrates ARToolKit's augmented reality [tracking][marker_about] with Unity's graphical and game development features. ARToolKit is a computer vision library that provides the tracking functionality required to build augmented reality applications, and ARToolKit for Unity extends the tools that content creators are already using, simplifying the process of creating AR applications. With ARToolKit for Unity, creators building games, visualizations, scientific, or marketing applications can easily build interactive AR leveraging Unity's strengths in cross platform support (namely [OS X][unity_on_osx], [Windows][unity_on_windows], [Android][unity_on_android], and [iOS][unity_on_ios]), powerful scripting capabilities, simple drag-and-drop editing, and a strong support community. Furthermore, ARToolKit and Unity work seamlessly so that you can deploy to all four platforms from the same Unity project.

##What does it do?
At the most basic level, what the plugin does is align a virtual camera within Unity with a real-world camera (such as a webcam) relative to a tracked marker target. For example, if you print a marker on a piece of paper and point your webcam at it, the corresponding virtual camera in Unity will "look" at the equivalent spot in the virtual world. If you then place a 3D model in the virtual world, and overlay it on the incoming video, you produce an augmented reality view. See our [Getting Started][unity_getting_started] guide to see how to do just that.

[Unity helicopter photo.][helicopter]

The plugin also manages all aspect of communicating with the camera and presenting the camera image as a video background for video see-through AR applications. It supports mono and stereo cameras, and mono and stereo displays, in either optical- or video see-through configurations.

You do not need to do a single line of scripting to begin working with ARToolKit. It includes [extensions to the Unity editor][unity_scripts] that allow you to configure the required AR objects directly, as well as live in-editor previewing of your AR scene. However for those who want to tightly integrate ARToolKit with their Unity project, full script control is available over all aspects of the functionality, allowing you to dynamically add markers, start and stop tracking, and change parameters.

##Requirements

-   A webcam or other video source supported by ARToolKit.
-   Unity v5.0 or later (tested with 5.2.3 and 5.3.4), for Mac OS X or Windows (development platform). Personal edition is sufficient. 
-   If deploying for Android: Android build support to build a Unity app for the Android platform.
-   If deploying for iOS: iOS build support to build a Unity app for the iOS platform plus Apple's Xcode v4.2 or later.


**Important:**

It is not possible to target iOS or Mac OS X desktop using Unity on a Windows system. 

It is also not possible to target Windows Store, Windows Phone or Windows Universal Platform on a Mac OS X system.

##Index

###User Guide

-   [Getting Started][unity_getting_started]
-   [Script Reference][unity_scripts]
-   [Scripting and Low-Level API][unity_low_level_api]

###Platform-Specific Information

-   [OS X][unity_on_osx]
-   [Windows][unity_on_windows]
-   [Android][unity_on_android]
-   [iOS][unity_on_ios]

###General Information

-   [Unity][unity] website. Get Unity here.
-   [Official Unity Forum][unity_forums] and [Unity Answers][unity_answers] are excellent places to ask questions.

[unity]:http://www.unity3d.com
[unity_forums]:http://forum.unity3d.com/
[unity_answers]:http://answers.unity3d.com/index.html
[unity_low_level_api]: 6_Unity:unity_low_level_api
[unity_getting_started]: 6_Unity:unity_getting_started
[unity_on_osx]: 6_Unity:unity_on_osx
[unity_on_windows]: 6_Unity:unity_on_windows
[unity_on_android]: 6_Unity:unity_on_android
[unity_on_ios]: 6_Unity:unity_on_ios
[unity_getting_started]: 6_Unity:unity_getting_started
[unity_scripts]: 6_Unity:unity_scripts
[marker_about]: 3_Marker_Training:marker_about

[helicopter]: :unityhelicopter.png
