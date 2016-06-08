#OpenSceneGraph (OSG) usage

ARToolKit can use OpenSceneGraph to render 3D scenes. Access to OSG features are facilitated by the ARosg.lib component of the ARToolKit SDK. ARosg.lib is linked against OSG binaries. ARToolKit examples like simpleOSG use the ARosg.lib library to access OSG functions.

ARToolKit currently uses the following OSG functions:

- Load/Unload an OSG model
- Show/Hide an OSG model
- Draw an OSG model
- Enable/Disable lighting
- Enable/Disable transparancy
- Pause/Resume the animation
- Set the projection matrix of an OSG model
- Set front facing polygones (counter-clockwise (default) or clockwise)
- Read/Set model pose (model-view matrix)
- Read/Set local model pose (transformation matrix)
- Enable/Disable 2D outlining of model boundary
- Determination if a model is intersected by a line segment
- Handle window reshape events
- Handle mouse and keyboard interactions

###Models with animation

- Read the animation time from the model
- Reset the animation
- Set the looping mode of an animation (0=disable, 1=loop, 2=swinging)

Detailed information can be found in the source code documentation of ARosg see `ARTOOLKIT_ROOT/doc/apiref/arosg_h`.
