# ARToolkit NFT FAQ

## Requirements

- Does ARToolKit NFT still require ARToolKit?

Yes, ARToolKit NFT effectively adds a new tracking component library to ARToolKit, names libAR2. This library provides the on-line tracking of textured surfaces, with ARToolKit providing video capture and OpenGL compositing. ARToolKit's libAR can also be used to perform tracking of an embedded fiducial marker to assist ARToolKit NFT.

- Does ARToolKit NFT still require black and white markers in the image?

Yes, and possibly, no. ARToolKit NFT's texture tracking requires 'initialisation', which is the process of choosing the tracking data set to use and acquiring the initial pose estimate. This is typically performed with the familiar black and white markers, which can be incorporated into the artwork to be tracked, or placed around it. As of July 2009, ARToolworks is introducing a new totally-markerless product consisting of a new library which can be used to perform the initialisation. At the time of writing, this library is still under test with a limited number of customers, and an announcement will be made when it becomes publicly available.

## Performance

- Why don't I get performance as good as your demos?

ARToolKit NFT works best with a controlled optical environment, in which the image acquired by the camera has a high signal-to-noise ratio, and when the properties of the optical environment are well known. In plain english: When the lighting is bright (so the camera gain is low, and depth of field is good), when the camera is a good quality camera (with a CMOS sensor, with a large sensor surface, and with good lenses with good light-gathering properties), and when the camera has been accurately calibrated. If any of these requirements can't be met, performance will be less than the ideal case, but in most cases still usable.