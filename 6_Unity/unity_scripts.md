#Scripts in ARToolKit for Unity
This page expounds upon the scripts referenced in the [getting started guide][unity_getting_started]. For lower-level usage, please see our [lower level API documentation][unity_low_level_api].

##ARController
The ARController script manages the overall operation of the tracking plugin. It performs the necessary native plugin calls, and allows the developer to configure general settings. There should only ever be one ARController script in a scene.

![ARToolKit Panel][artoolkit_panel]

-   Version: The version number of ARToolKit on which the plugin is built.

###Video Options

-   Configuration: Configuration string passed to the video capture module (more [details][details]).
-   Near Plane: Near plane value used when constructing projection matrix. Measured in metres by default. Decrease to allow a closer camera.
-   Far Plane: Far plane value used when constructing projection matrix. Measured in metres by default. Increase to allow a more distant camera.
-   Layer: The Unity layer in which the video plane will be rendered.

###Threshold Options

-   Mode: The thresholding mode to use. The standard ARToolKit options are available: Manual, Median, Otsu, Adaptive. Different configuration options appear depending on the selected mode.

##ARMarker
The ARMarker script represents one tracked marker in the system. Add one for each individual marker that you want to track.

![Marker Panel][marker_panel]

-   Tag: A unique name that identifies this marker.
-   ID: The internal ID number for this marker. Starting at -1, this number will simply increase. It can be safely ignored.
-   Type: The type of marker.
-   Marker: The marker to use. This list is populated by the marker
    files placed in the Assets/Resources/ardata/markers directory.
-   Width: The width of the marker in meters.

##ARTrackedObject
Represents the marker as tracked in space. Content relevant to the marker will be attached to this object.

-   Tag: The unique name of the marker that this camera should take its pose from. This should match an existing Marker script's tag.
-   Stay Visible: The length in seconds of how long the camera should stay active after marker tracking is lost. For example, using a value of 0.25 will give one quarter of a second delay before the marker's content disappears. This can reduce the effect of flickering.
-   Got marker: Simply displays whether the entered tag matches an existing Marker.
-   Marker ID: The ID of the marker that is linked to this camera via the tag. May be -1 until the pattern is actually loaded.

###Events
The ARTrackedObject generates the following events using Unity's SendMessage command. To handle these events, implement the matching event handler in a script, and attach it to the ARCamera.

-   void OnMarkerLost(ARMarker marker)
-   void OnMarkerFound(ARMarker marker)
-   void OnMarkerTracked(ARMarker marker)

## AROrigin
Represents the center of the ARToolKit world and is the root of the scene. Normally can be placed at {0, 0, 0}, but you may move it elsewhere, if you wish. The ARCamera and every ARTrackedObject should be children to this object. This allows for a few benefits:

-   All objects interact in the same coordinate space.
-   Finding objects by type becomes much less expensive once you know who the parent is.

##ARCamera
The ARCamera script associates a camera to the AR content. Add this to a camera under the AROrigin.

[details]: 2_Configuration:config_video_capture "wikilink"
[unity_getting_started]: 6_Unity:unity_getting_started
[artoolkit_panel]:/File:ARToolKitPanel.png "wikilink"
[marker_panel]:/File:MarkerPanel.png "wikilink"
[camera_panel]:/File:TrackedCameraPanel.png "wikilink"
[unity_low_level_api]: 6_Unity:unity_low_level_api

##Gizmos
Markers are visually represented within the Unity editor so that you can scale and position your content accordingly.
![Marker Gizmo][gizmo]

[artoolkit_panel]: :artoolkitpanel.png
[gizmo]: :markergizmo.png
[marker_panel]: :markerpanel.png
