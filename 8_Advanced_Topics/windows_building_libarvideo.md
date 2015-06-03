# Building libARvideo

## What is the relationship between libARvideo and a Video Library?
ARToolKit uses video libraries as a standardized way of accessing video capture hardware (like webcams) on your computer. On Windows, you have the option of using QuickTime or DirectShow. On OS X, we use QuickTime.

###What is DirectShow
DirectShow is Microsoft's media-handling library on the Windows Platform. While the DirectShow libraries are in every release of Windows, and can be used right away, compiling applications that use the DirectShow [SDK][1a] is difficult. This is mostly due to Microsoft's determination to force all users of video into using its [digital rights management][2a] model (as found in Windows Vista's MediaFoundation library) and the consequent withdrawal of the DirectShow SDK from the larger DirectX SDK and Visual Studio SDKs.

Because the process of installing the DirectShow SDK is tiresome, we supply compiled binaries of ARToolKit to customers - unless customers want to recompile libARvideo on Windows, installing the DirectShow SDK is unnecessary. For customers who do wish to recompile libARvideo for their own purposes, the following guide should be of help.

###What is QuickTime?
QuickTime is Apple's media-handling library, available on both Mac OS X and the Windows platforms. One benefit QuickTime has over DirectShow is the ability to read pre-recorded video from files on disk or via network streaming (for uses such as calibrating a camera on a device which the tools do not run).

While the QuickTime libraries and SDK are in every release of Mac OS X, and can be used right away, they are not installed by default on Windows. Every user who wants to run an ARToolKit application that uses QuickTime for video capture on Windows will need to install QuickTime. This is not onerous - any user who already has iTunes for Windows installed will have QuickTime installed already. Other users should visit the [QuickTime for Windows download page][1].

Additionally, for customers using Windows who do wish to recompile libARvideo for their own purposes, the QuickTime SDK must be downloaded and installed.

##Installing the DirectShow SDK

###Visual Studio 2013
Visual Studio 2013 is supplied with Windows SDK 8.1, which includes the required DirectShow link libraries, and some of the required headers. Interestingly, it also includes strmbase.lib, the library implementing the DirectShow base classes, but unfortunately does not include ether the Debug version of this library (strmbasd.lib) or the header files. These would normally be required to be manually installed from the Windows SDK 7.1 samples package. However, we have made a package which includes the DirectShow base classes source and compiled libraries for 32-bit and 64-bit architectures.

[Download the DirectShow base classes package][3a].

If the package is un-rared retaining the absolute paths, the final package path will be something similar to: `C:\Program Files\Microsoft SDKs\Windows\v7.1\Samples\multimedia\directshow\baseclasses\`. No further configuration is required.

### Visual Studio 2010 SP1 and earlier

Depending on which version of the Microsoft developer tools and/or SDK version you are using, the components of the DirectShow SDK may be split across two packages. These instructions are targeted at the simplest way to get the SDK working.

-   Download the latest DirectX SDK. At the time of writing, this is the August 2007 release. [DirectX SDK download page][4a]. Install the DirectX SDK.
-   **If you are using Microsoft Visual Studio 2005** or later, download the Microsoft Platform SDK. *N.B.: In June 2006, the Platform SDK was renamed "Windows SDK".* A version of the Platform SDK is included in Microsoft's Visual Studio 2005, but without the DirectShow SDK included. So all we need from the platform SDK is the DirectShow SDK, and this can be most easily obtained by using the "Microsoft ® Windows Server® 2003 R2 Platform SDK Web Install". Don't be put off by the name, this is the valid SDK for targeting Windows XP SP2. [Platform SDK download page][5a]. Install the Platform SDK, but do a custom install and deactivate everything except the DirectShow SDK.

###Setting up Microsoft Visual Studio 2010 SP1 and earlier to use the DirectShow SDK

You can only use the "Standard" or above version of Microsoft Visual Studio to compile libARvideo's DirectShow modules. Visual Studio "Express Edition" will not work, since the Express Edition does not support ATL (which is used by the DirectShow code) [1][6a]

Once you have installed the DirectX SDK (and Platform SDK if using VS2005), you need to tell Visual Studio where to find their header and library directories. Otherwise, when the ARToolKit source tries to include these files, Visual Studio won't know where to look for them. The way to tell VS where to look for files is to add them to the "search path" in the VS options.

1.  Open the dialog box for editing Visual Studio search paths settings. Go to the "Tools" menu, and choose "Options". Then in the dialog box that opens, in the left-hand pane click on "Projects and Solutions", and then underneath that click on "VC++ Directories". ![Adding DirectShow SDK to Visual Studio Path 1][Adding_DirectShow_SDK_to_Visual_Studio_path_1]
2.  In the right-hand pane, click the menu labelled "Show directories for" and choose "Include files". Check that the DirectX SDK Includes\\ path is listed. (It should have been automatically added by the DirectX SDK installer, but if not, add it manually, as per the image below.) If you are using VS 2005, you will need to add the path to the Microsoft Platform SDK Includes\\ path, and using the arrows, move it to the bottom of the list. It will be something like "C:\\Program Files\\Microsoft Platform SDK for Windows Server 2003 R2\\Include". Repeat for the Libraries\\ directories as indicated below. ![Adding DirectShow SDK to Visual Studio Path 2][Adding_DirectShow_SDK_to_Visual_Studio_path_2] ![Adding DirectShow SDK to Visual Studio Path 3][Adding_DirectShow_SDK_to_Visual_Studio_path_3]

## How to install the QuickTime SDK

Mac OS X: The QuickTime SDK is installed by default along with XCode, and no further action should be needed.

Windows: [Download the QuickTime SDK for Windows][2]. We recommend installing the SDK to the default location, `C:\\Program Files\\QuickTime SDK`. This is because the paths in ARToolKit’s build files expect this location.

### Setting up Microsoft Visual Studio to use the QuickTime SDK

ARToolKit's build files expect to find QuickTime at `C:\\Program Files\\QuickTime SDK`. Unless you change this location, no further setup is required.

## How to Recompile libARvideo under Microsoft Visual Studio
libARvideo will include the video interface defined in `AR/config.h`. To use DirectShow (default), define `AR_INPUT_WINDOWS_DIRECTSHOW`. To use QuickTime, define `AR_INPUT_QUICKTIME`. To define a constant, open `AR/config.h', locate the desired constant block, and change the `\#undef` in front of the variable to `\#define`.

*Note: Defining `AR_INPUT_QUICKTIME` enables the use of QuickTime, but does not make it the default video interface.* If you also wish to have the QuickTime module used by default, locate the constant AR_DEFAULT_INPUT_QUICKTIME in `AR/config.h` and enable it as described above. The QuickTime module can be selected at runtime by passing `-device=QUICKTIME` in the video config string (the parameter to `arVideoOpen()`).

From there, compiling should be just a matter of right-clicking on "ARVideo" in the solution explorer and choosing "Build."

If you are having difficulty with these instructions, please post a message on the [forum][3].

[1]: http://www.apple.com/quicktime/download/       "Download QuickTime For Windows"
[2]: http://developer.apple.com/quicktime/download/ "Download QuickTime SDK For Windows"
[3]: http://www.artoolworks.com/support/forum       "ARToolworks Forum"
[1a]: http://en.wikipedia.org/wiki/Software_development_kit      "Software Development Kit on Wikipedia"
[2a]: http://en.wikipedia.org/wiki/Digital_rights_management     "Digital Rights Management on Wikipedia"
[3a]: http://www.artoolworks.com/support/attachments/Microsoft%20DirectShow%20Base%20Classes%20(from%20Windows%20SDK%20v7.1%20samples).rar
[4a]: http://msdn.microsoft.com/en-us/xna/aa937788.aspx
[5a]: http://www.microsoft.com/downloads/details.aspx?FamilyID=0baf2b35-c656-4969-ace8-e4c0c0716adb&DisplayLang=en
[6a]: http://www.microsoft.com/express/support/support-faq.aspx
[Adding_DirectShow_SDK_to_Visual_Studio_path_1]: :adding_directshow_sdk_to_visual_studio_path_1.png
[Adding_DirectShow_SDK_to_Visual_Studio_path_2]: :adding_directshow_sdk_to_visual_studio_path_2.png
[Adding_DirectShow_SDK_to_Visual_Studio_path_3]: :adding_directshow_sdk_to_visual_studio_path_3.png
