#Dynamic AR Scenes with ARToolKit for Unity

##Introduction
ARToolKit for Unity allows for dynamic AR scenes with more than one marker. Previously, if you wanted content to appear on more than one AR marker, that content had to be divided into different layers. This was unwieldy when many markers were used, and introduced difficulties in dealing with relations between markers. With the new method, all marker content can live in the same
layer, and relations between content attached to different markers (e.g. physics) is much simpler.

These three new or changed components work together to provide a superset of the functionality previously provided by ARCamera:
-   `AROrigin`
-   `ARTrackedObject`
-   `ARCamera`

The old ARCamera functionality is still available for backwards-compatibility with old projects, and it has been renamed to `ARTrackedCamera`.

##Setting up a dynamic scene in the Editor
1.   First, create an object to hold the AR configuration objects, `ARController` and `ARMarker`. In the example projects, we have named this "ARToolKit". Drag an `ARController` onto this object, plus as many `ARMarker`s as you wish to configure. Configure these objects, being sure to set the "Tag" field on each `ARMarker` to something memorable -- this will be the name used by the dynamic scene to find this marker and get its data. Don't forget to set the layer you want the video background to appear in; usually this is "user layer 1", which you might want to rename to e.g. "AR background".
2.   Once this is done, you should be able to press "Play" in the Unity Editor and see the video background and observe "marker ... now visible/is no longer visible" messages in the console (but of course, no AR content will display yet).
3.   Next, decide on the point in your scene graph which you would like to be the root of your AR scene. All dynamic AR scene content will live under this root, and its transform will be the origin for AR calculations. Normally, this will be an empty GameObject at the root of your scene, but it can be any GameObject. In the examples, this object is named "Scene root". Drag an `AROrigin` script onto this object. It's also useful to put this object and all children into its own layer, e.g. create a new user layer and name it "AR foreground".
4.   Now, add a child GameObject beneath the scene root you created in the previous step. This object will hold the AR content for the first AR marker, so you could rename it to (for example) "Marker scene 1". Attach an `ARTrackedObject`, and configure its "Tag" property to the same name you used on an `ARMarker` earlier. This associates the `ARTrackedObject` with the `ARMarker`. The object to which the `ARTrackedObject` is attached will have its position and rotation changed at runtime depending on the pose of the marker, and its child objects will be enabled/disabled depending on the visibility of the marker. Be sure that all `ARTrackedObjects` have an `AROrigin` attached to one of their parents, or else they won't display any content.
5.   To give some AR content to look at, create a cube as a child object of the marker scene object you created in step 4.
6.   The last thing you need to add before content can be viewed is a Unity Camera object. This must be a child object of the AR scene root. Set its culling mask to the layer you chose earlier (and be sure that the "AR background" layer is not selected). Then, attach an `ARCamera` script to this camera.
7.   Now try pressing "Play" in the Editor again. If all goes well, you should now see the cube appear on your marker.
8.   To add a second marker scene, repeat steps 4-5 again. You can make it easier to see your content in the editor by setting the transform on the object holding each marker scene (i.e. the object the `ARTrackedObject` script is attached to). Remember that the position is overridden at runtime.

[Category:ARToolKit for Unity](/Category:ARToolKit_for_Unity "wikilink")