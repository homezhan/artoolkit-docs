# Using Stereo Tracking
ARToolKit is one of the few augmented reality tracking libraries with support for stereo tracking. What do we mean by stereo tracking? We mean that video streams from more than one camera can be simultaneously input into ARToolKit, and ARToolKit will extract tracking data from both video streams. When a tracked surface (a [marker][marker_about], a [barcode marker][marker_barcode] a [multimarker set][marker_multi], or a [textured NFT surface][marker_nft_training]) is in view of both cameras, the accuracy of tracking is potentially improved over the same tracking performed with a single camera.

Input from two cameras also provides the potential to display two images to the user, should that be appropriate, although it is perfectly permissible to display just one of the video streams while tracking from both.

Throughout this document, we will be referring to "left" and "right" cameras. We think of these cameras viewing a scene in the same sense as our eyes viewing the scene. That is, when looking at the scene in the same direction as the cameras are looking, we refer to the camera on our left as "left" and on our right as "right". Note, however, that the camera relationship need not actually be left and right. We could just as well name them "camera A" and "camera B" and use a stereo rig in which the cameras are offset vertically rather than horizontally, or even opposite each other! The only practical constraint is that both cameras will need to be able to see the tracked surface (marker or NFT texture) simultaneously for stereo tracking to be of advantage in improving accuracy. If only one camera can see the marker at once, the tracking quality will be the same for monocular tracking by that camera alone.

The following sections will help advise on the best stereo system setup.

##General Rules on Stereo Tracking
In order to get improved tracking data from stereo camera input, [each camera must be accurately calibrated][config_camera_calibration] (the lens calibrations) and the relationship between the two cameras (the *stereo calibration*) must be precisely known. Fortunately, ARToolKit provides easy-to-use utilities to help with these tasks; `calib_camera` and `calib_stereo`, respectively. However, it is generally not possible to use stereo tracking in situations where the cameras can move relative to each other during use. The expected scenario is a camera rig where the cameras are permanently mounted relative to each other, or are combined into a single physical housing.

Stereo tracking will likely at least double the data being processed by ARToolKit, at all stages of the tracking pipeline. This requires careful consideration of the system used for the tracking. Here are some questions to consider:

-   Does the system have sufficient CPU and I/O resources to acquire two real-time video streams simultaneously?
-   If you are using USB2 or Firewire cameras, can the I/O bus sustain adequate data transfer rates to get full frame rate at desired size from 2 cameras?
-   Is the CPU sufficiently fast to track from two streams?
-   Is sufficient system memory available for ARToolKit's buffers and data structures?
-   If you wish to present both video streams to the user, is OpenGL texturing speed sufficient?

## Hardware Selection
[Hardware selection][about_hardware_selection] is important in choosing a stereo rig. There are a variety of professional-level stereo cameras available in the market, or depending on your needs, you might wish to build your own stereo rig. Cameras such as the "Bumblebee" range from Point Grey which contain two matched cameras in a single housing with a single I/O bus are very convenient, and might even allow for stereo presentation to the user (using a stereo display). However, for some tracking applications, an even greater degree of stereo disparity (the distance between the cameras) may be desirable, justifying a custom mount for two separate cameras. This comes at an increased cost in setup, plus the need to accommodate two I/O buses.

It is not necessary that both cameras be identical in terms of lenses, sensors, or quality. However, if the aim of the stereo rig is to increase accuracy, it is advisable to make sure the two cameras are similar in terms of optical pathway quality (lens, sensor etc) as the achievable accuracy will be limited by the camera with the lower specification.

In some of the examples below, to illustrate ARToolKit's flexibility in this regard, you can see tracking from two consumer-level cameras (one a 4:3 ratio 1600x1200 sensor and the other a 5:4 1280x1024 sensor).

## Stereo Calibration
Stereo calibration is an essential step in stereo tracking. This is the step where the relationship between the two cameras (the precise offset and orientation from the sensor of one camera to the sensor of the other) is determined. ARToolKit provides the utility "calib_stereo" to perform this task. calib_stereo works by knowing in advance the [calibrated lens parameters][config_camera_calibration] of each camera, and then tracking the calibration chessboard pattern simultaneously with both cameras to infer the relative offset and orientation of each camera. Thus, before performing stereo calibration, you must have carefully calibrated each camera separately.

### Video Configuration
Using more than one camera simultaneously may require you to grapple with a problem you haven't encountered previously: how to get ARToolKit to choose the correct camera for use with an operation such as lens calibration with calib_camera. This is performed by using ARToolKit's video configuration capabilities. The exact video configuration options required to choose a particular camera vary between platforms, but can generally be specified to allow you to choose between cameras.

In the utilities calib_camera and calib_stereo, you will find command-line options allow you to specify strings to use as video configurations.

E.g. to select the second video device on your system for use with calib_camera:
On Linux, type:
<pre>
    ./calib_camera --vconf "-device=GStreamer v4l2src device=/dev/video1 use-fixed-fps=false ! ffmpegcolorspace ! video/x-raw-rgb,bpp=24 ! identity name=artoolkit sync=true ! fakesink"
</pre>
On OS X, type:
<pre>
    ./calib_camera --vconf "-device=QuickTime7 -source=1"
</pre>
On Windows, type:
<pre>
    calib_camera.exe --vconf "-device=WinDS -devNum=2"
</pre>

Similar options apply to calib_stereo, except the parameters are named with L and R suffixes:
<pre>
    ./calib_camera --vconfL "left config" --vconfR "right config"
</pre>

See [Configuring video capture][config_video_capture] for complete lists of video configuration options for each platform and video input module.

###Using calib_stereo
calib_stereo looks for the calibration information for each lens in the files Data/cparaL.dat and Data/cparaR.dat, for left and right cameras respectively. However, you can name these files as you wish, and just supply the pathnames to each using calib_stereo's command-line parameters:
<pre>
    ./calib_stereo -cparaL=left calibration file -cparaR=right calibration file
</pre>

Open a terminal / command prompt (on Mac OS X / Linux, open a Terminal window; on Windows, choose "Run" from the Start menu, type "cmd"). Then run the calib_stereo program from that window..
On Linux / OS X, type:
<pre>
    ./calib_stereo
</pre>
On Windows, type:
<pre>
    calib_stereo.exe
</pre>

Also supply any required video config and camera calibration file names. You will see output similar to this in your terminal:
<pre>
./calib_stereo --vconfL "-source=0" --vconfR "-source=1" -cparaL=quickcamvisionpromac.dat -cparaR=creativelivecamoptiapro.dat
CHESSBOARD_CORNER_NUM_X = 7
CHESSBOARD_CORNER_NUM_Y = 5
CHESSBOARD_PATTERN_WIDTH = 30.000000
CALIB_IMAGE_NUM = 10
Video parameter Left : -source=0
Video parameter Right: -source=1
Camera parameter Left : quickcamvisionpromac.dat
Camera parameter Right: creativelivecamoptiapro.dat
Using supplied video config "-source=0".
Video formatType is BGRA, size is 1600x1200.
Using supplied video config "-source=1".
Video formatType is BGRA, size is 1280x1024.
Image size for the left camera  = (1600,1200)
Image size for the right camera = (1280,1024)
*** Camera Parameter for the left camera ***
--------------------------------------
SIZE = 1600, 1200
Distortion factor: k1=0.0791388974, k2=-0.1812048256, p1=-0.0013435410, p2=-0.0004586111
                  fx=1338.975677, fy=1326.604156, x0=790.253296, y0=558.685112, s=0.990136
1352.31544 0.00000 790.25330 0.00000
0.00000 1339.82066 558.68511 0.00000
0.00000 0.00000 1.00000 0.00000
--------------------------------------
*** Camera Parameter for the right camera ***
--------------------------------------
SIZE = 1280, 1024
Distortion factor: k1=-0.0694990978, k2=0.0262184255, p1=0.0020496645, p2=0.0001065184
                  fx=1197.882080, fy=1192.068604, x0=646.941895, y0=525.006226, s=1.009049
1187.14020 0.00000 646.94189 0.00000
0.00000 1181.37885 525.00623 0.00000
0.00000 0.00000 1.00000 0.00000
--------------------------------------
Scaling 2880x1200 window by 0.600 to fit onto 1920x1080 screen (with 10% margin).
</pre>

At this point, if everything has loaded OK and the cameras can be opened, you should see the images from the camera appear (side by side in a single window).

Calibration requires the capturing of a series of images with both cameras. In the top-left corner of the capture window is displayed the number of images captured so far. Position the chessboard grid so that it is visible to both cameras, and the inner corners of the squares will be highlighted with "X" marks and numbered. *When the cameras can clearly see all the intermediate corners, the X marks turn RED, and a calibration image can be captured*:

![Both cameras with a good view of the calibration board, ready to capture][calib_stereo_screen]

If some of the corners are obscured by the edges of the camera frame, or poor lighting or reflection, the crosses will be GREEN, and no calibration image can be captured until the optical conditions are changed.

Once you have an image with all red crosses, you can press the space bar on the keyboard. The image will be captured, and the locations of the X points will be printed to the terminal window, and the counter will increment.

In order to obtain a good calibration for the cameras, it is important to obtain images of the calibration board at a variety of angles to the camera lenses.

Once all the calibration images have been captured (10 by default), the stereo calibration data will be calculated and output to the terminal window, and you will be prompted for a file name for the calibration data.

###Optional - Changing the Default Calibration Pattern Settings
If you need to, the size of the calibration squares, the number of intermediate corners in horizontal and vertical directions (i.e. the number of rows minus 1 and the number of columns minus 1), and the number of calibration images captured can all be adjusted from the command line. Running the utility with the `--help` option will show the various command-line options for adjusting the default calibration settings.

On Linux / OS X, type:
<pre>
    ./calib_stereo --help
</pre>
On Windows, type:
<pre>
    calib_stereo.exe --help
</pre>

The help text is reproduced here:
<pre>
    Usage: ./calib_stereo [options]
    -cornerx=n: specify the number of corners on chessboard in X direction.
    -cornery=n: specify the number of corners on chessboard in Y direction.
    -imagenum=n: specify the number of images captured for calibration.
    -pattwidth=n: specify the square width in the chessbaord.
    --cparaL <camera parameter file for the Left camera>
    --cparaR <camera parameter file for the Right camera>
    -cparaL=<camera parameter file for the Left camera>
    -cparaR=<camera parameter file for the Right camera>
    --vconfL <video parameter for the Left camera>
    --vconfR <video parameter for the Right camera>
    -h -help --help: show this message
</pre>

[marker_about]: Marker_Training:marker_about
[marker_barcode]: Marker_Training:marker_barcode
[marker_multi]: Marker_Training:marker_multi
[marker_nft_training]: Marker_Training:marker_nft_training
[about_hardware_selection]: Advanced:about_hardware_selection
[config_camera_calibration]: Configuration:config_camera_calibration
[config_video_capture]: Configuration:config_video_capture

[calib_stereo_screen]: /Calib_stereo_screen.png