# Intalling ARToolkit Professional

## Installing

ARToolKit Professional is supplied as pre-built binaries for each platform, plus source code for most of the SDK libraries and utilities, full source for the examples, and documentation.

### Windows

Run the ARToolKit installer executable and follow the prompts.

By default, ARToolKit will be installed into a folder inside your Program Files folder. Start menu items are created to allow you to quickly open the folder containing the installed software, to open a command-line prompt with the path set to this folder, and to read documentation and access this support site. The installer also automatically creates the ARTOOLKIT5_ROOT environment variable to point to your chosen install location.

If you are upgrading to a newer version, it is generally safe to install over the old version. Before upgrading, save any modifications you have made to any ARToolKit source or example code, and then run the installer. The installer will add or update new files, and remove unneeded old files.

### Mac OS X

The SDK is supplied as an archive file (.tar.gz or .zip file) which need only be unpacked to a location of your choice, e.g. \~/SDKs/. Drop the archive into your chosen location and double-click it in the Finder to unpack it.

Once unpacked, to set the ARTOOLKIT5_ROOT so that other software can find ARToolKit Professional, open a Terminal window, and run the script artoolkit5-setenv: (Example assumes ARToolKit5 is in \~/SDKs/):
<pre>
cd ~/SDKs/ARToolKit5/
./share/artoolkit5-setenv
</pre>

### Linux

The SDK is supplied as an archive file (.tar.gz) which need only be unpacked to a location of your choice, e.g. \~/SDKs/. Move the archive into your chosen location and use the following command in your terminal to unpack it:
<pre>
tar xzvf ARToolKit5-bin-*.tar.gz
</pre>

Once unpacked, to set the ARTOOLKIT5_ROOT so that other software can find ARToolKit Professional, open a terminal window, and run the script artoolkit5-setenv: (Example assumes ARToolKit5 is in \~/SDKs/):
<pre>
cd ~/SDKs/ARToolKit5/
./share/artoolkit5-setenv
</pre>

## Running the examples

ARToolKit Professional includes a variety of examples demonstrating ARToolKit programming techniques. After installation, the executables for these applications can be found in the `bin` directory inside your ARToolKit directory.

The simpleLite example is the most straightforward example. It can be run to test your ARToolKit installation is functioning correctly.

*An explanation of the sourcecode of this example can be found on the page [ARToolKit tutorial 1: First simple ARToolKit scene][1]. More detailed information about the techniques demonstrated in each example can be found on the page [ARToolKit Professional examples][2].*

### Windows:

simpleLite can be opened by double-clicking its icon in the ARToolKit5\\bin directory. Alternately, you can run it from the command line:

-   Open a command-line window (cmd.exe).
-   Navigate to your ARToolKit5\\bin directory.
-   Type: simpleLite.exe

### Mac OS X:

-   Bundled applications are generated for the examples. Open the "bin" directory in the Finder and double-click the "simpleLite" example app.

### Linux:

-   simpleLite can be launched from a terminal window thus:

`./simpleLite`

## Beginning your own development

In beginning your own development, it is recommended that you create your own project outside the ARToolKit folder, and treat ARToolKit Professional as an external SDK. However, it is also perfectly permissible to begin by modifying one or more of the example applications. ARToolKit is supplied with project files for each supported platform. The project files allow you to rebuild ARToolKit from source, and act as examples of how to structure your own application builds (e.g. required link libraries).

### Required external software

-   A supported compiler or IDE is required to use ARToolKit Professional:
    -   Windows: Microsoft Visual Studio 2012 and Microsoft Visual Studio 2010 SP1 are supported. The free Microsoft Visual Studio Express Edition will also work.
    -   Mac OS X: Xcode tools v5.1 under Mac OS X 10.9 or later is required. Xcode 6 under Mac OS X 10.10 is recommended. Xcode may be obtained free from [Apple][3].
    -   Linux: GCC 4.4 is required. GCC 4.8 or later is recommended.

Where ARToolKit libraries require external DLLs, these are generally supplied with ARToolKit. Exceptions are listed below.

#### Windows

-   The optional video capture sources require some external software:
    -   QuickTime movie files as video source: QuickTIme 6.4 or later must be installed. [Download here][4].
    -   Point Grey camera: The Flycapture SDK (distributed with Point Grey Cameras) must be installed.
    -   Canon HDCam64 cameras: The Canon HDCam64 camera control library must be installed.

#### Mac OS X

-   OpenSceneGraph (optional; The ARToolKit OSG renderer requires OpenSceneGraph). Use the installer provided [here][5].

#### Linux

ARToolKit follows the Linux model whereby required software is externally installed. The following packages are required to be installed in your package manager to **run** the ARToolKit examples. (Additional packages required to build ARToolKit from source are listed on that help page.)

-   OpenGL: Package 'xorg'
-   GLUT: Package 'freeglut3'. *Alternatively, GLUT can be built from source and is also included in the MESA 3D libraries: [1][6]*
-   Video4Linux, lib1394dc, or GStreamer. Packages: 'libv4l2-0", 'libdc1394-22' (for lib1394 version 2.x) or 'libdc1394-13' (for lib1394 version 1.x), and 'libgstreamer0.10'.
-   OpenSceneGraph (optional; The ARToolKit OSG renderer requires OpenSceneGraph). Package 'openscenegraph'.
-   OpenVRML (optional; the ARToolKit VRML renderer requires OpenVRML): Binary deb packages are available [here][7].

### Opening the project files

#### Windows

Open the "VisualStudio" directory, then the appropriate directory for your compiler version, and then the "ARToolKit5.sln" solution file.

#### Mac OS X

Open the ARToolKit5.xcodeproj, found inside the Xcode folder.

#### Linux

The SDK build system uses a Configure script and makefiles.

[1]: /ARToolKit_tutorial_1:_First_simple_ARToolKit_scene
[2]: /ARToolKit_Professional_examples
[3]: http://developer.apple.com/xcode/
[4]: http://www.apple.com/quicktime/download/
[5]: http://www.artoolworks.com/dist/openscenegraph/
[6]: http://mesa3d.sourceforge.net/
[7]: http://www.openvrml.org/