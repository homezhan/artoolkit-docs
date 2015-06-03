#ARToolKit for Unity on Android
To get started with using ARToolKit for Unity on Android, first visit our [Getting Started][unity_getting_started] guide.

##Requirements

-   You must have a Unity Pro with Android Pro license to be able to export projects from Unity that use the ARToolKit for Unity plugins.
-   Limited to devices "Android 2.3.1 'Gingerbread' (API Level 9)" or higher, or if using only square tracking "Android 2.2 'Froyo' (API Level 8)" or higher.

##Player Settings
When exporting to Android, some [Player Settings][android_player_settings] must be configured as follows to work correctly with ARToolKit for Unity (settings not mentioned can be adjusted to suit the user):
![Screenshot of Player Settings][player_settings]

-   Resolution and Presentation
    -   Orientation: "Landscape Left" - required so that the live video is oriented to match the screen.
    -   Use 32-bit Display Buffer: True
-   Other Settings
    -   Bundle Identifier: ARToolKit for Unity on Android comes with its own AndroidManifest.xml. In this manifest, the bundle identifier is "com.mycompany.myapp". Note: *This must be changed to match the bundle identifier as written in your player settings before building your application. See below for instructions on how to change this.
    -   Minimum API Level: "Android 2.3.1 'Gingerbread' (API Level 9)" or higher, or if using only square tracking "Android 2.2 'Froyo' (API Level 8)" or higher.
    -   Graphics Level: OpenGL ES 2.0
    -   Internet Access: "Require"

### Setting the Bundle Identifier
All Android applications must be uniquely identified by a bundle identifier. ARToolKit for Android is supplied with a default bundle ID of "com.mycompany.myapp" but *this will need to be changed before deployment of your finished application*.

Note that when using ARToolKit for Unity, the bundle ID has to be set in two places: the Unity Player settings, and in the file "Assets/Plugins/Android/AndroidManifest.xml".

First set the bundle ID in Unity (replacing com.mycompany.myapp with your chosen ID):
![Screenshot of Player Settings and Bundle ID Field][player_settings_id]

Secondly, the bundle ID must be manually changed in the Android manifest that ARToolKit provides. To do this, look inside your Unity project folder, for the file "Assets/Plugins/Android/AndroidManifest.xml". Open the file in a text editor and locate the text `package="com.mycompany.myapp"`, editing the "com.mycompany.myapp" to match the bundle identifier set in Unity.
![Screenshot of AndroidManifest.xml and Bundle ID Field][android_manifest_id]

##Using ARToolKit for Unity in a Larger Android Project
It is possible to modify the Android Java portion of ARToolKit for Unity to allow for incorporation into a larger Android application, or any other type of conceivable customization.

Unity for Android comes bundled with the source code for its outermost Activity subclass (UnityPlayerActivity). ARToolKit for Unity subclasses this in a new class UnityARPlayerActivity. This class is packaged as a .jar file and provided in ARToolKit for Unity at path Assets/Plugins/Android/UnityARPlayer.jar. It is linked into the final product by Unity. Source for UnityARPlayerActivity is also supplied. You can find it in ARToolKit for Unity at path extras/Android UnityARPlayer source/.

The following images show how to package this source into the .jar file.

First, ensure that the project correctly references the locations of "android.jar" (from the Android SDK) and the "classes.jar" provided by Unity.

"classes.jar" is part of the Unity installed package on your system. On OS X this is typically inside the Unity application package at path
`/Applications/Unity/Unity.app/Contents/PlaybackEngines/AndroidPlayer/bin/classes.jar`
and on Windows at path
`C:\Program Files\Unity\Editor\Data\PlaybackEngines\AndroidPlayer\bin\classes.jar`.
![Compiling][compile_setup]

Next, invoke an export jar operation in Eclipse (File-\>Export...)

![Exporting a JAR 1][unity_export_1]
![Exporting a JAR 2][unity_export_2]

The correct classes must be exported. This includes:
`org/artoolkit/ar/base/NativeInterface.class
org/artoolkit/ar/unity/CameraSurface.class
org/artoolkit/ar/unity/UnityARPlayerActivity.class`

See the following image for how to select the classes.
![Selecting Classes for Export][unity_export_3]

Once the jar has been exported, place it in your Unity project at path `Assets/Plugins/Android/UnityARPlayer.jar`

###Errata
Why is NFT only API 9 and above? On Android OS releases v2.2.x and earlier, a defect in the handling of compressed resources inside .jar files embedded in .apks limits the size of compressed resources to as little as 1.0 megabyte (although this can be higher on some variants of the 2.2 OS series, depending on the device manufacturer). This imposes a limitation on the size of the NFT datasets which can be used if targeting Android 2.2 to 1.0 megabyte. This limitation was removed in Android OS 2.3.

[unity_getting_started]: 6_Unity:unity_getting_started
[android_player_settings]:http://docs.unity3d.com/Manual/class-PlayerSettingsAndroid.html "Unity - Manual: Android Player Settings"
[player_settings]: :unity_player_settings_menu.png
[player_settings_id]: :unity_player_settings_android_bundle_id.png
[android_manifest_id]: :artoolkit_for_unity_android_manifest_bundle_id.png
[compile_setup]: :unityarplayer_compile_setup.png
[unity_export_1]: :unityarplayer_export_1.png
[unity_export_2]: :unityarplayer_export_2.png
[unity_export_3]: :unityarplayer_export_3.png
