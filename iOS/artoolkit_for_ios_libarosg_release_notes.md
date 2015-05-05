# ARToolkit for iOS libARosg Release Notes

These release notes apply to version: ARToolKit Professional v4.5.1 for iOS release 2

An iOS port of OpenSceneGraph's 2.9.x development branch is bundled with the current ARToolKit for iOS release. The source code from which the OSG libraries were compiled is available publicly at <http://www.artoolworks.com/dist/OpenSceneGraph/2.9.x/>.

## Usage

Projects wishing to use arOSG need to link to the statically-compiled version of the OSG libraries. Additionally a file "osgPlugins.h" needs to be included in the app's project files. (See ARAppOSG for an example.) This file should be edited to define the required libraries and plugins used in your project. If loading arbitrary .osg and .ive files, you will likely need to define all libraries and plugins as available. While the OSG static libraries themselves are large, so long as you enable optimisation and symbol stripping in your project (see the project settings for ARAppOSG) the resultant binary will be a managable size. The finished universal ARAppOSG binary, including all resources, is 16.9 MB in size, of which 13.6 MB is the actual executable, and of which just 6.6 MB would be loaded into memory for execution.

Basically, you should carefully study the project settings, files, dependencies and build phases of the ARAppOSG example for a guide to the settings you will need in your own project.

## Limitations

The following limitations apply to the bundled version of OpenSceneGraph:

-   TexGen nodes are not supported (since OpenGL ES does not support the glTexGen() functions). Therefore, models such as cow.osg (supplied with OSG) will not render their textures correctly.
-   Streaming textures are not supported, meaning that textures embedded in .ive files will not load. It is recommended that either external texture references are used in .ive files, or you can use the "osgconv" utility to convert .ive files with embedded textures to .osg files.