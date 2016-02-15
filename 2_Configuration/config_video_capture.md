#Configuring Video Capture in ARToolKit
ARToolKit includes libARvideo, a cross-platform library which captures video from a variety of different sources. In general, most users of ARToolKit who have a single webcam attached to their system will never delve into the workings of this library. However, the module or modules inside this library generally allow for a degree of configuration to control parameters of the capture sources with which they interface.

##Changing Video Configuration
This section of the manual details some of the configuration options available with libARvideo.

### Setting Configuration at Run Time
Video configurations are passed to libARvideo in a standard way; as a c-string containing text. What to put in the *contents* of the string depends on your capture source.

The contents of the string are different for different capture sources because although libARvideo presents a standard API for passing video to other code (e.g. libAR, libARgsub_lite and libARgsub), there is custom code inside libARvideo for each capture source (e.g. QuickTime, DirectShow, libdc1394). The capture sources generally implement a variety of different approaches to video stream acquisition. So, the configuration parameters are different depending on the underlying capture module being used.

The simplest way to specify the video configuration (without recompiling the example applications) is to create an [environment variable][general_environment_variables] `ARTOOLKIT5_VCONF` with the video configuration you wish to use.

####ARToolKit Utilities
Some of the ARToolKit utilities (including [calib_camera][config_camera_calibration], [calib_stereo][config_camera_stereo_tracking] and check_id) accept video configuration(s) as command-line parameters. The desired configuration is passed after a parameter "--vconf" (or --vconfL or --vconfR for calib_stereo). Note that if the video configuration string includes spaces, it must be quoted to prevent the shell passing it as multiple parameters.

### Setting Configuration Programmatically
Video configuration can also be passed to libARvideo programmatically (as the sole parameter to the arVideoOpen() call). When no string (NULL) or an empty string ("") is passed, libARvideo looks for an environment variable "ARTOOLKIT5_VCONF" (as mentioned above) for the string. If this environment variable is not found, the video module will use a default configuration.

In most of the ARToolKit examples, the video configuration is specified in a string named "vconf". Do a search in your source editor for "vconf" to see this. So in most of the examples, editing the vconf string in the source code will change the video configuration being used.

Of course, editing source code requires recompiling for the changes to take effect, so a few of the examples accept a command-line parameter and use this as vconf. You can look at the source code to see if a given example does so.

#### ARToolKit for Unity
ARToolKit for Unity allows you to specify video configuration separately for each supported platform directly in the Unity Editor.

##Capture Sources and Switching Them
Where more than one capture source has been compiled into libARvideo on a given platform, you are allowed to switch between the options.

This table lists the capture sources available on each platform. _Note: If you have a binary release of ARToolKit, not all of these capture sources may have been compiled into your copy!_:

| Platform                                          | Capture source (descriptive name) | Constant required in <AR/config.h> for this source to be compiled into libARvideo | video config string to select this capture source | Avail.: (1)             | Unavail.: (2) |
|---------------------------------------------------|-----------------------------------|-----------------------------------------------------------------------------------|---------------------------------------------------|-------------------------|---------------|
| All                                               | Dummy input                       | AR\_INPUT\_DUMMY                                                                    | -device=Dummy                                     | 4.0.0                   |               |
| Mac OS X, Windows, Linux                          | JPEG image input                  | AR\_INPUT\_IMAGE                                                                    | -device=Image                                     | 4.6.2                   |               |
| Linux                                             | Video4Linux                       | AR\_INPUT\_V4L                                                                      | -device=LinuxV4L                                  | 4.0.0                   |               |
| Linux                                             | GStreamer                         | AR\_INPUT\_GSTREAMER                                                                | -device=GStreamer                                 | 4.3.2                   |               |
| Linux                                             | libdc1394                         | AR\_INPUT\_1394CAM                                                                  | -device=Linux1394Cam                              | 4.0.0                   |               |
| Mac OS X, Windows                                 | QuickTime® (enhanced)            | AR\_INPUT\_QUICKTIME                                                                | -device=QUICKTIME                                 | 4.3.0                   |               |
| Windows                                           | DirectShow®                      | AR\_INPUT\_WINDOWS\_DIRECTSHOW                                                       | -device=WinDS                                     | 4.0.0644                | 4.0.065,4.1.x |
| Windows                                           | DSVideoLib                        | AR\_INPUT\_WINDOWS\_DSVIDEOLIB                                                       | -device=WinDSVL                                   | 4.1.0                   |               |
| Windows                                           | DragonFly FlyCapture®            | AR\_INPUT\_WINDOWS\_DRAGONFLY                                                        | -device=WinDF                                     | 4.0.0644                | 4.0.065       |
| Mac OS X                                          | QuickTime®                       | AR\_INPUT\_QUICKTIME\_OLD                                                            | -device=QUICKTIME_OLD                             | 4.0.0                   |               |
| Windows                                           | HDCam64                           | AR\_INPUT\_WINDOWS\_HDCAM                                                            | -device=WinHD                                     | 4.0.0644                | 4.0.065       |
| Linux                                             | libdv                             | AR\_INPUT\_DV                                                                       | -device=LinuxDV                                   | 4.0.0                   | 4.1.x, 4.3.x  |
| SGI Irix                                          | SGI video input                   | AR\_INPUT\_SGI                                                                      | -device=SGI                                       | 4.0.0                   | 4.1.x, 4.3.x  |
| Mac OS X                                          | QuickTime® (v7.0 and later)      | AR\_INPUT\_QUICKTIME7                                                               | -device=QuickTime7                                | 4.5.0                   |               |
| iOS                                               | iOS video input                   | AR\_INPUT\_IPHONE                                                                   | -device=iPhone                                    | 4.4.3 (iOS release 1.0) |               |
| Windows                                           | Media Foundation                  | AR\_INPUT\_WINDOWS\_MEDIA\_FOUNDATION                                                 | -device=WinMF                                     | 5.1.5                   |               |
| Windows Store (Windows 8.1 and Windows Phone 8.1) | Windows Media Capture             | AR\_INPUT\_WINDOWS\_MEDIA\_CAPTURE                                                    | -device=WinMC                                     | 5.1.7                   |               |

(1): First version of ARToolKit Professional in which this capture source became available.
(2): Version(s) of ARToolKit Professional in which this source is/was unavailable or unusable.

####Video configuration options

Notes on the tables below:

-   Items inside square brackets ("[" and "]") are optional modifications to parameters, e.g. an option listed below as "-[no]foo" means that option "-foo" activates some option "foo", and option "-nofoo" deactivates it.
-   Items separated by a vertical bar ("|") are mutually-exclusive options. Use only one.
-   Items in italic typeface are placeholders, which you should replace. E.g. N indicates an integer number should be inserted.

###AR_VIDEO_DEVICE_DUMMY

| video config string | usage notes                                                                                                                   | Default value                   | Avail.: (1) | Unavail.: (2) |
|---------------------|-------------------------------------------------------------------------------------------------------------------------------|---------------------------------|-------------|---------------|
| -device=Dummy       | Select this device for use.                                                                                                   |                                 | 4.0.0       |               |
| -width=N            | Specify the width of the returned image.                                                                                      | 640                             | 4.0.0       |               |
| -height=N           | Specify the height of the returned image.                                                                                     | 480                             | 4.0.0       |               |
| -bufferpow2         | Requests that images are returned in a buffer which has power-of-two dimensions.                                              | Buffers are same size as image. | 4.4.3       |               |
| -format=X           | Return images with pixels in format X, where X is one of the following format tokens: BGRA, RGBA, RGBA_5551, RGBA_4444, y420 | BGRA                            |             |               |

###AR_VIDEO_DEVICE_IMAGE

| video config string           | usage notes                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   | Default value                                                                       | Avail.: (1) | Unavail.: (2) |
|-------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------|-------------|---------------|
| -device=Image                 | Select this device for use.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |                                                                                     | 4.6.2       |               |
| -width=N                      | Specify the width of the returned image.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      | Width of first JPEG in image list.                                                  | 4.6.2       |               |
| -height=N                     | Specify the height of the returned image.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     | Height of first JPEG in image list.                                                 | 4.6.2       |               |
| -bufferpow2                   | Requests that images are returned in a buffer which has power-of-two dimensions.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              | Buffer of same size as first JPEG in image list.                                    | 4.6.2       |               |
| -format=X                     | Return images with pixels in format X, where X is one of the following format tokens: RGB, RGBA, MONO. Note that where the format requires a conversion from the native JPEG format (usually RGB) to anything other than MONO, there is a performance penalty imposed by the conversion. ARToolKit can natively handle RGB, RGBA and MONO JPEG formats, however in some circumstances, displaying RGB format images may have a performance penalty compared to RGBA format images because of data alignment issues. Benchmarking is recommended if performance is of concern. | RGB for RGB-format JPEGs, RGBA for RGBA-format JPEGs, or MONO for monochrome JPEGs. | 4.6.2       |               |
| -[no]loop                     | In loop mode, after reading last image, the next read will return the first image. In noloop mode, no after reading the last image, no further images will be returned. May be used multiple times; later invocations will override earlier.                                                                                                                                                                                                                                                                                                                                  | -noloop                                                                             | 4.6.2       |               |
| -image=pathname               |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |                                                                                     |             |               |
| -image="pathname with spaces" | Specifies image to be read from file. Pathname is relative to the current working directory, or an absolute pathname in the system-native format. May be used an arbitrary number of times in a single config. string.                                                                                                                                                                                                                                                                                                                                                        |                                                                                     | 4.6.2       |               |

###AR_VIDEO_DEVICE_V4L

| video config string    | usage notes                               | Default value | Avail.: (1) | Unavail.: (2) |
|------------------------|-------------------------------------------|---------------|-------------|---------------|
| -device=LinuxV4L       | Select this device for use.               |               | 4.0.0       |               |
| -width=N               | Specify the width of the returned image.  | 640           | 4.0.0       |               |
| -height=N              | Specify the height of the returned image. | 480           | 4.0.0       |               |
| -contrast=N            | specifies contrast. (0.0 <-> 1.0)         |               | 4.0.0       |               |
| -brightness=N          | specifies brightness. (0.0 <-> 1.0)       |               | 4.0.0       |               |
| -color=N               | specifies color. (0.0 <-> 1.0)            |               | 4.0.0       |               |
| -hue=N                 | specifies hue. (0.0 <-> 1.0)              |               | 4.0.0       |               |
| -whiteness=N           | specifies whiteness. (0.0 <-> 1.0)        |               | 4.0.0       |               |
| -channel=N             | specifies source channel.                 | 3             | 4.0.0       |               |
| -dev=filepath          | specifies device file.                    | /dev/video0   | 4.0.0       |               |
| -mode=[PAL/NTSC/SECAM] | specifies TV signal mode.                 | NTSC          | 4.0.0       |               |
| -format=[BGR/BGRA]     | specifies pixel format.                   | BGR           | 4.0.0       |               |

###AR_VIDEO_DEVICE_DV

###AR_VIDEO_DEVICE_1394CAM

Extra help on building this video capture module can be found on the page [Building libARvideo][libarvideo].

| video config string                                                                                                                                                                                                                                                                                | usage notes                                                                                           | Default value                                  | Avail.: (1) | Unavail.: (2) |
|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------|------------------------------------------------|-------------|---------------|
| -device=Linux1394Cam                                                                                                                                                                                                                                                                               | Select this device for use.                                                                           |                                                | 4.0.0       |               |
| -port=N                                                                                                                                                                                                                                                                                            | specifies a FireWire adaptor port (-1: Any).                                                          | 0                                              | 4.0.0       |               |
| -euid=N                                                                                                                                                                                                                                                                                            | specifies EUID of a FireWire camera (-1: Any).                                                        | 0                                              | 4.0.0       |               |
| -mode=[320x240\_YUV422 / 640x480\_YUV422 / 640x480\_RGB / 640x480\_YUV411 / 640x480\_YUV411_HALF / 640x480\_MONO / 640x480\_MONO\_COLOR / 640x480\_MONO\_COLOR2 / 640x480\_MONO\_COLOR3 / 640x480\_MONO\_COLOR\_HALF / 640x480\_MONO\_COLOR\_HALF2 / 640x480\_MONO\_COLOR\_HALF3 / 1024x768\_MONO / 1024x768\_MONO\_COLOR] | specifies input image format.                                                                         | Depends on camera selected during execution of | 4.0.0       |               |
| -rate=N                                                                                                                                                                                                                                                                                            | specifies desired framerate of a FireWire camera. (1.875, 3.75, 7.5, 15, 30, 60)                      | 30                                             | 4.0.0       |               |
| -reset                                                                                                                                                                                                                                                                                             | resets camera to factory default settings. This is required for DFK21AF04 when it has been connected. |                                                | 4.0.0       |               |

###AR_VIDEO_DEVICE_SGI

###AR_VIDEO_DEVICE_WINDOWS_DIRECTSHOW

Extra help on building this video capture module can be found on the page [Building libARvideo][libarvideo].

| video config string | usage notes | Default value | Avail.: (1) | Unavail.: (2) |
|---------------------|---------------|-------------|---------------|-------------|
| -device=WinDS | Select this device for use. | 4.0.0644 | 4.0.065 |
| -showDialog | Request that the WDM capture PIN (configuration sheet) be shown to the user when the video stream is opened. | -showDialog (only if no config string is supplied). | 4.0.0644 | 4.0.065 |
| -showDeviceList | Do not actually open the device, but instead dump a list of device numbers and device names to the standard output. The format of the dump is up to 2 decimal digits (beginning with '1' for the first device), followed by a colon and a space, and the remaining characters before the new line constituting the device name, as known to WDM. | 4.0.0644 | 4.0.065 |
| -devNum=*n* | Open device *n*, rather than the default device. | 1 | 4.0.0644 | 4.0.065 |
| -flipH | Flip camera image horizontally. | 4.0.0644 | 4.0.065 |
| -flipV | Flip camera image vertically. | -flipV (only if no config string is supplied). | 4.0.0644 | 4.0.065 |


###AR_VIDEO_DEVICE_WINDOWS_DRAGONFLY

| video config string                                                                                                                                                                                                                                                                                         | usage notes                                                                                       | Default value | Avail.: (1) | Unavail.: (2) |
|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------|---------------|-------------|---------------|
| -device=WinDF                                                                                                                                                                                                                                                                                               | Select this device for use.                                                                       |               |             |               |
| -rate=N                                                                                                                                                                                                                                                                                                     | Specifies desired input framerate. (1.875, 3.75, 7.5, 15, 30, 60, 120)                            | 15            | 4.6.0       |               |
| -mode=[160x120YUV444 / 320x240YUV422 / 640x480YUV411 / 640x480YUV422 / 640x480RGB / 640x480Y8 / 640x480Y16 / 800x600YUV422 / 800x600RGB / 800x600Y8 / 800x600Y16 / 1024x768YUV422 / 1024x768RGB / 1024x768Y8 / 1024x768Y16 / 1280x960YUV422 / 1280x960RGB / 1280x960Y8 / 1280x960Y16 / 1600x1200YUV422 / 1600x1200RGB / 1600x1200Y8 / 1600x1200Y16] | Specifies input image format. N.B. Not all formats listed may be supported by ARToolKit.          | 1024x768RGB   | 4.6.0       |               |
| -index=N                                                                                                                                                                                                                                                                                                    | Specifies bus index of device to use. (Range is from 0 to number of connected devices minus one.) | 0             | 4.6.0       |               |

###AR_VIDEO_DEVICE_WINDOWS_HDCAM

| video config string | usage notes | Default value | Avail.: (1) | Unavail.: (2) |
|---------------------|-------------|---------------|-------------|---------------|
| -device=WinHD | Select this device for use. | | | |

###AR_VIDEO_DEVICE_QUICKTIME7
The QuickTime7 video plugin uses the QTKit API introduced with QuickTime version 7 on Mac OS X. It offers improved performance over the previous QuickTime modules, however as of ARToolKit Professional v4.5.0, it does not yet support reading from file or network stream, so the previous QUICKTIME module should still be used in that case.

| video config string | usage notes | Default value | Avail.: (1) | Unavail.: (2) |
|---------------------|-------------|---------------|-------------|---------------|
| -device=QuickTime7 | Select this device for use. | | 4.5.0 |
| -width=*w* | Scale camera native image to width w. | camera native image width | 4.5.0 | |
| -height=*h* | Scale camera native image to height h. | camera native image height | 4.5.0 | |
| -pixelformat=*cccc* | Return images with pixels in format cccc, where cccc is either a numeric pixel format number or a valid 4-character-code for a pixel format. The following numeric values are supported: 24 (24-bit RGB), 32 (32-bit ARGB), 40 (8-bit grey) The following 4-character-codes are supported: BGRA, RGBA, ABGR, 24BG, 2vuy, yuvs. (See http://developer.apple.com/library/mac/#technotes/tn2010/tn2273.html) | Depends on camera; for many USB video-class devices, either '2vuy' or 'yuvs'. | 4.5.0 | |
| -source=*N* | Acquire video from connected source device with index N. | 0 | 4.5.0 | |
| -nomuxed | Do not search for video from multiplexed video/audio devices (e.g. DV cams). | Off (i.e. muxed sources are included in the search) | 4.6.0 | |


###AR_VIDEO_DEVICE_QUICKTIME
Extra help on building this video capture module can be found on the page [Building libARvideo][libarvideo].

The QuickTime video plugin can operate in two modes:

-   In the first mode (the default), it acquires live video from a video capture source via QuickTime's video grabber. (Note that QuickTime for Windows does not come with a video digitizer component, and a third party component (e.g. [WinVDIG][winvidg] must be installed.)
-   In the second mode, specified by passing a video configure parameter "-movie=*pathnameOrURL*", the plugin can open any valid QuickTime resource, including movies from disk, or movies streamed via http, rtsp or ftp protocols.

####QuickTime Video Input from VDIG

| video config string | usage notes | Default value | Avail.: (1) | Unavail.: (2) |
|---------------------|-------------|---------------|-------------|---------------|
| -device=QUICKTIME | Select this device for use. | | 4.3.0 | |
| -[no]dialog | Don't display video settings dialog. | -dialog | 4.3.0 | |
| -[no]standarddialog | Don't remove unnecessary panels from video settings dialog. | -nostandarddialog | 4.3.0 | |
| -width=*w* | Scale camera native image to width w. | 640 | 4.3.0 | |
| -height=*h* | Scale camera native image to height h. | 480 | 4.3.0 | |
| -[no]fps | Overlay camera frame counter on image. | -nofps | 4.3.0 | |
| -grabber=*n* | With multiple QuickTime video grabber components installed, use component n (default n=1). N.B. It is NOT necessary to use this option if you have installed more than one video input device (e.g. two cameras) as the default QuickTime grabber can manage multiple video channels. | 1 | 4.3.0 | |
| -pixelformat=*cccc* | Return images with pixels in format cccc, where cccc is either a numeric pixel format number or a valid 4-character-code for a pixel format. The following numeric values are supported: 24 (24-bit RGB), 32 (32-bit ARGB), 40 (8-bit grey) The following 4-character-codes are supported: BGRA, RGBA, ABGR, 24BG, 2vuy, yuvs. (See http://developer.apple.com/library/mac/#technotes/tn2010/tn2273.html) | Depends on platform; default for Mac OS X is 32 (i.e. ARGB), default for Windows is BGRA. | 4.3.0 | |
| -[no]fliph | Flip camera image horizontally. | -nofliph | 4.3.0 | |
| -[no]flipv | Flip camera image vertically. | -noflipv | 4.3.0 | |
| -[no]singlebuffer | Use single buffering of captured video instead of triple-buffering. | -nosinglebuffer | 4.3.0 |


####QuickTime Video Input from Movie File or Stream

| video config string | usage notes | Default value | Avail.: (1) | Unavail.: (2) |
|---------------------|-------------|---------------|-------------|---------------|
| -device=QUICKTIME | Select this device for use. | 4.3.0 |  |
| -movie=*file:///path/to/file* or -movie="*file:///path/to/file*" | Specifies that video should be acquired from a QuickTime movie resource. This can be any valid movie resource that QuickTime can open, including files and streams. If a movie file is to be opened, supply a file URI specifying the full pathname. Pathnames must be URI-encoded, i.e. if the pathname contains spaces, these should be replaced with '+' characters. e.g. -movie="file:///C:/Program+Files/QuickTime/Sample.mov" or -movie=file:///Developer/Examples/WebKit/WebKitMoviePlugIn/sample.mov . If a movie stream is to be opened, it may be specified via an "http://", "rtsp://" or "ftp://" URL, or it can be referred to in a stream description file (a .sdp file). In ARToolKit versions 4.3.0 - 4.4.4, the maximum URL length was 255 characters. As of ARToolKit 4.5.0, this has been increased to 1023 characters. | 4.3.0 |  |
| -[no]1to1 | Do not fit the movie to the window or buffer size, but instead display it at its original size (1 to 1 scaling). | -no1to1 | 4.3.0 |  |
| -[no]fill | Rather than fitting the movie into the window so that all the movie is visible, scale it so that it completely fills the window or buffer. The movie's aspect ratio will be maintained, and this may result in some of the movie being clipped at the top and bottom or left and right. | -nofill | 4.3.0 |  |
| -[no]stretch | Rather than fitting the movie into the window so that all the movie is visible, scale it so that it completely fills the window or buffer. The movie's aspect ratio will be stretched if necessary so that no pixels are clipped. | -nostretch | 4.3.0 |  |
| -[no]loop | Request that the movie loop continuously. This parameter has no effect for streaming movies. Unless this parameter is specified, calls to arVideoQuickTimeMovieIdle() will return AR_E_EOF when the movie has finished playing. | -loop | 4.3.0 |  |
| -[no]showcontroller | Show the QuickTime movie controller in the frame. (Unfortunately, the user will not be able to interact with the controller to pause and jog the movie.) | -showcontroller | 4.3.0 |  |
| -[no]mute | Set movie audio volume to 0. | -nomute | 4.3.0 |  |
| -[no]pause | Open movie in paused state. A call to arVideoCapStart() would be required to unpause the movie. | -pause | 4.3.0 |  |
| -width=*w* | Scale movie native frame to width w. | Width of movie frame. | 4.3.0 |  |
| -height=*h* | Scale movie native frame to height h. | Height of movie frame. | 4.3.0 |  |
| -[no]fliph | Flip movie frame horizontally. | -nofliph | 4.3.0 |  |
| -[no]flipv | Flip movie frame vertically. | -noflipv | 4.3.0 |  |
| -pixelformat=*cccc* | Ignored unless -offscreen is also passed, requests return of movie frames with pixels in format cccc, where cccc is either a numeric pixel format number or a valid 4-character-code for a pixel format. The following values are supported: 32, BGRA, RGBA, ABGR, 24, 24BG, 2vuy, yuvs. (See http://developer.apple.com/quicktime/icefloe/dispatch020.html) | Depends on platform; default for Mac OS X is 32 (i.e. ARGB), default for Windows is BGRA. | 4.3.0 |  |
| -[no]singlebuffer | Ignored unless -offscreen is also passed, use single buffering of captured movie instead of triple-buffering. | -nosinglebuffer | 4.3.0 |  |

###AR_VIDEO_DEVICE_QUICKTIME_OLD

| video config string   | usage notes                               | Default value | Avail.: (1) | Unavail.: (2) |
|-----------------------|-------------------------------------------|---------------|-------------|---------------|
| -device=QUICKTIME_OLD | Select this device for use.               |               | 4.0.0       |               |
| -width=N              | Specify the width of the returned image.  | 640           | 4.0.0       |               |
| -height=N             | Specify the height of the returned image. | 480           | 4.0.0       |               |

###AR_VIDEO_DEVICE_WINDOWS_DSVIDEOLIB

| video config string          | usage notes                                                                                                                                                                                                                                | Default value                                                                                                                                                                                   | Avail.: (1) | Unavail.: (2) |
|------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------|---------------|
| -device=WinDSVL              | Select this device for use.                                                                                                                                                                                                                |                                                                                                                                                                                                 | 4.1.0       |               |
| *remainder of config string* | Specify either an XML string (i.e. beginning '<?xml') or a pathname to an XML file (e.g. 'config.XML'), conforming to the DSVideoLib XML Schema ([DsVideoLib.xsd](http://www.artoolworks.com/support/attachments/DsVideoLib.xsd)). [View an interactive SVG view of the DSVideoLib XML Schema](http://www.artoolworks.com/support/attachments/DsVideoLib.svg). | `<?xml version="1.0" encoding="UTF-8"?><dsvl_input><camera show_format_dialog="true" friendly_name=""><pixel_format><RGB32 flip_h="false" flip_v="true"/></pixel_format></camera></dsvl_input>` | 4.1.0       |               |

###AR_VIDEO_DEVICE_GSTREAMER

| video config string          | usage notes                                                                                                     | Default value | Avail.: (1) | Unavail.: (2) |
|------------------------------|-----------------------------------------------------------------------------------------------------------------|---------------|-------------|---------------|
| -device=GStreamer            | Select this device for use.                                                                                     |               | 4.3.2       |               |
| *remainder of config string* | Specifies a configuration string following the gst-launch syntax. See more at [GStreamer Configuration](config_video_capture_gstreamer). |               | 4.3.2       |               |

###AR_VIDEO_DEVICE_IPHONE
The iOS video plugin is available on Apple iOS devices including iPhone 3G, iPhone 3GS, iPhone 4, iPod touch 4G and iPad 2.
As of ARToolKit for iOS version 4.5.5 (release 4) the iOS video plugin can operate in either two modes; either acquiring live video from a camera on the iOS device, or playing a pre-recorded video file stored in the app's bundle resource directory.

####iOS Video Input from Camera

| video config string | usage notes                                                                                                                                                                                                                                                                                                                 | Default value                                                      | Avail.: (1)         | Unavail.: (2) |
|---------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------|---------------------|---------------|
| -device=iPhone      | Select this device for use.                                                                                                                                                                                                                                                                                                 |                                                                    | 4.4.3 (release 1.0) |               |
| -format=*X*           | Return images with pixels in format X, where X is one of the following format tokens: 420v, 420f, BGRA, RGBA, RGBA_5551, RGBA_4444                                                                                                                                                                                          | 420f (ARToolKit v5.0 and later.), BGRA (ARToolKit version pre-5.0) | 4.4.3 (release 1.0) |               |
| -preset=*X*           | Specify use of camera settings preset X, where X is one of: cif, 480p, 720p, 1080p, low, medium, high, photo. (N.B.:480p=640x480, i.e. 4:3 aspect ratio, 720p=1280x720 and 1080p=1920x1080 i.e. 16:9 aspect ratio).                                                                                                         | medium                                                             | 4.5.1 (release 2.0) |               |
| -position=*X*         | Choose between rear/back and front-mounted camera (where available). Allowable values for X include: rear, back, front. (N.B.:rear is a synonym for back). Front is not supported on iPhone 3G or iPhone 3GS.                                                                                                               | rear                                                               | 4.5.1 (release 2.0) |               |
| -[no]flipv          | Flip the incoming image from the camera vertically. On front mounted-cameras, this option is on by default (but can be overridden by specifying -noflipv). Flipping the video vertically matches the orientation of the video image (when displayed on the screen of the device) to the physical orientation of the device. | noflipv (on rear camera). flipv (on front camera)                  | 4.5.4 (release 3.0) |               |
| -[no]fliph          | Flip the incoming image from the camera horizontally.                                                                                                                                                                                                                                                                       | nofliph                                                            | 4.6.6 (release 16)  |               |
| -width=*w*            | Crop native camera image width to w.                                                                                                                                                                                                                                                                                        | camera native image width for given preset (see above.)            | 4.4.3 (release 1.0) | 4.5.0-        |
| -height=*h*           | Crop native camera image height to h.                                                                                                                                                                                                                                                                                       | camera native image height for given preset (see above.)           | 4.4.3 (release 1.0) | 4.5.0-        |
| -bufferpow2         | Requests that images are returned in a buffer which has power-of-two dimensions.                                                                                                                                                                                                                                            | camera native image size for given preset (see below.)             | 4.4.3 (release 1.0) | 4.5.0-        |

####iOS Video Input from Movie File

| video config string                      | usage notes                                                                                                                                                                                                                                                                                                                                                                      | Default value          | Avail.: (1)         | Unavail.: (2) |
|------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------|---------------------|---------------|
| -device=iPhone                           | Select this device for use.                                                                                                                                                                                                                                                                                                                                                      |                        | 4.5.5 (release 4.0) |               |
| -movie=*pathname* or -movie="*pathname*" | Specifies that video should be acquired from a movie resource. This can be any valid movie file resource that iOS can open, but typically MPEG-4 (h.264 video with optional AAC audio). The pathname is relative to the resources directory of the app bundle. If the pathname contains spaces, it must be surrounded with double quotes ("). e.g. -movie="My great sample.mov". |                        | 4.5.5 (release 4.0) |               |
| -[no]1to1                                | **N.B. CURRENTLY IGNORED.** Do not fit the movie to the window or buffer size, but instead display it at its original size (1 to 1 scaling).                                                                                                                                                                                                                                     | -no1to1                | 4.5.5 (release 4.0) |               |
| -[no]fill                                | **N.B. CURRENTLY IGNORED.** Rather than fitting the movie into the window so that all the movie is visible, scale it so that it completely fills the window or buffer. The movie's aspect ratio will be maintained, and this may result in some of the movie being clipped at the top and bottom or left and right.                                                              | -nofill                | 4.5.5 (release 4.0) |               |
| -[no]stretch                             | **N.B. CURRENTLY IGNORED.** Rather than fitting the movie into the window so that all the movie is visible, scale it so that it completely fills the window or buffer. The movie's aspect ratio will be stretched if necessary so that no pixels are clipped.                                                                                                                    | -stretch               | 4.5.5 (release 4.0) |               |
| -[no]loop                                | Request that the movie loop continuously.                                                                                                                                                                                                                                                                                                                                        | -loop                  | 4.5.5 (release 4.0) |               |
| -[no]mute                                | Set movie audio volume to 0.                                                                                                                                                                                                                                                                                                                                                     | -nomute                | 4.5.5 (release 4.0) |               |
| -[no]pause                               | Open movie in paused state. A call to arVideoCapStart() would be required to unpause the movie.                                                                                                                                                                                                                                                                                  | -pause                 | 4.5.5 (release 4.0) |               |
| -width=*w*                               | Scale movie native frame to width w.                                                                                                                                                                                                                                                                                                                                             | Width of movie frame.  | 4.5.5 (release 4.0) |               |
| -height=*h*                              | Scale movie native frame to height h.                                                                                                                                                                                                                                                                                                                                            | Height of movie frame. | 4.5.5 (release 4.0) |               |
| -[no]fliph                               | **N.B. CURRENTLY IGNORED.** Flip movie frame horizontally.                                                                                                                                                                                                                                                                                                                       | -nofliph               | 4.5.5 (release 4.0) |               |
| -[no]flipv                               | Flip movie frame vertically.                                                                                                                                                                                                                                                                                                                                                     | -noflipv               | 4.5.5 (release 4.0) |               |
| -pixelformat=*cccc*                      | Ignored unless -offscreen is also passed, requests return of movie frames with pixels in format cccc, where cccc is either a numeric pixel format number or a valid 4-character-code for a pixel format. The following values are supported: 32, BGRA, RGBA, ABGR, 24, 24BG, 2vuy, yuvs. (See http://developer.apple.com/quicktime/icefloe/dispatch020.html)                     | BGRA                   | 4.5.5 (release 4.0) |               |

###AR_VIDEO_DEVICE_WINDOWS_MEDIA_FOUNDATION

| video config string | usage notes | Default value | Avail.: (1) | Unavail.: (2) |
|---------------------|-------------|---------------|-------------|---------------|
| -device=WinMF | Select this device for use. |  | 5.1.5 |  |
| -showDeviceList | Do not actually open the device, but instead dump a list of device numbers and device names to the standard output. The format of the dump is up to 2 decimal digits (beginning with '1' for the first device), followed by a colon and a space, and the remaining characters before the new line constituting the device name, as known to WDM. | -noShowDeviceList | 5.1.5 |  |
| -noShowDeviceList | Override a previous -showDeviceList option | -noShowDeviceList | 5.1.5 |  |
| -devNum=*n* | Open device n, rather than the default device. E.g. if two cameras are connected, use -devNum=2 to access the second camera. | 1 | 5.1.5 |  |
| -format=*X* | Return images with pixels in format X, where X is one of: BGRA, BGR, NV12/420f, 2vuy/UYVY, yuvs/YUY2, RGB\_565, RGBA\_5551. The most reliable format is BGRA, due to support within Media Foundation for conversion from YUV-colour spaces to RGB colour space. Other formats must be supported natively on the device in order for the request to succeed. | Default pixel format. | 5.1.5 |  |
| -width=*w* | Request video format of width w pixels | Default frame width | 5.1.5 |  |
| -height=*h* | Request video format of height h pixels | Default frame height | 5.1.5 |  |
| -flipV | Flip image vertically. | -noFlipV | 5.1.5 |  |
| -noFlipV | Override a previous -flipV option and do not flip image vertically. | -noFlipV | 5.1.5 |  |
| -showFormats | Dump the full list of native formats to the console. This is helpful in determining device capabilities. | -noShowFormats | 5.1.5 |  |
| -noShowFormats | Override a previous -showFormats option | -noShowFormats | 5.1.5 |  |


###AR_VIDEO_DEVICE_WINDOWS_MEDIA_CAPTURE

| video config string | usage notes                                                                                                                                                                                                                                                                                                                                                    | Default value         | Avail.: (1) | Unavail.: (2) |
|---------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------|-------------|---------------|
| -device=WinMC       | Select this device for use.                                                                                                                                                                                                                                                                                                                                    |                       | 5.1.7       |               |
| -position=*X*       | Choose between rear/back and front-mounted (where available). Other options include cameras mounted on left, right, top or bottom edges of the device. Allowable values for X include: rear, back, front, left, right, top, bottom, default. (N.B.:rear is a synonym for back).                                                                                | default               | 5.1.7       |               |
| -devNum=*n*         | Open device *n*, rather than the default device. E.g. if two cameras are connected, use -devNum=2 to access the second camera. If this option is combined with the -position option, then it will choose the n'th device at the preferred position. E.g. to choose the second of two rear cameras, you could use -position=rear -devNum=2.                     | 1                     | 5.1.7       |               |
| -format=*X*         | Return images with pixels in format X, where X is one of: BGRA, BGR, NV12/420f, 2vuy/UYVY, yuvs/YUY2, RGB_565, RGBA_5551. The most reliable format is BGRA, due to support within Windows Media Capture for conversion from YUV-colour spaces to RGB colour space. Other formats must be supported natively on the device in order for the request to succeed. | Default pixel format. | 5.1.7       |               |
| -width=*w*          | Request video format of width w pixels                                                                                                                                                                                                                                                                                                                         | Default frame height  | 5.1.7       |               |
| -height=*h*         | Request video format of height h pixels                                                                                                                                                                                                                                                                                                                        | Default frame height  | 5.1.7       |               |
| -flipV              | Flip image vertically.                                                                                                                                                                                                                                                                                                                                         | -noFlipV              | 5.1.7       |               |
| -noFlipV            | Override a previous -flipV option and do not flip image vertically.                                                                                                                                                                                                                                                                                            | -noFlipV              | 5.1.7       |               |

[winvidg]: http://www.eden.net.nz/7/20071008/
[libarvideo]: 8_Advanced_Topics:windows_building_libarvideo
[general_environment_variables]: 1_Getting_Started:general_environment_variables
[config_camera_calibration]: 2_Configuration:config_camera_calibration
[config_camera_stereo_tracking]: 8_Advanced_Topics:config_camera_stereo_tracking
