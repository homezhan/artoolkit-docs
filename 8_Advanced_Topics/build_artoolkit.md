#Building ARToolKit from Source
*If you have been supplied with pre-built ARToolKit binaries, you will not need to build ARToolKit from source. The instructions below apply only to users who wish to modify the internals of ARToolKit.* Source code and project files are supplied for all of ARToolKit. This allows you to not only see how the toolkit works, but also to modify its operation should you so wish.

##Required Software / Source Packages
External dependencies for building ARToolKit from source include all the dependencies for building your own ARToolKit-based applications (as listed on page [Installing ARToolKit][about_installing] but also additional dependencies required to build the utilities and libraries. Where ARToolKit libraries require external DLLs, these are generally supplied with ARToolKit. Exceptions are listed below.

-   A supported compiler/IDE:
    -   Windows: Microsoft Visual Studio 2013 and Microsoft Visual Studio 2010 SP1 are supported. The free Microsoft Visual Studio Express Edition will also work.
    -   Mac OS X: Xcode tools v5.1.1 under Mac OS X 10.9 or later is required. Xcode 6 under Mac OS X 10.10 is recommended. These may be obtained free from [Apple][2].
    -   Linux: GCC 4.4 is required. GCC 4.8 or later is recommended.
-   OpenGL
-   libjpeg
    -   Windows/Mac OS X: libjpeg headers and libraries are supplied with ARToolKit.
    -   Linux: install package libjpeg-dev.
-   GLUT - Required to build libARgsub and the utilities and examples.
    -   libARgsub_lite provides equivalent functionality to libARgsub without requiring GLUT.
    -   Windows: GLUT 3.7.6 is included with ARToolKit.
    -   Mac OS X: included in OS.
    -   Linux: GLUT should be available in your distribution (e.g. packages freeglut3-dev and xorg-dev). Otherwise, GLUT is included in the MESA 3D libraries: [1][3]
-   OpenCV - Required to build calib_camera. 
	- Generally OpenCV headers and libraries are provided with ARToolKit.
	- On Linux you can choose between Clang and GNU compiler for building ARToolKit. 
		- We recommend building ARToolKit with GNU gcc and g++ (answer fist question of the *configuration script* with no). In this case you need to install the OpenCV libraries manually `sudo apt-get install libopencv-dev`. 
		- If you prefer building with Clang, then the OpenCV headers and libraries are provided with ARToolKit and you need to install libc++-dev. Be aware that libARosg and some examples are excluded from this build because per default OpenSceneGraph comes compiled with GNU. If you would like to use them you need to compile OpenSceneGraph with Clang and then build libARosg and the examples manually.
-   Video capture libraries.
    -   Windows: By default, on Windows ARToolKit's video library (libARvideo) uses Microsoft's DirectShow libraries. Unfortunately, this requires installation of the DirectX SDK and either the Windows SDK or the DirectShow package from the Microsoft Platform SDK to compile libARvideo. Please see the separate page [Building libARvideo][4]. Alternative video sources on Windows include:
        -   QuickTime, either using the VideoDigitizer or movie files or streams. Please see the separate page [Building libARvideo][4].
        -   [Thomas Pintaric's DSVideoLib][6], which was the default video source for ARToolKit v2.x, is now LGPL licensed and may be used in proprietary software.
        -   Point Grey's flycapture SDK (only for use with Point Grey Cameras).
        -   Canon's HDCam64 camera control library (Canon HDCam64 users only).
    -   Mac OS X: QuickTime v6.4 or later is required, and is included in all versions of Mac OS X \> 10.3. For systems with QuickTime 7 or later, QTKit is also used.
    -   Linux: Video4Linux, lib1394dc, or GStreamer is required. The corresponding packages required to be installed in your package manager are "libv4l2-dev" or "libv4l-dev", "libdc1394-22-dev" (for lib1394 version 2.x) or "libdc1394-13-dev" (for lib1394 version 1.x), and "libgstreamer0.10-dev".
-   OpenVRML (optional) - The ARToolKit VRML renderer requires the OpenVRML SDK.
    -   Windows: OpenVRML-0.16.6 or later (for Visual Studio 2005) must be on the include and library path to rebuild ARvrml.lib. Suitable binaries of OpenVRML for Windows can be downloaded [here][7].
    -   Mac OS X: OpenVRML should be installed using the [Fink][8] packagemanager. Once fink is installed, the required command to install OpenVRML is `fink -b install openvrml6-dev openvrml-gl6-dev`. Alternately, a Universal binary build of OpenVRML-0.16.6 suitable for inclusion in application bundles can be downloaded from [here][9].
    -   Linux: Binary deb packages are available from [here][10].
-   OpenSceneGraph (required for building examples) - The ARToolKit OSG renderer requires OpenSceneGraph.
    -   OSG version 2.6 or later is required, version 2.8.2 is recommended.
    -   Windows: ARToolKit supplies binaries of [OSG 3.0.1][11]
    -   Mac OS X: ARToolKit supplies binaries of [OSG 3.2.2][12]
    -   ARToolKit uses the [environment variable][setting_env] OSG_ROOT to find your OpenSceneGraph installation:
        -  Mac OS X: OSG_ROOT=/Library/Frameworks
        -  Windows: OSG_ROOT=<Path to where you extracted OSG file to>
    -   Linux: OpenSceneGraph is available as a package for most Linux distributions (e.g. package libopenscenegraph-dev).

##Compiling ARToolKit

###Windows

-   After unpacking ARToolKit, run the configure-win32 script. This generates AR/config.h for Windows builds. If you wish to change the default video library, or enable extra video libraries such as QuickTime, see [building libARvideo][4].
-   Open the ARToolKit5.sln file inside the appropriate directory inside of the "VisualStudio" directory.
-   Build the ToolKit and the sample applications. The VRML and OSG renderers are not built by default, but can be manually selected and built.

###Mac OS X

-   Open the ARToolKit5.xcodeproj, found inside the Xcode folder.
-   The configure step (which creates AR/config.h) will be run automatically during the build process. If you wish to override the defaults, you may manually edit AR/config.h after this.
-   Select a target to build. The default target builds the complete toolkit with the exception of the OpenVRML and OSG-dependent projects, which can be manually selected and built.

###Linux

-   Building proceeds with the usual steps `./Configure; make` During the configure process, you will be asked to select video libraries to build against.

##Post-Compilation Steps

###Verifying the Compilation
ARToolKit includes a variety of examples demonstrating ARToolKit programming techniques. After compiling, the executables for these applications can be found in the `bin` directory inside your ARToolKit directory. Running the simpleLight example is one of the most straight-forward ways to test that your ARToolKit installation is functioning correctly. An explanation of simpleLight, including how to run it, and its source code can be found on the page [ARToolKit Tutorial 1: First Simple ARToolKit Scene][tutorial_1_first_scene]. More detailed information about the techniques demonstrated in each example can be found on the page [ARToolKit Examples][examples].

#### Windows:
simpleLite can be opened by double-clicking its icon in the ARToolKit4\\bin directory. Alternately, you can run it from the command line:

-   Open a command-line window (cmd.exe).
-   Navigate to your ARToolKit4\\bin directory.
-   Type: simpleLite.exe

#### Mac OS X:

-   Bundled applications are generated for the examples. The utilities are generated as command-line tools. Both can be run in the Finder (with output in Console) or from within Xcode or a Terminal window.

#### Linux:
simpleLite can be launched from a terminal window thus:
<pre>
./simpleLite
</pre>

### Setting up the ARTOOLKIT5_ROOT environment variable
[Click here to see how to set an environment variable.]

[about_installing]: 1_Getting_Started:about_installing
[tutorial_1_first_scene]: 7_Examples:example_simplelite
[setting_env]: 1_Getting_Started:general_environment_variables
[examples]:
[2]: http://developer.apple.com/xcode/
[3]: http://mesa3d.sourceforge.net/
[4]: 8_Advanced_Topics:windows_building_libarvideo
[6]: http://sourceforge.net/projects/dsvideolib
[7]: http://www.artoolworks.com/dist/openvrml/
[8]: http://www.finkproject.org/
[9]: http://www.artoolworks.com/dist/openvrml/
[10]: http://www.openvrml.org/
[11]: http://www.artoolkit.org/dist/3rdparty/openscenegraph/3.0.1/
[12]: http://www.artoolkit.org/dist/3rdparty/openscenegraph/3.2.x/
