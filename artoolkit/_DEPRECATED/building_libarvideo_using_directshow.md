# Building libARvideo Using DirectShow

## What is the relationship between libARvideo and DirectShow?

DirectShow is Microsoft's media-handling library on the Windows Platform. From the point of view of ARToolKit Professional, DirectShow provides a standardized way of accessing video capture hardware on Windows. This allows ARToolKit Professional to acquire video from a large range of USB webcams and other video capture hardware.

## Why do I need to know about DirectShow?

While the DirectShow libraries are in every release of Windows, and can be used right away, compiling applications that use the DirectShow [SDK][1] is difficult. This is mostly due to Microsoft's determination to force all users of video into using its [digital rights management][2] model (as found in Windows Vista's MediaFoundation library) and the consequent withdrawl of the DirectShow SDK from the larger DirectX SDK and Visual Studio SDKs.

Because the process of installing the DirectShow SDK is tiresome, we supply compiled binaries of ARToolKit Professional to customers - unless customers want to recompile libARvideo on Windows, installing the DirectShow SDK is unnecessary. For customers who do wish to recompiled libARvideo for their own purposes, the following guide should be of help.

#### How to install the DirectShow SDK

##### Visual Studio 2013

Visual Studio 2013 is supplied with Windows SDK 8.1, which includes the required DirectShow link libraries, and some of the required headers. Interestingly, it also includes strmbase.lib, the library implementing the DirectShow base classes, but unfortunately does not include ether the Debug version of this library (strmbasd.lib) or the header files. These would normally be required to be manually installed from the Windows SDK 7.1 samples package, however we have made a package which includes the DirectShow base classes source and compiled libraries for 32-bit and 64-bit architectures.

[Download the DirectShow base classes package][3].

If the package is un-rared retaining the absolute paths, the final package path will be something similar to: <pre>C:\Program Files\Microsoft SDKs\Windows\v7.1\Samples\multimedia\directshow\baseclasses\</pre>. No further configuration is required.

##### Visual Studio 2010 SP1 and earlier

Depending on which version of the Microsoft developer tools and/or SDK version you are using, the components of the DirectShow SDK may be split across two packages. These instructions are targeted at the simplest way to get the SDK working.

-   Download the latest DirectX SDK. At the time of writing, this is the August 2007 release. [DirectX SDK download page][4]. Install the DirectX SDK.
-   **If you are using Microsoft Visual Studio 2005** or later, download the Microsoft Platform SDK. *N.B.: In June 2006, the Platform SDK was renamed "Windows SDK".* A version of the Platform SDK is included in Microsoft's Visual Studio 2005, but without the DirectShow SDK included. So all we need from the platform SDK is the DirectShow SDK, and this can be most easily obtained by using the "Microsoft ® Windows Server® 2003 R2 Platform SDK Web Install". Don't be put off by the name, this is the valid SDK for targeting Windows XP SP2. [Platform SDK download page][5]. Install the Platform SDK, but do a custom install and deactivate everything except the DirectShow SDK.

##### Setting up Microsoft Visual Studio 2010 SP1 and earlier to use the DirectShow SDK

You can only use the "Standard" or above version of Microsoft Visual Studio to compile libARvideo's DirectShow modules. Visual Studio "Express Edition" will not work, since the Express Edition does not support ATL (which is used by the DirectShow code) [1][6]

Once you have installed the DirectX SDK (and Platform SDK if using VS2005), you need to tell Visual Studio where to find their header and library directories. Otherwise, when the ARToolKit source tries to include these files, Visual Studio won't know where to look for them. The way to tell VS where to look for files is to add them to the "search path" in the VS options.

1.  Open the dialog box for editing Visual Studio search paths settings. Go to the "Tools" menu, and choose "Options". Then in the dialog box that opens, in the left-hand pane click on "Projects and Solutions", and then underneath that click on "VC++ Directories". ![Adding DirectShow SDK to Visual Studio Path 1][Adding_DirectShow_SDK_to_Visual_Studio_path_1]
2.  In the right-hand pane, click the menu labelled "Show directories for" and choose "Include files". Check that the DirectX SDK Includes\\ path is listed. (It should have been automatically added by the DirectX SDK installer, but if not, add it manually, as per the image below.) If you are using VS 2005, you will need to add the path to the Microsoft Platform SDK Includes\\ path, and using the arrows, move it to the bottom of the list. It will be something like "C:\\Program Files\\Microsoft Platform SDK for Windows Server 2003 R2\\Include". Repeat for the Libraries\\ directories as indicated below. ![Adding DirectShow SDK to Visual Studio Path 2][Adding_DirectShow_SDK_to_Visual_Studio_path_2] ![Adding DirectShow SDK to Visual Studio Path 3][Adding_DirectShow_SDK_to_Visual_Studio_path_3]

## How to recompile libARvideo under Microsoft Visual Studio

libARvideo will only include the DirectShow video interface if the constant AR_INPUT_WINDOWS_DIRECTSHOW is defined in <AR/config.h>. This is the default, but you can double check it by opening config.h, locating the constant and checking that it has \#define in front of it, and not \#undef.

From there, compiling should be just a matter of right-clicking on "ARVideo" in the solution explorer and choosing "Build."

If you are having difficulty with these instructions, please post a message on the [forum][7]) or contact an ARToolworks support person.


[1]: http://en.wikipedia.org/wiki/Software_development_kit      "Software Development Kit on Wikipedia"
[2]: http://en.wikipedia.org/wiki/Digital_rights_management     "Digital Rights Management on Wikipedia"
[3]: http://www.artoolworks.com/support/attachments/Microsoft%20DirectShow%20Base%20Classes%20(from%20Windows%20SDK%20v7.1%20samples).rar
[4]: http://msdn.microsoft.com/en-us/xna/aa937788.aspx
[5]: http://www.microsoft.com/downloads/details.aspx?FamilyID=0baf2b35-c656-4969-ace8-e4c0c0716adb&DisplayLang=en
[6]: http://www.microsoft.com/express/support/support-faq.aspx
[7]: http://www.artoolworks.com/support/forum       "ARToolworks Forum"

[Adding_DirectShow_SDK_to_Visual_Studio_path_1.png]: Adding_DirectShow_SDK_to_Visual_Studio_path_1.png
[Adding_DirectShow_SDK_to_Visual_Studio_path_2.png]: Adding_DirectShow_SDK_to_Visual_Studio_path_2.png
[Adding_DirectShow_SDK_to_Visual_Studio_path_3.png]: Adding_DirectShow_SDK_to_Visual_Studio_path_3.png