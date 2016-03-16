#Deploying an Application on Windows/OS X
This page lists additional information useful when deploying an application based on ARToolKit. Deployment might mean (for
example) creating an installer for users to install your application on a Windows-based PC, or submitting an OS-X application to Apple's Mac AppStore.

##Windows

### Required DLLs
When deploying a standalone ARToolKit application for Windows, you must also deploy ARToolKit's dependent DLLs. Traditionally, you would create an installer for your standalone app. Your installer, along with installing your app's .exe file, also installs the required DLLs (including the Visual Studio runtimes). The Visual Studio runtimes are installed by the vc_redist.exe (or vc_redist64.exe, for 64-bit executables) application which must be run to ensure that Visual Studio runtime libraries are available in the Windows system on the user's machine. The latter is an unfortunate requirement faced by *all* 3rd-party software for Windows.

####Deployment Example:

[Innosetup][innosetup]

Once you have specified the other parts of your app which need to be installed, the required lines for an InnoSetup .iss file to install the dependencies for a 32-bit executable would be something like:

    [Files]
    Source: "{pf32}\redist\vcredist_x86.exe"; DestDir: "{app}"; Flags: ignoreversion
    Source: "{pf32}\redist\ARvideo.dll"; DestDir: "{app}"; Flags: ignoreversion
    Source: "{pf32}\redist\DSVL.dll"; DestDir: "{app}"; Flags: ignoreversion
    Source: "{pf32}\redist\pthreadVC2.dll"; DestDir: "{app}"; Flags: ignoreversion

    [Run]
    Filename: {app}\vcredist_x86.exe; Parameters: "/install /quiet /norestart"; StatusMsg: Installing Visual Studio 2013 RunTime...

or for a 64-bit executable:

    [Files]
    Source: "{pf32}\redist64\vcredist_x64.exe"; DestDir: "{app}"; Flags: ignoreversion
    Source: "{pf32}\redist64\ARvideo.dll"; DestDir: "{app}"; Flags: ignoreversion
    Source: "{pf32}\redist64\DSVL.dll"; DestDir: "{app}"; Flags: ignoreversion
    Source: "{pf32}\redist64\pthreadVC2.dll"; DestDir: "{app}"; Flags: ignoreversion

    [Run]
    Filename: {app}\vcredist_x64.exe; Parameters: "/install /quiet /norestart"; StatusMsg: Installing Visual Studio 2013 RunTime...

You might need to adjust the above if the path to your standalone's .exe is a subfolder of {app}.

Additionally, if you use the QuickTime support included in ARvideo, you should obtain the redistributable installer for QuickTime from Apple via Apple Developer Support.

##OS X

### Bundling and code signing dependent dylibs
ARToolKit Professional for OS X has dependency on some .dylibs. At the time of writing, these are the OpenCV core and flann libraries. These should be copied into your application package. When code signing your application, you will find that the .dylibs required to be bundled inside your application package need to also be code signed and that Xcode doesn't automatically do this. The easiest way to do this is to add a "Run script" build step to your build. Set things up as indicated in the following image:

![Code signing dylibs in Xcode.][dylibs]

[innosetup]: http://www.jrsoftware.org/isinfo.php
[dylibs]: :artoolkit_xcode_code_sign_dylibs.png
