#ARToolKit for Unity on Windows
To get started with using ARToolKit for Unity on Windows, first visit our [Getting Started][unity_getting_started] guide.

##Requirements
- You must have a Unity Pro or Personal license to be able to use the ARToolKit plugin.  
- ARToolKit for Unity has a set of dependent DLLs which you must include along with any standalone app built for Windows. Please see [**Deployment**] [general_deploy_application] for more details.

##Setup

### Choosing Between Multiple Webcams
ARToolKit for Unity follows the standard ARToolKit video configuration commands using [DirectShow][config_video_capture].

If using the default video module (WinDS), you can have ARToolKit for Unity use a second webcam or video input source by adding `-devNum=2` in the video configuration dialog.
![Screenshot using a second camera with WinDS.][winds_camera]

If you wish to use the alternate video module (WinDSVL), you must specify either the DirectShow "friendly name" for the device, or a device UUID, using XML. An example is: `-device=WinDSVL <?xml version="1.0" encoding="UTF-8"?><dsvl_input><camera show_format_dialog="false" friendly_name="Logitech Quickcam"><pixel_format><RGB32 flip_h="false" flip_v="true" /></pixel_format></camera></dsvl_input>`

##Troubleshooting
Many common issues can be diagnosed by looking at Unity's Editor.log or Player.log. On Windows, Player.log is located in the folder `EXECNAME_Data\output_log.txt` where EXECNAME_Data is a folder next to the executable with your game.

### DllNotFoundException
If you encounter an error like "DllNotFoundException: [...]/Assets/Plugins/ARWrapper.dll" (with [...] as the path to your Unity project).

In spite of the ARWrapper.dll clearly being in the referred to folder, the Unity Editor may not be able to find a required dependent DLL (i.e. a DLL on which the ARWrapper DLL depends). Confusingly, the dependent DLLs must be present in same folder as the .exe file of the *host application* (the Unity Editor, in this case), which is typically `C:\Program Files (x86)\Unity\Editor`. The required DLLs are normally (at least since ARToolKit for Unity v2.0.3) installed by the ARToolKit for Unity installer, but if you are having difficulty, you can double check. Check that the following are present in that folder:

-   ARvideo.dll
-   pthreadVC2.dll
-   opencv_core246.dll
-   opencv_flann246.dll
-   DSVL.dll

Also required are the Visual Studio 2010 runtimes, although these must be installed into the Windows system.

##Deployment
See [Deploying an ARToolKit Application on Windows][general_deploy_application].


[unity_getting_started]: 6_Unity:unity_getting_started
[config_video_capture]: 2_Configuration:config_video_capture
[general_deploy_application]: 1_Getting_Started:general_deploy_application
[winds_camera]: :artoolkit_for_unity_windows_winds_second_camera.png
