#Movie Textures on iOS
ARToolKit natively supports real-time playback of movie files (including audio) in the augmented environment on iOS. Video can be manipulated in the scene, including being attached to a marker.

A fully functional example named "ARAppMovie" is provided with ARToolKit for iOS.

Movie support is provided via at 3 different levels of abstraction.

-   A subclass of VEObject, VEObjectMovie provides a means to directly included a video file as an object in an application like ARAppMovie, which uses the VirtualEnvironment class.
-   A private Objective-C class named "MovieVideo" provides the underlying interface between VEObjectMovie and iOS's AVFoundation. The interface to this class may be found at `include/AR/sys/MovieVideo.h`.
-   Video files may also be used as the video input stream to the tracking process, via libARvideo.

As MovieVideo is linked to by libARvideo on iOS, all applications must link against `AVFoundation.framework` and `AudioToolbox.framework`.

##Format Support
Any video file playable on that iOS device can be handled by the MovieVideo class, provided the movie media is on the local filesystem. I.e. streaming media cannot be handled. If you wish to play media over the network, you will need to use another means to fetch the media completely in advance, cache it on the local filesystem, and then pass the path to the media to ARToolKit.

Media decoding is resource intensive. It is highly recommended that you test the media on your preferred range of target devices. Additionally, performance benefits will be realised if the media fits inside power-of-two sized textures, e.g. width and height of 512 pixels or fewer.

## VEObjectMovie
For applications which use the VirtualEnvironment class, objects specified in objects.dat which end in ".mov", ".mp4", or ".m4v" will be loaded by the VEObjectMovie class (provided VEObjectMovie has been compiled into the application binary).

VEObjectMovie loads and draws a movie file from the local file system as a video texture, using the MovieVideo class. It allows playback of MPEG4 video (with or without audio) in the virtual environment. Recommended maximum movie size is 512 pixels or less in both the vertical and horizontal dimensions.

Without any scaling or offset, the movie object is sized so that its largest side is the equivalent of 80 drawing units (usually 80 millimeters). The origin of the object is the lower-left corner of the movie texture. Unrotated, the movie file will be placed in the x-y plane, with its upper surface facing the +z axis. To position the movie differently, apply translation/rotation/scale factors in the VEObject configuration file.

## MovieVideo class
MovieVideo can be used directly when more complicated movie manipulation is required (for example, adjustment of the playback position, or user-interaction).

See the class header for more detail.

Users of the MovieVideo class can listen for the NSNotification `MovieVideoPlayBackEndedNotification` to be notified of the end of playback of a movie file.

## Movies in libARvideo
Video input via [libARvideo][config_video_capture] requires frames to be fetched via polling. A new parameter `AR_VIDEO_PARAM_IOS_ASYNC` can be queried to find out if frames are delivered asynchronously (CameraVideo) or must be fetched by polling (MovieVideo).

[config_video_capture]: 2_Configuration:config_video_capture
