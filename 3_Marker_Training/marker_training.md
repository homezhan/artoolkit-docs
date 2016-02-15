# Creating and Training Traditional Template Square Markers
Markers are the optical inputs to ARToolKit. [Square markers][marker_about] are one of several types of markers that ARToolKit recognizes and tracks in a video stream. A marker is simply a graphic image. ARToolKit comes with sample png, jpeg and PDF marker pattern and sample marker image files. For example, below, the Hiro square marker can be printed and affix to card stock (so that the marker remains flat).

![The Hiro marker][Hiro_marker]

Square markers have only a few constraints. 

-   They must be square.
-   They must have a continuous border (generally either full black or pure white). And, with the marker in foreground, the background must be a contrasting color (generally, a dark versus a light color or shade). By default, the border thickness is 25% of the length of an edge of the marker.  
-   The final constraint is that the area inside the border, which we refer to as the *pattern*, must be [rotationally asymmetric][1]. The area inside the border can be black and white, or colored (and ARToolKit provides a means to track with greater accuracy when the marker pattern is colored).  

ARToolKit supports the recognition of a marker type referred to as a matrix marker which is made up of a [grid of black and white squares][marker_barcode] that is a form of two-dimensional barcode. Matrix markers can speed up tracking when many markers are required in a scene, and when used with error correction and detection (EDC) offer increased resistance to one marker being misrecognized as a different marker.

##Designing a New Square Marker
A new marker can be designed and created by editing the marker template image file provided in the ARToolKit SDK: `doc/patterns/Blank pattern.png`. Markers can be scaled to any size and placed anywhere in a target scene. An ARToolKit utility is used to generate a data file that specifies the size of the marker as well as other marker attributes.

![Marker Dimensions][Markerdimensions]

The inner 50% of the marker is interpreted as the marker image by ARToolKit, as per the image at right. Note that the image can be color, white on black or black on white, and it can extend into the border region. Remember that the part of the image outside the inner 50% will be ignored by ARToolKit though, and also be sure not to extend too far into the border, or else ARToolKit might not recognize the marker at all when its at a very oblique angle to the camera.

Even easier to use is [Julian Looser's web-based marker generator][2].

If you are using 2D-barcode markers, you can find the marker images in your ARToolKit distribution, in the folder doc/patterns/Matrix code 3x3/

##Training ARToolKit to Recognize Markers
Given a new square marker (i.e. a padded contrasting square with an embedded rotationally asymmetric pattern), ARToolKit must be trained to recognize it. The output of the training process is a pattern recognition data file referred to as the marker's "pattern file." Pattern files enable ARToolKit to detect, recognize, identify and track new markers in a captured video stream.

The naming convention for pattern files is to prepend "patt." to name the represents the pattern. For example, the pattern file filename for the Hiro marker that is included with the ARToolKit SDK is "patt.hiro" (found in the \[ARToolKit SDK\]/bin/Data/ directory). Note: ARToolKit SDK may later, in addition, support ".patt" file name extensions (".patt" as a filename suffix).

2D-barcode markers do not require pattern files but instead require the identifying number of the barcode.

Training is done using the `mk_patt` utility found in ARToolKit SDK. Or, alternately, training can be done using the online (Adobe Flash-based) training application: ["Tarotaro"][3].

###Using mk_patt
mk_patt is an easy to use utility for training new markers. Open a command-line session window (on Mac OS X / Linux, open a Terminal window, on Windows, choose "Run" from the Start menu, type "cmd").
On Linux / OS X, type:
<pre>
    ./mk_patt
</pre>
On Windows, type:
<pre>
    mk_patt.exe
</pre>

You will see output similar to this in your terminal:
<pre>
    ./mk_patt
    Enter camera parameter filename(Data/camera_para.dat):
</pre>

mk_patt prompts for a [camera calibration file][config_camera_calibration] (filename extension *.dat*). It's possible to use another tool that comes with ARToolKit SDK to calibrate your camera. The tool generates a calibration data file specific to the camera. If there is calibration data file available, enter the path.

You can forego the step to create a calibration data file for a specific camera and use the default calibration data file that comes with the ARToolKit SDK. To select this, simply press enter to the above prompt.

At this point, the camera is activated:
![mk_patt][Mkpatt]

Point the camera directly at your marker. Try to align the camera so that the marker appears square on the screen and fills the camera's view. If ARToolKit has identified the marker, it will outline it with red and green lines.

Rotate the marker so that the *red corner of the square is at the top-left corner of your marker*, then press the left mouse button (for left-handed mouse users, this may be the configured primary mouse button). The image will be captured, and in your terminal window you will see the prompt:
<pre>
Enter filename:
</pre>

Type a filename starting with "patt." prepended (by convention) followed by a unique pattern name and press return. If you don't want to save it, just press return to restart the video. That's it! You can train more patterns, or click the right mouse button (for left-handed mouse users, this may be the configured secondary mouse button) to exit the program.

There are more options that you can customize when training markers (such as size of the marker border). Running the utility with the `--help` option will show the various command-line options for adjusting the default settings. The help text is reproduced here:

<!--
Can't use HTML pre tags here. For some reason, the tags were not interpreted as HTML tags and the tags displayed literally in the browser view.
JWolf 11/06/15
-->

	Usage: ./mk_patt [options]
	--borderSize f: specify the width of the pattern border,  as a
	                percentage of the marker width. Range (0.0 - 0.5)
	                (not inclusive).
	-border=f: specify the width of the pattern border, as a percentage
	           of the marker width. Range (0.0 - 0.5) (not inclusive).
	--cpara <camera parameter file for the camera>
	-cpara=<camera parameter file for the camera>
	--vconf <video parameter for the camera>
	-h -help --help: show this message

###Testing the Marker and the New Pattern File
You can change [simpleLite][example_simplelite] or simple applications to use your new pattern by editing the source code and recompiling. First drop your pattern file into the bin/Data directory. Then, in your source code editor, locate the code `char *patt_name = "Data/patt.hiro";` and replace `patt.hiro` with the name of your pattern. Recompile, and voila!

##Marker Customizations

###Changing Marker Border Width
The border width can be set at runtime. See the documentation for [arSetPattRatio][arsetpattratio].

###Changing Marker Pattern Size
As of ARToolKit v5.3, the marker's pattern size (the number of pixels sampled for the pattern) can be changed at runtime. By default it is 16x16 pixels, and if you wish to maintain compatibility with previous versions, it is recommended to retain this setting. If you wish to change the size this is done during AR setup by using parameters to the arPattCreateHandle2 function.

### Using Really Large Square Markers
If using large images, you may want to edit `#define`s `AR_SQUARE_MAX`, `AR_CHAIN_MAX`, and `AR_PATT_NUM_MAX` in config.h. These influence memory use so are usually set to a conservative minimum.

##Tips for Best Results
- The markers will work best if they're trained on the same camera that is used for the actual application. The camera should be [accurately calibrated][config_camera_calibration] prior to running mk_patt.
- Don't forget that markers can be color. Adding color to markers can enhance the AR application.
- A common mistake is to try and use markers with too much fine detail in the pattern. By default, ARToolKit samples the pattern at only a resolution of 16x16 pixels, so if you're getting markers mistaken for each other or not recognized, check whether your markers appear similar to each other when the pattern graphic is scaled down to a 16x16 pixel image.

[marker_about]: 3_Marker_Training:marker_about
[marker_barcode]: 3_Marker_Training:marker_barcode
[config_camera_calibration]: 2_Configuration:config_camera_calibration
[example_simplelite]: 7_Examples:example_simplelite
[arsetpattratio]: http://www.artoolworks.com/support/doc/artoolkit4/apiref/ar_h/index.html#//apple_ref/c/func/arSetPattRatio

[1]: http://en.wikipedia.org/wiki/Rotational_symmetry
[2]: http://www.roarmot.co.nz/ar/
[3]: http://flash.tarotaro.org/blog/2009/07/12/mgo2/

[Hiro_marker]: :hiro_marker.png
[Markerdimensions]: :markerdimensions.png
[Mkpatt]: :mkpatt.jpg
