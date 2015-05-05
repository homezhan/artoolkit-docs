#ARToolKit for Unity on OS X

##Requirements
1.   You must have a Unity Pro license to be able to export projects from Unity that use the ARToolKit for Unity plugins.

##Troubleshooting
Many common issues can be diagnosed by looking at Unity's Editor.log or Player.log. On OS X, these are located in the folder \~/Library/Logs/Unity/. The OS X console viewer (/Applications/Utilities/Console.app) is a good means of easily viewing these logs.

### NFT Tracking Works in Editor, not in Player
This is a known issue with Unity 4.x (confirmed on Unity 4.1.x and 4.2.x) where when building the standalone OS X player, the StreamingAssets folder from the Unity project is not being correctly copied into the built application bundle. You can confirm this problem by looking for errors in the Unity Player.log which indicate that StreamingAssets folder is missing.

A workaround is to manually copy the StreamingAssets folder into the bundle. To do this:

1.  Locate the built standalone Unity Player application, right-click on
    it, and choose "Show package contents..." [<File:Unity> Player OS X
    show pacakge
    contents.png](/File:Unity_Player_OS_X_show_pacakge_contents.png "wikilink")
2.  Locate the "StreamingAssets" folder from your project (with the NFT
    datasets inside) [<File:Unity> OS X StreamingAssets
    folder.png](/File:Unity_OS_X_StreamingAssets_folder.png "wikilink")
3.  Drag that folder into the "Contents" folder of the built application
    package. [<File:Unity> OS X dragging StreamingAssets
    folder.png](/File:Unity_OS_X_dragging_StreamingAssets_folder.png "wikilink")

[Category:ARToolKit for Unity](/Category:ARToolKit_for_Unity "wikilink")