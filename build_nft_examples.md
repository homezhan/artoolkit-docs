# Building ARToolkit NFT Example Code

ARToolKit NFT is supplied with pre-built binaries for all of the examples (as well as the libraries and utilities). If you want to experiment with the examples right away, it is not necessary to build them first. However, ARToolKit NFT's example(s) functions as both a demo of the NFT functionality, as well as a template which you can copy, to change various options and to add your own customisations. You will want to build your own example applications from source at some point.

## Required software/source packages:

-   ARToolKit Professional v4.5.4.
    -   You must have ARToolKit Professional installed prior to attempting to build any ARToolKit NFT examples. The ARTOOLKIT_4_ROOT environment variable must be defined and point the root of the ARToolKit4 directory. On Windows, this environment variable is set by the ARToolKit Professional installer. On Mac OS X and Linux, you will need to manually run the script 'share/artoolkit4-setenv' inside your ARToolKit Professional installation.
-   A compiler.
    -   Windows: Microsoft Visual Studio 2010, and Microsoft Visual Studio 2008 SP1 are supported.
    -   Mac OS X: Xcode tools v3.1 under Mac OS X 10.5 or later is required. These may be obtained free from [Apple][1].
    -   Linux: GCC 4.4 is recommended.
-   OpenGL
-   GLUT; required to build the examples. (libARgsub_lite provides equivalent functionality to libARgsub without requiring GLUT).
    -   Windows: GLUT 3.7.6 is included with ARToolKit NFT.
    -   Mac OS X: included in OS.
    -   Linux: GLUT should be available in your distribution (e.g. packages freeglut3-dev and xorg-dev). Otherwise, GLUT is included in the MESA 3D libraries: [1][2]
-   OpenCV; version 2.2 is required by libKPM, and is included with ARToolKit NFT.
-   A video capture source
    -   Windows: By default, on Windows ARToolKit Professional's video library (libARvideo) uses Microsoft's DirectShow as a video source. Unfortunately, this requires installation of the DirectX SDK and either the Windows SDK or the DirectShow package from the Microsoft Platform SDK to compile libARvideo. Please see the separate page Building libARvideo using DirectShow. Alternative video sources on Windows include:
        -   QuickTime, either using the VideoDigitizer or movie files or streams. Please see the separate page Building libARvideo using QuickTime.
        -   Thomas Pintaric's DSVideoLib which is the default video source for ARToolKit v2.x (N.B.: DSVideoLib is now LGPL licensed and may be used in proprietary software.)
        -   Point Grey's flycapture SDK (only for use with Point Grey Cameras).
        -   Canon's HDCam64 camera control library (Canon HDCam64 users only).
    -   Mac OS X: QuickTime v6.4 or later is required, and is included in all versions of Mac OS X \> 10.3.
    -   Linux: Video4Linux (e.g. package libv4l-dev), or libdc1394 (e.g. package libdc1394-22-dev), or gstreamer (e.g. package libgstreamer0.10-dev) is required.

## Compiling the ARToolKit NFT examples

Windows

-   Open the ARToolKit NFT.sln file inside the appropriate directory in side the "VisualStudio" directory.
-   Build the sample applications.

Mac OS X

-   Open the ARToolKitNFT.xcodeproj, found inside the Xcode folder.
-   Select a target to build.

Linux

-   Building proceeds with the usual steps ./Configure; make.

[1]: http://developer.apple.com/tools/xcode/
[2]: http://mesa3d.sourceforge.net/