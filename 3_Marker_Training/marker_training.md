# Creating and Training New Markers
[Markers][marker_about] are the squares that ARToolKit recognizes and tracks in a video stream. That is, markers are the physical patterns that you've created or printed out. ARToolKit comes with PDF files for some pre-made markers, e.g. the Hiro marker, which you can print out and affix to card or board (so that they stay flat). Markers are the optical inputs to ARToolKit.

![The Hiro marker][Hiro_marker]

Markers have only a few constraints.

-   They must be square.
-   They must have a continuous border (generally either full black or pure white) and they must sit on a background of contrasting color (generally the opposite of the border color). By default, the border thickness is 25% of the length of an edge of the marker.
-   The final constraint is that the area inside the border, which we refer to as the *marker image*, must not be [rotationally symmetric][1] (specifically, it must not have rotational symmetry of an even order). The area inside the border can be black and white, or colored (and ARToolKit provides a means to track with greater accuracy when the marker image is colored).

ARToolKit has an additional feature to use markers which contain a [special two-dimensional grid of black and white squares][marker_barcode] (a little like a 2D-barcode) in place of the usual marker image. Use of these markers can speed up tracking when there are lots of markers in the scene.

##Designing New Markers
You can design a new marker by editing the template provided in your ARToolKit distribution, in the file `doc/patterns/Blank pattern.png`. You can create the marker any size you wish, and you can mix different marker sizes. When you use the marker in ARToolKit, you can tell ARToolKit how big the marker actually is through a configuration file.

![Marker Dimensions][Markerdimensions]

The inner 50% of the marker is interpreted as the marker image by ARToolKit, as per the image at right. Note that the image can be color, white on black or black on white, and it can extend into the border region. Remember that the part of the image outside the inner 50% will be ignored by ARToolKit though, and also be sure not to extend too far into the border, or else ARToolKit might not recognize the marker at all when its at a very oblique angle to the camera.

Even easier to use is [Julian Looser's web-based marker generator][2].

If you are using 2D-barcode markers, you can find the marker images in your ARToolKit distribution, in the folder doc/patterns/Matrix code 3x3/

##Training Markers
Once you have a new marker, you need to let ARToolKit know what it looks like by "training" ARToolKit to the marker's appearance. The output of the training is a pattern file. Pattern files are files that contain data that represents the image in the center of a marker. Pattern files allow ARToolKit to distinguish the markers you wish to track from other square objects in the scene, and to distinguish one marker from another.

You can find the pattern file for the Hiro marker in your ARToolKit distribution, in the file `bin/Data/patt.hiro`.

If you choose to use 2D-barcode markers, you won't need pattern files, just the identifying number of the barcode.

You perform the training using the `mk_patt` utility found in ARToolKit, or you can use an [online (Adobe Flash-based) training program on Tarotaro][3].

###Using mk_patt
mk_patt is an easy to use utility for training new markers. Open a terminal/command prompt window (on Mac OS X / Linux, open a Terminal window, on Windows, choose "Run" from the Start menu, type "cmd").
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

mk_patt wants to know which [camera calibration file][config_camera_calibration] to use. If you want to use the default calibration file, just press enter. If you've got a calibration file saved elsewhere, enter the path to it instead. At this point, you should see the image from the camera appear:
![mk_patt][Mkpatt]

Point the camera directly at your marker. Try to align the camera so that the marker appears square on the screen, and as large as possible. If ARToolKit has identified the marker, it will outline it with a red/green square.

Rotate the marker so that the *red corner of the square is at the top-left corner of your marker*, then press the left mouse button. The image will be captured, and in your terminal window you will see the prompt:
<pre>
Enter filename:
</pre>

Type a name for your pattern file (usually something ending in ".patt") and press return. If you don't want to save it, just press return to restart the video. That's it! You can train more patterns, or click the right mouse button to exit the program.

There are more options that you can customize when training markers (such as size of the marker border). Running the utility with the `--help` option will show the various command-line options for adjusting the default settings. The help text is reproduced here:
<pre>
Options:
Usage: ./mk_patt [options]
  --borderSize f: specify the width of the pattern border, as a percentage
             of the marker width. Range (0.0 - 0.5) (not inclusive).
  -border=f: specify the width of the pattern border, as a percentage
             of the marker width. Range (0.0 - 0.5) (not inclusive).
  --cpara <camera parameter file for the camera>
  -cpara=<camera parameter file for the camera>
  --vconf <video parameter for the camera>
  -h -help --help: show this message
</pre>

###Testing the Pattern File
You can change [simpleLite][example_simplelite] or simple applications to use your new pattern by editing the source code and recompiling. First drop your pattern file into the bin/Data directory. Then, in your source code editor, locate the code `char *patt_name = "Data/patt.hiro";` and replace `patt.hiro` with the name of your pattern. Recompile, and voila!

##Marker Customisations

###Changing Marker Border Width
The border width can be set at run time. See the documentation for [arSetPattRatio][arsetpattratio]

###Changing Marker Template Size
The maker template size (the number of pixels sampled in the marker image) IS editable, in `include/AR/config.h` (or config.h.in if you want to make the change permanent). The values in question are `AR_PATT_SIZE_X` and `AR_PATT_SIZE_Y` and `AR_PATT_SAMPLE_NUM` *which must be an integer multiple of the pattern size*.

### Using Really Large Images
If using large images, you may want to edit `#define`s `AR_SQUARE_MAX`, `AR_CHAIN_MAX`, and `AR_PATT_NUM_MAX` in config.h. These influence memory use so are usually set to a conservative minimum.

##Tips for Best Results
- The markers will work best if they're trained on the same camera that is used for the actual application. The camera should be [accurately calibrated][config_camera_calibration] prior to running mk_patt.
- Don't forget that markers can be color! Let's see some non-boring markers out there people!
- A common mistake is to try and use markers with much too-fine detail in the marker image. ARToolKit samples the marker image at only a resolution of 16x16 pixels, so if you're getting markers mistaken for each other, check whether your markers look too similar to each other when the marker image is downsampled to 16x16 pixels.

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
