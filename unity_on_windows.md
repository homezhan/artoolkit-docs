#ARToolKit for Unity on Windows

##Requirements
1.   You must have a Unity Pro license to be able to run plugins (which ARToolKit is).
2.   ARToolKit for Unity has a set of dependent DLLs which you must include along with any standalone app built for Windows. Please see below under "Deployment" for more detail.

##Setup

### Choosing Between Multiple Webcams
ARToolKit for Unity follows the standard ARToolKit video configuration commands using [DirectShow][directshow_config].

If using the default video module (WinDS), you can have ARToolKit for Unity use a second webcam or video input source by adding `-devNum=2` in the video configuration dialog.
![Screenshot using a second camera with WinDS.][winds_camera]

If you wish to use the alternate video module (WinDSVL), you must specify either the DirectShow "friendly name" for the device, or a device UUID, using XML. An example is: `-device=WinDSVL <?xml version="1.0" encoding="UTF-8"?><dsvl_input><camera show_format_dialog="false" friendly_name="Logitech Quickcam"><pixel_format><RGB32 flip_h="false" flip_v="true" /></pixel_format></camera></dsvl_input>`

##Troubleshooting
Many common issues can be diagnosed by looking at Unity's Editor.log or Player.log. On Windows, Player.log is located in the folder `EXECNAME_Data\output_log.txt` where EXECNAME_Data is a folder next to the executable with your game.

### DllNotFoundException
If you encounter an error like "DllNotFoundException: [...]/Assets/Plugins/ARWrapper.dll" (with [...] as the path to your Unity project).

In spite of the ARWrapper.dll clearly being in the referred to folder, the Unity Editor may not be able to find a required dependent DLL (i.e. a DLL on which the ARWrapper DLL depends). Confusingly, the dependent DLLs must be present in same folder as the .exe file of the **host application** (the Unity Editor, in this case), which is typically C:\\Program Files (x86)\\Unity\\Editor. The required DLLs are normally (at least since ARToolKit for Unity v2.0.3) installed by the ARToolKit for Unity installer, but if you are having difficulty, you can double check. Check that the following are present in that folder:
-   ARvideo.dll
-   pthreadVC2.dll
-   opencv_core246.dll
-   opencv_flann246.dll
-   DSVL.dll

Also required are the Visual Studio 2010 runtimes, although these must be installed into the Windows system.

##Deployment
When deploying a standalone Unity application for Windows, you must also deploy the ARToolKit for Unity plugin's dependent DLLs. In this case, you should create an installer for your standalone app. Your installer, as well as installing your app's .exe file, also installs the required DLLs, including the Visual Studio runtimes (ARToolKit for Unity is built with Visual Studio 2013 update 3 at the time of writing). For your convenience, ARToolKit for Unity comes with a folder named "redist"
which contains the required DLLs, plus the vc_redist installer application which your installer must run to ensure that Visual Studio runtime libraries are available in the Windows system on the user's machine. The latter is an unfortunate requirement faced by *all* 3rd-party software for Windows. If you are deploying a 64-bit executable, use the "redist64" folder instead.

###Deployment Example: [Innosetup][innosetup]
Once you have specified the other parts of your app which need to be installed, the required lines for an InnoSetup .iss file to install the dependencies for a 32-bit executable would be something like:

    [Files]
    Source: "{pf32}\ARUnity\redist\vcredist_x86.exe"; DestDir: "{app}"; Flags: ignoreversion
    Source: "{pf32}\ARUnity\redist\ARvideo.dll"; DestDir: "{app}"; Flags: ignoreversion
    Source: "{pf32}\ARUnity\redist\DSVL.dll"; DestDir: "{app}"; Flags: ignoreversion
    Source: "{pf32}\ARUnity\redist\pthreadVC2.dll"; DestDir: "{app}"; Flags: ignoreversion
    Source: "{pf32}\ARUnity\redist\opencv_core2410.dll"; DestDir: "{app}"; Flags: ignoreversion
    Source: "{pf32}\ARUnity\redist\opencv_flann2410.dll"; DestDir: "{app}"; Flags: ignoreversion
    
    [Run]
    Filename: {app}\vcredist_x86.exe; Components: runtime; Parameters: "/passive /Q:a /c:""msiexec /qb /i vcredist.msi"" "; StatusMsg: Installing Visual Studio 2013 RunTime...

or for a 64-bit executable:

    [Files]
    Source: "{pf32}\ARUnity\redist64\vcredist_x64.exe"; DestDir: "{app}"; Flags: ignoreversion
    Source: "{pf32}\ARUnity\redist64\ARvideo.dll"; DestDir: "{app}"; Flags: ignoreversion
    Source: "{pf32}\ARUnity\redist64\DSVL.dll"; DestDir: "{app}"; Flags: ignoreversion
    Source: "{pf32}\ARUnity\redist64\pthreadVC2.dll"; DestDir: "{app}"; Flags: ignoreversion
    Source: "{pf32}\ARUnity\redist64\opencv_core2410.dll"; DestDir: "{app}"; Flags: ignoreversion
    Source: "{pf32}\ARUnity\redist64\opencv_flann2410.dll"; DestDir: "{app}"; Flags: ignoreversion
    
    [Run]
    Filename: {app}\vcredist_x64.exe; Components: runtime; Parameters: "/passive /Q:a /c:""msiexec /qb /i vcredist.msi"" "; StatusMsg: Installing Visual Studio 2013 RunTime...

You might need to adjust the above if the path to your standalone's .exe
is a subfolder of {app}.

[directshow_config]:/Configuring_video_capture_in_ARToolKit_Professional#AR_VIDEO_DEVICE_WINDOWS_DIRECTSHOW "wikilink"
[winds_camera]:/File:ARToolKit_for_Unity_Windows_WinDS_second_camera.png "wikilink"
[innosetup]:http://www.jrsoftware.org/isinfo.php/
[Category:ARToolKit for Unity](/Category:ARToolKit_for_Unity "wikilink")