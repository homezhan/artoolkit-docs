#Configuring Video Capture in ARToolKit
ARToolKit includes libARvideo, a cross-platform library which captures video from a variety of different sources. In general, most users of ARToolKit who have a single webcam attached to their system will never delve into the workings of this library. However, the module or modules inside this library generally allow for a degree of configuration to control parameters of the capture sources with which they interface.

##Changing Video Configuration
This section of the manual details some of the configuration options available with libARvideo.

### Setting Configuration at Run Time
Video configurations are passed to libARvideo in a standard way; as a c-string containing text. What to put in the *contents* of the string depends on your capture source.

The contents of the string are different for different capture sources because although libARvideo presents a standard API for passing video to other code (e.g. libAR, libARgsub_lite and libARgsub), there is custom code inside libARvideo for each capture source (e.g. QuickTime, DirectShow, libdc1394). The capture sources generally implement a variety of different approaches to video stream acquisition. So, the configuration parameters are different depending on the underlying capture module being used.

The simplest way to specify the video configuration (without recompiling the example applications) is to create an [environment variable][general_environment_variables] `ARTOOLKIT5_CONFIG` with the video configuration you wish to use.

####ARToolKit Utilities
Some of the ARToolKit utilities (including [calib_camera][config_camera_calibration], [calib_stereo][config_camera_stereo_tracking] and check_id) accept video configuration(s) as command-line parameters. The desired configuration is passed after a parameter "--vconf" (or --vconfL or --vconfR for calib_stereo). Note that if the video configuration string includes spaces, it must be quoted to prevent the shell passing it as multiple parameters.

### Setting Configuration Programmatically
Video configuration can also be passed to libARvideo programmatically (as the sole parameter to the arVideoOpen() call). When no string (NULL) or an empty string ("") is passed, libARvideo looks for an environment variable "ARTOOLKIT5_CONFIG" (as mentioned above) for the string. If this environment variable is not found, the video module will use a default configuration.

In most of the ARToolKit examples, the video configuration is specified in a string named "vconf". Do a search in your source editor for "vconf" to see this. So in most of the examples, editing the vconf string in the source code will change the video configuration being used.

Of course, editing source code requires recompiling for the changes to take effect, so a few of the examples accept a command-line parameter and use this as vconf. You can look at the source code to see if a given example does so.

#### ARToolKit for Unity
ARToolKit for Unity allows you to specify video configuration separately for each supported platform directly in the Unity Editor.

##Capture Sources and Switching Them
Where more than one capture source has been compiled into libARvideo on a given platform, you are allowed to switch between the options.

This table lists the capture sources available on each platform. _Note: If you have a binary release of ARToolKit, not all of these capture sources may have been compiled into your copy!_:
<html>
    <body>
        <table border="2" cellspacing="4" cellpadding="3" rules="all" style="margin:1em 1em 1em 0; border:solid 1px #AAAAAA; border-collapse:collapse;empty-cells:show;">
            <tr>
                <th>
                    Platform
                </th>
                <th>
                    Capture source (descriptive name)
                </th>
                <th>
                    Constant required in &lt;AR/config.h&gt; for this source to be compiled into libARvideo
                </th>
                <th>
                    video config string to select this capture source
                </th>
                <th>
                    Avail.: (1)
                </th>
                <th>
                    Unavail.: (2)
                </th>
            </tr>
            <tr>
                <td>
                    All
                </td>
                <td>
                    Dummy input
                </td>
                <td>
                    AR_INPUT_DUMMY
                </td>
                <td>
                    -device=Dummy
                </td>
                <td>
                    4.0.0
                </td>
                <td></td>
            </tr>
            <tr>
                <td>
                    Mac OS X, Windows, Linux
                </td>
                <td>
                    JPEG image input
                </td>
                <td>
                    AR_INPUT_IMAGE
                </td>
                <td>
                    -device=Image
                </td>
                <td>
                    4.6.2
                </td>
                <td></td>
            </tr>
            <tr>
                <td>
                    Linux
                </td>
                <td>
                    <a href="http://www.video4linux.net/" class="external text" rel="nofollow">Video4Linux</a>
                </td>
                <td>
                    AR_INPUT_V4L
                </td>
                <td>
                    -device=LinuxV4L
                </td>
                <td>
                    4.0.0
                </td>
                <td></td>
            </tr>
            <tr>
                <td>
                    Linux
                </td>
                <td>
                    <a href="http://gstreamer.freedesktop.org/" class="external text" rel="nofollow">GStreamer</a>
                </td>
                <td>
                    AR_INPUT_GSTREAMER
                </td>
                <td>
                    -device=GStreamer
                </td>
                <td>
                    4.3.2
                </td>
                <td></td>
            </tr>
            <tr>
                <td>
                    Linux
                </td>
                <td>
                    <a href="http://sourceforge.net/projects/libdc1394/" class="external text" rel="nofollow">libdc1394</a>
                </td>
                <td>
                    AR_INPUT_1394CAM
                </td>
                <td>
                    -device=Linux1394Cam
                </td>
                <td>
                    4.0.0
                </td>
                <td></td>
            </tr>
            <tr>
                <td>
                    Mac OS X, Windows
                </td>
                <td>
                    <a href="http://www.apple.com/quicktime/" class="external text" rel="nofollow">QuickTime®</a> (enhanced)
                </td>
                <td>
                    AR_INPUT_QUICKTIME
                </td>
                <td>
                    -device=QUICKTIME
                </td>
                <td>
                    4.3.0
                </td>
                <td></td>
            </tr>
            <tr>
                <td>
                    Windows
                </td>
                <td>
                    <a href="http://msdn2.microsoft.com/en-us/library/ms783323.aspx" class="external text" rel="nofollow">DirectShow®</a>
                </td>
                <td>
                    AR_INPUT_WINDOWS_DIRECTSHOW
                </td>
                <td>
                    -device=WinDS
                </td>
                <td>
                    4.0.0644
                </td>
                <td>
                    4.0.065,4.1.x
                </td>
            </tr>
            <tr>
                <td>
                    Windows
                </td>
                <td>
                    <a href="http://sourceforge.net/projects/dsvideolib" class="external text" rel="nofollow">DSVideoLib</a>
                </td>
                <td>
                    AR_INPUT_WINDOWS_DSVIDEOLIB
                </td>
                <td>
                    -device=WinDSVL
                </td>
                <td>
                    4.1.0
                </td>
                <td></td>
            </tr>
            <tr>
                <td>
                    Windows
                </td>
                <td>
                    <a href="http://www.ptgrey.com/products/pgrflycapture/" class="external text" rel="nofollow">DragonFly FlyCapture®</a>
                </td>
                <td>
                    AR_INPUT_WINDOWS_DRAGONFLY
                </td>
                <td>
                    -device=WinDF
                </td>
                <td>
                    4.0.0644
                </td>
                <td>
                    4.0.065
                </td>
            </tr>
            <tr>
                <td>
                    Mac OS X
                </td>
                <td>
                    <a href="http://www.apple.com/quicktime/" class="external text" rel="nofollow">QuickTime®</a>
                </td>
                <td>
                    AR_INPUT_QUICKTIME_OLD
                </td>
                <td>
                    -device=QUICKTIME_OLD
                </td>
                <td>
                    4.0.0
                </td>
                <td></td>
            </tr>
            <tr>
                <td>
                    Windows
                </td>
                <td>
                    HDCam64
                </td>
                <td>
                    AR_INPUT_WINDOWS_HDCAM
                </td>
                <td>
                    -device=WinHD
                </td>
                <td>
                    4.0.0644
                </td>
                <td>
                    4.0.065
                </td>
            </tr>
            <tr>
                <td>
                    Linux
                </td>
                <td>
                    <a href="http://libdv.sourceforge.net/" class="external text" rel="nofollow">libdv</a>
                </td>
                <td>
                    AR_INPUT_DV
                </td>
                <td>
                    -device=LinuxDV
                </td>
                <td>
                    4.0.0
                </td>
                <td>
                    4.1.x, 4.3.x
                </td>
            </tr>
            <tr>
                <td>
                    SGI Irix
                </td>
                <td>
                    SGI video input
                </td>
                <td>
                    AR_INPUT_SGI
                </td>
                <td>
                    -device=SGI
                </td>
                <td>
                    4.0.0
                </td>
                <td>
                    4.1.x, 4.3.x
                </td>
            </tr>
            <tr>
                <td>
                    Mac OS X
                </td>
                <td>
                    <a href="http://www.apple.com/quicktime/" class="external text" rel="nofollow">QuickTime®</a> (v7.0 and later)
                </td>
                <td>
                    AR_INPUT_QUICKTIME7
                </td>
                <td>
                    -device=QuickTime7
                </td>
                <td>
                    4.5.0
                </td>
                <td></td>
            </tr>
            <tr>
                <td>
                    iOS
                </td>
                <td>
                    iOS video input
                </td>
                <td>
                    AR_INPUT_IPHONE
                </td>
                <td>
                    -device=iPhone
                </td>
                <td>
                    4.4.3 (iOS release 1.0)
                </td>
                <td></td>
            </tr>
            <tr>
                <td>
                    Windows
                </td>
                <td>
                    Media Foundation
                </td>
                <td>
                    AR_INPUT_WINDOWS_MEDIA_FOUNDATION
                </td>
                <td>
                    -device=WinMF
                </td>
                <td>
                    5.1.5
                </td>
                <td></td>
            </tr>
            <tr>
                <td>
                    Windows Store (Windows 8.1 and Windows Phone 8.1)
                </td>
                <td>
                    Windows Media Capture
                </td>
                <td>
                    AR_INPUT_WINDOWS_MEDIA_CAPTURE
                </td>
                <td>
                    -device=WinMC
                </td>
                <td>
                    5.1.7
                </td>
                <td></td>
            </tr>
        </table>
    </body>
</html>
(1): First version of ARToolKit Professional in which this capture source became available.
(2):Version(s) of ARToolKit Professional in which this source is/was unavailable or unusable.

####Video configuration options

Notes on the tables below:

-   Items inside square brackets ("[" and "]") are optional modifications to parameters, e.g. an option listed below as "-[no]foo" means that option "-foo" activates some option "foo", and option "-nofoo" deactivates it.
-   Items separated by a vertical bar ("|") are mutually-exclusive options. Use only one.
-   Items in italic typeface are placeholders, which you should replace. E.g. N indicates an integer number should be inserted.

###AR_VIDEO_DEVICE_DUMMY
<html>
    <body>
        <table border="2" cellspacing="4" cellpadding="3" rules="all" style="margin:1em 1em 1em 0; border:solid 1px #AAAAAA; border-collapse:collapse;empty-cells:show;">
            <tr>
                <th>
                    video config string
                </th>
                <th>
                    usage notes
                </th>
                <th>
                    Default value
                </th>
                <th>
                    Avail.: (1)
                </th>
                <th>
                    Unavail.: (2)
                </th>
            </tr>
            <tr>
                <td>
                    -device=Dummy
                </td>
                <td>
                    Select this device for use.
                </td>
                <td></td>
                <td>
                    4.0.0
                </td>
                <td></td>
            </tr>
            <tr>
                <td>
                    -width=<i>N</i>
                </td>
                <td>
                    Specify the width of the returned image.
                </td>
                <td>
                    640
                </td>
                <td>
                    4.0.0
                </td>
                <td></td>
            </tr>
            <tr>
                <td>
                    -height=<i>N</i>
                </td>
                <td>
                    Specify the height of the returned image.
                </td>
                <td>
                    480
                </td>
                <td>
                    4.0.0
                </td>
                <td></td>
            </tr>
            <tr>
                <td>
                    -bufferpow2
                </td>
                <td>
                    Requests that images are returned in a buffer which has power-of-two dimensions.
                </td>
                <td>
                    Buffers are same size as image.
                </td>
                <td>
                    4.4.3
                </td>
                <td></td>
            </tr>
            <tr>
                <td>
                    -format=X
                </td>
                <td>
                    Return images with pixels in format X, where X is one of the following format tokens:
                    <p>
                        BGRA, RGBA, RGBA_5551, RGBA_4444, y420
                    </p>
                </td>
                <td>
                    BGRA
                </td>
                <td>
                    4.4.3
                </td>
                <td></td>
            </tr>
        </table>
    </body>
</html>
###AR_VIDEO_DEVICE_IMAGE
<html>
    <body>
        <table border="2" cellspacing="4" cellpadding="3" rules="all" style="margin:1em 1em 1em 0; border:solid 1px #AAAAAA; border-collapse:collapse;empty-cells:show;">
            <tr>
                <th>
                    video config string
                </th>
                <th>
                    usage notes
                </th>
                <th>
                    Default value
                </th>
                <th>
                    Avail.: (1)
                </th>
                <th>
                    Unavail.: (2)
                </th>
            </tr>
            <tr>
                <td>
                    -device=Image
                </td>
                <td>
                    Select this device for use.
                </td>
                <td></td>
                <td>
                    4.6.2
                </td>
                <td></td>
            </tr>
            <tr>
                <td>
                    -width=<i>N</i>
                </td>
                <td>
                    Specify the width of the returned image.
                </td>
                <td>
                    Width of first JPEG in image list.
                </td>
                <td>
                    4.6.2
                </td>
                <td></td>
            </tr>
            <tr>
                <td>
                    -height=<i>N</i>
                </td>
                <td>
                    Specify the height of the returned image.
                </td>
                <td>
                    Height of first JPEG in image list.
                </td>
                <td>
                    4.6.2
                </td>
                <td></td>
            </tr>
            <tr>
                <td>
                    -bufferpow2
                </td>
                <td>
                    Requests that images are returned in a buffer which has power-of-two dimensions.
                </td>
                <td>
                    Buffer of same size as first JPEG in image list.
                </td>
                <td>
                    4.6.2
                </td>
                <td></td>
            </tr>
            <tr>
                <td>
                    -format=X
                </td>
                <td>
                    Return images with pixels in format X, where X is one of the following format tokens:
                    <p>
                        RGB, RGBA, MONO. Note that where the format requires a conversion from the native JPEG format (usually RGB) to anything other than MONO, there is a performance penalty imposed by the conversion. ARToolKit can natively handle RGB, RGBA and MONO JPEG formats, however in some circumstances, displaying RGB format images may have a performance penalty compared to RGBA format images because of data alignment issues. Benchmarking is recommended if performance is of concern.
                    </p>
                </td>
                <td>
                    RGB for RGB-format JPEGs, RGBA for RGBA-format JPEGs, or MONO for monochrome JPEGs.
                </td>
                <td>
                    4.6.2
                </td>
                <td></td>
            </tr>
            <tr>
                <td>
                    -[no]loop
                </td>
                <td>
                    In loop mode, after reading last image, the next read will return the first image. In noloop mode, no after reading the last image, no further images will be returned. May be used multiple times; later invocations will override earlier.
                </td>
                <td>
                    -noloop
                </td>
                <td>
                    4.6.2
                </td>
                <td></td>
            </tr>
            <tr>
                <td>
                    -image=pathname<br />
                    -image="pathname with spaces"
                </td>
                <td>
                    Specifies image to be read from file. Pathname is relative to the current working directory, or an absolute pathname in the system-native format. May be used an arbitrary number of times in a single config. string.
                </td>
                <td></td>
                <td>
                    4.6.2
                </td>
                <td></td>
            </tr>
        </table>
    </body>
</html>
###AR_VIDEO_DEVICE_V4L
<html>
    <body>
        <table border="2" cellspacing="4" cellpadding="3" rules="all" style="margin:1em 1em 1em 0; border:solid 1px #AAAAAA; border-collapse:collapse;empty-cells:show;">
            <tr>
                <th>
                    video config string
                </th>
                <th>
                    usage notes
                </th>
                <th>
                    Default value
                </th>
                <th>
                    Avail.: (1)
                </th>
                <th>
                    Unavail.: (2)
                </th>
            </tr>
            <tr>
                <td>
                    -device=LinuxV4L
                </td>
                <td>
                    Select this device for use.
                </td>
                <td></td>
                <td>
                    4.0.0
                </td>
                <td></td>
            </tr>
            <tr>
                <td>
                    -width=<i>N</i>
                </td>
                <td>
                    Specify the width of the returned image.
                </td>
                <td>
                    640
                </td>
                <td>
                    4.0.0
                </td>
                <td></td>
            </tr>
            <tr>
                <td>
                    -height=<i>N</i>
                </td>
                <td>
                    Specify the height of the returned image.
                </td>
                <td>
                    480
                </td>
                <td>
                    4.0.0
                </td>
                <td></td>
            </tr>
            <tr>
                <td>
                    -contrast=<i>N</i>
                </td>
                <td>
                    specifies contrast. (0.0 &lt;-&gt; 1.0)
                </td>
                <td></td>
                <td>
                    4.0.0
                </td>
                <td></td>
            </tr>
            <tr>
                <td>
                    -brightness=<i>N</i>
                </td>
                <td>
                    specifies brightness. (0.0 &lt;-&gt; 1.0)
                </td>
                <td></td>
                <td>
                    4.0.0
                </td>
                <td></td>
            </tr>
            <tr>
                <td>
                    -color=<i>N</i>
                </td>
                <td>
                    specifies color. (0.0 &lt;-&gt; 1.0)
                </td>
                <td></td>
                <td>
                    4.0.0
                </td>
                <td></td>
            </tr>
            <tr>
                <td>
                    -hue=<i>N</i>
                </td>
                <td>
                    specifies hue. (0.0 &lt;-&gt; 1.0)
                </td>
                <td></td>
                <td>
                    4.0.0
                </td>
                <td></td>
            </tr>
            <tr>
                <td>
                    -whiteness=<i>N</i>
                </td>
                <td>
                    specifies whiteness. (0.0 &lt;-&gt; 1.0)
                </td>
                <td></td>
                <td>
                    4.0.0
                </td>
                <td></td>
            </tr>
            <tr>
                <td>
                    -channel=<i>N</i>
                </td>
                <td>
                    specifies source channel.
                </td>
                <td>
                    3
                </td>
                <td>
                    4.0.0
                </td>
                <td></td>
            </tr>
            <tr>
                <td>
                    -dev=<i>filepath</i>
                </td>
                <td>
                    specifies device file.
                </td>
                <td>
                    /dev/video0
                </td>
                <td>
                    4.0.0
                </td>
                <td></td>
            </tr>
            <tr>
                <td>
                    -mode=<i>[PAL|NTSC|SECAM]</i>
                </td>
                <td>
                    specifies TV signal mode.
                </td>
                <td>
                    NTSC
                </td>
                <td>
                    4.0.0
                </td>
                <td></td>
            </tr>
            <tr>
                <td>
                    -format=<i>[BGR|BGRA]</i>
                </td>
                <td>
                    specifies pixel format.
                </td>
                <td>
                    BGR
                </td>
                <td>
                    4.0.0
                </td>
                <td></td>
            </tr>
        </table>
    </body>
</html>
###AR_VIDEO_DEVICE_DV
###AR_VIDEO_DEVICE_1394CAM
Extra help on building this video capture module can be found on the page [Building libARvideo][libarvideo].
<html>
    <body>
        <table border="2" cellspacing="4" cellpadding="3" rules="all" style="margin:1em 1em 1em 0; border:solid 1px #AAAAAA; border-collapse:collapse;empty-cells:show;">
            <tr>
                <th>
                    video config string
                </th>
                <th>
                    usage notes
                </th>
                <th>
                    Default value
                </th>
                <th>
                    Avail.: (1)
                </th>
                <th>
                    Unavail.: (2)
                </th>
            </tr>
            <tr>
                <td>
                    -device=Linux1394Cam
                </td>
                <td>
                    Select this device for use.
                </td>
                <td></td>
                <td>
                    4.0.0
                </td>
                <td></td>
            </tr>
            <tr>
                <td>
                    -port=<i>N</i>
                </td>
                <td>
                    specifies a FireWire adaptor port (-1: Any).
                </td>
                <td>
                    0
                </td>
                <td>
                    4.0.0
                </td>
                <td></td>
            </tr>
            <tr>
                <td>
                    -euid=<i>N</i>
                </td>
                <td>
                    specifies EUID of a FireWire camera (-1: Any).
                </td>
                <td>
                    0
                </td>
                <td>
                    4.0.0
                </td>
                <td></td>
            </tr>
            <tr>
                <td>
                    -mode=<i>[320x240_YUV422 | 640x480_YUV422 | 640x480_RGB | 640x480_YUV411 | 640x480_YUV411_HALF | 640x480_MONO | 640x480_MONO_COLOR | 640x480_MONO_COLOR2 | 640x480_MONO_COLOR3 | 640x480_MONO_COLOR_HALF | 640x480_MONO_COLOR_HALF2 | 640x480_MONO_COLOR_HALF3 | 1024x768_MONO | 1024x768_MONO_COLOR]</i>
                </td>
                <td>
                    specifies input image format.
                </td>
                <td>
                    Depends on camera selected during execution of
                </td>
                <td>
                    4.0.0
                </td>
                <td></td>
            </tr>
            <tr>
                <td>
                    -rate=<i>N</i>
                </td>
                <td>
                    specifies desired framerate of a FireWire camera. (1.875, 3.75, 7.5, 15, 30, 60)
                </td>
                <td>
                    30
                </td>
                <td>
                    4.0.0
                </td>
                <td></td>
            </tr>
            <tr>
                <td>
                    -reset
                </td>
                <td>
                    resets camera to factory default settings. This is required for DFK21AF04 when it has been connected.
                </td>
                <td></td>
                <td>
                    4.0.0
                </td>
                <td></td>
            </tr>
        </table>
    </body>
</html>
###AR_VIDEO_DEVICE_SGI
###AR_VIDEO_DEVICE_WINDOWS_DIRECTSHOW
Extra help on building this video capture module can be found on the page [Building libARvideo][libarvideo].
<html>
    <body>
        <h3>
            <span class="mw-headline" id="AR_VIDEO_DEVICE_SGI">AR_VIDEO_DEVICE_SGI</span>
        </h3>
        <h3>
            <span class="mw-headline" id="AR_VIDEO_DEVICE_WINDOWS_DIRECTSHOW">AR_VIDEO_DEVICE_WINDOWS_DIRECTSHOW</span>
        </h3>
        <p>
            Extra help on building this video capture module can be found on the page <a href="/support/library/Building_libARvideo_using_DirectShow" title="Building libARvideo using DirectShow">Building libARvideo using DirectShow</a>.
        </p>
        <table border="2" cellspacing="4" cellpadding="3" rules="all" style="margin:1em 1em 1em 0; border:solid 1px #AAAAAA; border-collapse:collapse;empty-cells:show;">
            <tr>
                <th>
                    video config string
                </th>
                <th>
                    usage notes
                </th>
                <th>
                    Default value
                </th>
                <th>
                    Avail.: (1)
                </th>
                <th>
                    Unavail.: (2)
                </th>
            </tr>
            <tr>
                <td>
                    -device=WinDS
                </td>
                <td>
                    Select this device for use.
                </td>
                <td></td>
                <td>
                    4.0.0644
                </td>
                <td>
                    4.0.065
                </td>
            </tr>
            <tr>
                <td>
                    -showDialog
                </td>
                <td>
                    Request that the WDM capture PIN (configuration sheet) be shown to the user when the video stream is opened.
                </td>
                <td>
                    -showDialog (only if no config string is supplied).
                </td>
                <td>
                    4.0.0644
                </td>
                <td>
                    4.0.065
                </td>
            </tr>
            <tr>
                <td>
                    -showDeviceList
                </td>
                <td>
                    Do not actually open the device, but instead dump a list of device numbers and device names to the standard output. The format of the dump is up to 2 decimal digits (beginning with '1' for the first device), followed by a colon and a space, and the remaining characters before the new line constituting the device name, as known to WDM.
                </td>
                <td></td>
                <td>
                    4.0.0644
                </td>
                <td>
                    4.0.065
                </td>
            </tr>
            <tr>
                <td>
                    -devNum=<i>n</i>
                </td>
                <td>
                    Open device <i>n</i>, rather than the default device.
                </td>
                <td>
                    1
                </td>
                <td>
                    4.0.0644
                </td>
                <td>
                    4.0.065
                </td>
            </tr>
            <tr>
                <td>
                    -flipH
                </td>
                <td>
                    Flip camera image horizontally.
                </td>
                <td></td>
                <td>
                    4.0.0644
                </td>
                <td>
                    4.0.065
                </td>
            </tr>
            <tr>
                <td>
                    -flipV
                </td>
                <td>
                    Flip camera image vertically.
                </td>
                <td>
                    -flipV (only if no config string is supplied).
                </td>
                <td>
                    4.0.0644
                </td>
                <td>
                    4.0.065
                </td>
            </tr>
        </table>
    </body>
</html>
###AR_VIDEO_DEVICE_WINDOWS_DRAGONFLY
<html>
    <body>
        <table border="2" cellspacing="4" cellpadding="3" rules="all" style="margin:1em 1em 1em 0; border:solid 1px #AAAAAA; border-collapse:collapse;empty-cells:show;">
            <tr>
                <th>
                    video config string
                </th>
                <th>
                    usage notes
                </th>
                <th>
                    Default value
                </th>
                <th>
                    Avail.: (1)
                </th>
                <th>
                    Unavail.: (2)
                </th>
            </tr>
            <tr>
                <td>
                    -device=WinDF
                </td>
                <td>
                    Select this device for use.
                </td>
                <td></td>
                <td></td>
                <td></td>
            </tr>
            <tr>
                <td>
                    -rate=<i>N</i>
                </td>
                <td>
                    Specifies desired input framerate. (1.875, 3.75, 7.5, 15, 30, 60, 120)
                </td>
                <td>
                    15
                </td>
                <td>
                    4.6.0
                </td>
                <td></td>
            </tr>
            <tr>
                <td>
                    -mode=<i>[160x120YUV444|320x240YUV422|640x480YUV411|640x480YUV422| 640x480RGB|640x480Y8|640x480Y16|800x600YUV422|800x600RGB| 800x600Y8|800x600Y16|1024x768YUV422|1024x768RGB|1024x768Y8| 1024x768Y16|1280x960YUV422|1280x960RGB|1280x960Y8|1280x960Y16| 1600x1200YUV422|1600x1200RGB|1600x1200Y8|1600x1200Y16]</i>
                </td>
                <td>
                    Specifies input image format. N.B. Not all formats listed may be supported by ARToolKit.
                </td>
                <td>
                    1024x768RGB
                </td>
                <td>
                    4.6.0
                </td>
                <td></td>
            </tr>
            <tr>
                <td>
                    -index=<i>N</i>
                </td>
                <td>
                    Specifies bus index of device to use. (Range is from 0 to number of connected devices minus one.)
                </td>
                <td>
                    0
                </td>
                <td>
                    4.6.0
                </td>
                <td></td>
            </tr>
        </table>
        <h3>
            <span class="mw-headline" id="AR_VIDEO_DEVICE_WINDOWS_HDCAM">AR_VIDEO_DEVICE_WINDOWS_HDCAM</span>
        </h3>
        <table border="2" cellspacing="4" cellpadding="3" rules="all" style="margin:1em 1em 1em 0; border:solid 1px #AAAAAA; border-collapse:collapse;empty-cells:show;">
            <tr>
                <th>
                    video config string
                </th>
                <th>
                    usage notes
                </th>
                <th>
                    Default value
                </th>
                <th>
                    Avail.: (1)
                </th>
                <th>
                    Unavail.: (2)
                </th>
            </tr>
            <tr>
                <td>
                    -device=WinHD
                </td>
                <td>
                    Select this device for use.
                </td>
                <td></td>
                <td></td>
                <td></td>
            </tr>
        </table>
    </body>
</html>
###AR_VIDEO_DEVICE_QUICKTIME7
The QuickTime7 video plugin uses the QTKit API introduced with QuickTime version 7 on Mac OS X. It offers improved performance over the previous QuickTime modules, however as of ARToolKit Professional v4.5.0, it does not yet support reading from file or network stream, so the previous QUICKTIME module should still be used in that case.
<html>
    <body>
        <table border="2" cellspacing="4" cellpadding="3" rules="all" style="margin:1em 1em 1em 0; border:solid 1px #AAAAAA; border-collapse:collapse;empty-cells:show;">
            <tr>
                <th>
                    video config string
                </th>
                <th>
                    usage notes
                </th>
                <th>
                    Default value
                </th>
                <th>
                    Avail.: (1)
                </th>
                <th>
                    Unavail.: (2)
                </th>
            </tr>
            <tr>
                <td>
                    -device=QuickTime7
                </td>
                <td>
                    Select this device for use.
                </td>
                <td></td>
                <td>
                    4.5.0
                </td>
                <td></td>
            </tr>
            <tr>
                <td>
                    -width=<i>w</i>
                </td>
                <td>
                    Scale camera native image to width w.
                </td>
                <td>
                    camera native image width
                </td>
                <td>
                    4.5.0
                </td>
                <td></td>
            </tr>
            <tr>
                <td>
                    -height=<i>h</i>
                </td>
                <td>
                    Scale camera native image to height h.
                </td>
                <td>
                    camera native image height
                </td>
                <td>
                    4.5.0
                </td>
                <td></td>
            </tr>
            <tr>
                <td>
                    -pixelformat=<i>cccc</i>
                </td>
                <td>
                    Return images with pixels in format cccc, where cccc is either a
                    <p>
                        numeric pixel format number or a valid 4-character-code for a pixel format. The following numeric values are supported: 24 (24-bit RGB), 32 (32-bit ARGB), 40 (8-bit grey) The following 4-character-codes are supported: BGRA, RGBA, ABGR, 24BG, 2vuy, yuvs. (See <a href="http://developer.apple.com/library/mac/#technotes/tn2010/tn2273.html" class="external free" rel="nofollow">http://developer.apple.com/library/mac/#technotes/tn2010/tn2273.html</a>.)
                    </p>
                </td>
                <td>
                    Depends on camera; for many USB video-class devices, either '2vuy' or 'yuvs'.
                </td>
                <td>
                    4.5.0
                </td>
                <td></td>
            </tr>
            <tr>
                <td>
                    -source=<i>N</i>
                </td>
                <td>
                    Acquire video from connected source device with index N.
                </td>
                <td>
                    0
                </td>
                <td>
                    4.5.0
                </td>
                <td></td>
            </tr>
            <tr>
                <td>
                    -nomuxed
                </td>
                <td>
                    Do not search for video from multiplexed video/audio devices (e.g. DV cams).
                </td>
                <td>
                    Off (i.e. muxed sources are included in the search).
                </td>
                <td>
                    4.6.0
                </td>
                <td></td>
            </tr>
        </table>
    </body>
</html>
###AR_VIDEO_DEVICE_QUICKTIME
Extra help on building this video capture module can be found on the page [Building libARvideo][libarvideo].

The QuickTime video plugin can operate in two modes:

-   In the first mode (the default), it acquires live video from a video capture source via QuickTime's video grabber. (Note that QuickTime for Windows does not come with a video digitizer component, and a third party component (e.g. [WinVDIG][winvidg] must be installed.)
-   In the second mode, specified by passing a video configure parameter "-movie=*pathnameOrURL*", the plugin can open any valid QuickTime resource, including movies from disk, or movies streamed via http, rtsp or ftp protocols.

####QuickTime Video Input from VDIG
<html>
    <body>
        <table border="2" cellspacing="4" cellpadding="3" rules="all" style="margin:1em 1em 1em 0; border:solid 1px #AAAAAA; border-collapse:collapse;empty-cells:show;">
            <tr>
                <th>
                    video config string
                </th>
                <th>
                    usage notes
                </th>
                <th>
                    Default value
                </th>
                <th>
                    Avail.: (1)
                </th>
                <th>
                    Unavail.: (2)
                </th>
            </tr>
            <tr>
                <td>
                    -device=QUICKTIME
                </td>
                <td>
                    Select this device for use.
                </td>
                <td></td>
                <td>
                    4.3.0
                </td>
                <td></td>
            </tr>
            <tr>
                <td>
                    -[no]dialog
                </td>
                <td>
                    Don't display video settings dialog.
                </td>
                <td>
                    -dialog
                </td>
                <td>
                    4.3.0
                </td>
                <td></td>
            </tr>
            <tr>
                <td>
                    -[no]standarddialog
                </td>
                <td>
                    Don't remove unnecessary panels from video settings dialog.
                </td>
                <td>
                    -nostandarddialog
                </td>
                <td>
                    4.3.0
                </td>
                <td></td>
            </tr>
            <tr>
                <td>
                    -width=<i>w</i>
                </td>
                <td>
                    Scale camera native image to width w.
                </td>
                <td>
                    640
                </td>
                <td>
                    4.3.0
                </td>
                <td></td>
            </tr>
            <tr>
                <td>
                    -height=<i>h</i>
                </td>
                <td>
                    Scale camera native image to height h.
                </td>
                <td>
                    480
                </td>
                <td>
                    4.3.0
                </td>
                <td></td>
            </tr>
            <tr>
                <td>
                    -[no]fps
                </td>
                <td>
                    Overlay camera frame counter on image.
                </td>
                <td>
                    -nofps
                </td>
                <td>
                    4.3.0
                </td>
                <td></td>
            </tr>
            <tr>
                <td>
                    -grabber=<i>n</i>
                </td>
                <td>
                    With multiple QuickTime video grabber components installed,
                    <p>
                        use component n (default n=1). N.B. It is NOT necessary to use this option if you have installed more than one video input device (e.g. two cameras) as the default QuickTime grabber can manage multiple video channels.
                    </p>
                </td>
                <td>
                    1
                </td>
                <td>
                    4.3.0
                </td>
                <td></td>
            </tr>
            <tr>
                <td>
                    -pixelformat=<i>cccc</i>
                </td>
                <td>
                    Return images with pixels in format cccc, where cccc is either a
                    <p>
                        numeric pixel format number or a valid 4-character-code for a pixel format. The following numeric values are supported: 24 (24-bit RGB), 32 (32-bit ARGB), 40 (8-bit grey) The following 4-character-codes are supported: BGRA, RGBA, ABGR, 24BG, 2vuy, yuvs. (See <a href="http://developer.apple.com/library/mac/#technotes/tn2010/tn2273.html" class="external free" rel="nofollow">http://developer.apple.com/library/mac/#technotes/tn2010/tn2273.html</a>.)
                    </p>
                </td>
                <td>
                    Depends on platform; default for Mac OS X is 32 (i.e. ARGB), default for Windows is BGRA.
                </td>
                <td>
                    4.3.0
                </td>
                <td></td>
            </tr>
            <tr>
                <td>
                    -[no]fliph
                </td>
                <td>
                    Flip camera image horizontally.
                </td>
                <td>
                    -nofliph
                </td>
                <td>
                    4.3.0
                </td>
                <td></td>
            </tr>
            <tr>
                <td>
                    -[no]flipv
                </td>
                <td>
                    Flip camera image vertically.
                </td>
                <td>
                    -noflipv
                </td>
                <td>
                    4.3.0
                </td>
                <td></td>
            </tr>
            <tr>
                <td>
                    -[no]singlebuffer
                </td>
                <td>
                    Use single buffering of captured video instead of triple-buffering.
                </td>
                <td>
                    -nosinglebuffer
                </td>
                <td>
                    4.3.0
                </td>
                <td></td>
            </tr>
        </table>
    </body>
</html>
####QuickTime Video Input from Movie File or Stream
<html>
    <body>
        <table border="2" cellspacing="4" cellpadding="3" rules="all" style="margin:1em 1em 1em 0; border:solid 1px #AAAAAA; border-collapse:collapse;empty-cells:show;">
            <tr>
                <th>
                    video config string
                </th>
                <th>
                    usage notes
                </th>
                <th>
                    Default value
                </th>
                <th>
                    Avail.: (1)
                </th>
                <th>
                    Unavail.: (2)
                </th>
            </tr>
            <tr>
                <td>
                    -device=QUICKTIME
                </td>
                <td>
                    Select this device for use.
                </td>
                <td></td>
                <td>
                    4.3.0
                </td>
                <td></td>
            </tr>
            <tr>
                <td>
                    -movie=<i>file:///path/to/file</i><br />
                    -movie="<i>file:///path/to/file</i>"
                </td>
                <td>
                    Specifies that video should be acquired from a QuickTime movie resource.
                    <p>
                        This can be any valid movie resource that QuickTime can open, including files and streams. If a movie file is to be opened, supply a file URI specifying the full pathname. Pathnames must be URI-encoded, i.e. if the pathname contains spaces, these should be replaced with '+' characters. e.g. -movie="file:///C:/Program+Files/QuickTime/Sample.mov" or -movie=file:///Developer/Examples/WebKit/WebKitMoviePlugIn/sample.mov . If a movie stream is to be opened, it may be specified via an "http://", "rtsp://" or "ftp://" URL, or it can be referred to in a stream description file (a .sdp file). In ARToolKit versions 4.3.0 - 4.4.4, the maximum URL length was 255 characters. As of ARToolKit 4.5.0, this has been increased to 1023 characters.
                    </p>
                </td>
                <td></td>
                <td>
                    4.3.0
                </td>
                <td></td>
            </tr>
            <tr>
                <td>
                    -[no]1to1
                </td>
                <td>
                    Do not fit the movie to the window or buffer size, but
                    <p>
                        instead display it at its original size (1 to 1 scaling).
                    </p>
                </td>
                <td>
                    -no1to1
                </td>
                <td>
                    4.3.0
                </td>
                <td></td>
            </tr>
            <tr>
                <td>
                    -[no]fill
                </td>
                <td>
                    Rather than fitting the movie into the window so that all
                    <p>
                        the movie is visible, scale it so that it completely fills the window or buffer. The movie's aspect ratio will be maintained, and this may result in some of the movie being clipped at the top and bottom or left and right.
                    </p>
                </td>
                <td>
                    -nofill
                </td>
                <td>
                    4.3.0
                </td>
                <td></td>
            </tr>
            <tr>
                <td>
                    -[no]stretch
                </td>
                <td>
                    Rather than fitting the movie into the window so that all
                    <p>
                        the movie is visible, scale it so that it completely fills the window or buffer. The movie's aspect ratio will be stretched if necessary so that no pixels are clipped.
                    </p>
                </td>
                <td>
                    -nostretch
                </td>
                <td>
                    4.3.0
                </td>
                <td></td>
            </tr>
            <tr>
                <td>
                    -[no]loop
                </td>
                <td>
                    Request that the movie loop continuously. This
                    <p>
                        parameter has no effect for streaming movies. Unless this parameter is specified, calls to arVideoQuickTimeMovieIdle() will return AR_E_EOF when the movie has finished playing.
                    </p>
                </td>
                <td>
                    -loop
                </td>
                <td>
                    4.3.0
                </td>
                <td></td>
            </tr>
            <tr>
                <td>
                    -[no]showcontroller
                </td>
                <td>
                    Show the QuickTime movie controller in the frame.
                    <p>
                        (Unfortunately, the user will not be able to interact with the controller to pause and jog the movie.)
                    </p>
                </td>
                <td>
                    -showcontroller
                </td>
                <td>
                    4.3.0
                </td>
                <td></td>
            </tr>
            <tr>
                <td>
                    -[no]mute
                </td>
                <td>
                    Set movie audio volume to 0.
                </td>
                <td>
                    -nomute
                </td>
                <td>
                    4.3.0
                </td>
                <td></td>
            </tr>
            <tr>
                <td>
                    -[no]pause
                </td>
                <td>
                    Open movie in paused state. A call to arVideoCapStart()
                    <p>
                        would be required to unpause the movie.
                    </p>
                </td>
                <td>
                    -pause
                </td>
                <td>
                    4.3.0
                </td>
                <td></td>
            </tr>
            <tr>
                <td>
                    -width=<i>w</i>
                </td>
                <td>
                    Scale movie native frame to width w.
                </td>
                <td>
                    Width of movie frame.
                </td>
                <td>
                    4.3.0
                </td>
                <td></td>
            </tr>
            <tr>
                <td>
                    -height=<i>h</i>
                </td>
                <td>
                    Scale movie native frame to height h.
                </td>
                <td>
                    Height of movie frame.
                </td>
                <td>
                    4.3.0
                </td>
                <td></td>
            </tr>
            <tr>
                <td>
                    -[no]fliph
                </td>
                <td>
                    Flip movie frame horizontally.
                </td>
                <td>
                    -nofliph
                </td>
                <td>
                    4.3.0
                </td>
                <td></td>
            </tr>
            <tr>
                <td>
                    -[no]flipv
                </td>
                <td>
                    Flip movie frame vertically.
                </td>
                <td>
                    -noflipv
                </td>
                <td>
                    4.3.0
                </td>
                <td></td>
            </tr>
            <tr>
                <td>
                    -pixelformat=cccc
                </td>
                <td>
                    Ignored unless -offscreen is also passed, requests return of
                    <p>
                        movie frames with pixels in format cccc, where cccc is either a numeric pixel format number or a valid 4-character-code for a pixel format. The following values are supported: 32, BGRA, RGBA, ABGR, 24, 24BG, 2vuy, yuvs. (See <a href="http://developer.apple.com/quicktime/icefloe/dispatch020.html" class="external free" rel="nofollow">http://developer.apple.com/quicktime/icefloe/dispatch020.html</a>.)
                    </p>
                </td>
                <td>
                    Depends on platform; default for Mac OS X is 32 (i.e. ARGB), default for Windows is BGRA.
                </td>
                <td>
                    4.3.0
                </td>
                <td></td>
            </tr>
            <tr>
                <td>
                    -[no]singlebuffer
                </td>
                <td>
                    Ignored unless -offscreen is also passed, use single buffering of
                    <p>
                        captured movie instead of triple-buffering.
                    </p>
                </td>
                <td>
                    -nosinglebuffer
                </td>
                <td>
                    4.3.0
                </td>
                <td></td>
            </tr>
        </table>
    </body>
</html>
###AR_VIDEO_DEVICE_QUICKTIME_OLD
<html>
    <body>
        <table border="2" cellspacing="4" cellpadding="3" rules="all" style="margin:1em 1em 1em 0; border:solid 1px #AAAAAA; border-collapse:collapse;empty-cells:show;">
            <tr>
                <th>
                    video config string
                </th>
                <th>
                    usage notes
                </th>
                <th>
                    Default value
                </th>
                <th>
                    Avail.: (1)
                </th>
                <th>
                    Unavail.: (2)
                </th>
            </tr>
            <tr>
                <td>
                    -device=QUICKTIME_OLD
                </td>
                <td>
                    Select this device for use.
                </td>
                <td></td>
                <td>
                    4.0.0
                </td>
                <td></td>
            </tr>
            <tr>
                <td>
                    -width=<i>N</i>
                </td>
                <td>
                    Specify the width of the returned image.
                </td>
                <td>
                    640
                </td>
                <td>
                    4.0.0
                </td>
                <td></td>
            </tr>
            <tr>
                <td>
                    -height=<i>N</i>
                </td>
                <td>
                    Specify the height of the returned image.
                </td>
                <td>
                    480
                </td>
                <td>
                    4.0.0
                </td>
                <td></td>
            </tr>
        </table>
    </body>
</html>
###AR_VIDEO_DEVICE_WINDOWS_DSVIDEOLIB
<html>
    <body>
        <table border="2" cellspacing="4" cellpadding="3" rules="all" style="margin:1em 1em 1em 0; border:solid 1px #AAAAAA; border-collapse:collapse;empty-cells:show;">
            <tr>
                <th>
                    video config string
                </th>
                <th>
                    usage notes
                </th>
                <th>
                    Default value
                </th>
                <th>
                    Avail.: (1)
                </th>
                <th>
                    Unavail.: (2)
                </th>
            </tr>
            <tr>
                <td>
                    -device=WinDSVL
                </td>
                <td>
                    Select this device for use.
                </td>
                <td></td>
                <td>
                    4.1.0
                </td>
                <td></td>
            </tr>
            <tr>
                <td>
                    <i>remainder of config string</i>
                </td>
                <td>
                    Specify either an XML string (i.e. beginning '&lt;?xml') or a pathname to an XML file (e.g. 'config.XML'), conforming to the DSVideoLib XML Schema (<a href="http://www.artoolworks.com/support/attachments/DsVideoLib.xsd" class="external text" rel="nofollow">DsVideoLib.xsd</a>). <b><a href="http://www.artoolworks.com/support/attachments/DsVideoLib.svg" class="external text" rel="nofollow">Click here to load an interactive SVG view of the DSVideoLib XML Schema</a>.</b>
                </td>
                <td>
                    &lt;?xml version="1.0" encoding="UTF-8"?&gt;&lt;dsvl_input&gt;&lt;camera show_format_dialog="true" friendly_name=""&gt;&lt;pixel_format&gt;&lt;RGB32 flip_h="false" flip_v="true"/&gt;&lt;/pixel_format&gt;&lt;/camera&gt;&lt;/dsvl_input&gt;
                </td>
                <td>
                    4.1.0
                </td>
                <td></td>
            </tr>
        </table>
    </body>
</html>
###AR_VIDEO_DEVICE_GSTREAMER
<html>
    <body>
        <table border="2" cellspacing="4" cellpadding="3" rules="all" style="margin:1em 1em 1em 0; border:solid 1px #AAAAAA; border-collapse:collapse;empty-cells:show;">
            <tr>
                <th>
                    video config string
                </th>
                <th>
                    usage notes
                </th>
                <th>
                    Default value
                </th>
                <th>
                    Avail.: (1)
                </th>
                <th>
                    Unavail.: (2)
                </th>
            </tr>
            <tr>
                <td>
                    -device=GStreamer
                </td>
                <td>
                    Select this device for use.
                </td>
                <td></td>
                <td>
                    4.3.2
                </td>
                <td></td>
            </tr>
            <tr>
                <td>
                    <i>remainder of config string</i>
                </td>
                <td>
                    Specifies a configuration string following the <code><a href="http://linux.die.net/man/1/gst-launch-0.10" class="external text" rel="nofollow">gst-launch</a></code> syntax.
                    <p>
                        A variety of GStreamer pipelines can be constructed, for example to pull video from a webcam, local file, or network stream. These are the important points to observe regarding where ARToolKit fits into a GStreamer pipeline:
                    </p>
                    <ul>
                        <li>ARToolKit accepts video only in 24-bit RGB format, so must be prefixed with a capsfilter element 'video/x-raw-rgb,bpp=24'. Usually, you will also need to use a 'ffmpegcolorspace' element to convert incoming video into this format, unless the upstream source can already produce this format.
                        </li>
                        <li>ARToolKit acquires the video from a GStreamer 'identity' element, with the property 'name=artoolkit'. You should also set the property 'sync=true' on this element, or else some types of sources (e.g. video from a file) may run faster or slower than normal.
                        </li>
                        <li>ARToolKit is NOT a sink pad, so generally, you should pipe the stream for ARToolKit to a 'fakesink' element.
                        </li>
                    </ul>
                    <p>
                        Putting these points together, the last part of the GStreamer pipeline for ARToolKit will usually be:
                    </p>
        deo/x-raw-rgb,bpp=24 ! identity name=artoolkit sync=true ! fakesink
                    <p>
                        Note also that ARToolKit will respect the size of incoming video, so you can add the 'width=' and 'height=' properties to the capsfilter element, should you so desire.
                    </p>
                    <p>
                        Some more examples:
                    </p>
                    <ul>
                        <li>A webcam on /dev/video0 through Video4Linux v2 (V4L2):
        o0 use-fixed-fps=false ! ffmpegcolorspace ! video/x-raw-rgb,bpp=24 ! identity name=artoolkit sync=true ! fakesink
                        </li>
                        <li>A file from disk:
        er_test_xvid.avi ! decodebin2 ! ffmpegcolorspace ! video/x-raw-rgb,bpp=24 ! identity name=artoolkit sync=true ! fakesink
                        </li>
                        <li>A dummy test source:
        aw-rgb,bpp=24 ! identity name=artoolkit sync=true ! fakesink
                        </li>
                    </ul>
                    <p>
                        Further interesting reading concerning webcam control can be found here: <a href="http://www.oz9aec.net/index.php/gstreamer/345-a-weekend-with-gstreamer" class="external free" rel="nofollow">http://www.oz9aec.net/index.php/gstreamer/345-a-weekend-with-gstreamer</a> and here: <a href="http://www.oz9aec.net/index.php/gstreamer/367-webcam-pixel-formats-and-gstreamer-caps-filters" class="external free" rel="nofollow">http://www.oz9aec.net/index.php/gstreamer/367-webcam-pixel-formats-and-gstreamer-caps-filters</a> . A tool to help configure gstreamer can be found here: <a href="http://benlau.blog.opensource.hk/2008/09/gstreamer-pipeline-description.html" class="external free" rel="nofollow">http://benlau.blog.opensource.hk/2008/09/gstreamer-pipeline-description.html</a>
                    </p>
                </td>
                <td></td>
                <td>
                    4.3.2
                </td>
                <td></td>
            </tr>
        </table>
    </body>
</html>
###AR_VIDEO_DEVICE_IPHONE
The iOS video plugin is available on Apple iOS devices including iPhone 3G, iPhone 3GS, iPhone 4, iPod touch 4G and iPad 2.
As of ARToolKit for iOS version 4.5.5 (release 4) the iOS video plugin can operate in either two modes; either acquiring live video from a camera on the iOS device, or playing a pre-recorded video file stored in the app's bundle resource directory.
####iOS Video Input from Camera
<html>
    <body>
        <table border="2" cellspacing="4" cellpadding="3" rules="all" style="margin:1em 1em 1em 0; border:solid 1px #AAAAAA; border-collapse:collapse;empty-cells:show;">
            <tr>
                <th>
                    video config string
                </th>
                <th>
                    usage notes
                </th>
                <th>
                    Default value
                </th>
                <th>
                    Avail.: (1)
                </th>
                <th>
                    Unavail.: (2)
                </th>
            </tr>
            <tr>
                <td>
                    -device=iPhone
                </td>
                <td>
                    Select this device for use.
                </td>
                <td></td>
                <td>
                    4.4.3 (release 1.0)
                </td>
                <td></td>
            </tr>
            <tr>
                <td>
                    -format=X
                </td>
                <td>
                    Return images with pixels in format X, where X is one of the following format tokens:
                    <p>
                        420v, 420f, BGRA, RGBA, RGBA_5551, RGBA_4444
                    </p>
                </td>
                <td>
                    420f (ARToolKit v5.0 and later.)<br />
                    BGRA (ARToolKit version pre-5.0)
                </td>
                <td>
                    4.4.3 (release 1.0)
                </td>
                <td></td>
            </tr>
            <tr>
                <td>
                    -preset=X
                </td>
                <td>
                    Specify use of camera settings preset X, where X is one of:
                    <p>
                        cif, 480p, 720p, 1080p, low, medium, high, photo. (N.B.:480p=640x480, i.e. 4:3 aspect ratio, 720p=1280x720 and 1080p=1920x1080 i.e. 16:9 aspect ratio).
                    </p>
                </td>
                <td>
                    medium
                </td>
                <td>
                    4.5.1 (release 2.0)
                </td>
                <td></td>
            </tr>
            <tr>
                <td>
                    -position=X
                </td>
                <td>
                    Choose between rear/back and front-mounted camera (where available).
                    <p>
                        Allowable values for X include: rear, back, front. (N.B.:rear is a synonym for back). Front is not supported on iPhone 3G or iPhone 3GS.
                    </p>
                </td>
                <td>
                    rear
                </td>
                <td>
                    4.5.1 (release 2.0)
                </td>
                <td></td>
            </tr>
            <tr>
                <td>
                    -[no]flipv
                </td>
                <td>
                    Flip the incoming image from the camera vertically. On front mounted-cameras, this option is on by default (but can be overridden by specifying -noflipv). Flipping the video vertically matches the orientation of the video image (when displayed on the screen of the device) to the physical orientation of the device.
                </td>
                <td>
                    noflipv (on rear camera). flipv (on front camera)
                </td>
                <td>
                    4.5.4 (release 3.0)
                </td>
                <td></td>
            </tr>
            <tr>
                <td>
                    -[no]fliph
                </td>
                <td>
                    Flip the incoming image from the camera horizontally.
                </td>
                <td>
                    nofliph
                </td>
                <td>
                    4.6.6 (release 16)
                </td>
                <td></td>
            </tr>
            <tr>
                <td>
                    -width=<i>w</i>
                </td>
                <td>
                    Crop native camera image width to w.
                </td>
                <td>
                    camera native image width for given preset (see above.)
                </td>
                <td>
                    4.4.3 (release 1.0)
                </td>
                <td>
                    4.5.0-
                </td>
            </tr>
            <tr>
                <td>
                    -height=<i>h</i>
                </td>
                <td>
                    Crop native camera image height to h.
                </td>
                <td>
                    camera native image height for given preset (see above.)
                </td>
                <td>
                    4.4.3 (release 1.0)
                </td>
                <td>
                    4.5.0-
                </td>
            </tr>
            <tr>
                <td>
                    -bufferpow2
                </td>
                <td>
                    Requests that images are returned in a buffer which has power-of-two dimensions.
                </td>
                <td>
                    camera native image size for given preset (see below.)
                </td>
                <td>
                    4.4.3 (release 1.0)
                </td>
                <td>
                    4.5.0-
                </td>
            </tr>
        </table>
    </body>
</html>
####iOS Video Input from Movie File
<html>
    <body>
        <table border="2" cellspacing="4" cellpadding="3" rules="all" style="margin:1em 1em 1em 0; border:solid 1px #AAAAAA; border-collapse:collapse;empty-cells:show;">
            <tr>
                <th>
                    video config string
                </th>
                <th>
                    usage notes
                </th>
                <th>
                    Default value
                </th>
                <th>
                    Avail.: (1)
                </th>
                <th>
                    Unavail.: (2)
                </th>
            </tr>
            <tr>
                <td>
                    -device=iPhone
                </td>
                <td>
                    Select this device for use.
                </td>
                <td></td>
                <td>
                    4.5.5 (release 4.0)
                </td>
                <td></td>
            </tr>
            <tr>
                <td>
                    -movie=<i>pathname</i><br />
                    -movie="<i>pathname</i>"
                </td>
                <td>
                    Specifies that video should be acquired from a movie resource.
                    <p>
                        This can be any valid movie file resource that iOS can open, but typically MPEG-4 (h.264 video with optional AAC audio). The pathname is relative to the resources directory of the app bundle. If the pathname contains spaces, it must be surrounded with double quotes ("). e.g. -movie="My great sample.mov".
                    </p>
                </td>
                <td></td>
                <td>
                    4.5.5 (release 4.0)
                </td>
                <td></td>
            </tr>
            <tr>
                <td>
                    -[no]1to1
                </td>
                <td>
                    <b>N.B. CURRENTLY IGNORED.</b> Do not fit the movie to the window or buffer size, but
                    <p>
                        instead display it at its original size (1 to 1 scaling).
                    </p>
                </td>
                <td>
                    -no1to1
                </td>
                <td>
                    4.5.5 (release 4.0)
                </td>
                <td></td>
            </tr>
            <tr>
                <td>
                    -[no]fill
                </td>
                <td>
                    <b>N.B. CURRENTLY IGNORED.</b> Rather than fitting the movie into the window so that all
                    <p>
                        the movie is visible, scale it so that it completely fills the window or buffer. The movie's aspect ratio will be maintained, and this may result in some of the movie being clipped at the top and bottom or left and right.
                    </p>
                </td>
                <td>
                    -nofill
                </td>
                <td>
                    4.5.5 (release 4.0)
                </td>
                <td></td>
            </tr>
            <tr>
                <td>
                    -[no]stretch
                </td>
                <td>
                    <b>N.B. CURRENTLY IGNORED.</b> Rather than fitting the movie into the window so that all
                    <p>
                        the movie is visible, scale it so that it completely fills the window or buffer. The movie's aspect ratio will be stretched if necessary so that no pixels are clipped.
                    </p>
                </td>
                <td>
                    -stretch
                </td>
                <td>
                    4.5.5 (release 4.0)
                </td>
                <td></td>
            </tr>
            <tr>
                <td>
                    -[no]loop
                </td>
                <td>
                    Request that the movie loop continuously.
                </td>
                <td>
                    -loop
                </td>
                <td>
                    4.5.5 (release 4.0)
                </td>
                <td></td>
            </tr>
            <tr>
                <td>
                    -[no]mute
                </td>
                <td>
                    Set movie audio volume to 0.
                </td>
                <td>
                    -nomute
                </td>
                <td>
                    4.5.5 (release 4.0)
                </td>
                <td></td>
            </tr>
            <tr>
                <td>
                    -[no]pause
                </td>
                <td>
                    Open movie in paused state. A call to arVideoCapStart()
                    <p>
                        would be required to unpause the movie.
                    </p>
                </td>
                <td>
                    -pause
                </td>
                <td>
                    4.5.5 (release 4.0)
                </td>
                <td></td>
            </tr>
            <tr>
                <td>
                    -width=<i>w</i>
                </td>
                <td>
                    Scale movie native frame to width w.
                </td>
                <td>
                    Width of movie frame.
                </td>
                <td>
                    4.5.5 (release 4.0)
                </td>
                <td></td>
            </tr>
            <tr>
                <td>
                    -height=<i>h</i>
                </td>
                <td>
                    Scale movie native frame to height h.
                </td>
                <td>
                    Height of movie frame.
                </td>
                <td>
                    4.5.5 (release 4.0)
                </td>
                <td></td>
            </tr>
            <tr>
                <td>
                    -[no]fliph
                </td>
                <td>
                    <b>N.B. CURRENTLY IGNORED.</b> Flip movie frame horizontally.
                </td>
                <td>
                    -nofliph
                </td>
                <td>
                    4.5.5 (release 4.0)
                </td>
                <td></td>
            </tr>
            <tr>
                <td>
                    -[no]flipv
                </td>
                <td>
                    Flip movie frame vertically.
                </td>
                <td>
                    -noflipv
                </td>
                <td>
                    4.5.5 (release 4.0)
                </td>
                <td></td>
            </tr>
            <tr>
                <td>
                    -pixelformat=cccc
                </td>
                <td>
                    Ignored unless -offscreen is also passed, requests return of
                    <p>
                        movie frames with pixels in format cccc, where cccc is either a numeric pixel format number or a valid 4-character-code for a pixel format. The following values are supported: 32, BGRA, RGBA, ABGR, 24, 24BG, 2vuy, yuvs. (See <a href="http://developer.apple.com/quicktime/icefloe/dispatch020.html" class="external free" rel="nofollow">http://developer.apple.com/quicktime/icefloe/dispatch020.html</a>.)
                    </p>
                </td>
                <td>
                    BGRA
                </td>
                <td>
                    4.5.5 (release 4.0)
                </td>
                <td></td>
            </tr>
        </table>
    </body>
</html>
###AR_VIDEO_DEVICE_WINDOWS_MEDIA_FOUNDATION
<html>
    <body>
        <table border="2" cellspacing="4" cellpadding="3" rules="all" style="margin:1em 1em 1em 0; border:solid 1px #AAAAAA; border-collapse:collapse;empty-cells:show;">
            <tr>
                <th>
                    video config string
                </th>
                <th>
                    usage notes
                </th>
                <th>
                    Default value
                </th>
                <th>
                    Avail.: (1)
                </th>
                <th>
                    Unavail.: (2)
                </th>
            </tr>
            <tr>
                <td>
                    -device=WinMF
                </td>
                <td>
                    Select this device for use.
                </td>
                <td></td>
                <td>
                    5.1.5
                </td>
                <td></td>
            </tr>
            <tr>
                <td>
                    -showDeviceList
                </td>
                <td>
                    Do not actually open the device, but instead dump a list of device numbers and device names to the standard output. The format of the dump is up to 2 decimal digits (beginning with '1' for the first device), followed by a colon and a space, and the remaining characters before the new line constituting the device name, as known to WDM.
                </td>
                <td>
                    -noShowDeviceList
                </td>
                <td>
                    5.1.5
                </td>
                <td></td>
            </tr>
            <tr>
                <td>
                    -noShowDeviceList
                </td>
                <td>
                    Override a previous -showDeviceList option
                </td>
                <td>
                    -noShowDeviceList
                </td>
                <td>
                    5.1.5
                </td>
                <td></td>
            </tr>
            <tr>
                <td>
                    -devNum=<i>n</i>
                </td>
                <td>
                    Open device <i>n</i>, rather than the default device. E.g. if two cameras are connected, use -devNum=2 to access the second camera.
                </td>
                <td>
                    1
                </td>
                <td>
                    5.1.5
                </td>
                <td></td>
            </tr>
            <tr>
                <td>
                    -format=<i>X</i>
                </td>
                <td>
                    Return images with pixels in format X, where X is one of: BGRA, BGR, NV12/420f, 2vuy/UYVY, yuvs/YUY2, RGB_565, RGBA_5551. The most reliable format is BGRA, due to support within Media Foundation for conversion from YUV-colour spaces to RGB colour space. Other formats must be supported natively on the device in order for the request to succeed.
                </td>
                <td>
                    Default pixel format.
                </td>
                <td>
                    5.1.5
                </td>
                <td></td>
            </tr>
            <tr>
                <td>
                    -width=<i>w</i>
                </td>
                <td>
                    Request video format of width w pixels
                </td>
                <td>
                    Default frame width
                </td>
                <td>
                    5.1.5
                </td>
                <td></td>
            </tr>
            <tr>
                <td>
                    -height=<i>h</i>
                </td>
                <td>
                    Request video format of height h pixels
                </td>
                <td>
                    Default frame height
                </td>
                <td>
                    5.1.5
                </td>
                <td></td>
            </tr>
            <tr>
                <td>
                    -flipV
                </td>
                <td>
                    Flip image vertically.
                </td>
                <td>
                    -noFlipV
                </td>
                <td>
                    5.1.5
                </td>
                <td></td>
            </tr>
            <tr>
                <td>
                    -noFlipV
                </td>
                <td>
                    Override a previous -flipV option and do not flip image vertically.
                </td>
                <td>
                    -noFlipV
                </td>
                <td>
                    5.1.5
                </td>
                <td></td>
            </tr>
            <tr>
                <td>
                    -showFormats
                </td>
                <td>
                    Dump the full list of native formats to the console. This is helpful in determining device capabilities.
                </td>
                <td>
                    -noShowFormats
                </td>
                <td>
                    5.1.5
                </td>
                <td></td>
            </tr>
            <tr>
                <td>
                    -noShowFormats
                </td>
                <td>
                    Override a previous -showFormats option
                </td>
                <td>
                    -noShowFormats
                </td>
                <td>
                    5.1.5
                </td>
                <td></td>
            </tr>
        </table>
    </body>
</html>
###AR_VIDEO_DEVICE_WINDOWS_MEDIA_CAPTURE
<html>
    <body>
        <table border="2" cellspacing="4" cellpadding="3" rules="all" style="margin:1em 1em 1em 0; border:solid 1px #AAAAAA; border-collapse:collapse;empty-cells:show;">
            <tr>
                <th>
                    video config string
                </th>
                <th>
                    usage notes
                </th>
                <th>
                    Default value
                </th>
                <th>
                    Avail.: (1)
                </th>
                <th>
                    Unavail.: (2)
                </th>
            </tr>
            <tr>
                <td>
                    -device=WinMC
                </td>
                <td>
                    Select this device for use.
                </td>
                <td></td>
                <td>
                    5.1.7
                </td>
                <td></td>
            </tr>
            <tr>
                <td>
                    -position=X
                </td>
                <td>
                    Choose between rear/back and front-mounted (where available). Other options include cameras mounted on left, right, top or bottom edges of the device.
                    <p>
                        Allowable values for X include: rear, back, front, left, right, top, bottom, default. (N.B.:rear is a synonym for back).
                    </p>
                </td>
                <td>
                    default
                </td>
                <td>
                    5.1.7
                </td>
                <td></td>
            </tr>
            <tr>
                <td>
                    -devNum=<i>n</i>
                </td>
                <td>
                    Open device <i>n</i>, rather than the default device. E.g. if two cameras are connected, use -devNum=2 to access the second camera. If this option is combined with the <code>-position</code> option, then it will choose the n'th device at the preferred position. E.g. to choose the second of two rear cameras, you could use <code>-position=rear -devNum=2</code>.
                </td>
                <td>
                    1
                </td>
                <td>
                    5.1.7
                </td>
                <td></td>
            </tr>
            <tr>
                <td>
                    -format=<i>X</i>
                </td>
                <td>
                    Return images with pixels in format X, where X is one of: BGRA, BGR, NV12/420f, 2vuy/UYVY, yuvs/YUY2, RGB_565, RGBA_5551. The most reliable format is BGRA, due to support within Windows Media Capture for conversion from YUV-colour spaces to RGB colour space. Other formats must be supported natively on the device in order for the request to succeed.
                </td>
                <td>
                    Default pixel format.
                </td>
                <td>
                    5.1.7
                </td>
                <td></td>
            </tr>
            <tr>
                <td>
                    -width=<i>w</i>
                </td>
                <td>
                    Request video format of width w pixels
                </td>
                <td>
                    Default frame height
                </td>
                <td>
                    5.1.7
                </td>
                <td></td>
            </tr>
            <tr>
                <td>
                    -height=<i>h</i>
                </td>
                <td>
                    Request video format of height h pixels
                </td>
                <td>
                    Default frame height
                </td>
                <td>
                    5.1.7
                </td>
                <td></td>
            </tr>
            <tr>
                <td>
                    -flipV
                </td>
                <td>
                    Flip image vertically.
                </td>
                <td>
                    -noFlipV
                </td>
                <td>
                    5.1.7
                </td>
                <td></td>
            </tr>
            <tr>
                <td>
                    -noFlipV
                </td>
                <td>
                    Override a previous -flipV option and do not flip image vertically.
                </td>
                <td>
                    -noFlipV
                </td>
                <td>
                    5.1.7
                </td>
                <td></td>
            </tr>
        </table>
    </body>
</html>

[winvidg]: http://www.eden.net.nz/7/20071008/
[libarvideo]: 8_Advanced_Topics:windows_building_libarvideo
[general_environment_variables]: 1_Getting_Started:general_environment_variables
[config_camera_calibration]: 2_Configuration:config_camera_calibration
[config_camera_stereo_tracking]: 8_Advanced_Topics:config_camera_stereo_tracking
