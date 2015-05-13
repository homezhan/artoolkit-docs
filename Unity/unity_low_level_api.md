#ARToolKit for Unity Scripting and Low-Level API

##Unity Scripting Environment and ARToolKit as Plugin
Unity provides a rich scripting interface for developing interactive applications. Scripts can be written in Javascript or C\#, and have access to the vast library of objects and functions. Basically any object that can be added manually in the Unity editor can also be scripted. Scripts also integrate seamlessly into the editor. For example, public fields in a script will automatically be presented in the UI using a suitable control so that their values can be easily configured.

Unity’s C\# support is possible through the Mono framework, which provides a cross-platform implementation of Microsoft’s .NET framework. C\# is a modern object-oriented language, and due to its general popularity, there is abundant information and sets of tutorials on its use. The Mono implementation does not provide all the feature of .NET on Windows but the core language features are present.

An additional feature of the Mono runtime is its support for native code, that is, compiled CPU-specific code which communicates directly with the operating system application programming interfaces (APIs) on the platform. Communication between code running in the Mono managed C\# environment communicates with the native unmanaged code via Platform Invocation Services (P/Invoke). This permits a C\# script, running within Unity, to call a native function implemented in C/C++. This is
the mechanism by which plugins are supported in Unity, and this is how ARToolKit for Unity is implemented. ARToolKit communicates with the OS to retrieve images from the camera, perform the compute-intensive tasks associated with marker tracking, and even push the camera image to a native texture, all in native code. Then, a simplified set of simple function calls to configure, run, and shutdown the library are exposed externally. These function calls are mapped across to DllImport definitions in a C\# script, and can then be directly called from Unity.

On Windows, OS X, and Android, libARWrapper is implemented as a dynamic library (packaged as a .dll, a bundled .dylib, and a .so file respectively). On iOS which does not allow dynamic linking in user code, libARWrapper is provided as a static library (.a file) which is linked into the final application.

This illustration shows the relationship between the various entities that make up ARToolKit for Unity:
[<ARToolKit for Unity functional schematic.][functional_schematic]

##Controlling ARToolKit for Unity via Scripting
While ARToolKit for Unity does not require scripting and allows for most configuration to be achieved directly in the Unity Editor, it nonetheless supports full script control. This is useful in cases where you need tighter control over the AR portions of your application, or when you want to customise or modify the way that ARToolKit entities are represented in Unity.

The key scripts are:
-   `ARController`
-   `ARMarker`
-   `ARCamera`

ARController performs most of the key tasks, including setup and
cleanup, as well as the frame-by-frame AR tasks such retrieving and
drawing new video frames, performing tracking, and getting tracking
results. ARMarker provides a convenient abstraction of a single square,
square barcode, multi-square or NFT marker and its pose. ARCamera
provides a simple way to connect the pose held by an ARMarker to the
position of a Unity Camera in a scene, and thus achieve spatial
registration of the AR scene with the marker.

As well as these scripts, you can also directly access the native plugin API via the `PluginFunctions` script.

##Controlling Main ARToolKit Operation
ARToolKit is added to your project by adding an instance of the `ARController` script to a GameObject in your scene. It does not matter where in the scene the GameObject is, and in most ARToolKit for Unity examples, a single object at the scene root holds the `ARController`.

It is highly recommended that the `ARController` is added to the scene using the Unity Editor, as programmatic configuration of the `ARController` is complex. If you wish to ignore this recommendation, you are encouraged to examine the public properties of the `ARController` script and the way these are configured in the `ARControllerEditor` Unity Editor script.

By default, `ARController` implements the `Start()`, `Stop()`, and `Update()` MonoBehaviours, and calls these functions, respectively:
-   `StartAR()` - takes a configured AR scene and begin tracking
-   `UpdateAR()` - perform tracking updates and housekeeping
-   `StopAR()` - stops tracking.

By default, `StartAR()` is called during `Start()`. If you wish to override the auto-start, set the public property `AutoStartAR`:
<csharp>
GameObject myARObject;
ARController myARController = myARObject.GetComponent<ARMarker>();
myARController.AutoStartAR = false;
</csharp>
and then you can manually invoke `StartAR()`/`StopAR()` at more appropriate times for your application.

###Adding, Removing, Finding and Querying Markers
The `ARMarker` script presents an abstraction of a marker for use in Unity.

#### Adding a new marker
To dynamically load a new marker for tracking, you should instantiate a GameObject somewhere in your scene, and attach an ARMarker to it. Usually all `ARMarker` instances are added to the same GameObject that holds the `ARController` instance:
<csharp>
GameObject myARObject;
myMarker = myARObject.AddComponent("ARMarker") as ARMarker;
// Configure
myMarker. myMarker.Tag = "myMarker1";
myMarker.MarkerType = MarkerType.SquareBarcode;
myMarker.BarcodeID = 0;
myMarker.PatternWidth = 0.08f;
// In metres, i.e. 0.08 = 8cm, or 3.15"
myMarker.Load();
</csharp>

You can take a look at the source for ARMarker to see the other options.

Here are some points to note when adding an ARMarker via a script:
-   Unless `ARController.StartAR()` has already been called, actual marker loading into ARToolKit is deferred until AR startup, and errors such as missing data may not show up until then.
-   If you are using pattern-based square markers, you must supply the contents of the pattern file yourself (for an `ARMarker` added in the Unity Editor, this is done by the ARMarkerEditor script which runs in the Unity Editor.)
-   If you are using NFT markers OR multi-marker sets which refer to pattern files (not barcodes), you must ensure that the files which provide the marker data are available in the file system, normally in the deployed "StreamingAssets" folder inside your Unity project.

#### Getting a list of all markers
<csharp>
// Note that FindObjectsOfType is expensive; don't use every frame.
ARMarker[] markers = FindObjectsOfType(typeof(ARMarker)) as ARMarker[];
</csharp>

#### Removing a marker
<csharp>
// If you need to get a reference to it...
GameObject myARObject;
ARMarker myMarker = myARObject.GetComponent<ARMarker>();
// Now destroy it.
Destroy(GetComponent(myMarker));
// If you just want to disable it instead:
myMarker.enabled = false;
</csharp>

#### Querying a marker for its visibility and pose
<csharp>
ARMarker myMarker;
if (myMarker.Visible) Debug.Log("Marker is visible.");
// Pose is a 4x4 homogenous coordinate transform, in left-hand coordinates.
// Pose is the transform of the marker with respect to the observing camera. To get the camera
// pose with respect to the marker, take pose.inverse;
Matrix4x4 pose = myMarker.TransformationMatrix;
Vec3 position = ARUtilityFunctions.PositionFromMatrix(pose);
Quaternion orientation = ARUtilityFunctions.QuaternionFromMatrix(pose);
</csharp>

##Connecting Markers to the Scene

###Using an ARCamera
A simple means of connecting a single `ARMarker` (which might represent either a single pictorial or barcode square marker, a multi- square marker set, or an NFT marker) to the Unity scene is to use the `ARCamera` script. This script must be attached to a Unity Camera object.

The `ARCamera` is associated with an `ARMarker` by setting `ARCamera` Marker Tag to the same value as the desired `ARMarker` Tag. When the `ARMarker` appears and is tracked, the `ARCamera`'s Unity Camera draws its' view at the same pose relative to its parent as the real camera to the real marker, and when the ARMarker disappears, the Camera's output is hidden. By putting game objects into layers, and setting the culling mask of the camera to display only the layer with desired objects, this allows content to be easily shown/hidden in concert with a marker.

<csharp>
    // Generally, you should use a tag or other means to identify the camera you want to modify.
    Camera[] Cameras = FindObjectsOfType(typeof(Camera)) as Camera[];
    myCamera = Cameras[0];
    // Set the culling mask for this camera to identify the layers you want to be shown/hidden. Do this before adding the ARCamera. 
    myARForegroundLayer = 9;
    // 0-based index, so 9 = user layer 2.
    myCamera.cullingMask = 1\<\< myARForegroundLayer;
    myCamera.AddComponent("ARCamera") as ARCamera;
</csharp>

Configuring the ARCamera:
<csharp>
    myARCamera = myCamera.GetComponent<ARCamera>();
    myARCamera.MarkerTag = "myMarker1";
    // As set in example above.
</csharp>

To allow control other aspects of GameObjects than their visibility, you can connect your GameObject to the `ARCamera`'s `eventReceiver` property. When the marker appears, is tracked, or disappears, these methods in the eventReceiver or any of its children are called via Unity's [BroadcastMessage][broadcast_message] system.
<csharp>
    // All optional. OnMarkerFound(ARMarker marker);
    OnMarkerTracked(ARMarker marker);
    OnMarkerLost(ARMarker marker);
</csharp>

The `ARCamera`'s projection and viewport are set during AR startup. At present, it is not possible to add an `ARCamera` after `StartAR()` has been called, unless you modify ARController.cs and change `ConfigureForegroundCameras()` and `ConfigureViewports()` from private to public methods.

###Via Custom Means
While it is simple to use, the layer-based system can become unwieldy when more than a few markers are in use. In that case, you will most likely want to directly query ARMarkers in your scripts and decide how you want to use the pose information.

##Using the Low-Level Plugin Interface
Ultimately, all AR-related functions in ARToolKit for Unity's C\# scripts call API defined by the native plugin, libARWrapper. You are free to make calls to this API too.

Full API documentation for libARWrapper's simplified C-based API is available [on our website][c_docs].

[functional_schematic]:/File:ARToolKit_for_Unity_functional_schematic.png "wikilink"
[broadcast_message]:http://docs.unity3d.com/ScriptReference/GameObject.BroadcastMessage.html
[c_docs]:http://www.artoolworks.com/support/doc/artoolkit5/apiref-ARWrapper/html/_a_r_tool_kit_wrapper_exported_a_p_i_8h.html

[Category:ARToolKit for Unity](/Category:ARToolKit_for_Unity "wikilink")