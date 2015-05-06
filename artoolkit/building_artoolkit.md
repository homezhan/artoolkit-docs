# Building ARToolkit Professional From Source

**If you have been supplied with pre-built ARToolKit binaries, you will not need to build ARToolKit from source. The instructions below apply only to users who wish to modify the internals of ARToolKit.**

Source code and project files are supplied for most of ARToolKit Professional. (The exception is libARICP, which is supplied only in binary form). This allows you to not only see how the toolkit works, but also to modify its operation should you so wish.

To build ARToolKit from source, carefully follow these instructions.

## Required software/source packages

External dependencies for building ARToolKit from source include all the dependencies for building your own ARToolKit-based applications (as listed on page [Installing ARToolKit Professional][1] but also additional dependencies required to build the utilities and libraries.

-   A compiler.
    -   Windows: Microsoft Visual Studio 2013 and Microsoft Visual Studio 2010 SP1 are supported. The free Microsoft Visual Studio Express Edition will also work.
    -   Mac OS X: Xcode tools v5.1.1 under Mac OS X 10.9 or later is required. These may be obtained free from [Apple][2].
    -   Linux: install packages gcc and g++ (GCC 4.4 or later required, GCC 4.8 is recommended).
-   OpenGL
-   libjpeg
    -   Windows/Mac OS X: libjpeg headers and libraries are supplied with ARToolKit.
    -   Linux: install package libjpeg-dev.
-   GLUT; required to build libARgsub and the utilities and examples.
    (libARgsub_lite provides equivalent functionality to libARgsub
    without requiring GLUT).
    -   Windows: GLUT 3.7.6 is included with ARToolKit.
    -   Mac OS X: included in OS.
    -   Linux: GLUT should be available in your distribution (e.g. packages freeglut3-dev and xorg-dev). Otherwise, GLUT is included in the MESA 3D libraries: [1][3]
-   OpenCV; required to build calib_camera. OpenCV headers and libraries are provided with ARToolKit Professional.
-   Video capture libraries.
    -   Windows: By default, on Windows ARToolKit Professional's video library (libARvideo) uses Microsoft's DirectShow libraries. Unfortunately, this requires installation of the DirectX SDK and either the Windows SDK or the DirectShow package from the Microsoft Platform SDK to compile libARvideo. Please see the separate page [Building libARvideo using DirectShow][4]. Alternative video sources on Windows include:
        -   QuickTime, either using the VideoDigitizer or movie files or streams. Please see the separate page [Building libARvideo using QuickTime][5].
        -   Thomas Pintaric's DSVideoLib [2][6] which is the default video source for ARToolKit v2.x (N.B.: DSVideoLib is now LGPL licensed and may be used in proprietary software.)
        -   Point Grey's flycapture SDK (only for use with Point Grey Cameras).
        -   Canon's HDCam64 camera control library (Canon HDCam64 users only).
    -   Mac OS X: QuickTime v6.4 or later is required, and is included in all versions of Mac OS X \> 10.3. For systems with QuickTime 7 or later, QTKit is also used.
    -   Linux: Video4Linux, lib1394dc, or GStreamer is required. The corresponding packages required to be installed in your package manager are "libv4l2-dev" or "libv4l-dev", "libdc1394-22-dev" (for lib1394 version 2.x) or "libdc1394-13-dev" (for lib1394 version 1.x), and "libgstreamer0.10-dev".
-   OpenVRML (optional); The ARToolKit VRML renderer requires the OpenVRML SDK.
    -   Windows: OpenVRML-0.16.6 or later (for Visual Studio 2005) must be on the include and library path to rebuild ARvrml.lib. Suitable binaries of OpenVRML for Windows can be downloaded [here][7].
    -   Mac OS X: OpenVRML should be installed using the [Fink][8] packagemanager. Once fink is installed, the required command to install OpenVRML is `fink -b install openvrml6-dev openvrml-gl6-dev`. Alternately, a Universal binary build of OpenVRML-0.16.6 suitable for inclusion in application bundles can be downloaded from [here][9].
    -   Linux: Binary deb packages are available from [here][10].
-   OpenSceneGraph (optional); The ARToolKit OSG renderer requires OpenSceneGraph. OSG version 2.6 or later is required, version 2.8.2 is recommended.
    -   Windows / Mac OS X: ARToolworks supplies binaries of [OSG][11]. ARToolKit uses the environment variable OSG_ROOT to find your OpenSceneGraph installation.
    -   Linux: OpenSceneGraph is available as a package for most Linux distributions (e.g. package libopenscenegraph-dev).

## Compiling ARToolKit Professional

### Windows

-   After unpacking ARToolKit, run the configure-win32 script. This generates AR/config.h for Windows builds. If you wish to change the default video library, or enable extra video libraries such as QuickTime, edit the file include/AR/config.h. See the additional help pages [Building libARvideo using DirectShow][12] and [Building libARvideo using QuickTime][13] for more help.
-   Open the ARToolKit5.sln file inside the appropriate directory in side the "VisualStudio" directory.
-   Build the ToolKit and the sample applications. The VRML and OSG renderers are not built by default, but can be manually selected and built.

### Mac OS X

-   Open the ARToolKit5.xcodeproj, found inside the Xcode folder.
-   The configure step (which creates AR/config.h) will be run automatically during the build process. If you wish to override the defaults, you may manually edit AR/config.h after this.
-   Select a target to build. The default target builds the complete toolkit with the exception of the OpenVRML and OSG-dependent projects, which can be manually selected and built.

### Linux

-   Building proceeds with the usual steps `./configure; make` During the configure process, you will be asked to select video libraries to build against.

## Post-compilation steps

### Running the simpleLite example

ARToolKit Professional includes a variety of examples demonstrating ARToolKit programming techniques. After compiling, the executables for these applications can be found in the `bin` directory inside your ARToolKit directory.

The simpleLite example is the most straightforward example. It can be run to test your ARToolKit installation is functioning correctly.

*An explanation of the sourcecode of this example can be found on the page [ARToolKit tutorial 1: First simple ARToolKit scene][14]. More detailed information about the techniques demonstrated in each example can be found on the page [ARToolKit Professional examples][15].*

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

As there is no specific directory into which ARToolKit's binaries (libraries, utilities and examples) must be placed, you can decide where to move ARToolKit to after compilation. However, if you are building other software that depends on ARToolKit Professional (e.g. osgART Professional Edition), that software attempts to locate ARToolKit via the `ARTOOLKIT5_ROOT` environment variable.

For the ARToolKit releases, assistance is provided to do this. On Windows, the installer creates this environment variable. On OS X and Linux, a script is provided at path share/artoolkit5-setenv to set the variable for all future login shells. (The script share/artoolkit5-unsetenv removes the setting).

If you are building from source, you may wish to manually set or change this environment variable, which can be done as follows:

#### Windows

Image:Windows_system_control_panel.png|Open the system control panel
Image:Windows_env_vars_button.png|Click the environment variables
button Image:OsgART_Windows_environment_vars.png|Enter the environment variables above (changing the paths to point to where you
installed ARToolKit.

#### Mac OS X

1.  Environment variables can be set from a Terminal window.
2.  From a terminal window, type the following lines, replacing "/path/to/artoolkit" with the actual path:

<pre>
echo "ARTOOLKIT5_ROOT=/path/to/artoolkit; export ARTOOLKIT5_ROOT" >> ~/.profile
echo "setenv ARTOOLKIT5_ROOT /path/to/artoolkit" >> ~/.cshrc
defaults write ~/.MacOSX/environment ARTOOLKIT5_ROOT -string "/path/to/artoolkit"; plutil -convert xml1 ~/.MacOSX/environment.plist
</pre>

The first line sets the environment for users with users with sh or bash as their shell, the second for users with csh or tcsh as their shell, and the third for programs launched by the Finder (including Xcode).

#### Linux

1.  Environment variables can be set from a Terminal window.
2.  From a terminal window, type the following lines, replacing "/path/to/artoolkit" with the actual path:

<pre>
echo "ARTOOLKIT5_ROOT=/path/to/artoolkit; export ARTOOLKIT5_ROOT" >> ~/.profile
echo "setenv ARTOOLKIT5_ROOT /path/to/artoolkit" >> ~/.cshrc
</pre>

The first line sets the environment for users with users with sh or bash as their shell, the second for users with csh or tcsh as their shell. Note that \~/.profile is only read for login shells. If you prefer to use an interactive non-login bash shell, then add the following line:

<pre>
echo "ARTOOLKIT5_ROOT=/path/to/artoolkit; export ARTOOLKIT5_ROOT" >> ~/.bashrc
</pre>

[1]: /Installing_ARToolKit_Professional
[2]: http://developer.apple.com/xcode/
[3]: http://mesa3d.sourceforge.net/
[4]: /Building_libARvideo_using_DirectShow
[5]: /Building_libARvideo_using_QuickTime
[6]: http://sourceforge.net/projects/dsvideolib
[7]: http://www.artoolworks.com/dist/openvrml/
[8]: http://www.finkproject.org/
[9]: http://www.artoolworks.com/dist/openvrml/
[10]: http://www.openvrml.org/
[11]: http://www.artoolworks.com/dist/openscenegraph/
[12]: /Building_libARvideo_using_DirectShow
[13]: /Building_libARvideo_using_QuickTime
[14]: /ARToolKit_tutorial_1:_First_simple_ARToolKit_scene
[15]: /ARToolKit_Professional_examples