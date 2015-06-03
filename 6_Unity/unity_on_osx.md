#ARToolKit for Unity on OS X
To get started with using ARToolKit for Unity on OS X, first visit our [Getting Started][unity_getting_started] guide.

##Requirements

-   You must have a Unity Pro license to be able to export projects from Unity that use the ARToolKit for Unity plugins.

##Troubleshooting
Many common issues can be diagnosed by looking at Unity's Editor.log or Player.log. On OS X, these are located in the folder `\~/Library/Logs/Unity/`. The OS X console viewer (`/Applications/Utilities/Console.app1) is a good means of easily viewing these logs.

### NFT Tracking Works in Editor, not in Player
This is a known issue with Unity 4.x (confirmed on Unity 4.1.x and 4.2.x) when building the standalone OS X player, the StreamingAssets folder from the Unity project is not being correctly copied into the built application bundle. You can confirm this problem by looking for errors in the Unity Player.log which indicate that StreamingAssets folder is missing.

A workaround is to manually copy the StreamingAssets folder into the bundle. To do this:

1.  Locate the built standalone Unity Player application, right-click on it, and choose "Show package contents..." ![Show package contents screenshot.][show_package_contents]
2.  Locate the "StreamingAssets" folder from your project (with the NFT datasets inside) ![OS X StreamingAssets folder screenshot.][streamingassets_folder]
3.  Drag that folder into the "Contents" folder of the built application package. ![Dragging contents into StreamingAssets folder.][dragging_streamingassets_folder]


[unity_getting_started]: 6_Unity:unity_getting_started
[show_pacakge_contents]: :unity_player_os_x_show_pacakge_contents.png
[streamingassets_folder]: :unity_os_x_streamingassets_folder.png
[dragging_streamingassets_folder]: :unity_os_x_dragging_streamingassets_folder.png
