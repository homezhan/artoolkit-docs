#Advanced FAQs

##What is the difference between arGetTransMatSquare, arGetTransMatSquareCont, and arGetTransMat?
These are variants on the same algorithm:

- arGetTransMat is the most generic, and gets a pose estimate based on a set of 2D feature points.
- arGetTransMatSquare is the primary use of arGetTransMat, and works with the constrained case when the 2D feature points are corners of a square. All of the fiducial tracking uses this variant in the user-facing API, the more generic version being used only in our NFT library.
- arGetTransMatSquareCont enables optimizations in the pose estimate search when a previous valid pose (i.e. the pose from the last frame) is known. It basically begins the pose estimate search with the previous pose and is thus both significantly faster and affords greatly stability of the pose estimate from frame to frame. However, if no previous pose exists, or if there is likely to be significant change between the previous pose and the current pose (e.g. a significant amount of time has passed, or other means such as inertial tracking have been used to determine that significant inter-frame motion has occurred) then arGetTransMatSquare should be called for that frame instead.

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

##Why isn’t my performance as good as your demos?
ARToolKit works best with a controlled optical environment, in which the image acquired by the camera has a high signal-to-noise ratio, and when the properties of the optical environment are well known; when the lighting is bright (so the camera gain is low, and depth of field is good), when the camera is a good quality camera (with a CMOS sensor, with a large sensor surface, and with good lenses with good light-gathering properties), and when the camera has been accurately calibrated. If any of these requirements can't be met, performance will be less than the ideal case, but in most cases still usable. See [about hardware selection here][about_hardware_selection]

[about_hardware_selection]: 8_Advanced_Topics:about_hardware_selection
