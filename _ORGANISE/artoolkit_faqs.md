#ARToolkit FAQs

##What is the difference between arGetTransMatSquare, arGetTransMatSquareCont, and arGetTransMat?

These are variants on the same algorithm.

- arGetTransMat is the most generic, and gets a pose estimate based on a set of 2D feature points.
- arGetTransMatSquare is the primary use of arGetTransMat, and works with the constrained case when the 2D feature points are corners of a square. All of the fiducial tracking uses this variant in the user-facing API, the more generic version being used only in our NFT library.
- arGetTransMatSquareCont enables optimisations in the pose estimate search when a previous valid pose (i.e. the pose from the last frame) is known. It basically begins the pose estimate search with the previous pose and is thus both significantly faster and affords greatly stability of the pose estimate from frame to frame. However, if no previous pose exists, or if there is likely to be significant change between the previous pose and the current pose (e.g. a significant amount of time has passed, or other means such as inertial tracking have been used to determine that significant inter-frame motion has occured) then arGetTransMatSquare should be called for that frame instead.

The sample tracking algorithm supplied with the ARToolKit examples displays a good usage strategy (code from simpleOSG.c, with extra commenting):

<pre>

if (k != -1) {
    // Get the transformation between the marker and the real camera.
    //fprintf(stderr, "Saw object %d.\n", i);
    if (gObjectData[i].visible == 0) { // .visible is 0 when the marker was not seen in the previous frame.
        err = arGetTransMatSquare(gAR3DHandle, &(gARHandle->markerInfo[k]),
                                  gObjectData[i].marker_width, gObjectData[i].trans);
    } else {
        err = arGetTransMatSquareCont(gAR3DHandle, &(gARHandle->markerInfo[k]),
                                      gObjectData[i].trans,
                                      gObjectData[i].marker_width, gObjectData[i].trans);
    }
    gObjectData[i].visible = 1; // Next time around, arGetTransMatSquareCont will be used.
} else {
    gObjectData[i].visible = 0;
}

</pre>

#ARToolkit NFT FAQ

##Requirements

- Does ARToolKit NFT still require ARToolKit?

Yes, ARToolKit NFT effectively adds a new tracking component library to ARToolKit, names libAR2. This library provides the on-line tracking of textured surfaces, with ARToolKit providing video capture and OpenGL compositing. ARToolKit's libAR can also be used to perform tracking of an embedded fiducial marker to assist ARToolKit NFT.

- Does ARToolKit NFT still require black and white markers in the image?

Yes, and possibly, no. ARToolKit NFT's texture tracking requires 'initialisation', which is the process of choosing the tracking data set to use and acquiring the initial pose estimate. This is typically performed with the familiar black and white markers, which can be incorporated into the artwork to be tracked, or placed around it. As of July 2009, ARToolworks is introducing a new totally-markerless product consisting of a new library which can be used to perform the initialisation. At the time of writing, this library is still under test with a limited number of customers, and an announcement will be made when it becomes publicly available.

##Performance

- Why don't I get performance as good as your demos?

ARToolKit NFT works best with a controlled optical environment, in which the image acquired by the camera has a high signal-to-noise ratio, and when the properties of the optical environment are well known. In plain english: When the lighting is bright (so the camera gain is low, and depth of field is good), when the camera is a good quality camera (with a CMOS sensor, with a large sensor surface, and with good lenses with good light-gathering properties), and when the camera has been accurately calibrated. If any of these requirements can't be met, performance will be less than the ideal case, but in most cases still usable.