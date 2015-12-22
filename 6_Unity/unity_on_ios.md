#ARToolKit for Unity on iOS
To get started with using ARToolKit for Unity on iOS, first visit our [Getting Started][unity_getting_started] guide. Also, look [here][ios_about] for iOS specific documentation.

##Requirements

-   You must have a Unity Pro with iOS Pro license to be able to export projects from Unity that use the ARToolKit plugin.
-   You must be using an [iOS device listed on our supported systems page][ios_supported_systems].

##Player Settings

-   Resolution and Presentation
    -   Use 32-bit Display Buffer: ticked (yes)
-   Other Settings
    -   Bundle identifier: Set this to the same as the bundle ID of the Xcode provisioning profile you intend to use. E.g. if your iOS provisioning profile will be "com.mycompany.myapp" then set that here.
    -   Target platform: If you are targeting only iOS v4.3 and newer, set to "armv7". If you intend to also target iOS v4.0-4.2.x, set this to "Universal".
    -   SDK version: iOS latest
    -   Target iOS version
        -   Set to 4.3 or higher if using ARToolKit for Unity v2.0.5 or later.
        -   Set to 4.0 or higher if using ARToolKit for Unity v2.0 - v2.0.4. You may wish to support only iOS 4.3 and later (and thus drop support for the iPhone 3G) or iOS v5.0 and later, at your discretion.
    -   Stripping level: it should be safe to strip to at least "strip assemblies" level.
    -   Script call optimization: Fast.

##Building Xcode Project Exported from Unity
Once the Xcode project has been exported from Unity, the following adjustments should be made in Xcode Acclerate.framework will need to be added (in addition to the Unity-selected frameworks).
![Screenshot of Accelerate.framework being added.][accelerate_screenshot]

For reference, the complete list of iOS frameworks and libraries required for correct linking is:

-   Accelerate.framework (weak-linked)
-   AudioToolbox.framework
-   AVFoundation.framework
-   CoreGraphics.framework
-   CoreMedia.framework
-   CoreVideo.framework
-   OpenGLES.framework
-   QuartzCore.framework
-   libjpeg (libjpeg.a from ARToolKit for iOS can be used)
-   libstdc++.6

[ios_about]: 5_iOS:ios_about
[ios_supported_systems]: 5_iOS:ios_supported_systems
[unity_getting_started]: 6_Unity:unity_getting_started

[accelerate_screenshot]: :unity_ios_-_add_accelerate.framework.png
