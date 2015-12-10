#Getting Started with ARToolKit for Unity

##Installation
ARToolKit for Unity is distributed as a Unity package. A package is an archive of files which can be imported and unpacked into your Unity project. In this case, the package contains the plugin, scripts and resources necessary to integrate ARToolKit with your Unity application.

The ARToolKit for Unity package is available for download from ARToolKit. Download and store this package on your machine.

You can import the package into a fresh or existing project. Select menu `Assets -\> Import Package -\> Custom Package...` and browse to the location where you have stored the ARToolKit package. Select the package, and Unity will ask which files to import. Simply import all files at this stage.

![Assets -\> Import Package -\> Custom Package...][menu_screenshot]

![Use the default (Import all)][import_all]

Your Unity project now contains the necessary files for augmented reality with ARToolKit.

##Package Overview
The package contains:

-   Unity scripts: A set of C\# scripts that handle communication between Unity and the native plugin. These are the scripts that developers will use to access ARToolKit functionality. They are contained inside the file `ARToolKit5-Unity.dll`.
-   Unity Editor scripts: A second set of C\# scripts that extend the Unity editor itself to simplify development with customized editor panels and 3D gizmos. These are contained inside the file `Editor/ARToolKit5-UnityEditor`.
-   ARToolKit plugins: The native plugin implementation. There are various versions for different supported platforms, such as Windows, Mac OS X, Android and iOS. This is stored in the `Assets/Plugins` directory (and subdirectories).
-   ARToolKit data files: The default [camera parameters][config_camera_calibration] file and two sample patterns are included in the `Resources/ardata directory`. A sample [NFT dataset][marker_nft_train] is included in the `Assets/StreamingAssets` directory.
-   Android Activity: A customized version of the Unity player for Android (packaged as a JAR file). Also required is a custom Manifest.xml file, and Android resources in the "res" subdirectory.
-   Simple examples: A set of very basic example scenes which you can use as starting points for various AR techniques are found in `Example scenes`.

![Unity scripts are revealed by turning down the reveal arrow on the "ARToolKit5-Unity" object.][editor_screenshot]

##Scene Setup
ARToolKit allows for dynamic AR scenes with more than one marker in Unity. All marker content can live in the same layer, and relations between content attached to different markers (e.g. physics) is easy to understand. The following three components work together to create an AR scene:

-   ARController - Manages the overall initialization, setup, running and shutdown of ARToolKit. Singleton.
-   AROrigin - Represents the center of the ARToolKit world and is the root of the scene. Normally can be placed at {0, 0, 0}.
-   ARTrackedObject - Represents the marker as tracked in space. Content relevant to the marker will be attached to this parent.
-   ARCamera - Associates a Unity Camera to the AR content. Allows it to be rendered.

###1 - ARController
Create an object to hold the AR configuration objects, ARController and ARMarker. In the example projects, we have named this "ARToolKit". Drag an ARController onto this object.

![Dragging an instance of the "ARController" script from the Asset browser onto an empty GameObject.][arcontroller_setup]

The ARController script will handle the creation and management of the AR tracking, including the video background. All the developer needs to provide is the Unity [layer][layer] in which to display the video; usually this is "user layer 1", which you might want to rename to e.g. "AR Background". Layers are used to separate out parts of the scene so only certain parts are visible to certain cameras. In this case, the video background will be in its own background layer. You can take a moment now to define an "AR Foreground" layer, as well. This is where every marker's content will be shown.

![Choose "Edit layers..." in Unity.][edit_layers]
![Choose two of the User layers and give them appropriate names.][name_layers]

You should now be able to run the scene and see the live video. The developer can choose how the input video's aspect ratio is treated in respect to the display's aspect ratio. If they do not match, such as 4:3 video on a 16:10 screen, then the developer can choose either to stretch the video (which will introduce distortion), or use less of the screen (which will introduce empty bars). Empty bars will have the color of the background clearing camera which always renders to the entire screen.

-   Fill screen: Possibly stretch the rendering and introduce distortion.
-   Maintain video aspect ratio (bars): Correct rendering, but bars at edges if the video is more square than display, or at top and bottom if display is more square than video.
-   Maintain video aspect ratio (overfill screen): Unfortunately this mode is unavailable because Unity does not permit viewport rectangles outside the bounds of the screen. There are solutions to this problem coming in an update.

###2- ARMarkers
Tracking requires markers, so drag as many ARMarkers as you wish to track. Configure these objects, being sure to set the "Tag" field on each ARMarker to something memorable -- this will be the name used by the dynamic scene to find this marker and get its data.

####Template Markers
The ARMarker script will automatically locate [pattern files][marker_train] that have been placed in the project's `Resources/ardata/markers` directory. The default installation will include the standard Hiro and Kanji [patterns][marker_about]. These will appear in the dropdown list in the Marker's properties. Select the pattern you want to track. Give this marker a tag (a unique name to identify it within your project).

####NFT Markers
[NFT][marker_nft_training] markers can be used by choosing "NFT" as the marker type on the ARMarker component. This makes available an additional field where you can enter the name of the dataset. The actual NFT data (.iset, .fset, and .fset2) which are generated by the genTexData utility should placed into the folder `Assets/StreamingAssets` of your Unity project.

![NFT options panel.][nft_options]

The SDK includes an example dataset (file names: gibraltar.iset, gibraltar.fset, gibraltar.fset2). The example NFT dataset can be enabled by entering the basename of the datafiles (in this case: gibraltar) into the "dataset" field.

###3- AROrigin
Next, decide on the point in your scene graph which you would like to be the root of your AR scene. All dynamic AR scene content will live under this root, and its transform will be the origin for AR calculations. Normally, this will be an empty GameObject at the root of your scene, but it can be any GameObject. In the examples, this object is named "Scene root". Drag an AROrigin script onto this object. It's also useful to put this object and all children into its own layer, e.g. create a new user layer and name it "AR foreground".

###4 - ARTrackedObjects
Now, add a child GameObject beneath the scene root you created in the previous step. This object will hold the AR content for the first AR marker, so you could rename it to (for example) "Marker Scene 1". Attach an `ARTrackedObject`, and configure its "Tag" property to the same name you used on its corresponding ARMarker earlier. This associates the ARTrackedObject with the ARMarker. The object to which the ARTrackedObject is attached will have its position and rotation changed at runtime depending on the pose of the marker, and its child objects will be enabled/disabled depending on the visibility of the marker. Be sure that all ARTrackedObjects have an AROrigin attached to one of their parents, or else they won't display any content.

###5 - ARCamera
The last thing you need to add before content can be viewed is a Unity Camera object. This must be a child object of the AR scene root. Set its culling mask to the layer you chose earlier (We suggest "AR Foreground", and be sure that the "AR Background" is not selected). Attach an ARCamera script to this camera.

####Testing and Adding Content
At this point you can run the scene again. Although no content appears on the marker yet, you should notice console messages appearing to notify that the marker has been found or lost.

Start with the ARTrackedObject you want to augment. This object will act as parent to the sub-scene that will appear on the marker. By default, markers appear in the scene standing vertically (like a billboard) at the origin. Usually however, you want the marker to lie flat on the ground, and this is what we'll do in this case. Add a GameObject under the ARTrackedObject you've selected, and in the Inspector, change its "Rotation: X" value to 90. This will rotate the child objects of this new GameObject by 90 degrees about the X axis (in a left-hand sense), appearing correctly to the ARCamera.

![Setting the rotation on the scene root to orient the marker flat on the ground layer.][rotating]

Add a cube to the rotated GameObject. This will be the initial simple scene. Set the scale to `{0.08, 0.08, 0.08}`, and position to `{0, 0.04, 0}`, to sit on the marker correctly.

Select the new group you created and ensure it is assigned to the foreground layer created earlier (applying the change to all children when prompted).

Press "Play" again, and you should now be able to see the cube on the marker. Congratulations!

##Notes

###Required Data Files
In a standard ARToolKit application, there are several data files required, such as [camera calibrations][config_camera_calibration] and [patterns][marker_train]. When working with the Unity plugin, these files are included in the projects Assets directory, under the `Resources/ardata` directory. In order to be recognized by Unity, the files must follow a particular naming scheme:

-   The camera parameters file, `camera_para.dat`, should be stored in `Assets/Resources/ardata/` as `camera_para.bytes`.
-   Pattern files should be stored in Assets/Resources/ardata/ with a .txt extension (e.g. `patt.hiro.txt`).

These files can still be generated using the standard ARToolKit utilities; it is simply the filenames and locations that are important for the Unity plugin.

###Units in Unity World Space
By default the plugin operates in meters. The default marker size is therefore 0.08 (8cm) and the camera has near and far planes of 0.1 and 5.0 respectively (10cm - 5m). These can be changed in the ARController and ARMarker properties.

###Deployment Notes
If you are not using NFT markers, be sure to remove any NFT datasets from the StreamingAssets folder before final build to avoid unwanted extra disk usage. The same convention goes for traditional template markers, as well- We suggest you remove them if you do not plan to use them.

##Next Steps
Read up on [the scripts of ARToolKit][unity_scripts] in Unity. Also check out our [low-level API][unity_low_level_api].

[marker_about]: 3_Marker_Training:marker_about
[marker_train]: 3_Marker_Training:marker_training
[config_camera_calibration]: 2_Configuration:config_camera_calibration
[marker_nft_train]: 3_Marker_Training:marker_nft_train
[unity_scripts]: 6_Unity:unity_scripts
[unity_low_level_api]: 6_Unity:unity_low_level_api

[menu_screenshot]: :unity_import_package.png
[import_all]: :unity_import_artoolkit_2012-06.png
[editor_screenshot]: :artoolkit_for_unity_scripts.png
[arcontroller_setup]: :unity_drag_artoolkit_script_onto_empty_gameobject.png
[layer]:http://unity3d.com/support/documentation/Components/Layers.html
[edit_layers]: :unity_-_edit_layers.jpg
[name_layers]: :unity_-_ar_layers.jpg
[rotating]: :artoolkit_for_unity_-_setting_scene_root_rotation.png
[nft_options]: :artoolkit_for_unity_-_nft_options.png
