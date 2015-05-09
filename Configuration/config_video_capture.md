#Configuring Video Capture in ARToolkit

##About libARvideo's Configuration Options
ARToolKit Professional includes libARvideo, a cross-platform library which captures video from a variety of different sources. In general, most users of ARToolKit who have a single webcam attached to their system will never delve into the workings of this library. However, the module or modules inside this library generally allow for a degree of configuration to control parameters of the capture sources with which they interface.

This section of the manual details some of the configuration options available with libARvideo.

##Changing Video Configuration
### Setting Configuration at Run Time
Video configurations are passed to libARvideo in a standard way; as a c-string containing text. What to put in the *contents* of the string depends on your capture source.

The contents of the string are different for different capture sources because although libARvideo presents a standard API for passing video to other code (e.g. libAR, libARgsub_lite and libARgsub), there is custom code inside libARvideo for each capture source (e.g. QuickTime, DirectShow, libdc1394). The capture sources generally implement a variety of different approaches to video stream acquisition. So, the configuration parameters are different depending on the underlying capture module being used.

The simplest way to specify the video configuration (without recompiling the example applications) is to create an [environment variable][1] "ARTOOLKIT5_CONFIG" with the video configuration you wish to use.

####ARToolKit Utilities
Some of the ARToolKit utilities (including calib_camera, calib_stereo and check_id) accept video configuration(s) as command-line parameters. The desired configuration is passed after a parameter "--vconf" (or --vconfL or --vconfR for calib_stereo). Note that if the video configuration string includes spaces, it must be quoted to prevent the shell passing it as multiple parameters.

### Setting Configuration Programmatically
Video configuration can also be passed to libARvideo programmatically (as the sole parameter to the arVideoOpen() call). When no string (NULL) or an empty string ("") is passed, libARvideo looks for an environment variable "ARTOOLKIT5_CONFIG" (as mentioned above) for the string. If this environment variable is not found, the video module will use a default configuration.

In most of the ARToolKit Professional examples, the video config is specified in a string named "vconf". Do a search in your source editor for "vconf" to see this. So in most of the examples, editing the vconf string in the sourcecode will change the video configuration being used.

Of course, editing sourcecode requires recompiling for the changes to take effect, so a few of the examples accept a command-line parameter and use this as vconf. You can look at the sourcecode to see if a given example does so.

#### ARToolKit for Unity
ARToolKit for Unity allows you to specify video configuration separately for each supported platform directly in the Unity Editor.

##Capture Sources and Switching Them
Where more than one capture source has been compiled into libARvideo on a given platform, you are allowed to switch between the options.

This table lists the capture sources available on each platform. *Note: If you have a binary release of ARToolKit, not all of these capture sources may have been compiled into your copy!*:

<table rules="all" style="margin:1em 1em 1em 0; border:solid 1px #AAAAAA; border-collapse:collapse;empty-cells:show;" border="2" cellpadding="3" cellspacing="4">

<tbody><tr>
<th>Platform </th><th> Capture source (descriptive name) </th><th> Constant required in &lt;AR/config.h&gt; for this source to be compiled into libARvideo </th><th>  video config string to select this capture source </th><th> Avail.: (1) </th><th> Unavail.: (2)
</th></tr>
<tr>
<td>All
</td><td>Dummy input
</td><td>AR_INPUT_DUMMY
</td><td> -device=Dummy
</td><td>4.0.0
</td><td>
</td></tr>
<tr>
<td>Mac OS X, Windows, Linux
</td><td>JPEG image input
</td><td>AR_INPUT_IMAGE
</td><td> -device=Image
</td><td>4.6.2
</td><td>
</td></tr>
<tr>
<td>Linux
</td><td><a href="http://www.video4linux.net/" class="external text" rel="nofollow">Video4Linux</a>
</td><td>AR_INPUT_V4L
</td><td> -device=LinuxV4L
</td><td>4.0.0
</td><td>
</td></tr>
<tr>
<td>Linux
</td><td><a href="http://gstreamer.freedesktop.org/" class="external text" rel="nofollow">GStreamer</a>
</td><td>AR_INPUT_GSTREAMER
</td><td> -device=GStreamer
</td><td>4.3.2
</td><td>
</td></tr>
<tr>
<td>Linux
</td><td><a href="http://sourceforge.net/projects/libdc1394/" class="external text" rel="nofollow">libdc1394</a>
</td><td>AR_INPUT_1394CAM
</td><td> -device=Linux1394Cam
</td><td>4.0.0
</td><td>
</td></tr>
<tr>
<td>Mac OS X, Windows
</td><td><a href="http://www.apple.com/quicktime/" class="external text" rel="nofollow">QuickTime®</a> (enhanced)
</td><td>AR_INPUT_QUICKTIME
</td><td> -device=QUICKTIME
</td><td>4.3.0
</td><td>
</td></tr>
<tr>
<td>Windows
</td><td><a href="http://msdn2.microsoft.com/en-us/library/ms783323.aspx" class="external text" rel="nofollow">DirectShow®</a>
</td><td>AR_INPUT_WINDOWS_DIRECTSHOW
</td><td> -device=WinDS
</td><td>4.0.0644
</td><td>4.0.065,4.1.x
</td></tr>
<tr>
<td>Windows
</td><td><a href="http://sourceforge.net/projects/dsvideolib" class="external text" rel="nofollow">DSVideoLib</a>
</td><td>AR_INPUT_WINDOWS_DSVIDEOLIB
</td><td> -device=WinDSVL
</td><td>4.1.0
</td><td>
</td></tr>
<tr>
<td>Windows
</td><td><a href="http://www.ptgrey.com/products/pgrflycapture/" class="external text" rel="nofollow">DragonFly FlyCapture®</a>
</td><td>AR_INPUT_WINDOWS_DRAGONFLY
</td><td> -device=WinDF
</td><td>4.0.0644
</td><td>4.0.065
</td></tr>
<tr>
<td>Mac OS X
</td><td><a href="http://www.apple.com/quicktime/" class="external text" rel="nofollow">QuickTime®</a>
</td><td>AR_INPUT_QUICKTIME_OLD
</td><td> -device=QUICKTIME_OLD
</td><td>4.0.0
</td><td>
</td></tr>
<tr>
<td>Windows
</td><td>HDCam64
</td><td>AR_INPUT_WINDOWS_HDCAM
</td><td> -device=WinHD
</td><td>4.0.0644
</td><td>4.0.065
</td></tr>
<tr>
<td>Linux
</td><td><a href="http://libdv.sourceforge.net/" class="external text" rel="nofollow">libdv</a>
</td><td>AR_INPUT_DV
</td><td> -device=LinuxDV
</td><td>4.0.0
</td><td>4.1.x, 4.3.x
</td></tr>
<tr>
<td>SGI Irix
</td><td>SGI video input
</td><td>AR_INPUT_SGI
</td><td> -device=SGI
</td><td>4.0.0
</td><td>4.1.x, 4.3.x
</td></tr>
<tr>
<td>Mac OS X
</td><td><a href="http://www.apple.com/quicktime/" class="external text" rel="nofollow">QuickTime®</a> (v7.0 and later)
</td><td>AR_INPUT_QUICKTIME7
</td><td> -device=QuickTime7
</td><td>4.5.0
</td><td>
</td></tr>
<tr>
<td>iOS
</td><td>iOS video input
</td><td>AR_INPUT_IPHONE
</td><td> -device=iPhone
</td><td>4.4.3 (iOS release 1.0)
</td><td>
</td></tr>
<tr>
<td>Windows
</td><td>Media Foundation
</td><td>AR_INPUT_WINDOWS_MEDIA_FOUNDATION
</td><td> -device=WinMF
</td><td>5.1.5
</td><td>
</td></tr>
<tr>
<td>Windows Store (Windows 8.1 and Windows Phone 8.1)
</td><td>Windows Media Capture
</td><td>AR_INPUT_WINDOWS_MEDIA_CAPTURE
</td><td> -device=WinMC
</td><td>5.1.7
</td><td>
</td></tr></tbody></table>

[1]: general_environment_variables