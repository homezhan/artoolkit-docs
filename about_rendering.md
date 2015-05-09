#Graphics, Models, and Rendering

##Introduction
ARToolKit includes support for loading models from the filesystem and rendering them in your scene. However, this aspect of your application is completely customisable. The support ranges from use of basic OpenGL drawing commands in some of the demos, through to high-quality rendering of a large variety of models via the OpenSceneGraph framework. Additionally, ARToolKit integrates with a wide variety of third-party rendering and game engines, including the popular Unity3D game engine via [ARToolKit for Unity][artk_unity].

ARToolKit for iOS and Android also include loading of static Wavefront .obj files (including materials) via **libEden**.

The rendering method used in the example applications in ARToolKit for Desktop is as follows:

-   OpenGL (using libARgsub_lite): simpleLite, simpleMovie, optical, opticalStereo, nftSimple, multiCube
-   OpenGL (using libARgsub): simple, stereo, multi, multiWin
-   OpenSceneGraph rendering: simpleOSG, nftBook

In ARToolKit for iOS, it is as follows:

-   OpenGL ES 1.1 (using libARgsub_es): ARAppES1
-   OpenGL ES 1.1 + libEden: ARApp2, ARAppNFT
-   OpenGL ES 2.0 (using libARgsub_es2): ARApp
-   OpenSceneGraph rendering: ARAppOSG, ARAppNFTOSG

In ARToolKit for Android, it is as follows:

-   OpenGL ES 1.1 (using javax.microedition.khronos.opengles.GL10) ARSimple, ARSimpleInteraction
-   OpenGL ES 1.1 (using libARgsub_es): ARSimpleNative, ARNativeES1, nftSimple
-   OpenGL ES 1.1 + libEden: ARSimpleNativeCars
-   OpenGL ES 2.0 (using libARgsub_es2): ARNative
-   OpenSceneGraph rendering: ARNativeOSG, nftBook

##OpenGL
ARToolKit calculates coordinates in a form suitable for use directly with OpenGL, and also includes support for drawing the video background via OpenGL. This support is available in two separate libraries. The recommended library for new applications is libARgsub_lite. The older libARgsub is also supported for legacy applications.

If you wish to plug in a new renderer, or write your own rendering code, any of the example applications that draws directly via OpenGL will provide a good framework for connecting your own renderer and/or model loader into the application.

##OpenSceneGraph
OpenSceneGraph (OSG) is a high-quality open-source scene graph framework, that allows users to deal with graphics and models in an efficient, high-performance and flexible manner. ARToolKit includes a utility library, libARosg, which exposes a small portion of the OpenSceneGraph framework to allow users to perform basic tasks of model loading and rendering.

Users wishing to perform advanced techniques with OSG can connect directly to the OSG C++ API, or extend the code provided in libARosg -- we provide full source for libARosg to enable this.

ARToolworks provides either bundled pre-built OSG binaries and headers with ARToolKit, or an installer.

###OSG licensing
OpenSceneGraph comes with it's own license, similar to the LGPL license, which allows it to be linked into a closed-source commercial application if so desired. Changes to OSG itself must be published. ARToolworks publishes its binary builds of OSG, and its source code modifications freely online [here][2].

##OpenVRML
Earlier versions of ARToolKit included an OpenVRML renderer, libARvrml. While the source code for this library is still included, this library is not actively supported, and users are encouraged to use OSG for new projects.

Although [VRML][5] is not usually associated with visually-realistic 3D content, it is flexible and well-supported by many 3D toolsets. [OpenVRML][6] provides an open-source parser and renderer for VRML97 and X3D files, including support for texturing, animation and networked content, and is supported on a variety of platforms including Windows, Mac OS X (through the [Fink package manager][3]) and Linux (through the [Debian package system][4]).

##DirectX
ARToolKit does not directly support DirectX. However, the core ARToolKit tracking is renderer-independent, so DirectX could be used provided you are able to perform any graphics-related tasks in your own code. Three core functions of libARgsub_lite would need to be emulated: code to convert an ARToolKit camera parameter matrix to a DirectX viewing frustum, code to convert an ARToolKit pose matrix to a DirectX modelview matrix, and code to draw the camera image as a video background (should this be required).

[artk_unity]: Unity:unity_about
[2]: http://www.artoolworks.com/dist/openscenegraph/
[3]: http://pdb.finkproject.org/pdb/search.php?summary=openvrml
[4]: http://packages.debian.org/src:openvrml
[5]: http://en.wikipedia.org/wiki/VRML
[6]: http://www.openvrml.org