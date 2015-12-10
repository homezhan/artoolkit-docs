#Optical - Optical See-Through Example
The applications "optical" and "opticalStereo" are example applications demonstrating *monocular* and *stereo optical see-through with a [calibrated camera][config_camera_calibration] and display, respectively.

-   It expects to load calibrated camera parameters from the file `Data/camera_para.dat` and [calibrated optical see-through parameters][config_optical_see-through] from the file Data/optical_param.dat, so be sure that you have run the calibration programs (calib\_camera and calib\_optical) and moved the results of your calibration into the Data directory.
-   Print out the Hiro and Kanji markers and make sure that they are exactly 80mm on each side. *(Unlike video-see through where a marker of incorrect size will still be overlaid with the content, in optical see-through, the axis of the camera and the axis of the display do not usually align, and so a mis-sized marker will result in radically incorrect display)*.
-   Run either "optical" for a monocular display, or "opticalStereo" for a stereo display.

The screen will initially be blank, as the application is in optical see-through mode. Just like [calib\_optical][config_optical_see-through], if at any point you need to see the video-image (temporarily, e.g. to see if the camera is correctly focussed or has correct brightness or contrast) press the "o" key. While in this mode, you can press "d" to see the debug (binarized image) and "-" and "+" to adjust the binarization threshold to get nice black and white borders on the pattern.

When the Hiro marker is held in the field of view of the camera and display, you should see the OSG "axes" model overlaid on top of the marker. If your calibration was accurate the two should be quite well aligned (registered). If your calibration was poor, you will observe position and orientation offsets between the cube and the marker, and the 3D objects may appear to float above or below the cards or may be distorted. The same will apply if the camera has moved relative to the display since it was calibrated, or if the display has moved on your head, or if the calibration was done by another person.

Below is the listing for "optical":

<pre>
Usage: ./optical [options]
Options:
  --vconf <video parameter for the camera>
  --cpara <camera parameter file for the camera>
  -cpara=<camera parameter file for the camera>
  --width w     Use display/window width of w pixels.
  --height h    Use display/window height of h pixels.
  --refresh f   Use display refresh rate of f Hz.
  --windowed    Display in window, rather than fullscreen.
  --fullscreen  Display fullscreen, rather than in window.
  -h -help --help: show this message
</pre>

Below is the listing for "opticalStereo":
<pre>
Usage: ./opticalStereo [options]
Options:
  --vconf <video parameter for the camera>
  --cpara <camera parameter file for the camera>
  -cpara=<camera parameter file for the camera>
  --width w     Use display/window width of w pixels.
  --height h    Use display/window height of h pixels.
  --refresh f   Use display refresh rate of f Hz.
  --windowed    Display in window, rather than fullscreen.
  --fullscreen  Display fullscreen, rather than in window.
  --stereo [INACTIVE|DUAL_OUTPUT|QUADBUFFERED|FRAME_SEQUENTIAL|
            SIDE_BY_SIDE|OVER_UNDER|HALF_SIDE_BY_SIDE|
            OVER_UNDER_HALF_HEIGHT|ANAGLYPH_RED_BLUE|ANAGLYPH_RED_GREEN
            ROW_INTERLACED|COLUMN_INTERLACED|CHECKERBOARD].
            Select mono or stereo mode. (Not all modes supported).
  -h -help --help: show this message
</pre>

If you want to change the markers, you can edit the file Data/markers.dat. If you want to change the content, edit the file Data/objects.dat.

[config_camera_calibration]: 2_Configuration:config_camera_calibration
[config_optical_see-through]: 8_Advanced_Topics:config_optical_see-through
