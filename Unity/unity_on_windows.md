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
Deploying an ARToolKit for Unity application on Windows is much like deploying a normal ARToolKit application on Windows. We have examples and documentation [here][deploy].

[directshow_config]:/Configuring_video_capture_in_ARToolKit_Professional#AR_VIDEO_DEVICE_WINDOWS_DIRECTSHOW "wikilink"
[winds_camera]:/File:ARToolKit_for_Unity_Windows_WinDS_second_camera.png "wikilink"
[deploy]:/deploying_an_application
[Category:ARToolKit for Unity](/Category:ARToolKit_for_Unity "wikilink")